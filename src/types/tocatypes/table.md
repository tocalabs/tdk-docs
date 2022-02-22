# Table

## Definition
The `Table` type is used to represent a table of data. Under the hood this is defined as the `DataContext` class. The `DataContext` class holds all the table data but when an action defines a table as an input, an instance of the `DataTableHelper` gets constructed using the `DataContext` object. This means your table input will actually be an instance of the `DataTableHelper` class.

`DataTableHelper` is a wrapper class for the data which is represented by the `DataContext` class. The `DataTableHelper` class provides many methods which allow you to easily access and manipulate the data.

> N.B. You'll always receive a `DataTableHelper` as an input to an action, but when you return a table as a result you need to return an instance of the `DataContext` class as this is the object that actually stores the data. You can do this by calling `dataTableHelper.GetDataContext()`.


```csharp
public class DataTableHelper
{
    private DataContext DataContext { get; }
}

public class DataContext
{
    public string Name { get; set; }
    public List<TableHeader> Headers { get; set; } = new();
    public List<DataContextRow> Rows { get; set; } = new();
}

public class TableHeader
{
    public string Uid { get; set; }
    public string Name { get; set; }
    public string Type { get; set; }
}

public class DataContextRow
{
    public string Uid = Guid.NewGuid().ToString();
    public double Index { get; set; }
    public List<DataContextRecord> Records { get; set; } = new List<DataContextRecord>();
}

public class DataContextRecord
{
    public string Uid = Guid.NewGuid().ToString();
    public TableHeader Heading { get; set; }
    public double ColumnIndex { get; set; }
    public double RowIndex { get; set; }
    public string Type { get; set; }
    public string Value { get; set; }
}

```

## Methods

There are lots of methods defined on the various types defined above to make working with this type easy and ergonomic.


<details>
<summary>DataTableHelper Methods</summary>

```csharp
class DataTableHelper
{
    /// <summary>
    ///     Add header to a column, if index is null it will update 
    ///     the last column
    /// </summary>
    List<TableHeader> AddHeader(string header, string type, int? index = null);
    
    /// <summary>
    ///     Replace header in a column, specify the column using either the
    ///     header name or uid of the header
    /// </summary>
    List<TableHeader> ReplaceHeader(string newHeader, string header = null, string uid = null);
    
    /// <summary>
    ///     Remove the header specified by name, only works if there
    ///     are no cells under this header
    /// </summary>
    List<TableHeader> RemoveHeader(string header);
    
    /// <summary>
    ///     Retrieve the data context
    /// </summary>
    DataContext GetDataContext() => DataContext;
    
    /// <summary>
    ///     Return the serialized data context
    /// </summary>
    string SerializeDataContext() => DataContext.Serialize();
    
    /// <summary>
    ///     Replace all existing headers with new ones
    /// </summary>
    DataContext UpdateHeaders(List<string> newHeaders);
    
    /// <summary>
    ///     Add column to the data table at the specified index.
    ///     A column is simply a List type
    /// </summary>
    DataContext AddColumn(List<Parameter> column, int index, string columnName);
    
    /// <summary>
    ///     Create a row in the data table, if index is null
    ///     then add row to end of table
    /// </summary>
    List<DataContextRow> AddRow(DataContextRow row, int? index = null);
    
    /// <summary>
    ///     Remove a row from the data table by index
    /// </summary>
    List<DataContextRow> RemoveRow(int index);
}
```
</details>
