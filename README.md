# Logic App backuper - Find correlations between Logic Apps, API connections and On-premises Data Gateways



[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjoeshen117%2FAzure-ARM-template-deploy-test1%2Fmain%2Ftemplate.json)


This template deploys a SaaS solution to backup all your Logic App related resources information utilizing a Logic App and an Integration account:

- A Logic apps which extracts the resource information via API requests and map the correlations between Logic Apps, API connection resources and On-premises Data Gateways.

- A free tier Integration Account to enable Inline JavaScript code action in the Logic App.


**Important**: This template creates multiple Azure resources, which may incur costs. For more information, see [Azure Logic Apps pricing](https://azure.microsoft.com/pricing/details/logic-apps/) and [Pricing and billing models for Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-pricing).

`Tags: Logic Apps, Integration Account, API connections, On-premises Data Gateways`


## Prerequisites

  - An Azure account and subscription. If you don't have a subscription, [Sign up for a free Azure account](https://azure.microsoft.com/free/).

  - A resource group which the Logic App and the Integration Account will be deployed into. **(Please make sure there is no existing free tier Integration Account in this resource group.)**

  - Make sure the account which you are using to for deployment has the permissions to add role assignments on a subscription scope.

## Deployment steps

1. Click the **Deploy to Azure** button at the top of this page, and then put in the parameter values in the opened broswer page.

2. Navigate to the **Identity** blade and Add a role assignment to the new Logic App with System Managed Identity.
   
   <img src="https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/Add-role-assignment.png?raw=true" width="700">

3. Assign a **Reader** role to the Logic App on a subscription scope. 
   
    <img src="https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/new-role-assignment.png?raw=true" width="700">

## Data delivery options

With the pre-built definitions, the deployed Logic App is capable of retrieve and process the correlations into following format.


```json
[
   ...
   {
      LogicApp:"/subscriptions/<subId>/resourceGroups/<resourceGroup>/providers/Microsoft.Logic/workflows/<flowName>",
      Connection:"/subscriptions/<subId>/resourceGroups/<resourceGroup>/providers/Microsoft.Web/connections/<connectionName>",
      Gateway:"/subscriptions/<subId>/resourceGroups/<resourceGroup>/providers/Microsoft.Web/connectionGateways/<gatewayName>"
   }
   ...
]

```

Using the data structure of the output from **"Execute JavaScript code"** action, we have many options to deliver the information to a destination system.

- #### **Send out correlation information in a csv file via email**
  Add a ***Create CSV table*** action and a ***Send an email (V2)*** action to send the formatted data to an inbox periodically.

   <img src="https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/send-email.png?raw=true" width="700">

- #### **Format the data into csv file and store it to a blob storage**
  Add a ***Create CSV table*** action and a ***Create blob*** action to backup the correlation csv file to a blob storage container.

  <img src="https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/save-to-blob.png?raw=true" width="700">

- #### **Put the data in a SQL DB**
  Use a ***For each*** loop and a ***Insert row*** action to populate the data into a Azure SQL database table. 

  <img src="https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/insert-to-sql.png?raw=true" width="700">

  **Import**: Please make sure you have created suitable table with 3 columns in type of CHAR to store the extracted data.

## Data processing principal

- Logic Apps with two or more API connections will be processed into mutiple records.

   ```json
   [
      ...
      {
         LogicApp:"LogicApp1",
         Connection:"Connection1",
         Gateway:"Gateway1"
      },
      {
         LogicApp:"LogicApp1",
         Connection:"Connection2",
         Gateway:null
      }
      ...
   ]

   ```
- Orpahn API connections will be recorded with **null** Logic App property.
   ```json
   [
      ...
      {
         LogicApp:null,
         Connection:"OrphanConnection1",
         Gateway:"Gateway1"
      },
      {
         LogicApp:null,
         Connection:"OrphanConnection2",
         Gateway:null
      }
      ...
   ]

   ```

## Next step
For detailed walkthrough on the Logic App structure and the methodlogy used for data processing. Please visit [my blog](https://google.com) here.

In the upcoming series, we will talk about how to retrieve Logic App information accross subscriptions and backup all correlations for disaster recovery solution.

Learn more about Azure Logic Apps:

* [Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-overview)