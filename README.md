# Logic App backuper

## Backup your Logic App Integrations - Automatically backup your Logic Apps, API connections and On-premises Data Gateway correlations  with Logic App itself.


[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjoeshen117%2FAzure-ARM-template-deploy-test1%2Fmain%2Ftemplate.json)


This template creates an SaaS solution to backup all your Logic App resources using a Logic App and an Integration account:

- A Logic apps which extracts the resources information and map the correalation between Logic Apps, API connection resrouces and On-premises Data Gateways.

- An Integration accounts in free tier sku to enable Inline Javascript code action in the Logic App.


**Important**: This template creates mutiple Azure resources, which incur costs. For more information, see [Azure Logic Apps pricing](https://azure.microsoft.com/pricing/details/logic-apps/) and [Pricing and billing models for Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-pricing).

`Tags: Logic Apps, Integration Account, API connections, On-premises Data Gateways`

## Deployment steps

Click the **Deploy to Azure** button at the top of this page, and then put in the parameter values in the opened broswer page.

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
