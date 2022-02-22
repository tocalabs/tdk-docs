# Parameter

## Definition
A parameter is the most important type in the TDK as everything is actually a Parameter type where other types sit in the `Value` property of the `Parameter` type.

```csharp
public class Parameter 
{
    public string Key { get; set; }
    public string Type { get; set; }
    public object Value { get; set; }
}
```

- `Key` is a unique identifier for this particular value
- `Type` is a string representation of the value's type, it is a stringified version of the corresponding `ActionTypes` variant
- `Value` is the actual value, this is defined as an `object` as it could be any type. You can get this into the desired type by using the `Cast` extension

## Methods
There are no methods defined for this class but you can cast between the `object` in the Value property to another type using the `Cast` extension.

Cast is defined as follows:
```csharp
static TCast Cast<TCast>(this object source);
```

This can be used like so:
```csharp
var bbox = new BoundingBox {
    X = 45,
    Y = 60,
    Width = 100,
    Height = 250
};

var newParameter = new Parameter {
    Key = "bbox",
    Type = ActionTypes.BoundingBox.ToString(),
    Value = bbox
};

var castBBox = newParameter.Value.Cast<BoundingBox>();
```
