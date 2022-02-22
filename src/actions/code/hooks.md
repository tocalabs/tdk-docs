# Hooks

## Helpers

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
