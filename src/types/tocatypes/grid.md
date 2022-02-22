# Grid

## Defintion

The `Grid` type is used for defining a table like structure over a 2 dimensional space. This is used in actions such as Image Grid, OCR Grid and Grid to Table.

```csharp
public class GridArray
{
    public string Key { get; set; }
    public double Column { get; set; }
    public double Row { get; set; }
    public BoundingBox CellBox { get; set; }
}

public class Grid
{
    public Coordinates Position { get; set; }
    public List<GridArray> GridArray { get; set; }
}

```
- `Grid.Position` represents the top left hand corner of the Grid
- `Grid.GridArray` is the list of cells in the grid
- `Grid.GridArray.Key` is a unique identifier for that particular grid cell
- `Grid.GridArray.Column` is the column index of the current cell. Index starts at 0 and moves left to right
- `Grid.GridArray.Row` is the row index of the current cell. Index starts at 0 and moves top to bottom
- `Grid.GridArray.CellBox` represents the region covered by the current cell

 > Note: This type should always be accessed through the `Grid` class, don't use the `GridArray` class in isolation.

## Methods
There are no additional methods defined for the `Grid` or `GridArray` class.
