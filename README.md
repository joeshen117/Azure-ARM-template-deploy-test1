# Logic App backuper - Find correlations between Logic Apps, API connections and On-premises Data Gateways

<!-- ### Backup your Logic App Integrations - Automatically backup your Logic Apps, API connections and On-premises Data Gateway correlations  with Logic App itself. -->


[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjoeshen117%2FAzure-ARM-template-deploy-test1%2Fmain%2Ftemplate.json)


This template deploys a SaaS solution to backup all your Logic App related resources information utilizing a Logic App and an Integration account:

- A Logic apps which extracts the resources information via API requests and map the correlation between Logic Apps, API connection resources and On-premises Data Gateways.

- A free tier Integration to enable Inline JavaScript code action in the Logic App.


**Important**: This template creates multiple Azure resources, which may incur costs. For more information, see [Azure Logic Apps pricing](https://azure.microsoft.com/pricing/details/logic-apps/) and [Pricing and billing models for Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-pricing).

`Tags: Logic Apps, Integration Account, API connections, On-premises Data Gateways`


## Prerequisites

  - An Azure account and subscription. If you don't have a subscription, [Sign up for a free Azure account](https://azure.microsoft.com/free/).

  - A resource group which the Logic App and the Integration Account will be deployed into. **(Please make sure there is no existing free tier Integration Account in this resource group.)**

  - Make sure the account which you are using to for deployment has the permissions to add role assignments on a subscription scope.

## Deployment steps

1. Click the **Deploy to Azure** button at the top of this page, and then put in the parameter values in the opened broswer page.

2. Navigate to the **Identity** blade and Add a role assignment to the new Logic App with System Managed Identity.
   
   ![Move-to-identity](https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/Add-role-assignment.png?raw=true | width=500)

3. Assign a **Reader** role to the Logic App on a subscription scope. 
   
   ![add-role-assignment](https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/new-role-assignment.png?raw=true | width=500)

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

   ![Create CSV and send email](https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/send-email.png?raw=true | width=500)

- #### **Format the data into csv file and store it to a blob storage**
  Add a ***Create CSV table*** action and a ***Create blob*** action to backup the correlation csv file to a blob storage container.

  ![Create CSV and save to blob](https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/save-to-blob.png?raw=true | width=500)

- #### **Put the data in a SQL DB**
  Use a ***For each*** loop and a ***Insert row*** action to populate the data into a Azure SQL database table. 

  ![Save to SQL](https://github.com/joeshen117/Azure-ARM-template-deploy-test1/blob/main/images/insert-to-sql.png?raw=true | width=500)

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
<!-- * [B2B Processing capabilities in Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-enterprise-integration-overview) -->

<!-- 1. Add data delivery actions with you own choice.
   1. s
   2. s
   3. s
   4. s
      1. s
      2. s
      3. s
      4. s
2. WTFF

## In-depth drill through -->
<!-- ## Usage

To test your logic apps after deployment completes, you can perform these steps:

1. In the Azure portal, open the resource group page that shows where you deployed all the resources.

   ![Screenshot that shows Azure resources](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-logic-app-as2-send-receive/images/azure-resources.png "Azure resources")

   The logic apps, FabrikamSales-AS2Send and Contoso-Receive, show the sync send receive scenario. 
  
1. Open the logic app for FabrikamSales-AS2Send. On the logic app's **Overview** page, and select **Run Trigger**.

   ![Screenshot that shows FabrikamSales-AS2Send logic app](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-logic-app-as2-send-receive/images/fabrikamsales-as2send.png "Run FabrikamSales-AS2Send Logic App")

1. On the **Overview** page, you can also review the run history, inputs, and outputs for each action in these logic apps:

   ![Screenshot that shows Contoso-AS2Receive run history](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-logic-app-as2-send-receive/images/contoso-as2receive-runhistory.png "Contoso-AS2Receive run history")

   The logic apps, FabrikamFinance-AS2Send and Contoso-Receive, show the async send receive scenario.
   
1. Open the logic app for FabrikamFinance-AS2Send. On the logic app's **Overview** page, and select **Run Trigger**.

   The async MDN is received by the logic app, FabrikamFinance-AS2ReceiveMDN.

   ![Screenshot that shows FabrikamFinance-AS2ReceiveMDN run history](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-logic-app-as2-send-receive/images/fabrikamfinance-as2receivemdn-runhistory.png "FabrikamFinance-AS2ReceiveMDN run history")

1. Again, you can review the run history, inputs, and outputs for each action in these logic apps.

**Important**: The logic apps, FabrikamSales-AS2Send and FabrikamFinance-AS2Send, start with a Recurrence trigger that runs every hour. To run the logic apps more or less often, you can change the trigger's frequency and interval as appropriate by using the Logic App Designer.

## Next steps

Learn more about Azure Logic Apps:

* [Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-overview)
* [B2B Processing capabilities in Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-enterprise-integration-overview) -->
