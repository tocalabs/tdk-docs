# Hooks

When writing an action, there are a number of properties, functions and methods available to use which can interact with the underlying machinery to do things such as return results, cancel a running action and manipulate the flow of the activity.

## Services

Services are instances of helper classes which allow you to interact with different parts of the platform such as datastores, cryptography and identities.

### Cryptography Service

The cryptography service allows you to interact with a central service on the platform which has endpoints to allow you to encrpyt and decrypt values. The reason this is a central service is so that everything is encrypted and decrypted with the same key to avoid mistakes where different items require different keys to be locked and unlocked.

#### Action Interface

The action interface is the way that you interact with this service from the code you write for an action in the TDK.
```csharp
protected readonly CryptographyService CryptographyService;
```
So if we want to use this in our action, we can just use the CryptographyService property.

#### Method Definitions
The `CryptographyService` has the following methods available to us:
```csharp
string Encrypt(string request);

string Decrypt(string request);
```

An example of an action that uses this is the Paste Password action:
```csharp
var plainText = CryptographyService.Decrypt(pointer);
```

We take a variable called pointer as an input to the action and the pointer is the encrypted version of the password so we make a call to the `Decrypt` method.

### Identity Service

The Identity service allows us to use Identities as a way of authentication in actions. An Identity represents some login credential such as a Microsoft Office365 login. This allows us to run actions acting on behalf of the logged in user allowing us to see that users emails, files and calendar appointments etc. When you use an identity as an input to an action you receive a `string` which is the unique identifier to that identity. Before you can actually use it, you need to retrieve the access token for that Identity from the Identity service.

The Identity service stores an associated access token and refresh token, so if the access token is going to expire within 5 minutes then it will automatically be refreshed by the service, meaning you don't have to worry about any of this logic yourself.

#### Action Interface
The Identity service is defined on an action as shown below:

```csharp
protected readonly IdentityService IdentityService;
```

#### Method Definitions

The `IdentityService` class has the following methods available to us:
```csharp
async Task<string> Get(string identityId);
```

This allows us to pass in the unique identitifer we receive as the action input and use it to get the access token we require.

An example of an action that uses this is the Outlook Inbox action:
```csharp
var accessToken = await IdentityService.Get(identityId).ConfigureAwait(false);
```
Here, the identityId variable is the input to the action which is the Identity and we are using it to get the access token by calling the `Get` method.

### Documentstore Service

The Documentstore service is the central service used for the storage of images. If images were passed around the system in their original state then this would be a very heavy and inefficient way of moving images around the system and would lead to poor user experience. 

The Documentstore service acts as a database for storing all images and instead hands out references to a specific image when it is saved. This allows us to simply store a reference to the image rather than store the entire image in activities for example. More information on how this works can be found [here](../../types/tocatypes/image.md).

#### Action Interface

```csharp
protected readonly DataHelper DataHelper;
```

#### Method Definitions

```csharp
IDocument GetDocumentEntity(string guid);

async Task<string> SaveToDocStore(string value);

async Task<string> SetDocumentFromRegion(BoundingBox region, StorageType type = StorageType.Perm);
```

Most of the time you won't need to use the `GetDocumentEntity` method as images will arrive as inputs already in their full form as the retrieval of the image has been done for you already.

We can look at the Image Search action to see how we use the `SaveToDocStore` method.
```csharp
var image = await DataHelper.SaveToDocStore(result.dataUrl).ConfigureAwait(false);
```
Here the `result` variable is an object which contains the screenshot in the `dataUrl` property. We now want to save that to the Documentstore service so we can just use the refencece, here represented by the variable called `image`.

## Cancellation

Actions can be cancelled externally either through a manual trigger or alternatively through a failure which might cause the whole activity to stop and fail. The mechanism through which this happens internally is a [`CancellationToken`](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken?view=net-6.0).

Each action has a property called `Token` implemented on the `Action` property so you can access this through `Action.Token`, this property contains the CancellationToken. The Cancellation token is also used by the `Timeout` mechanism under the hood so when a timeout is triggered, it cancels the current running action via the cancellation token.

Here a few common ways that you can utilise this property to gracefully handle cancellation within your action.

#### Cancelling an asynchronous process

Some actions will need to make calls to do things like read files and make network calls and it is best practice to use the `async` equivalent of all of these methods, this is so that the Bot is not performing a "blocking" call. Most of these async methods will have a parameter for a cancellation token so that you can cancel a process from an external source.
If we look at an example such as the [`ReadAllTextAsync`](https://docs.microsoft.com/en-us/dotnet/api/system.io.file.readalltextasync?view=net-6.0) call in C#'s `System.IO.File` namespace then we can see it takes a cancellation token:
```csharp
Task<string> ReadAllTextAsync (string path, CancellationToken cancellationToken);
```

In an action we can now call this using `Action.Token` as follows:
```csharp
var readText = await System.IO.File.ReadAllTextAsync(path, Action.Token);
```
This is an example from the Read Text in File action.


#### Checking if an action has been cancelled

If an action is inside a busy loop, then you probably want to check each iteration of the loop whether the cancellation of the task has been requested.

```csharp
var lookAgain = true;
do {
    .
    .
    .
} while (lookAgain && !Action.Token.IsCancellationRequested);
```
This code above will check every loop that the action has not been cancelled, this way it will break out of the loop when either cancellation is requested or if the action's timeout is triggered.

This excerpt has been taken from the Image Search action.


## State

If you are writing a looping action then there may be a requirement to store state between each iteration of a loop. For example if you are writing a Repeat action then you need to keep track of how many iterations there have been so it knows when to stop the action.

For occassions like this, there is a thread-safe global state object called `Session` which allows actions to Set and Get data from the store.

The Set method is defined as shown below:

```csharp
void Set(string key, object value);
```

The Get method is defined as shown below:

```csharp
T Get<T>(string key, T defaultIfValueDoesNotExist);
```

Example usage might look like the following:

```csharp
// At the start of each iteration in the repeating action
var currentIteration = Session.Get<int>("currentIteration", 0);
.
.
.
// At the end of each iteration
currentIteration += 1;
Session.Set("currentIteration", currentIteration);
```

## Execution Flow

There are times when you need to manipulate the flow of an activity, whether that means finishing a loop early, executing child actions or stop the whole activity prematurely.

#### Executing nested actions

If you wish to execute the actions which are nested under the action you are designing, then you can use the `ActivityManagerExecuteChildren` method. 
This method expects an input of `true` if you wish to execute the nested actions and `false` if the nested actions should not be executed.

```csharp
public virtual void ActivityManagerExecuteChildren(bool execute);
```
An example of this is the If Then action where we only want to execute the nested action _if_ the expression is evaluated to be `true`.

#### Looping actions

If you want to tell the underlying machinery that your action should repeat, then you can use the `ActivityManagerRepeat` method. You will usually use and see this in the `PostExecute` part of an action.

```csharp
public virtual void ActivityManagerRepeat(bool repeat);
```

An example of this is the Repeat action where we want to keep repeating all actions nested underneath the Repeat until the repeat count has been reached.

#### Stopping an Activity

When you need to break out of an activity prematurely, you can use the `ActivityManagerStopActivity` method which also allows you to pass in a bool as the only argument which dictates whether or not to mark the activity as failed.
`true` means the activity will just stop but be marked as Completed and `false` will stop the activity whilst marking it as Failed.

```csharp
public virtual void ActivityManagerStopActivity(bool markAsFailed);
```

This is used in the Stop Execution action.

You should also use the `ActivityManagerContinue` method which will make sure that no further actions are run, this is commonly used in conjunction with `ActivityManagerStopActivity` to perform a "hard" stop.
```csharp
public virtual void ActivityManagerContinue(bool continueToNextAction);
```


## Results

If the action should return one or more results that can be used as datachips then we need to manually add the results.
This is done using the `AddResult` method which takes a key, the value and the type.

Add Result definition

```csharp
void AddResult(string key, object value, ActionType type);
```

`ActionType` is defined as shown below:

```csharp
enum ActionType
{
    String,
    Number,
    Coordinate,
    BoundingBox,
    Grid,
    Image,
    List,
    Table,
}
```

Example of use

```csharp
// Action will take two number inputs called inputOne and inputTwo and add them

var additionResult = inputOne + inputTwo;
AddResult(nameof(additionResult), additionResult, ActionTypes.Number);
```

## Logging

When an action runs it logs certain values. By default it will log the parameters and any exception that occurs during the action but there are ways you can log additional information if it is required, prehaps when first developing the action and testing.

There are different log functions for the different `LogLevel` that the Bot is set to in it's configuration file. These levels are:
- Debug
- Information
- Warning
- Error

The hooks for each level are defined as such:
```csharp
void AddDebugLog(string message);
void AddInfoLog(string message);
void AddWarningLog(string message);
void AddErrorLog(string message);
```

## Status

```csharp
enum ActionStatus
{
    Failed,
    ContinuedWithErrors,
    Success,
}
```

Example of usage:

```csharp
// Comes at the end of the action after
// all previous code has executed correctly
Action.Status = ActionStatus.Success;
```
