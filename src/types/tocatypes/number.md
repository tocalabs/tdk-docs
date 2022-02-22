# Number

## Definition
A Number type in Toca is simply a [double](https://docs.microsoft.com/en-us/dotnet/api/system.double?view=net-6.0) type in C#. This allows us to have one type which covers whole numbers and numbers which require decimal point accuracy.

 > **Note:** Just remember that you will need to cast to an [`int`](https://docs.microsoft.com/en-us/dotnet/api/system.int32?view=net-6.0) when this type is used in methods which expect an `int`.

## Methods
There are no additional methods implemented on this type but you are of course able to use any standard methods and extensions which are available on the `double` type.

```csharp
var myNumber = -58.0;
if(double.IsNegative(myNumber))
{
    myNumber = Math.Abs(myNumber); // Make number positive if -ve
}
```
