![](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png 'Microsoft Cloud Workshops')

<div class="MCWHeader1">
Serverless architecture
</div>

<div class="MCWHeader2">
Hands-on lab unguided
</div>

<div class="MCWHeader3">
June 2018
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only, and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third-party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2018 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are the property of their respective owners.

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
      - [Tasks to complete](#tasks-to-complete)
      - [Exit criteria](#exit-criteria)
    - [Task 2: Provision the Function Apps](#task-2-provision-the-function-apps)
      - [Tasks to complete](#tasks-to-complete-1)
      - [Exit criteria](#exit-criteria-1)
    - [Task 3: Provision the Event Grid topic](#task-3-provision-the-event-grid-topic)
      - [Tasks to complete](#tasks-to-complete-2)
      - [Exit criteria](#exit-criteria-2)
    - [Task 4: Provision the Azure Cosmos DB account](#task-4-provision-the-azure-cosmos-db-account)
      - [Tasks to complete](#tasks-to-complete-3)
      - [Exit criteria](#exit-criteria-3)
    - [Task 5: Provision the Computer Vision API service](#task-5-provision-the-computer-vision-api-service)
      - [Tasks to complete](#tasks-to-complete-4)
      - [Exit criteria](#exit-criteria-4)
  - [Exercise 2: Develop and publish the photo processing and data export functions](#exercise-2-develop-and-publish-the-photo-processing-and-data-export-functions)
    - [Help references](#help-references-1)
    - [Task 1: Configure application settings](#task-1-configure-application-settings)
      - [Tasks to complete](#tasks-to-complete-5)
      - [Exit criteria](#exit-criteria-5)
    - [Task 2: Finish the ProcessImage function](#task-2-finish-the-processimage-function)
      - [Tasks to complete](#tasks-to-complete-6)
      - [Exit criteria](#exit-criteria-6)
    - [Task 3: Publish the Function App from Visual Studio](#task-3-publish-the-function-app-from-visual-studio)
      - [Tasks to complete](#tasks-to-complete-7)
      - [Exit criteria](#exit-criteria-7)
  - [](#)
  - [Exercise 3: Create functions in the portal](#exercise-3-create-functions-in-the-portal)
    - [Help references](#help-references-2)
    - [Task 1: Create function to save license plate data to Azure Cosmos DB](#task-1-create-function-to-save-license-plate-data-to-azure-cosmos-db)
      - [Tasks to complete](#tasks-to-complete-8)
      - [Exit criteria](#exit-criteria-8)
    - [Task 2: Add an Event Grid subscription to the SavePlateData function](#task-2-add-an-event-grid-subscription-to-the-saveplatedata-function)
      - [Tasks to complete](#tasks-to-complete-9)
      - [Exit criteria](#exit-criteria-9)
    - [Task 3: Add an Azure Cosmos DB output to the SavePlateData function](#task-3-add-an-azure-cosmos-db-output-to-the-saveplatedata-function)
      - [Tasks to complete](#tasks-to-complete-10)
      - [Exit criteria](#exit-criteria-10)
    - [Task 4: Create function to save manual verification info to Azure Cosmos DB](#task-4-create-function-to-save-manual-verification-info-to-azure-cosmos-db)
      - [Tasks to complete](#tasks-to-complete-11)
      - [Exit criteria](#exit-criteria-11)
    - [Task 5: Add an Event Grid subscription to the QueuePlateForManualCheckup function](#task-5-add-an-event-grid-subscription-to-the-queueplateformanualcheckup-function)
      - [Tasks to complete](#tasks-to-complete-12)
      - [Exit criteria](#exit-criteria-12)
    - [Task 6: Add an Azure Cosmos DB output to the QueuePlateForManualCheckup function](#task-6-add-an-azure-cosmos-db-output-to-the-queueplateformanualcheckup-function)
      - [Tasks to complete](#tasks-to-complete-13)
      - [Exit criteria](#exit-criteria-13)
    - [Task 7: Configure custom event types for the new Event Grid subscriptions](#task-7-configure-custom-event-types-for-the-new-event-grid-subscriptions)
      - [Tasks to complete](#tasks-to-complete-14)
      - [Exit criteria](#exit-criteria-14)
  - [Exercise 4: Monitor your functions with Application Insights](#exercise-4-monitor-your-functions-with-application-insights)
    - [Help references](#help-references-3)
    - [Task 1: Provision an Application Insights instance](#task-1-provision-an-application-insights-instance)
      - [Tasks to complete](#tasks-to-complete-15)
      - [Exit criteria](#exit-criteria-15)
    - [Task 2: Enable Application Insights integration in your Function Apps](#task-2-enable-application-insights-integration-in-your-function-apps)
      - [Tasks to complete](#tasks-to-complete-16)
    - [Task 3: Use the Live Metrics Stream to monitor functions in real time](#task-3-use-the-live-metrics-stream-to-monitor-functions-in-real-time)
      - [Tasks to complete](#tasks-to-complete-17)
      - [Exit criteria](#exit-criteria-16)
    - [Task 4: Observe your functions dynamically scaling when resource-constrained](#task-4-observe-your-functions-dynamically-scaling-when-resource-constrained)
      - [Tasks to complete](#tasks-to-complete-18)
      - [Exit criteria](#exit-criteria-17)
  - [Exercise 5: Explore your data in Azure Cosmos DB](#exercise-5-explore-your-data-in-azure-cosmos-db)
    - [Help references](#help-references-4)
    - [Task 1: Use the Azure Cosmos DB Data Explorer](#task-1-use-the-azure-cosmos-db-data-explorer)
      - [Tasks to complete](#tasks-to-complete-19)
      - [Exit criteria](#exit-criteria-18)
  - [Exercise 6: Create the data export workflow](#exercise-6-create-the-data-export-workflow)
    - [Help references](#help-references-5)
    - [Task 1: Create the Logic App](#task-1-create-the-logic-app)
      - [Tasks to complete](#tasks-to-complete-20)
      - [Exit criteria](#exit-criteria-19)
  - [Exercise 7: Configure continuous deployment for your Function App](#exercise-7-configure-continuous-deployment-for-your-function-app)
    - [Help references](#help-references-6)
    - [Task 1: Create a GitHub repository](#task-1-create-a-github-repository)
      - [Tasks to complete](#tasks-to-complete-21)
      - [Exit criteria](#exit-criteria-20)
    - [Task 2: Add GitHub repository to your Visual Studio solution](#task-2-add-github-repository-to-your-visual-studio-solution)
      - [Tasks to complete](#tasks-to-complete-22)
      - [Exit criteria](#exit-criteria-21)
    - [Task 3: Configure your Function App to use your GitHub repository for continuous deployment](#task-3-configure-your-function-app-to-use-your-github-repository-for-continuous-deployment)
      - [Tasks to complete](#tasks-to-complete-23)
      - [Exit criteria](#exit-criteria-22)
    - [Task 4: Finish your ExportLicensePlates function code and push changes to GitHub to trigger deployment](#task-4-finish-your-exportlicenseplates-function-code-and-push-changes-to-github-to-trigger-deployment)
      - [Tasks to complete](#tasks-to-complete-24)
      - [Exit criteria](#exit-criteria-23)
  - [Exercise 8: Rerun the workflow and verify data export](#exercise-8-rerun-the-workflow-and-verify-data-export)
    - [Task 1: Run the Logic App](#task-1-run-the-logic-app)
      - [Tasks to complete](#tasks-to-complete-25)
      - [Exit criteria](#exit-criteria-24)
    - [Task 2: View the exported CSV file](#task-2-view-the-exported-csv-file)
      - [Tasks to complete](#tasks-to-complete-26)
      - [Exit criteria](#exit-criteria-25)
  - [After the hands-on lab](#after-the-hands-on-lab)
    - [Task 1: Delete the Resource group in which you placed your Azure resources.](#task-1-delete-the-resource-group-in-which-you-placed-your-azure-resources)

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

    1.  <https://www.visualstudio.com/vs/>

    b. Azure development workload for Visual Studio 2017

    1.  <https://docs.microsoft.com/azure/azure-functions/functions-develop-vs#prerequisites>

    c. .NET Framework 4.7 runtime (or higher)

    1.  <https://www.microsoft.com/net/download/windows>

3.  Office 365 account. If required, you can sign up for an Office 365 trial at:

    a. <https://portal.office.com/Signup/MainSignup15.aspx?Dap=False&QuoteId=79a957e9-ad59-4d82-b787-a46955934171&ali=1>

4.  GitHub account. You can create a free account at <https://github.com>.

5.  Follow all the steps provided in [Before the Hands-on Lab](Before%20the%20HOL%20-%20Serverless%20architecture.md)

## Exercise 1: Azure data, storage, and serverless environment setup

**Duration**: 30 minutes

You must provision a few resources in Azure before you start developing the solution. Ensure all resources use the same resource group that was created for the App Service Environment.

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

In this exercise, you will provision a Blob storage account, using the Hot access tier and placing it in your resource group. You will copy the storage connection string from access keys, then create two private containers: images and export.

#### Tasks to complete

- Create a blob storage instance from within Azure

#### Exit criteria

- Save the storage connection string for later

- There should be two private containers: images and export

### Task 2: Provision the Function Apps

Provision two separate Function Apps. One will be deployed to from Visual Studio, and the other one will be managed through the portal.

#### Tasks to complete

- Create a Function App whose name ends with **Events**. Select the Consumption plan.

- Create a Function App whose name ends with **FunctionApp**. Make a note of the name, as this will be one deployed to from Visual Studio. Select the Consumption plan.

#### Exit criteria

- Save the names for later, marking which one you will be deploying to from Visual Studio

### Task 3: Provision the Event Grid topic

The Event Grid topic is the eventing backplane that allows the functions to trigger and send data to one another

#### Tasks to complete

- Create an Event Grid topic from within Azure

#### Exit criteria

- Save the topic endpoint for later

- Save the access key for later

### Task 4: Provision the Azure Cosmos DB account

Azure Cosmos DB will serve as your unstructured data store for processed license plates and those queued for manual review.

#### Tasks to complete

- Create an Azure Cosmos DB account from within Azure

- Select the SQL API

#### Exit criteria

- Create a collection named Processed with a Database Id of LicensePlates. It should have fixed storage capacity and have a throughput of 5000 RU/s.

- Create a collection named NeedsManualReview with a Database Id of LicensePlates. It should have fixed storage capacity and have a throughput of 5000 RU/s.

- Save the URI for later

- Save the key for later

### Task 5: Provision the Computer Vision API service

The Computer Vision API will provide OCR capability on-demand from your ProcessImages function.

#### Tasks to complete

- Create a Computer Vision API service from within Azure

- Select the S1 pricing tier

#### Exit criteria

- Save the Endpoint for later

- Save the key for later

## Exercise 2: Develop and publish the photo processing and data export functions

**Duration**: 45 minutes

Use Visual Studio 2017 and its integrated Azure Functions tooling to develop and debug the functions locally, then publish them to Azure. The starter project solution, TollBooths, contains most of the code needed. You will add in the missing code before deploying to Azure.

### Help references

|                                       |                                                                              |
| ------------------------------------- | :--------------------------------------------------------------------------: |
| **Description**                       |                                  **Links**                                   |
| Code and test Azure Functions locally | <https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local> |

### Task 1: Configure application settings

In this task, you will apply application settings using the Microsoft Azure Portal. You will then add the application settings to the TollBooth Starter Project.

#### Tasks to complete

- Open the TollBooth starter project in Visual Studio

- Open the local.settings.json file as a reference

- Navigate to the Function App you created whose name ends with **FunctionApp**. If you did not use this naming convention, that's fine. Just be sure to make a note of the name so you can distinguish it from the Function App you will be developing using the portal later on.

- Open the Function App's application settings, then add new application keys and values, using the local.settings.json file as a reference

#### Exit criteria

- Your Function App has the following new application settings populated with the correct values:

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

- Populate the save values in your local.settings.json files if you plan on debugging your Function App locally

### Task 2: Finish the ProcessImage function

There are a few components within the starter project that must be completed, marked as TODO in the code. The first set of TODO items we will address are in the ProcessImage function, the FindLicensePlateText class that calls the Computer Vision API, and finally the SendToEventGrid.cs class, which is responsible for sending processing results to the Event Grid topic you created earlier.

#### Tasks to complete

- Complete TODO item found in ProcessImage.cs

- Complete TODO item found in FindLicensePlateText.cs

- Complete TODO items found in SendToEventGrid.cs. Make note of the event types you define here, as they will be used later on when creating new functions in the second Function App you provisioned earlier. Suggested event type names are savePlateData and queuePlateForManualCheckup.

#### Exit criteria

- You completed TODO items 1-4

- You copied the two event type names you defined under TODO 3 & 4, for future reference

### Task 3: Publish the Function App from Visual Studio

In this task, you will publish the Function App from the starter project in Visual Studio to the existing Function App you provisioned in Azure.

#### Tasks to complete

- Publish the TollBooth project to the existing Function App you created whose name ends in FunctionApp

#### Exit criteria

- Navigate to the Function App in Azure and verify that both functions appear within

###

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

#### Tasks to complete

- Open the Function App you created whose name ends with **Events**. If you did not use this naming convention, make sure you select the Function App that you [did not]{.underline} deploy in the previous exercise.

- Create a new Event Grid trigger function named SavePlateData with the language set to JavaScript

- Update the function code to set the context.bindings.outputDocument to a new JSON file with the following signature:

```
{
    fileName : '',
    licensePlateText : '',
    timeStamp : '',
    exported : false
}
```

- The values should be set by the incoming Event Grid data properties

#### Exit criteria

- You have a new function triggered by Event Grid, saving that Event Grid data to an Azure Cosmos DB output binding

### Task 2: Add an Event Grid subscription to the SavePlateData function

In this task, you will add an Event Grid subscription to the SavePlateData function. This will ensure that the events sent to the Event Grid topic containing the savePlateData event type are routed to this function.

#### Tasks to complete

- Add an Event Grid subscription to the new SavePlateData function

- This subscription should subscribe to EventGrid Topics, and to all event types

#### Exit criteria

- You have a new Event Grid Subscription URL configured for your function's Event Grid Trigger

### Task 3: Add an Azure Cosmos DB output to the SavePlateData function

In this task, you will add an Azure Cosmos DB output binding to the SavePlateData function, enabling it to save its data to the Processed collection.

#### Tasks to complete

- Add a new Azure Cosmos DB output binding to the SavePlateData function

- Connect it to the Azure Cosmos DB account you created earlier

- Set the Database name to LicensePlates, and the Collection name to Processed

#### Exit criteria

- Your function has a new Azure Cosmos DB output configured under Integrate

### Task 4: Create function to save manual verification info to Azure Cosmos DB

In this task, you will create a new Node.js function triggered by Event Grid, and that outputs information about photos that need to be manually verified to Azure Cosmos DB.

#### Tasks to complete

- Open the Function App you created whose name ends with **Events**. If you did not use this naming convention, make sure you select the Function App that you [did not]{.underline} deploy in the previous exercise.

- Create a new Event Grid trigger function named QueuePlateForManualCheckup with the language set to JavaScript

- Update the function code to set the context.bindings.outputDocument to a new JSON file with the following signature:

```
    {
        fileName : '',
        licensePlateText : '',
        timeStamp : '',
        resolved : false
    }
```

- The values should be set by the incoming Event Grid data properties

#### Exit criteria

- You have a new function triggered by Event Grid, saving that Event Grid data to an Azure Cosmos DB output binding

### Task 5: Add an Event Grid subscription to the QueuePlateForManualCheckup function

In this task, you will add an Event Grid subscription to the QueuePlateForManualCheckup function. This will ensure that the events sent to the Event Grid topic containing the queuePlateForManualCheckup event type are routed to this function.

#### Tasks to complete

- Add an Event Grid subscription to the new QueuePlateForManualCheckup function

- This subscription should subscribe to EventGrid Topics, and to all event types

#### Exit criteria

- You have a new Event Grid Subscription URL configured for your function's Event Grid Trigger

### Task 6: Add an Azure Cosmos DB output to the QueuePlateForManualCheckup function

In this task, you will add an Azure Cosmos DB output binding to the QueuePlateForManualCheckup function, enabling it to save its data to the NeedsManualReview collection.

#### Tasks to complete

- Add a new Azure Cosmos DB output binding to the QueuePlateForManualCheckup function

- Connect it to the Azure Cosmos DB account you created earlier

- Set the Database name to LicensePlates, and the Collection name to NeedsManualReview

#### Exit criteria

- Your function has a new Azure Cosmos DB output configured under Integrate

### Task 7: Configure custom event types for the new Event Grid subscriptions

In this task, you will configure a custom event type for each new Event Grid subscription you created for your functions in the previous steps of this exercise. Currently the event types are set to All. We want to narrow this down to only the event types specified within the SendToEventGrid class in the TollBooth solution. This will ensure that all other event types are ignored by your functions.

#### Tasks to complete

- Open your Event Grid Topic, then select the Event Grid subscription for the SavePlateData function

- Configure a custom event type named **savePlateData**. If you specified a different name in the SendToEventGrid class in the TollBooth solution, use that instead.

- Select the Event Grid subscription for the QueuePlateForManualCheckup function

- Configure a custom event type named **queuePlateForManualCheckup**. If you specified a different name in the SendToEventGrid class in the TollBooth solution, use that instead.

#### Exit criteria

- Both Event Grid subscriptions have custom event types assigned, as specified within the SendToEventGrid class, instead of All

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

#### Tasks to complete

- Create an Application Insights instance from within Azure

- Select the ASP.NET web application type

#### Exit criteria

- Save the Instrumentation Key

### Task 2: Enable Application Insights integration in your Function Apps

Both of the Function Apps need to be updated with the Application Insights instrumentation key so they can start sending telemetry to your new instance.

#### Tasks to complete

- Add the Application Insights instrumentation key to both Function Apps

### Task 3: Use the Live Metrics Stream to monitor functions in real time

Now that Application Insights has been integrated into your Function Apps, you can use the Live Metrics Stream to see the functions' telemetry in real time.

#### Tasks to complete

- Open the Live Metrics Stream in your Application Insights instance. You can open your instance directly from the Function App.

- Open the starter solution in Visual Studio and update the App.config file in the UploadImages project with your Blob storage connection string

- Run the UploadImages project and choose Option 1 to upload a handful of test photos. View the incoming telemetry in the Live Metrics Stream. **Please note**, since our function with the blob trigger is running on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after the function app has gone idle. After the function app is running, blobs are processed immediately. To avoid this initial delay, consider one of the following options: Use an App Service plan with Always On enabled, or use another mechanism to trigger the blob processing, such as a queue message that contains the blob name or an Event Grid trigger. Sometimes simply opening the function on the portal speeds up the process.

- Re-run the UploadImages console application, this time choosing Option 2 to upload 1,000 photos

#### Exit criteria

- Take note of the number of servers online and the various graphs in the Live Metrics Stream, as you are uploading 1,000 photos. This data will be used as a comparison later.

### Task 4: Observe your functions dynamically scaling when resource-constrained

In this task, you will change the Computer Vision API to the Free tier. This will limit the number of requests to the OCR service to 10 per minute. Once changed, run the UploadImages console app to upload 1,000 images again. The resiliency policy programmed into the FindLicensePlateText.MakeOCRRequest method of the ProcessImage function will begin exponentially backing off requests to the Computer Vision API, allowing it to recover and lift the rate limit. This intentional delay will greatly increase the function's response time, thus causing the Consumption plan's dynamic scaling to kick in, allocating several more servers. You will watch all of this happen in real time using the Live Metrics Stream view.

#### Tasks to complete

- Set the Computer Vision API pricing tier to F0 Free

- Open the Live Metrics Stream in your Application Insights instance. You can open your instance directly from the Function App.

- Run the UploadImages console application, choosing Option 2 to upload 1,000 photos

#### Exit criteria

- Take note of the number of servers online and the various graphs in the Live Metrics Stream, as you are uploading 1,000 photos. After running for a couple of minutes, you should start to notice a few things. The Request Duration will start to increase over time. As this happens, you should notice more servers being brought online. Each time a server is brought online, you should see a message in the Sample Telemetry stating that it is "Generating 2 job function(s)", followed by a Starting Host message. You should also see messages logged by the resiliency policy that the Computer Vision API server is throttling the requests. This is known by the response codes sent back from the service (429). A sample message is "Computer Vision API server is throttling our requests. Automatically delaying for 32000ms".

- Stop uploading photos after some time, then set the Computer Vision API pricing tier back to S1 Standard

## Exercise 5: Explore your data in Azure Cosmos DB

**Duration**: 15 minutes

In this exercise, you will use the Azure Cosmos DB Data Explorer in the portal to view saved license plate data.

### Help references

|                       |                                                                 |
| --------------------- | :-------------------------------------------------------------: |
| **Description**       |                            **Links**                            |
| About Azure Cosmos DB | <https://docs.microsoft.com/en-us/azure/cosmos-db/introduction> |

### Task 1: Use the Azure Cosmos DB Data Explorer

In this exercise, the attendee will apply application settings using the Microsoft Azure Portal. The attendee will then deploy the Web API from the Starter Project.

#### Tasks to complete

- View a few documents saved to the Processed collection

- View a few documents saved to the NeedsManualReview collection

- Create a new SQL query on the Processed collection that counts the number of processed documents that have not been exported

#### Exit criteria

- You should see several documents in the Processed collection, and the license plate text that was extracted from the photos using the Computer Vision API's OCR capabilities

- Notice that the first four properties in the Processed document are properties added by your functions. The rest are standard properties assigned by Cosmos DB.

- You should see several documents in the NeedsManualReview collection

- Your SQL query should, at this point, equal to the number of total documents in the Processed collection

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

#### Tasks to complete

- Provision the Logic App service

- Design a new Logic App with a Recurrence trigger that fires every 15 minutes

- Add an action to the trigger using the Azure Functions connector to connect to your Function App whose name ends in **FunctionApp**, or contains the ExportLicensePlates function. Select the ExportLicensePlates function.

- Add a condition that evaluates your function's Status Code value where it is equal to 200. This evaluates the status code returned from the ExportLicensePlates function, which will return a 200 code when license plates are found and exported. Otherwise, it sends a 204 (NoContent) status code when no license plates were discovered that need to be exported. We will conditionally send an email if any response other than 200 is returned.

- Add an Office 365 Outlook Send Mail action to the condition's If false block. The email should be sent to you, have a subject of "Toll Booth license plate export failed" (or similar), and a message in the body that includes the Status code value from the ExportLicensePlates function.

- Save and run the Logic App

#### Exit criteria

- You should start receiving email alerts because the license plate data is not being exported. This is because we need to finish making changes to the ExportLicensePlates function so that it can extract the license plate data from Azure Cosmos DB, generate the CSV file, and upload it to Blob storage.

- While in the Logic Apps Designer, you will see the run result of each step of your workflow. A green checkmark is placed next to each step that successfully executed, showing the execution time to complete. This can be used to see how each step is working, and you can select the executed step and see the raw output.

  ![In the Logic App Designer, green check marks display next to Recurrence, ExportLicensePlates, Condition, and Send an email.](images/Hands-onlabunguided-Serverlessarchitectureimages/media/image11.png 'Logic App Designer')

- Disable the Logic App for now, so it doesn't keep emailing you while completing the next exercise

## Exercise 7: Configure continuous deployment for your Function App

**Duration**: 40 minutes

In this exercise, configure your Function App that contains the ProcessImages function for continuous deployment. You will first set up a GitHub source code repository, then set that as the deployment source for the Function App.

### Help references

|                                           |                                                                                          |
| ----------------------------------------- | :--------------------------------------------------------------------------------------: |
| **Description**                           |                                        **Links**                                         |
| Creating a new GitHub repository          |              <https://help.github.com/articles/creating-a-new-repository/>               |
| Continuous deployment for Azure Functions | <https://docs.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment> |

### Task 1: Create a GitHub repository

#### Tasks to complete

- Create a new public GitHub repository for this lab

#### Exit criteria

- Copy the repository's HTTPS git path and save for later

### Task 2: Add GitHub repository to your Visual Studio solution

#### Tasks to complete

- Commit your changes to the TollBooth starter project in Visual Studio

- Select Sync link after committing, then add the link to your GitHub repository under Push to Remote Repository. This should be the HTTPS git path you copied in the previous task.

- Publish to your GitHub repository

#### Exit criteria

- Refresh your GitHub repository page in your browser. You should see that the project files have been added. Navigate to the TollBooth folder of your repo. Notice that the local.settings.json file has not been uploaded. That's because the .gitignore file of the TollBooth project explicitly excludes that file from the repository, making sure you don't accidentally share your application secrets.

  ![On the GitHub Repository page for serverless-architecture-lab, on the Code tab, project files display.](images/Hands-onlabunguided-Serverlessarchitectureimages/media/image12.png 'GitHub Repository page')

### Task 3: Configure your Function App to use your GitHub repository for continuous deployment

#### Tasks to complete

- Open the Azure Function App you created whose name ends with **FunctionApp**, or the name you specified for the Function App containing the ProcessImage function

- Setup a new GitHub deployment option, pointing to your new GitHub repo

#### Exit criteria

- After continuous deployment is configured, all file changes in your deployment source are copied to the function app, and a full site deployment is triggered. The site is redeployed when files in the source are updated.

### Task 4: Finish your ExportLicensePlates function code and push changes to GitHub to trigger deployment

#### Tasks to complete

- Complete TODO items found in DatabaseMethods.cs

- Complete TODO item found in FileMethods.cs

- Commit and sync your changes to GitHub

#### Exit criteria

- You completed TODO items 5-7

- Go back to Deployments for your Function App in the portal. You should see an entry for the deployment kicked off by this last commit. Check the timestamp on the message to verify that you are looking at the latest one.

  ![On the Deployments blade, a partially-completed full-circle graph displays next to the message, Finished the ExportLicensePlates function, GitHub, building, 8:49 PM.](images/Hands-onlabunguided-Serverlessarchitectureimages/media/image13.png 'Deployments blade')

## Exercise 8: Rerun the workflow and verify data export

**Duration**: 10 minutes

With the latest code changes in place, run your Logic App and verify that the files are successfully exported.

### Task 1: Run the Logic App

#### Tasks to complete

- Re-enable your Logic App

- Run the Recurrence trigger

#### Exit criteria

- Select the latest run history item. If the expression result for the condition is **true**, then that means the CSV file should've been exported to Blob storage. Be sure to disable the Logic App so it doesn't keep sending you emails every 15 minutes.

  ![In Logic App Designer, in the Condition section, under Inputs, true is circled.](images/Hands-onlabunguided-Serverlessarchitectureimages/media/image14.png 'Logic App Designer')

### Task 2: View the exported CSV file

#### Tasks to complete

- Browse the export container in your Blob storage account

- Download the CSV file generated when you last ran your Logic App

#### Exit criteria

1.  The CSV file should look similar to the following:

    ![A CSV file displays with the following columns: FileName, LicensePlateText, TimeStamp, and LicencePlateFound.](images/Hands-onlabunguided-Serverlessarchitectureimages/media/image15.png 'CSV file')

- The ExportLicensePlates function updates all of the records it exported by setting the exported value to true. This makes sure that only new records since the last export are included in the next one. Verify this by re-executing the script in Azure Cosmos DB that counts the number of documents in the Processed collection where exported is false. It should return 0 unless you've subsequently uploaded new photos.

## After the hands-on lab

**Duration**: 10 minutes

In this exercise, attendees will deprovision any Azure resources that were created in support of the lab.

### Task 1: Delete the Resource group in which you placed your Azure resources.

1.  From the Portal, navigate to the blade of your **Resource Group** and select **Delete** in the command bar at the top

2.  Confirm the deletion by re-typing the **resource group name** and selecting **Delete**

3.  If you created a different resource group for your virtual machined, be sure to delete that as well

4.  Optionally, delete the GitHub repository you created for this lab by selecting **settings** and then **Delete this repository** from the GitHub website

You should follow all steps provided _after_ attending the hands-on lab.
