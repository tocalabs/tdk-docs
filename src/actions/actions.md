# Actions

Actions are the backbone of automation within the Toca platform, an action represents a single task for the Bot to carry out such as moving the mouse or typing some text in. The TDK allows users to extend the capability of the existing range of actions available on their platform and also add new actions.

When you write code for an action, it gets injected into a template code file that looks like this:
```csharp
public class ActionTemplate // gets replaced with ActionKey
{
    public string Jwt { get; set; }
    public CancellationToken Token { get; set; }
    public Action Action { get; set; }
    public bool FailOnError { get; set; }
    public bool ErrorOnTimeout { get; set; }
    
    
    public async Task ExecuteAction()
    { 
        // Your code gets injected here and replaces the exception below
        throw new NotImplentedException("No implementation written");
    }
}

public class Action 
{
    public string Name { get; set; }
    public List<Parameter> Parameters { get; set; }
    public List<Parameter> Results { get; set; }
    public ActionStatus Status { get; set; }
    public CancellationToken Token { get; set; }
}
```

In reality, an action is more complex than the code shown above but you can think of an action like this.
