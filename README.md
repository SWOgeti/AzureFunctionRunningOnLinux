# AzureFunctionRunningOnLinux
Example of an Azure function running on Linux executing a Java based executable.

Steps to create Azure Function with Azure Functions Core Tools: https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local#v2
1.  func init LinuxAzureFunction
2.  cd LinuxAzureFunction
3.  replace host.json contents with:
		{
			"version": "2.0",
			"extensionBundle": {
				"id": "Microsoft.Azure.Functions.ExtensionBundle",
				"version": "[1.*, 2.0.0)"
			}
		}
4.  func new --name RunJarOnDemand --template "HttpTrigger"
5.  func start --build

Function is now running on:  http://localhost:7071/api/RunJarOnDemand

To call it, add Name query string parameter: http://localhost:7071/api/RunJarOnDemand?name=Michael

Steps to deploy Azure Function with Azure CLI:  https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest
1.  az login
2.  az group create --name RunJarInAzure --location EastUS
3.  az storage account create --name runjarstorageaccount --location NorthCentralUS --resource-group RunJarInAzure --sku Standard_LRS
4.  az functionapp create --resource-group RunJarInAzure --consumption-plan-location EastUS --os-type Linux --name LinuxAzureFunction --storage-account runjarstorageaccount --runtime dotnet

Now the Azure Assets exist as expected.

Steps to deploy Function App to Azure Asset:
1.  az login
2.  func azure functionapp publish LinuxAzureFunction


