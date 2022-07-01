# Serverless architecture

## This workshop is archived and no longer being maintained.  Content is read-only.

Contoso is rapidly expanding its toll booth management business to operate in a much larger area. As this is not their primary business, which is online payment services, they are struggling with scaling up to meet the upcoming demand to extract license plate information from many new tollbooths, using photos of vehicles uploaded to cloud storage. Currently, they have a manual process where they send batches of images to a 3rd-party who manually transcodes the license plates to CSV files that they send back to Contoso to upload to their online processing system.

They want to automate this process in a way that is cost-effective and scalable. They believe serverless is the best route for them but do not have the expertise to build the solution.

November 2021

## Target Audience

Application developers

## Abstracts

### Workshop

In this workshop, you learn about setting up and configuring a serverless architecture within Azure using a combination of Azure Functions, Azure Logic Apps, Azure Event Grid, Azure Cosmos DB, and Azure Data Lake Storage. The focus is on removing server management from the equation, breaking down the solution into smaller components that are individually scalable, and allowing the customer to only pay for what they use.

At the end of this workshop, you will be able to break business logic down into discrete components that can independently scale and leverage vision algorithms to detect objects and extract text.  You’ll know how to utilize Cosmos DB as a highly available NoSQL data store, build workflows using Azure Logic Apps, and conditionally send alerts based on operations.  Finally, you’ll have the knowledge to monitor a serverless topology and implement a Continuous Deployment DevOps process to publish changes automatically.

### Whiteboard Design Session

In this whiteboard design session, you work with a group to design a solution for processing vehicle photos in near real-time, as they are uploaded to a data lake, using serverless technologies on Azure. The license plate data must be extracted and stored in a highly available NoSQL data store for exporting. The data export process is orchestrated by a serverless Azure component that coordinates exporting new license plate data to file storage and sending notifications as needed. You will also configure a Continuous Deployment process to publish new changes to Function Apps automatically. Finally, the entire processing pipeline will need to be monitored, with particular attention paid to components scaling to meet processing demand.

At the end of this whiteboard design session, you will have greater insight into how best to take advantage of serverless architectures. You will understand better how to design highly scalable and cost-effective solutions that require very little code and virtually no infrastructure compared to traditional hosted web applications and services.

### Hands-on Lab

In this hands-on lab, you implement an end-to-end solution using a supplied sample based on Microsoft Azure Functions, Azure Cosmos DB, Azure Event Grid, and related services. The scenario will include implementing compute, storage, workflows, and monitoring using various components of Microsoft Azure. You can implement the hands-on lab on your own. However, it is highly recommended to pair up with other members at the lab to model a real-world experience and to allow each member to share their expertise for the overall solution.

At the end of the hands-on-lab, you will have confidence in designing, developing, and monitoring a serverless solution that is resilient, scalable, and cost-effective.

## Azure services and related products

- [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)
- [Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/what-are-cognitive-services)
- [Azure Computer Vision](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/overview)
- [Azure Event Grid](https://docs.microsoft.com/azure/event-grid/overview)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)
- [Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview)
- [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)
- [Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-overview)
- [Visual Studio 2019](https://visualstudio.microsoft.com/vs/)

## Azure solution

Cloud-Native Apps

## Related references, resources, and material

- [Serverless Web Application Reference Architecture](https://docs.microsoft.com/azure/architecture/reference-architectures/serverless/web-app)
- [Serverless event processing using Azure Functions Reference Architecture](https://docs.microsoft.com/azure/architecture/reference-architectures/serverless/event-processing)
- [MCW](https://microsoftcloudworkshop.com/)

## Help & Support

We welcome feedback and comments from Microsoft SMEs & learning partners who deliver MCWs.

**_Having trouble?_**

- First, verify you have followed all written lab instructions (including the Before the Hands-on lab document).
- Next, submit an issue with a detailed description of the problem.
- Do not submit pull requests. Our content authors will make all changes and submit pull requests for approval.

If you are planning to present a workshop, _review and test the materials early_! We recommend at least two weeks prior.

### Please allow 5 - 10 business days for review and resolution of issues.
