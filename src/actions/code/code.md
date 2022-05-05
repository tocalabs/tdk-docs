# Writing an Action

This is how you write an action

```csharp
public virtual async Task PreChildExecuteAction()
{
	Action.Status = ActionStatus.Success;
}

public virtual async Task ExecuteAction()
{
        throw new Exception(
		"This action requires 1 or more actions to be nested below it");
}

public virtual async Task PostChildExecuteAction()
{
	Action.Status = ActionStatus.Success;
}
```

## Usings

Each action includes the following namespaces in the using:
```csharp
using Newtonsoft.Json;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Threading;
using System;
using System.Reflection;
using System.Runtime.Loader;
```

Currently in C# you cannot define usings within a method and so you cannot specify your own `usings` in an Action. For this reason, you must fully qualify any namespaces that you wish to use that don't exist in the above list. 

For example if you wish to use the System File methods then you must write the following:
```csharp
var file = System.IO.File.ReadAllLines("C:\Users\Administrator\Desktop\content.txt");
```
