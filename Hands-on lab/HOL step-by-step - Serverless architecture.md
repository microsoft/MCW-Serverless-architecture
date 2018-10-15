![](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Serverless architecture
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
June 2018
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2018 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Serverless architecture](#serverless-architecture)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Overview](#overview)
  - [Solution architecture](#solution-architecture)
  - [Requirements](#requirements)
  - [Exercise 1: Azure data, storage, and serverless environment setup](#exercise-1-azure-data-storage-and-serverless-environment-setup)
    - [Help references](#help-references)
    - [Task 1: Provision the storage account](#task-1-provision-the-storage-account)
    - [Task 2: Provision the Function Apps](#task-2-provision-the-function-apps)
    - [Task 3: Provision the Event Grid topic](#task-3-provision-the-event-grid-topic)
    - [Task 4: Provision the Azure Cosmos DB account](#task-4-provision-the-azure-cosmos-db-account)
    - [Task 5: Provision the Computer Vision API service](#task-5-provision-the-computer-vision-api-service)
  - [Exercise 2: Develop and publish the photo processing and data export functions](#exercise-2-develop-and-publish-the-photo-processing-and-data-export-functions)
    - [Help references](#help-references-1)
    - [Task 1: Configure application settings](#task-1-configure-application-settings)
    - [Task 2: Finish the ProcessImage function](#task-2-finish-the-processimage-function)
    - [Task 3: Publish the Function App from Visual Studio](#task-3-publish-the-function-app-from-visual-studio)
  - [Exercise 3: Create functions in the portal](#exercise-3-create-functions-in-the-portal)
    - [Help references](#help-references-2)
    - [Task 1: Create function to save license plate data to Azure Cosmos DB](#task-1-create-function-to-save-license-plate-data-to-azure-cosmos-db)
    - [Task 2: Add an Event Grid subscription to the SavePlateData function](#task-2-add-an-event-grid-subscription-to-the-saveplatedata-function)
    - [Task 3: Add an Azure Cosmos DB output to the SavePlateData function](#task-3-add-an-azure-cosmos-db-output-to-the-saveplatedata-function)
    - [Task 4: Create function to save manual verification info to Azure Cosmos DB](#task-4-create-function-to-save-manual-verification-info-to-azure-cosmos-db)
    - [Task 5: Add an Event Grid subscription to the QueuePlateForManualCheckup function](#task-5-add-an-event-grid-subscription-to-the-queueplateformanualcheckup-function)
    - [Task 6: Add an Azure Cosmos DB output to the QueuePlateForManualCheckup function](#task-6-add-an-azure-cosmos-db-output-to-the-queueplateformanualcheckup-function)
    - [Task 7: Configure custom event types for the new Event Grid subscriptions](#task-7-configure-custom-event-types-for-the-new-event-grid-subscriptions)
  - [Exercise 4: Monitor your functions with Application Insights](#exercise-4-monitor-your-functions-with-application-insights)
    - [Help references](#help-references-3)
    - [Task 1: Provision an Application Insights instance](#task-1-provision-an-application-insights-instance)
    - [Task 2: Enable Application Insights integration in your Function Apps](#task-2-enable-application-insights-integration-in-your-function-apps)
    - [Task 3: Use the Live Metrics Stream to monitor functions in real time](#task-3-use-the-live-metrics-stream-to-monitor-functions-in-real-time)
    - [Task 4: Observe your functions dynamically scaling when resource-constrained](#task-4-observe-your-functions-dynamically-scaling-when-resource-constrained)
  - [Exercise 5: Explore your data in Azure Cosmos DB](#exercise-5-explore-your-data-in-azure-cosmos-db)
    - [Help references](#help-references-4)
    - [Task 1: Use the Azure Cosmos DB Data Explorer](#task-1-use-the-azure-cosmos-db-data-explorer)
  - [Exercise 6: Create the data export workflow](#exercise-6-create-the-data-export-workflow)
    - [Help references](#help-references-5)
    - [Task 1: Create the Logic App](#task-1-create-the-logic-app)
  - [Exercise 7: Configure continuous deployment for your Function App](#exercise-7-configure-continuous-deployment-for-your-function-app)
    - [Help references](#help-references-6)
    - [Task 1: Create a GitHub repository](#task-1-create-a-github-repository)
    - [Task 2: Add GitHub repository to your Visual Studio solution](#task-2-add-github-repository-to-your-visual-studio-solution)
    - [Task 3: Configure your Function App to use your GitHub repository for continuous deployment](#task-3-configure-your-function-app-to-use-your-github-repository-for-continuous-deployment)
    - [Task 4: Finish your ExportLicensePlates function code and push changes to GitHub to trigger deployment](#task-4-finish-your-exportlicenseplates-function-code-and-push-changes-to-github-to-trigger-deployment)
  - [Exercise 8: Rerun the workflow and verify data export](#exercise-8-rerun-the-workflow-and-verify-data-export)
    - [Task 1: Run the Logic App](#task-1-run-the-logic-app)
    - [Task 2: View the exported CSV file](#task-2-view-the-exported-csv-file)
  - [After the hands-on lab](#after-the-hands-on-lab)
    - [Task 1: Delete the resource group in which you placed your Azure resources.](#task-1-delete-the-resource-group-in-which-you-placed-your-azure-resources)

<!-- /TOC -->

## Abstract and learning objectives

In this hand-on lab, you will be challenged to implement an end-to-end scenario using a supplied sample that is based on Microsoft Azure Functions, Azure Cosmos DB, Event Grid, and related services. The scenario will include implementing compute, storage, workflows, and monitoring, using various components of Microsoft Azure. The hands-on lab can be implemented on your own, but it is highly recommended to pair up with other members at the lab to model a real-world experience and to allow each member to share their expertise for the overall solution.

At the end of the hands-on-lab, you will have confidence in designing, developing, and monitoring a serverless solution that is resilient, scalable, and cost-effective.

## Overview

Contoso, ltd. is rapidly expanding their toll booth management business to operate in a much larger area. As this is not their primary business, which is online payment services, they are struggling with scaling up to meet the upcoming demand to extract license plate information from a large number of new tollbooths, using photos of vehicles uploaded to cloud storage. Currently, they have a manual process where they send batches of photos to a 3rd-party who manually transcodes the license plates to CSV files that they send back to Contoso to upload to their online processing system. They want to automate this process in a way that is cost effective and scalable. They believe serverless is the best route for them, but do not have the expertise to build the solution.

## Solution architecture

Below is a diagram of the solution architecture you will build in this lab. Please study this carefully, so you understand the whole of the solution as you are working on the various components.

![The Solution diagram is described in the text following this diagram.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image2.png 'Solution diagram')

The solution begins with vehicle photos being uploaded to an Azure Storage blobs container, as they are captured. A blob storage trigger fires on each image upload, executing the photo processing **Azure Function** endpoint (on the side of the diagram), which in turn sends the photo to the **Cognitive Services Computer Vision API OCR** service to extract the license plate data. If processing was successful and the license plate number was returned, the function submits a new Event Grid event, along with the data, to an Event Grid topic with an event type called "savePlateData". However, if the processing was unsuccessful, the function submits an Event Grid event to the topic with an event type called "queuePlateForManualCheckup". Two separate functions are configured to trigger when new events are added to the Event Grid topic, each filtering on a specific event type, both saving the relevant data to the appropriate **Azure Cosmos DB** collection for the outcome, using the Cosmos DB output binding. A **Logic App** that runs on a 15-minute interval executes an Azure Function via its HTTP trigger, which is responsible for obtaining new license plate data from Cosmos DB and exporting it to a new CSV file saved to Blob storage. If no new license plate records are found to export, the Logic App sends an email notification to the Customer Service department via their Office 365 subscription. **Application Insights** is used to monitor all of the Azure Functions in real-time as data is being processed through the serverless architecture. This real-time monitoring allows you to observe dynamic scaling first-hand and configure alerts when certain events take place.

## Requirements

1.  Microsoft Azure subscription (non-Microsoft subscription)

2.  Local machine or a virtual machine configured with (**complete the day before the lab!**):

    a. Visual Studio Community 2017 or greater, **version 15.4** or later

      1. <https://www.visualstudio.com/vs/>

    b. Azure development workload for Visual Studio 2017

      1. <https://docs.microsoft.com/azure/azure-functions/functions-develop-vs#prerequisites>

    c. .NET Framework 4.7 runtime (or higher)

      1. <https://www.microsoft.com/net/download/windows>

3.  Office 365 account. If required, you can sign up for an Office 365 trial at:

    a. <https://portal.office.com/Signup/MainSignup15.aspx?Dap=False&QuoteId=79a957e9-ad59-4d82-b787-a46955934171&ali=1>

4.  GitHub account. You can create a free account at <https://github.com>.

5.  Follow all the steps provided in [Before the Hands-on Lab](Before%20the%20HOL%20-%20Serverless%20architecture.md)

## Exercise 1: Azure data, storage, and serverless environment setup

**Duration**: 30 minutes

You must provision a few resources in Azure before you start developing the solution. Ensure all resources use the same resource group for easier cleanup.

In this exercise, you will provision a blob storage account using the Hot tier, and create two containers within to store uploaded photos and exported CSV files. You will then provision two Function Apps instances, one you will deploy from Visual Studio, and the other you will manage using the Azure portal. Next, you will create a new Event Grid topic. After that, you will create an Azure Cosmos DB account with two collections. Finally, you will provision a new Cognitive Services Computer Vision API service for applying object character recognition (OCR) on the license plates.

### Help references

|                                            |                                                                                                                                                             |
| ------------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------: |
| **Description**                            |                                                                          **Links**                                                                          |
| Creating a storage account (blob hot tier) | <https://docs.microsoft.com/en-us/azure/storage/common/storage-create-storage-account?toc=%2fazure%2fstorage%2fblobs%2ftoc.json%23create-a-storage-account> |
| Creating a function app                    |                   <https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function%23create-a-function-app>                    |
| Concepts in Event Grid                     |                                                <https://docs.microsoft.com/en-us/azure/event-grid/concepts>                                                 |
| Creating an Azure Cosmos DB account        |                   <https://docs.microsoft.com/en-us/azure/cosmos-db/tutorial-develop-sql-api-dotnet%23create-an-azure-cosmos-db-account>                    |

### Task 1: Provision the storage account

1.  Using a new tab or instance of your browser, navigate to the Azure Management portal, <http://portal.azure.com>

2.  Select **+New, Storage, Storage account -- blob, file, table, queue**

    ![In the menu pane of Azure Portal, New is selected. Under Azure Marketplace, Storage is selected, and under Featured, Storage account - blob, file, table, queue is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image11.png 'Azure Portal')

3.  On the **Create storage account** blade, specify the following configuration options:

    a. **Name**: enter a unique value for the storage account (ensure the green check mark appears)

    b. Select **Blob storage** as the account kind

    c. Select the **Hot** access tier

    d. For **Resource group**, select the **Use existing** radio button, and specify the **ServerlessArchitecture** resource group

    e. Ensure the **Location** is the same region as the resource group

    ![Fields in the Create storage account blade are set to the previously defined values.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image12.png 'Create strorage account blade')

4.  Select **Create**

    ![Screenshot of the Create button.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image13.png 'Create button')

5.  After the storage account has completed provisioning, open the storage account by opening the **ServerlessArchitecture** resource group, and then selecting the **storage account** name

    ![In the ServerlessArchitecture blade, Overview is selected. Under Name, the tollbooth storage account is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image14.png 'ServerlessArchitecture blade')

6.  On the **Storage account** blade, select **Access Keys**, under Settings in the menu. Then on the **Access keys** blade, select the **Click to copy** button for **key1 connection string.**

    ![In the Storage account blade, under Settings, Access keys is selected. Under Default keys, the copy button next to the key1 connection string is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image15.png 'Storage account blade')

7.  Paste the value into a text editor, such as Notepad, for later reference

8.  Select **Containers** under **Blob Service** in the menu. Then on the **Containers** blade, select the **+ Container** button to add a new container. In the **Name** field, enter **images**, select **Private** for the public access level, then select **OK** to save.

    ![In the Storage blade, under Settings, Containers is selected. In the Containers blade, the + (add icon) Container button is selected. Below, the Name field displays images, and the Public access level is set to Private (no anonymous access). ](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image16.png 'Storage and Containers blades')

9.  Repeat these steps to create a container named **export**

### Task 2: Provision the Function Apps

1.  Navigate to the Azure Management portal, <http://portal.azure.com>

2.  Select **+ New**, then enter **function** into the search box on top. Select **Function App** from the results.

    ![In the menu pane of the Azure Portal, the New button is selected. Function is typed in the search field, and Function App is selected from the search results.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image17.png 'Azure Portal')

3.  Select the **Create** button on the **Function App overview** blade

4.  On the **Create Function App** blade, specify the following configuration options:

    a. **Name**: unique value for the App name (ensure the green check mark appears). Provide a name similar to TollBooth**Events**.

    b. Specify the **Resource Group** ServerlessArchitecture

    c. Select the **Consumption Plan** Hosting Plan

    d. Select the same **location** as your Resource Group

    e. Leave the **storage** option as **create new**

    f. Ensure **Off** is selected for **Application Insights** (we'll add this later)

    ![Fields in the Function App blade are set to the previously defined settings.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image18.png 'Function App blade')

5.  Select **Create**

    ![Screenshot of the Create button.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image13.png 'Create button')

6.  **Repeat steps 1-5** to create a second Function App, named TollBooth**FunctionApp** or similar

### Task 3: Provision the Event Grid topic

1.  Navigate to the Azure Management portal, <http://portal.azure.com>

2.  Select **+ New**, then enter **event grid** into the search box on top. Select **Event Grid Topic** from the results.

    ![In the menu pane of the Azure Portal, the New button is selected. Event grid is typed in the search field, and Event Grid Topic is selected from the search results.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image19.png 'Azure Portal')

3.  Select the **Create** button on the **Event Grid Topic overview** blade

4.  On the **Create Topic** blade, specify the following configuration options:

    a. **Name:** unique value for the App name (ensure the green check mark appears)

    b. Specify the **Resource Group** ServerlessArchitecture

    c. Select the same **location** as your Resource Group

    ![In the Create Topic blade, the Name field is TollBoothTopic, Resource Group is using existing ServerlessArchitecture, and the location is West US 2.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image20.png 'Create Topic blade')

5.  Select **Create**

    ![Screenshot of the Create button.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image13.png 'Create button')

6.  After the Event Grid topic has completed provisioning, open the account by opening the **ServerlessArchitecture** resource group, and then selecting the **Event Grid** topic name

7.  Select **Overview** in the menu, and then copy the **Topic Endpoint** value

    ![In the TollBoothTopic blade, Overview is selected, and the copy button next to the Topic Endpoint is called out.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image21.png 'TollBoothTopic blade')

8.  Select **Access Keys** under Settings in the menu

9.  Within the **Access Keys** blade, copy the **Key 1** value

    ![In the TollBoothTopic - Access keys, under Settings, Access keys is selected. The copy button next to the Key 1 access key is also selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image22.png 'TollBoothTopic - Access keys blade')

10. Paste the values into a text editor, such as Notepad, for later reference.

### Task 4: Provision the Azure Cosmos DB account

1.  Navigate to the Azure Management portal, <http://portal.azure.com>

2.  Select **+ New, Databases, Azure Cosmos DB**

    ![In Azure Portal, in the menu, New is selected. Under Azure marketplace, Databases is selected, and under Featured, Azure Cosmos DB is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image23.png 'Azure Portal')

3.  On the **Create new Azure Cosmos DB** **account** blade, specify the following configuration options:

    a. **Name**: unique value for the App name (ensure the green check mark appears)

    b. Select the **SQL** **API**

    c. Specify the **Resource Group** ServerlessArchitecture

    d. Select the same **location** as your Resource Group if available. Otherwise, select the next closest **region**

    e. Check **geo-redundancy**

    ![Fields in the Azure Cosmos DB blade are set to the previously defined settings.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image24.png 'Azure Cosmos DB blade')

4.  Select **Create**

    ![Screenshot of the Create button.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image13.png 'Create button')

5.  After the Azure Cosmos DB account has completed provisioning, open the account by opening the **ServerlessArchitecture** resource group, and then selecting the **Azure Cosmos DB** account name

6.  On the **Cosmos DB overview** blade, select **+ Add Collection**

    ![In the Tollbooths blade, Overview is selected, and the Add Collection button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image25.png 'Tollbooths blade')

7.  On the **Add Collection** blade, specify the following configuration options:

    a. Enter **LicensePlates** for the **database id**

    b. Enter **Processed** for the **collection id**

    c. Storage capacity: **Fixed**

    d. Throughput: **5000**

    ![In the Add Collection blade, fields are set to the previously defined settings.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image26.png 'Add Collection blade')

8)  Select **OK**

9)  Select **New Collection** to add another collection

10) On the **Add Collection** blade, specify the following configuration options:

    a. Enter **LicensePlates** for the database id

    b. Enter **NeedsManualReview** for the collection id

    c. Storage capacity: **Fixed**

    d. Throughput: **5000**

    ![In the Add Collection blade, fields are set to the previously defined values.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image27.png 'Add Collection blade')

11) Select **OK**

12) Select **Keys** under Settings in the menu

13) Underneath the **Read-write Keys tab within the Keys** blade, copy the **URI** and **Primary Key** values

    ![In the tollbooth - Keys blade, under Settings, Keys is selected. On the Read-write Keys tab, the copy buttons for the URL and Primary Key fields are selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image28.png 'tollbooth - Keys blade')

14) Paste the values into a text editor, such as Notepad, for later reference

### Task 5: Provision the Computer Vision API service

1.  Navigate to the Azure Management portal, <http://portal.azure.com>

2.  Select **+ New**, then enter **computer vision** into the search box on top. Select **Computer Vision API** from the results

    ![In the Azure Portal, Computer version is typed in the search box.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image29.png 'Azure Portal')

3.  Select the **Create** button on the **Computer Vision API** **overview** blade

4.  On the **Create Computer Vision API** blade, specify the following configuration options:

    a. **Name**: unique value for the App name (ensure the green check mark appears)

    b. Specify the **Resource Group** **ServerlessArchitecture**

    c. Select the same **location** as your Resource Group

    d. Select the **S1** **pricing tier**

    ![In the Create blade, fields are set to the previously defined settings.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image30.png 'Create blade')

5.  Select **Create**

    ![Screenshot of the Create button.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image13.png 'Create button')

6.  After the Computer Vision API has completed provisioning, open the service by opening the **ServerlessArchitecture** resource group, and then selecting the **Computer Vision** **API** service name

7.  Select **Overview** in the menu, and then copy the **Endpoint** value

    ![In the TollboothOCR blade, in the pane, Overview is selected. In the  pane, the copy button next to the Endpoint URL is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image31.png 'TollboothOCR blade')

8.  Select **Keys** under **Resource Management** in the menu

9.  Within the **Keys** blade, copy the **Key 1** value

    ![In the TollboothOCR - Keys blade, under Resource Management, Keys is selected. The Copy button next to the Key 1 value is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image32.png 'TollboothOCR - Keys blade')

10. Paste the values into a text editor, such as Notepad, for later reference

## Exercise 2: Develop and publish the photo processing and data export functions

**Duration**: 45 minutes

Use Visual Studio 2017 and its integrated Azure Functions tooling to develop and debug the functions locally, and then publish them to Azure. The starter project solution, TollBooths, contains most of the code needed. You will add in the missing code before deploying to Azure.

### Help references

|                                       |                                                                              |
| ------------------------------------- | :--------------------------------------------------------------------------: |
| **Description**                       |                                  **Links**                                   |
| Code and test Azure Functions locally | <https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local> |

### Task 1: Configure application settings

In this task, you will apply application settings using the Microsoft Azure Portal. You will then add the application settings to the TollBooth Starter Project.

1.  Using a new tab or instance of your browser navigate to the Azure Management portal, <http://portal.azure.com>

2.  Open the **ServerlessArchitecture** resource group, and then select the Azure Function App you created whose name ends with **FunctionApp**. If you did not use this naming convention, that's fine. Just be sure to make note of the name so you can distinguish it from the Function App you will be developing using the portal later on.

    ![In the ServerlessArchtecture resource group, TollBoothFunctionApp is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image33.png 'ServerlessArchtecture resource group')

3.  Select on **Application settings** on the Overview pane

    ![In the TollBoothFunctionApp blade, under Configured features, Application settings is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image34.png 'TollBoothFunctionApp blade')

4.  Scroll down to the **Application settings** section. Use the **+ Add new setting** link to create the following additional Key or Value pairs (the key names must exactly match those found in the table below):

|                          |                                                                                                                                                   |
| ------------------------ | :-----------------------------------------------------------------------------------------------------------------------------------------------: |
| **Application Key**      |                                                                     **Value**                                                                     |
| computerVisionApiUrl     | Computer Vision API endpoint you copied earlier. Append **/ocr** to the end. Example: https://westus2.api.cognitive.microsoft.com/vision/v1.0/ocr |
| computerVisionApiKey     |                                                              Computer Vision API key                                                              |
| eventGridTopicEndpoint   |                                                             Event Grid Topic endpoint                                                             |
| eventGridTopicKey        |                                                            Event Grid Topic access key                                                            |
| cosmosDBEndPointUrl      |                                                                   Cosmos DB URI                                                                   |
| cosmosDBAuthorizationKey |                                                               Cosmos DB Primary Key                                                               |
| cosmosDBDatabaseId       |                                                       Cosmos DB database id (LicensePlates)                                                       |
| cosmosDBCollectionId     |                                                   Cosmos DB processed collection id (Processed)                                                   |
| exportCsvContainerName   |                                                  Blob storage CSV export container name (export)                                                  |
| blobStorageConnection    |                                                          Blob storage connection string                                                           |

![In the Application Settings section, the previously mentioned key / value pairs are called out with a purple line.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image35.png 'ApplicationSettings section')

5.  Select **Save**

    ![Screenshot of the Save icon.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image36.png 'Save icon')

6.  _Optional steps_, only if you wish to debug the functions locally on your development machine:

    a. Update the local.settings.json file with the same values

    b. Update the AzureWebJobsStorage and AzureWebJobsDashboard values in local.settings.json with those found under Application settings for the Function App. Save your changes.

### Task 2: Finish the ProcessImage function

There are a few components within the starter project that must be completed, marked as TODO in the code. The first set of TODO items we will address are in the ProcessImage function, the FindLicensePlateText class that calls the Computer Vision API, and finally the SendToEventGrid.cs class, which is responsible for sending processing results to the Event Grid topic you created earlier.

**Important Note:** Do **not** update the version of any NuGet package. This solution is built to function with the NuGet package versions currently defined within. Updating these packages to newer versions could cause unexpected results.

1.  Navigate to the **TollBooth** project using the Solution Explorer of Visual Studio

2.  From the Visual Studio **View** menu, select **Task List**

    ![The Visual Studio Menu displays, with View and Task List selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image37.png 'Visual Studio Menu')

3.  There you will see a list of TODO tasks, where each task represents one line of code that needs to be completed

> ![A list of TODO tasks, including their description, project, file, and line number display.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image38.png 'TODO tasks')

4.  Open **ProcessImage.cs**. Notice that the Run method is decorated with the FunctionName attribute, which sets the name of the Azure Function to "ProcessImage". This has a BlobTrigger that watches for new blobs being added to the images container of the storage account that was created in Exercise 1.

5.  The following code represents the completed task in ProcessImage.cs:

```
 // **TODO 1: Set the licensePlateText value by awaiting a new FindLicensePlateText.GetLicensePlate method.**

 licensePlateText = await new FindLicensePlateText(log, _client).GetLicensePlate(licensePlateImage);
```

6.  Open **FindLicensePlateText.cs**. This class is responsible for contacting the Computer Vision API to find and extract the license plate text from the photo, using OCR. Notice that this class also shows how you can implement a resiliency pattern using Polly. This is useful for ensuring that you do not overload downstream services, in this case, the Computer Vision API. This will be demonstrated later on when visualizing the Function's scalability.

7.  The following code represents the completed task in FindLicensePlateText.cs:

```
    // TODO 2: Populate the below two variables with the correct AppSettings properties.
    var uriBase = ConfigurationManager.AppSettings["computerVisionApiUrl"];
    var apiKey = ConfigurationManager.AppSettings["computerVisionApiKey"];
```

8.  Open **SendToEventGrid.cs**. This class is responsible for sending an Event to the Event Grid topic, including the event type and license plate data. Event listeners will use the event type to filter and act on the events they need to process. Make note of the event types defined here (the first parameter passed into the Send method), as they will be used later on when creating new functions in the second Function App you provisioned earlier.

9.  The following code represents the completed tasks in SendToEventGrid.cs:

```
    // TODO 3: Modify send method to include the proper eventType name value for saving plate data.
    await Send("savePlateData", "TollBooth/CustomerService", data);

    // TODO 4: Modify send method to include the proper eventType name value for queuing plate for manual review.
    await Send("queuePlateForManualCheckup", "TollBooth/CustomerService", data);
```

### Task 3: Publish the Function App from Visual Studio

In this task, you will publish the Function App from the starter project in Visual Studio to the existing Function App you provisioned in Azure.

1.  Navigate to the **TollBooth** project using the Solution Explorer of Visual Studio

2.  Right-click the **TollBooth** project and select **Publish...** from the context menu

    ![In Solution Explorer, TollBooth is selected, and in its right-click menu, Publish is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image39.png 'Solution Explorer ')

3.  In the Pick a Publish Target window that appears, make sure **Azure Function App** is selected, choose the **Select Existing** radio button, then select **Publish**

    ![In the Publish window, the Azure Function App tile is selected. Under this, both the Select Existing radio button and the Publish button are selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image40.png 'Publish window')

4.  In the App Service form, select your **Subscription**, select **Resource Group** under **View**, then expand your **ServerlessArchitecture** resource group and select the Function App whose name ends with **FunctionApp**

5.  Whatever you named the Function App when you provisioned it is fine. Just make sure it is the same one to which you applied the Application Settings in Task 1 of this exercise

    ![In the App Service form, Resource Group displays in the View field, and in the tree-view below, the ServerlessArchitecture folder is expanded, and TollBoothFunctionApp is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image41.png 'App Service form')

6.  After you select the Function App, select **OK**

7.  Watch the Output window in Visual Studio as the Function App publishes. When it is finished, you should see a message that says, "Publish Succeeded."

8.  Using a new tab or instance of your browser navigate to the Azure Management portal, <http://portal.azure.com>

9.  Open the **ServerlessArchitecture** resource group, then select the Azure Function App to which you just published

10. Expand the functions underneath your Function App in the menu. You should see both functions you just published from the Visual Studio solution listed

    ![In the TollBoothFunctionApp blade, in the pane, both TollBoothFunctionApp, and Functions (Read Only) are expanded. Below Functions, two functions (ExportLicensePlates and ProcessImage) are called out.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image42.png 'TollBoothFunctionApp blade')

## Exercise 3: Create functions in the portal

**Duration**: 45 minutes

Create two new Azure Functions written in Node.js, using the Azure portal. These will be triggered by Event Grid and output to Azure Cosmos DB to save the results of license plate processing done by the ProcessImage function.

### Help references

|                                                                   |                                                                                                               |
| ----------------------------------------------------------------- | :-----------------------------------------------------------------------------------------------------------: |
| **Description**                                                   |                                                   **Links**                                                   |
| Create your first function in the Azure portal                    |        <https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function>         |
| Store unstructured data using Azure Functions and Azure Cosmos DB | <https://docs.microsoft.com/en-us/azure/azure-functions/functions-integrate-store-unstructured-data-cosmosdb> |

### Task 1: Create function to save license plate data to Azure Cosmos DB

In this task, you will create a new Node.js function triggered by Event Grid and that outputs successfully processed license plate data to Azure Cosmos DB.

1.  Using a new tab or instance of your browser navigate to the Azure Management portal, <http://portal.azure.com>

2.  Open the **ServerlessArchitecture** resource group, then select the Azure Function App you created whose name ends with **Events**. If you did not use this naming convention, make sure you select the Function App that you [did not]{.underline} deploy to in the previous exercise.

3.  Select **Functions** in the menu. In the **Functions** blade, select **+ New Function**

    ![In the TollBoothEvents2 blade, in the pane under Function Apps, TollBoothEvents2 is expanded, and Functions is selected. In the pane, the + New function button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image43.png 'TollBoothEvents2 blade')

4.  Event **event grid** into the template search form, then select the **Event Grid trigger** template

    ![In the Template search form, event grid is typed in the search field. Below, the Event Grid trigger function option displays.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image44.png 'Template search form')

5.  In the New Function form, fill out the following properties:

    a. **Language**: JavaScript

    b. **Name**: SavePlateData

    ![In the New Function form, JavaScript is selected from the Language drop-down menu, and SavePlateData is typed in the Name field.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image45.png 'Event Grid trigger, New Function form')

6)  Select **Create**

7)  Replace the code in the new SavePlateData function with the following:

```
    module.exports = function (context, eventGridEvent) {
        context.log(typeof eventGridEvent);
        context.log(eventGridEvent);

        context.bindings.outputDocument = {
            fileName : eventGridEvent.data["fileName"],
            licensePlateText : eventGridEvent.data["licensePlateText"],
            timeStamp : eventGridEvent.data["timeStamp"],
            exported : false
        }

        context.done();
    };
```

8.  Select **Save**

### Task 2: Add an Event Grid subscription to the SavePlateData function

In this task, you will add an Event Grid subscription to the SavePlateData function. This will ensure that the events sent to the Event Grid topic containing the savePlateData event type are routed to this function.

1.  With the SavePlateData function open, select **Add Event Grid subscription**

    ![In the SavePlateData blade, the Add Event Grid subscription link is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image46.png 'SavePlateData blade')

2.  On the **Create Event Subscription** blade, specify the following configuration options:

    a. **Name**: unique value for the App name (ensure the green check mark appears). Provide a name similar to saveplatedatasub.

    b. Select **Event Grid Topics** under **Topic Type**

    c. Select your **subscription** and **ServerlessArchitecture** resource group

    d. Select your Event Grid topic under **Instance**

    e. Check **Subscribe to all event types**. You will enter a custom event type later.

3.  Leave the remaining fields at their default values and select **Create**

    ![In the Create Event Subscription blade, fields are set to the previously defined settings.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image47.png)

### Task 3: Add an Azure Cosmos DB output to the SavePlateData function

In this task, you will add an Azure Cosmos DB output binding to the SavePlateData function, enabling it to save its data to the Processed collection.

1.  Expand the SavePlateData function in the menu, the select **Integrate**

2.  Select **+ New Output** under Outputs, select **Azure Cosmos DB** from the list of outputs, then select **Select**

    ![In the SavePlateData blade, in the pane under Function Apps, TollBoothEvents2, Functions, and SavePlateData are expanded, and Integrate is selected. In the pane, + New Output is selected under Outputs. In the list of outputs, the Azure Cosmos DB tile is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image48.png 'SavePlateData blade')

3.  In the Azure Cosmos DB output form, select **new** next to the Azure Cosmos DB account connection field

    ![The New button is selected next to the Azure Cosmos DB account connection field.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image49.png 'New button')

4.  Select your Cosmos DB account from the list that appears

5.  Specify the following configuration options in the Azure Cosmos DB output form:

    a. Enter **LicensePlates** into the **database name** field

    b. Enter **Processed** into the **collection name** field

    ![Under Azure Cosmos DB output the following field values display: Document parameter name, outputDocument; Collection name, Processed; Database name, LicensePlates; Azure Cosmos DB account conection, tollbooths_DOCUMENTDB.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image50.png 'Azure Cosmos DB output section')

6.  Select **Save**

### Task 4: Create function to save manual verification info to Azure Cosmos DB

In this task, you will create a new Node.js function triggered by Event Grid and outputs information about photos that need to be manually verified to Azure Cosmos DB.

1.  Using a new tab or instance of your browser navigate to the Azure Management portal, <http://portal.azure.com>

2.  Open the **ServerlessArchitecture** resource group, then select the Azure Function App you created whose name ends with **Events**. If you did not use this naming convention, make sure you select the Function App that you [did not]{.underline} deploy to in the previous exercise.

3.  Select **Functions** in the menu. In the **Functions** blade, select **+ New Function**

    ![In the pane of the TollBoothEvents2 blade under Functions Apps, TollBoothEvents2 is expanded, and Functions is selected. In the pane, + New function is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image43.png 'TollBoothEvents2 blade')

4.  Enter **event grid** into the template search form, then select the **Event Grid trigger** template

    ![Event grid displays in the choose a template search field, and in the results, Event Grid trigger displays.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image44.png 'Event grid trigger')

5.  In the **New Function** form, fill out the following properties:

    a. **Language**: JavaScript

    b. **Name**: QueuePlateForManualCheckup

    ![In the New Function form, JavaScript is selected from the Language drop-down menu, and QueuePlateForManualCheckup is typed in the Name field.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image51.png 'Event Grid trigger, New Function form')

6.  Select **Create**

7.  Replace the code in the new QueuePlateForManualCheckup function with the following:

```
    module.exports = function (context, eventGridEvent) {
        context.log(typeof eventGridEvent);
        context.log(eventGridEvent);

        context.bindings.outputDocument = {
            fileName : eventGridEvent.data["fileName"],
            licensePlateText : "",
            timeStamp : eventGridEvent.data["timeStamp"],
            resolved : false
        }

        context.done();
    };
```

8.  Select **Save**

### Task 5: Add an Event Grid subscription to the QueuePlateForManualCheckup function

In this task, you will add an Event Grid subscription to the QueuePlateForManualCheckup function. This will ensure that the events sent to the Event Grid topic containing the queuePlateForManualCheckup event type are routed to this function.

1.  With the QueuePlateForManualCheckup function open, select **Add Event Grid subscription**

    ![In the QueuePlateForManualCheckup blade, the Add Event Grid subscription link is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image52.png 'QueuePlateForManualCheckup blade')

2.  On the **Create Event Subscription** blade, specify the following configuration options:

    a. **Name**: unique value for the App name (ensure the green check mark appears). Provide a name similar to queueplateformanualcheckupsub.

    b. Select **Event Grid Topics** under Topic Type

    c. Select your **subscription** and **ServerlessArchitecture** resource group

    d. Select your Event Grid topic under **Instance**

    e. Check **Subscribe to all event types**. You will enter a custom event type later.

3.  Leave the remaining fields at their default values and select **Create**

    ![In the Create Event Subscription blade, fields are set to the previously defined settings.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image53.png)

### Task 6: Add an Azure Cosmos DB output to the QueuePlateForManualCheckup function

In this task, you will add an Azure Cosmos DB output binding to the QueuePlateForManualCheckup function, enabling it to save its data to the NeedsManualReview collection.

1.  Expand the QueuePlateForManualCheckup function in the menu, the select **Integrate**

2.  Select **+ New Output** under Outputs, select **Azure Cosmos DB** from the list of outputs, then select **Select**

    ![In the blade, in the pane under Function Apps, TollBoothEvents2\ Functions\QueuePlateForManualCheckup are expanded, and Integrate is selected. In the pane, + New Output is selected under Outputs. In the list of outputs, the Azure Cosmos DB tile is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image54.png)

3.  Specify the following configuration options in the Azure Cosmos DB output form:

    a. Enter **LicensePlates** into the **database name** field

    b. Enter **NeedsManualReview** into the **collection name** field

    c. Select the **Azure Cosmos DB account connection** you created earlier

    ![In the Azure Cosmos DB output form, the following field values display: Document parameter name, outputDocument; Collection name, NeedsManualReview; Database name, LicensePlates; Azure Cosmos DB account conection, tollbooths_DOCUMENTDB.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image55.png 'Azure Cosmos DB output form')

4.  Select **Save**

### Task 7: Configure custom event types for the new Event Grid subscriptions

In this task, you will configure a custom event type for each new Event Grid subscription you created for your functions in the previous steps of this exercise. Currently the event types are set to All. We want to narrow this down to only the event types specified within the SendToEventGrid class in the TollBooth solution. This will ensure that all other event types are ignored by your functions.

1.  Using a new tab or instance of your browser navigate to the Azure Management portal, <http://portal.azure.com>

2.  Open the **ServerlessArchitecture** resource group, then select the Event Grid Topic

3.  At the bottom of the **Overview** blade, you will see both Event Grid subscriptions created from the functions. Select **saveplatedatasub**.

    ![On the Event Grid Topic overview blade, select the saveplatedatasub Event Grid subscription.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image56.png)

4.  Uncheck **Subscribe to all event types**

5.  Enter **savePlateData** into the event types field. If you specified a different name in the SendToEventGrid class in the TollBooth solution, use that instead.

6.  Select **Save Changes**

    ![In the Edit Event Subscription blade, uncheck Subscribe to all event types. Enter savePlateData into the Event Types field, then save your changes.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image57.png)

7.  Select the **queueplateformanualcheckupsub** Event Grid subscription at the bottom of the **Overview** blade

    ![On the Event Grid Topic overview blade, select the queueplateformanualcheckupsub Event Grid subscription.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image58.png)

8.  Uncheck **Subscribe to all event types**

9.  Enter **queuePlateForManualCheckup** into the event types field. If you specified a different name in the SendToEventGrid class in the TollBooth solution, use that instead.

10. Select **Save Changes**

    ![In the Edit Event Subscription blade, uncheck Subscribe to all event types. Enter queuePlateForManualCheckup into the Event Types field, then save your changes.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image59.png)

## Exercise 4: Monitor your functions with Application Insights

**Duration**: 45 minutes

Application Insights can be integrated with Azure Function Apps to provide robust monitoring for your functions. In this exercise, you will provision a new Application Insights account and configure your Function Apps to send telemetry to it.

### Help references

|                                                               |                                                                                        |
| ------------------------------------------------------------- | :------------------------------------------------------------------------------------: |
| **Description**                                               |                                       **Links**                                        |
| Monitor Azure Functions using Application Insights            |     <https://docs.microsoft.com/en-us/azure/azure-functions/functions-monitoring>      |
| Live Metrics Stream: Monitor & Diagnose with 1-second latency | <https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream> |

### Task 1: Provision an Application Insights instance

1.  Navigate to the Azure Management portal, <http://portal.azure.com>

2.  Select **+ New**, then type **application insights** into the search box on top. Select **Application Insights** from the results.

    ![In the Azure Portal menu pane, New is selected. In the New blade, application inisght is typed in the search box, and Application insights is selected from the search results.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image60.png 'Azure Portal')

3.  Select the **Create** button on the **Application Insights overview** blade

4.  On the **Application Insights** blade, specify the following configuration options:

    a. **Name**: unique value for the App name (ensure the green check mark appears)

    b. Select **ASP.NET web application** for the **Application Type**

    c. Specify the **Resource Group** **ServerlessArchitecture**

    d. Select the same **location** as your Resource Group

    ![Fields in the Application Insights blade are set to the previously defined settings.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image61.png 'Application Insights blade')

5.  Select **Create**

### Task 2: Enable Application Insights integration in your Function Apps

Both of the Function Apps need to be updated with the Application Insights instrumentation key so they can start sending telemetry to your new instance.

1.  After the Application Insights account has completed provisioning, open the instance by opening the **ServerlessArchitecture** resource group, and then selecting the **Application Insights** instance name

2.  Copy the **instrumentation key** from the Essentials section of the **Overview** blade

    ![In the pane of the TollBoothMonitor blade, Overview is selected. In the pane, the copy button next to the Instrumentation key is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image62.png 'TollBoothMonitor blade')

3.  Open the Azure Function App you created whose name ends with **FunctionApp**, or the name you specified for the Function App containing the ProcessImage function

4.  Select on **Application settings** on the **Overview** pane

    ![In the pane of the TollBoothFunctionApp blade, under Configured features, Application settings is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image34.png 'TollBoothFunctionApp blade')

5.  Scroll down to the **Application settings** section. Use the **+ Add new setting** link and name the new setting APPINSIGHTS_INSTRUMENTATIONKEY. Paste the copied instrumentation key into its value field.

    ![In the TollBoothFunctionApp blade, the + Add new setting link is selected. In the list of application settings, APPINSIGHTS_INSTRUMENTATIONKEY is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image63.png 'TollBoothFunctionApp blade')

6.  Select **Save**

    ![Screenshot of the Save icon.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image36.png 'Save icon')

7.  Follow the steps above to add the APPINSIGHTS_INSTRUMENTATIONKEY setting to the **other Function App**

### Task 3: Use the Live Metrics Stream to monitor functions in real time

Now that Application Insights has been integrated into your Function Apps, you can use the Live Metrics Stream to see the functions' telemetry in real time.

1.  Open the Azure Function App you created whose name ends with **FunctionApp**, or the name you specified for the Function App containing the ProcessImage function

2.  Select Application Insights on the Overview pane
    ![In the TollBoothFunctionApp blade, under Configured features, the Application Insights link is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image64.png 'TollBoothFunctionApp blade')

3.  In Application Insights, select **Live Metrics Stream** underneath Investigate in the menu

    ![In the TollBoothMonitor blade, in the pane under Investigate, Live Metrics Stream is selected. ](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image65.png 'TollBoothMonitor blade')

4.  Leave the Live Metrics Stream open and go back to the starter app solution in Visual Studio

5.  Navigate to the **UploadImages** project using the Solution Explorer of Visual Studio

    ![In Solution Explorer, UploadImages is expanded, and App.config is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image66.png 'Solution Explorer')

6.  Open **App.config**

7.  In App.config, update the **blobStorageConnection** appSetting value to the connection string for your Blob storage account

    ![On the App.config tab, a connection string is circled. To the side of the string is a green bar, and a hammer icon.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image67.png 'App.config tab')

8.  Save your changes to the file

9.  Right-click the UploadImages project in the Solution Explorer, then select **Start new instance** under the **Debug** menu

    ![In Solution Explorer, UploadImages is selected. From the Debug menu, Start new instance is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image68.png 'Solution Explorer')

10. When the console window appears, enter **1** and press **ENTER**. This uploads a handful of car photos to the images container of your Blob storage account

    ![A Command prompt window displays, showing images being uploaded.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image69.png 'Command prompt window')

11. Switch back to your browser window with the Live Metrics Stream still open within Application Insights. You should start seeing new telemetry arrive, showing the number of servers online, the incoming request rate, CPU process amount, etc. You can select some of the sample telemetry in the list to the side to view output data.

    **Please note**, since our function with the blob trigger is running on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after the function app has gone idle. After the function app is running, blobs are processed immediately. To avoid this initial delay, consider one of the following options: Use an App Service plan with Always On enabled, or use another mechanism to trigger the blob processing, such as a queue message that contains the blob name or an Event Grid trigger. Sometimes, simply opening the function on the portal speeds up the process

    ![The Live Metrics Stream window displays information for the two online servers. Displaying line and point graphs include incoming requests, outgoing requests, and overvall health. To the side is a list of Sample Telemetry information. ](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image70.png 'Live Metrics Stream window')

12. Leave the Live Metrics Stream window open once again, and close the console window for the image upload. Debug the UploadImages project again, then enter **2** and press **ENTER**. This will upload 1,000 new photos

    ![the Command prompt window displays with image uploading information.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image71.png 'Command prompt window')

13. Switch back to the Live Metrics Stream window and observe the activity as the photos are uploaded. It is possible that the process will run so efficiently that no more than two servers will be allocated at a time. You should also notice things such as a steady cadence for the Request Rate monitor, the Request Duration hovering below \~500ms second, and the Process CPU percentage roughly matching the Request Rate.

    ![In the Live Metrics Stream window, two servers are online. Under Incoming Requests. the Request Rate heartbeat line graph is selected, as is the Request Duration dot graph. Under Overall Health, the Process CPU heartbeat line graph is also selected, and a bi-directional dotted line points out the similarities between this graph and the Request Rate graph under Incoming Requests.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image72.png 'Live Metrics Stream window ')

14. After this has run for a while, close the image uploader console window once again, but leave the Live Metrics Stream window open

### Task 4: Observe your functions dynamically scaling when resource-constrained

In this task, you will change the Computer Vision API to the Free tier. This will limit the number of requests to the OCR service to 10 per minute. Once changed, run the UploadImages console app to upload 1,000 images again. The resiliency policy programmed into the FindLicensePlateText.MakeOCRRequest method of the ProcessImage function will begin exponentially backing off requests to the Computer Vision API, allowing it to recover and lift the rate limit. This intentional delay will greatly increase the function's response time, thus causing the Consumption plan's dynamic scaling to kick in, allocating several more servers. You will watch all of this happen in real time using the Live Metrics Stream view.

1.  Open your Computer Vision API service by opening the **ServerlessArchitecture** resource group, and then selecting the **Computer Vision API** service name

2.  Select **Pricing tier** under Resource Management in the menu. Select the **F0 Free** pricing tier, then select **Select**

    ![In the TollboothOCR blade, under Resource Manaement, Pricing tier is selected. In the Choose your pricing tier blade, the F0 Free option is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image73.png 'TollboothOCR and Choose your pricing tier blades')

3.  Debug the UploadImages project again, then enter **2** and press **ENTER**. This will upload 1,000 new photos.

    ![the Command prompt window displays image uploading information.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image71.png 'Command Prompt window')

4.  Switch back to the Live Metrics Stream window and observe the activity as the photos are uploaded. After running for a couple of minutes, you should start to notice a few things. The Request Duration will start to increase over time. As this happens, you should notice more servers being brought online. Each time a server is brought online, you should see a message in the Sample Telemetry stating that it is "Generating 2 job function(s)", followed by a Starting Host message. You should also see messages logged by the resiliency policy that the Computer Vision API server is throttling the requests. This is known by the response codes sent back from the service (429). A sample message is "Computer Vision API server is throttling our requests. Automatically delaying for 32000ms".


    **Please note:** if you do not see data flow after a short period, consider restarting the Function App.

    ![In the Live Metrics Stream window, 11 servers are now online.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image74.png "Live Metrics Stream window ")

5.  After this has run for some time, close the UploadImages console to stop uploading photos

6.  Navigate back to the **Computer Vision** API and set the pricing tier back to **S1 Standard**

## Exercise 5: Explore your data in Azure Cosmos DB

**Duration**: 15 minutes

In this exercise, you will use the Azure Cosmos DB Data Explorer in the portal to view saved license plate data.

### Help references

|                       |                                                                 |
| --------------------- | :-------------------------------------------------------------: |
| **Description**       |                            **Links**                            |
| About Azure Cosmos DB | <https://docs.microsoft.com/en-us/azure/cosmos-db/introduction> |

### Task 1: Use the Azure Cosmos DB Data Explorer

1.  Open your Azure Cosmos DB account by opening the **ServerlessArchitecture** resource group, and then selecting the **Azure Cosmos DB account** name

2.  Select **Data Explorer** from the menu

    ![In the Tollbooth - Data Explorer blade, Data Explorer is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image75.png 'Tollbooth - Data Explorer blade')

3.  Expand the **Processed** collection, then select **Documents**. This will list each of the JSON documents added to the collection.

4.  Select one of the documents to view its contents. The first four properties are ones that were added by your functions. The remaining properties are standard and are assigned by Cosmos DB.

    ![Under Collections, Processed is expanded, and Documents is selected. On the Documents tab, a document is selected, and to the side, the first four properties of the document (fileName, licencePlateText, timeStamp, and exported) are circled.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image76.png 'Tollbooth - Data Explorer blade')

5.  Expand the **NeedsManualReview** collection, then select **Documents**

6.  Select one of the documents to view its contents. Notice that the filename is provided, as well as a property named "resolved". While this is out of scope for this lab, those properties can be used together to provide a manual process for viewing the photo and entering the license plate.

    ![Under Collections, NeedsManualReview is expanded, and Documents is selected. On the Documents tab, a document is selected, and to the side, the first four properties of the document (fileName, licencePlateText, timeStamp, and resolved) are circled.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image77.png 'Tollbooth - Data Explorer blade')

7.  Right-click on the **Processed** collection and select **New SQL Query**

    ![Under Collections, LicencePlates is expanded, and Processed is selected. From its right-click menu, New SQL Query is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image78.png 'Tollbooth - Data Explorer blade')

8.  Modify the SQL query to count the number of processed documents that have not been exported:

```
SELECT COUNT(c.id) FROM c WHERE c.exported = false
```

9.  Execute the query and observe the results. In our case, we have 1,369 processed documents that need to be exported.

    ![On the Query 1 tab, under Execute Query, the previously defined SQL query displays. Under Results, the number 1369 is circled.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image79.png 'Query 1 tab')

## Exercise 6: Create the data export workflow

**Duration**: 30 minutes

In this exercise, you create a new Logic App for your data export workflow. This Logic App will execute periodically and call your ExportLicensePlates function, then conditionally send an email if there were no records to export.

### Help references

|                                      |                                                                                                                       |
| ------------------------------------ | :-------------------------------------------------------------------------------------------------------------------: |
| **Description**                      |                                                       **Links**                                                       |
| What are Logic Apps?                 |                  <https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-what-are-logic-apps>                   |
| Call Azure Functions from logic apps | <https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-azure-functions%23call-azure-functions-from-logic-apps> |

### Task 1: Create the Logic App

1.  Navigate to the Azure Management portal, <http://portal.azure.com>

2.  Select **+ New**, then enter **logic app** into the search box on top. Select **Logic App** from the results.

    ![In the Azure Portal, in the menu, New is selected. In the New blade, logic ap is typed in the search field, and Logic App is selected in the search results.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image80.png 'Azure Portal')

3.  Select the **Create** button on the Logic App overview blade

4.  On the **Create Logic App** blade, specify the following configuration options:

    a. **Name**: unique value for the App name (ensure the green check mark appears)

    b. Specify the **Resource Group** **ServerlessArchitecture**

    c. Select the same **location** as your Resource Group

    ![In the Create logic app blade, fields are set to the previously defined settings.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image81.png 'Create logic app blade')

5.  Open the Logic App once it has been provisioned

6.  In the Logic App Designer, scroll through the page until you located the _Start with a common trigger_ section. Select the **Recurrence** trigger

    ![The Recurrence tile is selected in the Logic App Designer.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image82.png 'Logic App Designer')

7.  Enter **15** into the **Interval** box, and make sure Frequency is set to Minute. This can be set to an hour or some other interval, depending on business requirements.

8.  Select **+ New step**

    ![Under Recurrence, the Interval field is set to 15, and the + New step button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image83.png 'Logic App Designer Recurrence section')

9.  Select **Add an action**

    ![Screenshot of the Add an action button.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image84.png 'Add an action button')

10. Enter **Functions** in the filter box, then select the **Azure Functions** connector

    ![Under Choose an action, Functions is typed in the search box. Under Connectors, Azure Functions is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image85.png 'Logic App Designer Choose an action section')

11. Select your Function App whose name ends in **FunctionApp**, or contains the ExportLicensePlates function

    ![Under Azure Functions, in the search results list, Azure Functions (TollBoothFunctionApp) is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image86.png 'Logic App Designer Azure Functions section')

12. Select the **ExportLicensePlates** function from the list

    ![Under Azure Functions, under Actions (2), Azure Functions (ExportLicensePlates) is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image87.png 'Logic App Designer Azure Functions section')

13. This function does not require any parameters that need to be sent when it gets called. Select **+ New step**, then **Add a condition**

    ![Under ExportLicensePlates, the field is blank. Under the + New step button, Add a condition is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image88.png 'Logic App Designer ExportLicensePlates section')

14. Select the **Status code** parameter in the first field. Make sure **is equal to** is selected in the second field, then enter **200** in the third field. This evaluates the status code returned from the ExportLicensePlates function, which will return a 200 code when license plates are found and exported. Otherwise, it sends a 204 (NoContent) status code when no license plates were discovered that need to be exported. We will conditionally send an email if any response other than 200 is returned.

    ![The first Condition field displays Status code. The second, drop-down menu field displays is equal to, and the third field is set to 200.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image89.png 'Condition fields')

15. We will ignore the If true condition because we don't want to perform an action if the license plates are successfully exported. Select **Add an action** within the **If false** condition block.

    ![Under the Conditions field is an If true (green checkmark) section, and an if false (red x) section. In the If false section, Add an action is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image90.png 'Logic App Designer Condition fields if true/false ')

16. Enter **Office 365 Outlook** in the filter box, then select the **Office 365 Outlook** connector from the results

    ![In the If false, Choose an action section, Office 365 Outlook is typed in the search field, and in the results below, Office 365 Outlook is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image91.png 'Condition fields If false section')

17. Select the **Send an email** action

    ![From the Actions list, Office 365 Outlook (Send an email) is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image92.png 'Office 365 Outlook Actions list')

18. When prompted **Sign in** to your Office 365 Outlook account

    ![In the Office 365 Outlook - Send an email prompt, the Sign in button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image93.png 'Office 365 Outlook Sign in prompt')

19. In the Send an email form, provide the following values:

    d. Enter your email address in the **To** box

    e. Provide a **subject**, such as "Toll Booth license plate export failed"

    f. Enter a message into the **body**, and select the **Status code** from the ExportLicensePlates function so that it is added to the email body

    ![Under Send an email, fields are set to the previously defined settings. ](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image94.png 'Logic App Designer , Send an email fields')

20. Select **Save** in the tool bar to save your Logic App

21. Select **Run** to execute the Logic App. You should start receiving email alerts because the license plate data is not being exported. This is because we need to finish making changes to the ExportLicensePlates function so that it can extract the license plate data from Azure Cosmos DB, generate the CSV file, and upload it to Blob storage.

    ![The Run button is selected on the Logic Apps Designer blade toolbar.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image95.png 'Logic Apps Designer blade')

22. While in the Logic Apps Designer, you will see the run result of each step of your workflow. A green checkmark is placed next to each step that successfully executed, showing the execution time to complete. This can be used to see how each step is working, and you can select the executed step and see the raw output.

    ![In the Logic App Designer, green check marks display next to Recurrence, ExportLicensePlates, Condition, and Send an email.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image96.png 'Logic App Designer ')

23. The Logic App will continue to run in the background, executing every 15 minutes (or whichever interval you set) until you disable it. To disable the app, go to the **Overview** blade for the Logic App and select the **Disable** button on the taskbar.

    ![The Disable button is selected on the TollBoothLogic blade top menu.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image97.png 'TollBoothLogic blade')

## Exercise 7: Configure continuous deployment for your Function App

**Duration**: 40 minutes

In this exercise, configure your Function App that contains the ProcessImage function for continuous deployment. You will first set up a GitHub source code repository, then set that as the deployment source for the Function App.

### Help references

|                                           |                                                                                          |
| ----------------------------------------- | :--------------------------------------------------------------------------------------: |
| **Description**                           |                                        **Links**                                         |
| Creating a new GitHub repository          |              <https://help.github.com/articles/creating-a-new-repository/>               |
| Continuous deployment for Azure Functions | <https://docs.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment> |

### Task 1: Create a GitHub repository

1.  Navigate to <https://github.com> and sign in

2.  From the top corner of any page (once signed in), select the **+** menu item, then select **New repository**

    ![From the Plus icon drop-down menu, New repository is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image98.png 'Plus icon drop-down menu')

3.  Select your owner account, enter a unique **repository name**, make sure it is set to **Public**, and then select **Create repository**

    ![In the New Repository section, the Repository name field is set to serverless-architecture-lab, and the Public radio button is selected. At the bottom, the Create repository button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image99.png 'New Repository section')

4.  On your new repository page, copy the **HTTPS git path** to your clipboard, using the **button** provided

    ![On the Repository page, the HTTPS git path copy to clipboard button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image100.png 'Repository page')

### Task 2: Add GitHub repository to your Visual Studio solution

1.  Open the **TollBooth** project in Visual Studio

2.  Right-click the **TollBooth** project in Solution Explorer, then select **Commit...** under the **Source Control** menu item

    ![In Solution Explorer, TollBooth is selected. From its right-click menu, Source Control and then Commit are selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image101.png 'Solution Explorer')

3.  Enter a commit message, then select **Commit All**

    ![In Team Explorer - Changes, under Changes, the commit message reads "Finishing function code." Below that, the Commit All button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image102.png 'Team Explorer - Changes')

4.  After committing, select the **Sync** link. This will allow us to add the remote GitHub repository.

    ![Under Team Explorer - Changes, in the informational message Commit 02886e85 created locally. Sync to share, the Sync link is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image103.png 'Team Explorer - Changes')

5.  Select the **Publish Git Repo** button, then paste the git URL for your new repository you copied from GitHub. Finally, select **Publish**.

    ![In the Team Explorer - Synchronization window, the Publish Git Repo button is selected, and in the field below, the copied URL displays.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image104.png 'Team Explorer - Synchronization')

6.  Refresh your GitHub repository page in your browser. You should see that the project files have been added. Navigate to the **TollBooth** folder of your repo. Notice that the local.settings.json file has not been uploaded. That's because the .gitignore file of the TollBooth project explicitly excludes that file from the repository, making sure you don't accidentally share your application secrets.

    ![On the GitHub Repository page for serverless-architecture-lab, on the Code tab, project files display.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image105.png 'GitHub Repository page')

### Task 3: Configure your Function App to use your GitHub repository for continuous deployment

1.  Open the Azure Function App you created whose name ends with **FunctionApp**, or the name you specified for the Function App containing the ProcessImage function

2.  Select **Deployment options** underneath the **Platform features** tab

    ![In the TollBoothFunctionApp blade, on the Platform features tab, under Code Deployment, Deployment options is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image106.png 'TollBoothFunctionApp blade')

3.  Select **Setup** in the **Deployments** blade

    ![In the Deployments blade, the Setup icon is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image107.png 'Deployments blade')

4.  Select **Choose Source**, then **GitHub** in the list of sources

    ![In the Deployment option blade, Choose source is selected. In the Choose source blade, GitHub is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image108.png 'Deployment option and Choose source blades')

5.  Select **Authorization**, then enter your GitHub credentials when prompted

6.  **Choose your organization**

7.  Choose your new repository under **Choose project**. Make sure the **master branch** is selected.

    ![Fields in the Deployment option blade set to the following settings: Choose Source, GitHub; Authorization, hidden; Choose your organization, Personal; Choose project, serverless-architecture-lab; Choose branch, master. Performance Test, not configured.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image109.png 'Deployment option blade')

8.  Select **OK**

9.  After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered. The site is redeployed when files in the source are updated.

### Task 4: Finish your ExportLicensePlates function code and push changes to GitHub to trigger deployment

1.  Navigate to the **TollBooth** project using the Solution Explorer of Visual Studio

2.  From the Visual Studio **View** menu, select **Task List**

    ![Task List is selected from the Visual Studio View menu.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image37.png 'Visual Studio View menu')

3.  There you will see a list of TODO tasks, where each task represents one line of code that needs to be completed

4.  Open **DatabaseMethods.cs**

5.  The following code represents the completed task in DatabaseMethods.cs:

```
    // TODO 5: Retrieve a List of LicensePlateDataDocument objects from the collectionLink where the exported value is false.
    licensePlates = _client.CreateDocumentQuery<LicensePlateDataDocument>(collectionLink,
            new FeedOptions() { MaxItemCount = 100 })
        .Where(l => l.exported == false)
        .ToList();
    // TODO 6: Remove the line below.
```

6.  Make sure that you deleted the following line under TODO 6: licensePlates = new List\<LicensePlateDataDocument\>();

7.  Save your changes then open **FileMethods.cs**

8.  The following code represents the completed task in DatabaseMethods.cs:

```
    // TODO 7: Asyncronously upload the blob from the memory stream.
    await blob.UploadFromStreamAsync(stream);
```

9.  Save your changes

10. Right-click the **TollBooth** project in Solution Explorer, then select **Commit...** under the **Source Control** menu item

    ![In Solution Explorer, TollBooth is selected. From its right-click menu, Source Control and Commit are both selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image101.png 'Solution Explorer')

11. Enter a commit message, then select **Commit All**

    ![In the Team Explorer - Changes window, "Finished the ExportLicensePlates function" displays in the message box, and the Commit All button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image110.png 'Team Explorer - Changes window')

12. After committing, select the **Sync** link. This will allow us to add the remote GitHub repository

    ![Under Team Explorer - Changes, in the informational message Commit 02886e85 created locally. Sync to share, the Sync link is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image103.png 'Team Explorer - Changes window')

13. Select the **Sync** button on the **Synchronization** step

    ![Under Synchronization in the Team Explorer - Synchronization window, the Sync link is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image111.png 'Team Explorer - Synchronization window')

    Afterward, you should see a message stating that the incoming and outgoing commits were successfully synchronized.

14. Go back to Deployments for your Function App in the portal. You should see an entry for the deployment kicked off by this last commit. Check the timestamp on the message to verify that you are looking at the latest one

    ![On the Deployments blade, a partially-completed full-circle graph displays next to the message, Finished the ExportLicensePlates function, GitHub, building, 8:49 PM.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image112.png 'Deployments blade')

## Exercise 8: Rerun the workflow and verify data export

**Duration**: 10 minutes

With the latest code changes in place, run your Logic App and verify that the files are successfully exported.

### Task 1: Run the Logic App

1.  Open your ServerlessArchitecture resource group in the Azure portal, then select your Logic App

2.  From the **Overview** blade, select **Enable**

    ![In the TollBoothLogic, the Enable enable button is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image113.png 'TollBoothLogic blade')

3.  Now select **Run Trigger**, then select **Recurrence** to immediately execute your workflow

    ![In the TollBoothLogic blade, Run Trigger / Recurrence is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image114.png 'TollBoothLogic blade')

4.  Select the **Refresh** button next to the Run Trigger button to refresh your run history. Select the latest run history item. If the expression result for the condition is **true**, then that means the CSV file should've been exported to Blob storage. Be sure to disable the Logic App so it doesn't keep sending you emails every 15 minutes. Please note that it may take longer than expected to start running, in some cases.

    ![In Logic App Designer, in the Condition section, under Inputs, true is circled.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image115.png 'Logic App Designer ')

### Task 2: View the exported CSV file

1.  Open your ServerlessArchitecture resource group in the Azure portal, then select your **Storage account** you had provisioned to store uploaded photos and exported CSV files

2.  In the Overview pane of your storage account, select **Blobs**

    ![Under Services, Blobs is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image116.png 'Services section')

3.  Select the **export** container

    ![Export is selected under Name.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image117.png 'Export option')

4.  You should see at least one recently uploaded CSV file. Select the filename to view its properties.

    ![In the Export blade, under name, a .csv file is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image118.png 'Export blade')

5.  Select **Download** in the blob properties window

    ![In the Blob properties blade, the Download butotn is selected.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image119.png 'Blob properties blade')

    The CSV file should look similar to the following:

    ![A CSV file displays with the following columns: FileName, LicensePlateText, TimeStamp, and LicencePlateFound.](images/Hands-onlabstep-by-step-Serverlessarchitectureimages/media/image120.png 'CSV file')

6.  The ExportLicensePlates function updates all of the records it exported by setting the exported value to true. This makes sure that only new records since the last export are included in the next one. Verify this by re-executing the script in Azure Cosmos DB that counts the number of documents in the Processed collection where exported is false. It should return 0 unless you've subsequently uploaded new photos.

## After the hands-on lab

**Duration**: 10 minutes

In this exercise, attendees will deprovision any Azure resources that were created in support of the lab.

### Task 1: Delete the resource group in which you placed your Azure resources.

1.  From the Portal, navigate to the blade of your **Resource Group** and select **Delete** in the command bar at the top

2.  Confirm the deletion by re-typing the **resource group name** and selecting **Delete**

3.  If you created a different resource group for your virtual machined, be sure to delete that as well

4.  Optionally, delete the GitHub repository you created for this lab by selecting **settings** and then **Delete this repository** from the GitHub website

You should follow all steps provided _after_ attending the hands-on lab.
