# Bounding Box

## Definition
The `BoundingBox` type is used for defining a box or region. It contains the coordinates of the top left hand corner and then a width and height property. This means that a bounding box is always a square or a rectangle, all corners must be at 90 degrees.

```csharp
public class BoundingBox
{
    public double X { get; set; }
    public double Y { get; set; }
    public double Width { get; set; }
    public double Height { get; set; }
}
```

## Methods
No there are no additional methods implemented on the `BoundingBox` class.
