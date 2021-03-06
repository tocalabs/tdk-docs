# Nested Actions

Nested actions are actions which expect to have one or more other actions nested underneath it, these are called child actions. This allows you to manipulate the behaviour of the child actions in the code of the parent action, such as a Repeat, If Then or For Each action.

Before we explain how these nested actions work, it's important to understand the difference between a regular action and a nested action.

A regular action template is shown in Figure 1.
```csharp
public class YourAction // gets replaced with the ActionKey you defined
{    
    public async Task ExecuteAction()
    { 
        // Your code gets injected here and replaces the exception below
        throw new NotImplentedException("No implementation written");
    }
}
```
*Figure 1 - Normal Action Template*

But a nested action has a template which looks like the one shown in Figure 2.
```csharp
public class YourAction // gets replaced with the ActionKey you defined
{    
    public async Task PreExecuteAction()
    { 
        // Your pre execute code gets injected here and replaces the exception below
        throw new NotImplentedException("No implementation written");
    }
    
    public async Task PostExecuteAction()
    { 
        // Your post execute code gets injected here and replaces the exception below
        throw new NotImplentedException("No implementation written");
    }
}
```
*Figure 2 - Nested Action Template*

The difference here is that a normal action has a single method which is called during execution called `ExecuteAction()` but nested actions have two methods, one called `PreExecuteAction()` and another called `PostExecuteAction()`.
Understanding when these two methods are called is key to writing nested actions.

## Normal Action

When a normal action is run, it calls the `ExecuteAction()` method and when it finishes it will move onto the next action within the activity or fail the activity if an exception has occurred.

## Nested Action

When an action which has actions nested underneath it runs, it will call the `PreExecuteAction` method first before executing the nested actions, once the nested actions have completed it will then execute the `PostExecuteAction` method.
The screenshot below shows where these two methods are called in relation to an activity executing.

![Nested Action Execution](./../../assets/nested_action.png)

You can use this to your benefit to control the flow of the activity at different points of your activity but within the same action. This allows you to convert a While action to a DoWhile by simply moving the conditional check to the `PostExecuteAction` method rather than the `PreExecuteAction` method call.
