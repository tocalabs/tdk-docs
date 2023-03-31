
# Table Helper
 
The Table Helper is designed to aid interactions with the DataSources which exist as part of the Toca platform.

The source code is accessible via the TDK: https://ui-tdk.**[TOCA_INSTANCE]**.toca.cloud/editors/helper/643dadea-9f1f-4b45-98c2-788d92d11733/68d45f9b-c7ba-40aa-828a-9d8b7b01187f.

## Getting Data

To get data, you must:

1. Build the query
2. Execute the query
3. Interrogate the results

### 1. Build the query

```
    var query = TableHelper.GetNewQuery(); 

    query.TableName = configurationTableId.ToString(); // The ID (not name) of the table to query. Can be accessed by a text input, limited to type "TableV3"
    query.RunId = RunId; // Included as default variable in the Action
    query.QueryString = $"[{{\"field\":\"{FIELD_NAME}\",\"operator\":\"=\",\"value\":\"{QUERY_VALUE}\"}}]"; // Stringified JSON
    query.IncludeRowCount = true; // Good for checking if we get results returned
```

### 2. Execute the query

Pass the _Table ID_ and _query_ to the TableHelper.GetData call
```
    var result = await TableHelper.GetData(configurationTableId, query, Action.Token).ConfigureAwait(false);
```

### 3. Interrogate the results

The Query returns `List<RecordValuesModel>`

Each `RecordValuesModel` has a property `RecordValue` which is a Dictionary of the query results.

You can either add this to the Results list:
```
    AddResult("table", result, ActionTypes.TableV3);
```

or interrogate the List/Dictionary to grab specific data:
```
    var value = result.Values.First().RecordValue["FIELD_NAME"]
    AddResult("FIELD_NAME", value, ActionTypes.String);
```            