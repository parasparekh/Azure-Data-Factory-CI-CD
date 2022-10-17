**Azure Data Factory CI/CD Lab prerequisites**

To have a successful experience for the Azure Data Factory CI/CD lab, please ensure that you meet the following pre-requisites:

one for Dev and one for Prod as the lab demonstrates deployment from Dev to Production.  

1. **Azure subscription** - Use your own internal subscription to create all resources
2. **Create Resource Groups** - Reference Link [Create Resource Group](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal#create-resource-groups) <br />

	* Create two Resource Groups (one for Dev and one for Prod) with the following naming convention (do not forget to use your alias):<br />
		 + {youralias}-dev-rg  <br />
		 + {youralias}-prod-rg <br />
	* Choose the region that is most appropriate to your current location.
	
3. **Deploy resources in Dev Resource Group** - In this repo, go to Azure-Data-Factory-CI-CD/ARMTemplates/Dev/MainARMTemplate.json
![Deploy to Azure](https://aka.ms/deploytoazurebutton)
7. **Create Secrets in Azure Key Vaults** - Here, we will create two secrets, one to store ADLS credential and one to store Azure SQL DB connection string.
	
	* **Dev Environment** - <br />
		 **ADLS Secret**
		+ To get connection string for storage account - Go to dev storage account created above, select Access Keys under Security + networking, click on show next to Connection string and copy the value.
		+ Go to dev azure key vault created above and select secrets under Objects. Click on Generate/Import
		+ Name - adlscredential
		+ Secret Value - Paste the connection string value copied above and click on create. <br />
	
		**Azure SQL DB Secret**
		+ To get connection string for SQL DB - Go to dev SQL DB created above, select Connection strings under Settings and copy ADO.NET (Active Directory integrated authentication) value. Replace {your_username} with your user ID
		+ Go to dev azure key vault created above and select secrets under Objects. Click on Generate/Import
		+ Name - sqlconnectionstring
		+ Secret Value - Paste the connection string value copied above and click on create.

	* **Prod Environment** - <br />
		 **ADLS Secret**
		+ To get connection string for storage account - Go to prod storage account created above, select Access Keys under Security + networking, click on show next to Connection string and copy the value.
		+ Go to prod azure key vault created above and select secrets under Objects. Click on Generate/Import
		+ Name - adlscredential
		+ Secret Value - Paste the connection string value copied above and click on create.<br />
		
		**Azure SQL DB Secret**
		+ To get connection string for SQL DB - Go to prod SQL DB created above, select Connection strings under Settings and copy ADO.NET (Active Directory integrated authentication) value. Replace {your_username} with your user ID
		+ Go to prod azure key vault created above and select secrets under Objects. Click on Generate/Import
		+ Name - sqlconnectionstring
		+ Secret Value - Paste the connection string value copied above and click on create. <br />
		
ADF should have access to Azure Key Vault to retrieve the secret value - Go to Access policies in Dev Key Vault and select create. Select All under Key and secret permissions and click on Next. Search for Dev ADF name and select it. Click Next and create. <br />

+ Repeat the same process to provide Prod ADF access to Prod Key Vault.<br />
	
If you do not have the required permissions to fulfil these pre-requisites or need assistance, please e-mail swmannepalli@microsoft.com to ensure a successful lab experience.