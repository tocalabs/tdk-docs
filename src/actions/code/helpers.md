# Helpers in Actions

Helpers allow you share common functionality across multiple actions, you can think of them like a local package or library that you can call methods amongst other things. You can find more information in the [Helpers](../../../helpers/helpers.md) section.

If you wish to use a Helper within your action then first you must go the Helpers tab as shown below:

![Helpers Tab](../../../assets/helper_tab.png)

Once you have selected the tab you can simply navigate the different Helpers which are available for use and select the appropriate version and tick the Helper.

![Helper Selection](../../../assets/helper_select.png)

Once you include a Helper class in your Action, it will get injected for use automatically by the underlying machinery. It will instantiate an instance of the Helper class and it will be named the same as the Helper name.
So, if you select the Graph API V2 as the Helper you wish to include then it will get injected into your action as shown below:

```csharp
public class YourAction // gets replaced with the ActionKey you defined
{
    public string Jwt { get; set; }
    public CancellationToken Token { get; set; }
    public Action Action { get; set; }
    public bool FailOnError { get; set; }
    public bool ErrorOnTimeout { get; set; }
    
    // Helpers injected here
    private Helpers.GraphAPIV2 GraphAPIV2 = new Helpers.GraphAPIV2();
    
    public async Task ExecuteAction()
    { 
        // Your code gets injected here and replaces the exception below
        throw new NotImplentedException("No implementation written");
    }
}
```
The format it injects it with is the following:

```csharp
$"private {helper.FullName} {helper.Key} = new {helper.FullName}();"
```

This means that the Helpers you include are automatically instantiated and ready for you to use in your action. Here's an example from the Outlook Inbox action to demonstrate how this looks in an action:
```csharp
var accessToken = await IdentityService.Get(identityId);
GraphAPIV2.SetAccessToken(accessToken);
var emails = await GraphAPIV2.GetMessages(maxResults, query, skip);
var tableContext = GraphAPIV2.CreateMessageTable("inbox", emails);
```
