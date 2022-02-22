# Types

Before we start writing any code, it is good to understand the concrete types that form the backbone of the TDK.

These types must be strictly adhered to for action inputs and action results, this is because the underlying machinery understands these types and knows how to deserialise them, serialise them and display them. These types are named by the `ActionTypes` enum which is defined as follows:

```csharp
public enum ActionTypes
{
    String,
    Number,
    Boolean,
    Image,
    Grid,
    Coordinates,
    BoundingBox,
    Array,
    Table,
    DateTime,
    Parameter,
}
```

In the following sections we will take a look at how each type is implemented and what methods are available on each type.
