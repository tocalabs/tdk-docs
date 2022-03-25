# Using External Packages in Actions

If an action you are developing relies on a third party package then you can add it to your code via the Packages tab at the top of the TDK.

![Packages Tab](../../../assets/packages_tab.png)

Once you have selected the Packages tab you can see a list of your installed Packages for the current action:

![Installed Packages](../../../assets/installed_packages.png)

You can also search for and install new packages that are required for the action by selecting the Package Search tab.

![Package Search](../../../assets/package_search.png)

From the Package Search tab you can simply select the version of the package you require and then tick the checkbox alongside it to include within your action.


As discussed in the Usings section of the [Code](code.md) page you cannot declare any `using` statements in an action, so when you write any code which utilises a nuget package, you must fully qualify the namespace of each method/class/struct etc. you use from the package.

For example the below excerpt is taken from the Azure Blob Download action and you can see how any usage of the:
```csharp
var urlConstructor = $"https://{accountName}.blob.core.windows.net/{sasToken}";
var uri = new Uri(urlConstructor);
var uriBuilder = new Azure.Storage.Blobs.BlobUriBuilder(uri);
blobServiceClient = new Azure.Storage.Blobs.BlobServiceClient(uriBuilder.ToUri());
```

You'll notice we don't have to do the same thing when instantiating the `Uri` class above, this is because the `Uri` class lives within the `System` namespace which is included by default in all actions.

  > **Note:** You cannot currently add custom Nuget package sources to the TDK. All Nuget packages that you wish to add _must_ come from [nuget.org](https://www.nuget.org). This is something we plan to resolve in the future.
