---
sort: 2
---

## Deploy Azure Services
In this section you will use automated deployment and ARM templates to automate the deployment of all Azure Data Services.

1. You can deploy all Azure services required by clicking the **Deploy to Azure** button below. 

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2Fazure-data-services-go-fast-codebase%2Fmain%2FDeploy%2Fazuredeploy.json)

[![Visualize](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.svg?sanitize=true)](http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2Fazure-data-services-go-fast-codebase%2Fmain%2FDeploy%2Fazuredeploy.json)

2. You will be directed to the Azure portal to deploy the ADS Go Fast ARM template from this repository. On the **Custom deployment** blade, enter the following details:


3. On the **Custom deployment** blade, enter the following details:
    <br>- **Subscription**: [your Azure subscription]
    <br>- **Resource group**: [you can select a existing Resource Group or create a new Resource Group]

    Please review the Terms and Conditions and check the box to indicate that you agree with them.

4. Click **Purchase**

![](../deploy/Media/Lab0-Image10.png)

5. Navigate to your resource group to monitor the progress of your ARM template deployment. A successful deployment should last less than 10 minutes.

    ![](../deploy/Media/Lab0-Image11.png)

5. Once your deployment is complete you are ready to start deploying the solution. Enjoy!

    ![](../deploy/Media/Lab0-Image09.png)