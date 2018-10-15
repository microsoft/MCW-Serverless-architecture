![](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Serverless architecture
</div>

<div class="MCWHeader2">
Whiteboard design session student guide
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

- [Serverless architecture whiteboard design session student guide](#serverless-architecture-whiteboard-design-session-student-guide)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Step 1: Review the customer case study](#step-1-review-the-customer-case-study)
    - [Customer situation](#customer-situation)
    - [Customer needs](#customer-needs)
    - [Customer objections](#customer-objections)
    - [Infographic for common scenarios](#infographic-for-common-scenarios)
  - [Step 2: Design a proof of concept solution](#step-2-design-a-proof-of-concept-solution)
  - [Step 3: Present the solution](#step-3-present-the-solution)
  - [Wrap-up](#wrap-up)
  - [Additional references](#additional-references)

<!-- /TOC -->

# Serverless architecture whiteboard design session student guide

## Abstract and learning objectives 

In this whiteboard design session, you will work with a group to design a solution for processing vehicle photos as they are uploaded to a storage account, using serverless technologies on Azure. The license plate data needs to be extracted and stored in a highly available NoSQL data store for exporting. The data export process will be orchestrated by a serverless Azure component that coordinates exporting new license plate data to file storage and sending notifications as needed. You will also configure a Continuous Deployment process to automatically publish new changes to Function Apps. Finally, the entire processing pipeline will need to be monitored, with particular attention paid to components scaling to meet processing demand.

At the end of this whiteboard design session, you will have gained insight on how best to take advantage of the new serverless wave by designing a highly scalable and cost-effective solution that requires very little code and virtually no infrastructure, compared to traditional hosted web applications and services.

## Step 1: Review the customer case study

**Outcome**

Analyze your customer’s needs.

Timeframe: 15 minutes

Directions: With all participants in the session, the facilitator/SME presents an overview of the customer case study along with technical tips.

1.  Meet your table participants and trainer
2.  Read all of the directions for steps 1–3 in the student guide
3.  As a table team, review the following customer case study

### Customer situation

Contoso, ltd. was founded in 2011 in Houston, Texas, and provides custom software development solutions for a number of clients. In addition to custom software development, they also have developed a financial billing and payment suite of software aimed at several vertical markets, from e-commerce to medical, financial services. They have recently added toll road booth management, as a new market opportunity opened to handle vehicle tracking and toll billing near their home office. Since this new business venture was a minor addition to their impressive portfolio of billing services, they have not dedicated significant resources to the vehicle processing portion of their custom-built TollBooth software suite. The most feature-rich component of this software suite is their existing payment management system that has been expanded to send bills to drivers after passing through any number of the managed toll booths. Included in the bill are a date/time stamp, toll booth location, and a photo of the vehicle as it passed through the booth.

Because so few resources were applied to the TollBooth software, which was meant to handle just a handful of local toll booths, Contoso has been using a manual process to identify license plates and send that data to their billing software. As a car passes through a toll booth, a medium resolution image is taken of the car to identify its license plate numbers/characters which will ultimately be used to look up and bill the customer. Currently, they periodically package and send those images to a 3^rd^ party vendor, who manually identifies the license plate numbers and sends the list back to Contoso when they are done. At this point, Contoso collects batches of 1,000 transactions, saves the information to a CSV file hosted by an FTP server, where their downstream accounting system extracts the license plate information and bills the customer.

Contoso has recently been awarded a large, yet unexpected contract to manage toll booths across most of the state, resulting in a 2500% increase in coverage, and is in talks with Oklahoma and New Mexico to provide toll booth services in those states as well. Despite the obvious benefits of such rapid growth, the company is concerned that they will be unable to meet the demand that comes with it. They are confident that their billing software can handle the load, as it has been the primary focus of development from the start, and has expanded into other markets, proving its ability to handle large-scale transactions and data processing. However, Contoso is concerned about how rapidly they can automate the license plate processing portion of their TollBooth infrastructure, while ensuring that the automated solution can scale to meet demand, particularly during unexpected spikes in traffic.

"What we need is a lightweight, yet powerful method that quickly pulls in vehicle photos as they are uploaded, and intelligently detect the license plate numbers, all while efficiently handling spikes in traffic," says Abby Burris, CIO, Contoso, ltd. "Most importantly, we do not want to manage long-lived application instances, we want to minimize our cost during slow traffic periods, and we need something our developers can quickly integrate into our existing infrastructure without a lot of training. Our primary goal is to rapidly replace this manual processing pipeline while continuing to devote our development resources to our core billing platform services."

Abby went on to say that she has been following the relatively new serverless computing movement, and believes that the benefits serverless brings a good match for what they are hoping to achieve in this project. The fewer infrastructure responsibilities for the already maxed out IT team, the better. However, she is not sure whether it is possible to locally develop the serverless components and automate the deployment process using CI/CD DevOps practices like they can with their more traditional web applications.

Since Contoso does not have any machine learning experts or data scientists on staff, they would like to know their options for using a ready-made machine learning service that can perform the license plate recognition task on the photos. They would prefer to go this route, rather than to train their staff to properly create and train advanced machine learning models, then having to incur the cost of hosting their own machine learning service for conducting this one task.

Contoso wants to store captured vehicle photos in cloud storage for retrieval via custom web and mobile applications. These photos will need to be accessible by the downstream billing service for inclusion on the customer bills. Also, any photos containing license plates that could not be automatically detected will need to be marked as such and accessed later on for manual validation. Similarly, as photos are successfully processed for license plate detection, the plate information needs to be saved to a database, along with the capture date/time and tollbooth Id. Contoso has a customer service department who can monitor the queue of photos marked for manual validation, and enter the license plates into a web-based form so they can be exported along with the automatically processed license plate data.

The process to export license plate data also needs to be automated. Contoso would like an automated workflow that runs on a regular interval to extract new license plate data since the last export and saves it in a CSV file that gets ingested by the billing software. They already have the CSV ingest process automated, so no changes are required beyond saving the file. Their FTP server would need to be modified to point to the cloud storage container instead of its local file system, which is a simple process that is out of scope for the automation task. The export interval should be set to one hour, but be flexible to increasing or decreasing the interval as needed. This interval is based on the automated file ingest process used by the billing system.

Customer service has requested that an alert email should be sent to a specific monitoring address if at any point the automated export does not complete due to no data. Given the export interval and the average number of vehicles that pass through the toll booths during any given hour, having no data to export would be the exception, not the rule. The alert would give them the peace of mind that they could go through internal support channels to investigate the license processing pipeline to address any issues promptly, without being inundated by too many unnecessary alert notifications. They are using Office 365 for their email services.

In addition to the email alert notifications, Contoso would like to have a centralized monitoring dashboard they can use to watch the automated process in real time and drill down into historical telemetry later on if needed. This dashboard will help them keep an eye on the various Azure components, watching for any bottlenecks or weak points in their overall solution. The monitoring dashboard should also allow them to add custom alert notifications that get sent to IT staff if anything goes wrong.

"Our directors want to see where we can take the notion of a serverless architecture, and see if there truly are long-term performance and cost benefits," says Burris. "With the unexpected windfall of the toll booths contract, they want to make sure we have a tested strategy we can fall back on in the future when our IT and development teams are called upon once again to achieve the impossible."

As a stretch goal, Contoso would like to know that the license processing pipeline they have implemented is extensible to any number of future scenarios that are made possible once the license plate has been successfully processed. The one scenario they currently have in mind is how the pipeline would support more advanced analytics, providing the capability to process the licenses plates in a streaming fashion as well as to process historical license plate capture events in a batch fashion (e.g., that could scale to analyze the historical data in the 10's of terabytes). They are curious if these analytic scenarios could also be implemented using a serverless architecture.

### Customer needs

1.  Replace manual process with a reliable, automated solution using serverless components

2.  Take advantage of a machine learning service that would allow them to accurately detect license plate numbers without needing artificial intelligence expertise

3.  Mechanism for manually entering license plate images that could not be processed

4.  Have a solution that can scale to any number of cars that pass through all toll booths, handling unforeseen traffic conditions that cause unexpected spikes in processed images

5.  Establish an automated workflow that periodically exports processed license plate data on a regular interval, and sends an alert email when no items are exported

6.  Would like to locally develop the serverless components and establish an automated deployment pipeline from source control

7.  Use a monitoring dashboard that can provide a real-time view of serverless components, historical telemetry data for deeper analysis, and supports custom alerts

8.  Design an extensible solution that could support serverless batch and real-time analytics, as well as other scenarios in the future

### Customer objections

1.  We are concerned about how individual serverless components will be able to "talk" to each other and reliably pass messages through the pipeline

2.  Will a serverless architecture that has the capacity to infinitely scale put us at risk for huge monthly bills?

3.  How do we make sure that erroneous image processing does not make certain toll bills fall through the cracks or, even worse, send a bill to the wrong person?

### Infographic for common scenarios

![The Common Scenario diagram begins with an Internet icon on the left. Two arrows point from this icon to an Azure Storage Blobs Icon, and an Azure API Management icon. The Azure Storage Blobs icon points to an Azure functions icon, which in turn points to both a second Azure Functions icon (via an Event Grid arrow), and a second Azure Storage Blobs icon, which then points and ends at a Logic Apps icon. The Azure API Management icon points to two separate Azure Functions icon, which both point back to an Azure Cosmos DB icon, when then points to and ends at a Power BI icon.](images/Whiteboarddesignsessiontrainerguide-Serverlessarchitectureimages/media/image2.png 'Common Scenario diagram')

## Step 2: Design a proof of concept solution

**Outcome**
Design a solution and prepare to present the solution to the target customer audience in a 15-minute chalk-talk format.

Timeframe: 60 minutes

**Business needs**

Directions: With all participants at your table, answer the following questions and list the answers on a flip chart.

1.  Who should you present this solution to? Who is your target customer audience? Who are the decision makers?
2.  What customer business needs do you need to address with your solution?

**Design**
Directions: With all participants at your table, respond to the following questions on a flip chart.

_High-level architecture_

1.  Without getting into the details (the following sections will address the particular details), diagram your initial vision for handling the top-level requirements for the license plate processing serverless components, OCR capabilities, data export workflow, and monitoring plus DevOps.

_License plate processing serverless components_

1.  Which Azure messaging service would you recommend using to orchestrate event-driven activities between the serverless components?

2.  What Azure service would you suggest Contoso use to execute custom business logic code when an event is triggered?

3.  Which pricing tier for the service would you recommend that would automatically scale to handle demand while charging only for work that was performed?

4.  How do you ensure that downstream components, such as machine learning APIs, databases, and file stores, are not overloaded by the potential high load created when your serverless components dynamically scale?

5.  What Azure service would you recommend for storing the license plate data? Consider options that automatically scale to meet demand, and offer bindings to other serverless components that simplify connecting to and storing data within the data store.

_License plate OCR_

1.  What service would you recommend Contoso use to conduct license plate object character recognition (OCR) processing to extract the license plate number from each photo as it enters the system?

2.  How would you integrate the OCR service to your license plate processing flow?

_Data export workflow_

1.  What Azure service would you recommend to create an automated workflow that runs on a regular interval to export processed license plate data and send alerts as needed?

2.  Which other services would you integrate into your workflow?

_Extensible serverless analytics_

1.  Assuming they would like to be able to plug-in more solutions that respond to the event when a license plate has been successfully extracted from an image, how would you extend your solution using Event Grid? Be specific on the system topics, custom topics and subscriptions at play.

2.  What pipeline would you plug-into an Event Grid subscription listening for license plate events that could be used to provide real-time and batch analytics as a serverless solution?

_Monitoring and DevOps_

1.  What tools and services would you recommend Contoso use to develop the serverless components locally, synchronize with a source code repository, and implement continuous deployment?

2.  How would you monitor all the executing serverless components in real time from a single dashboard?

3.  Does your monitoring solution support exploring historical telemetry and configuring alerts?

**Prepare**

Directions: With all participants at your table:

1.  Identify any customer needs that are not addressed with the proposed solution
2.  Identify the benefits of your solution
3.  Determine how you will respond to the customer’s objections

Prepare a 15-minute chalk-talk style presentation to the customer.

## Step 3: Present the solution

**Outcome**

Present a solution to the target customer audience in a 15-minute chalk-talk format.

Timeframe: 30 minutes

**Presentation**

Directions:

1.  Pair with another table
2.  One table is the Microsoft team and the other table is the customer
3.  The Microsoft team presents their proposed solution to the customer
4.  The customer makes one of the objections from the list of objections
5.  The Microsoft team responds to the objection
6.  The customer team gives feedback to the Microsoft team
7.  Tables switch roles and repeat Steps 2–6

## Wrap-up

Timeframe: 15 minutes

- Tables reconvene with the larger group to hear an SME share the preferred solution for the case study

## Additional references

|                                                     |                                                                                                                       |
| --------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------: |
| **Description**                                     |                                                       **Links**                                                       |
| Introduction to Azure Functions                     |                      <https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview>                      |
| What are Logic Apps?                                |                  <https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-what-are-logic-apps>                   |
| About Azure Cosmos DB                               |                            <https://docs.microsoft.com/en-us/azure/cosmos-db/introduction>                            |
| Choose between Azure services that deliver messages |                    <https://docs.microsoft.com/en-us/azure/event-grid/compare-messaging-services>                     |
| Monitor Azure Functions using Application Insights  |                     <https://docs.microsoft.com/en-us/azure/azure-functions/functions-monitoring>                     |
| Introduction to Azure Event Grid                    |                             <https://docs.microsoft.com/en-us/azure/event-grid/overview>                              |
| Call Azure Functions from logic apps                | <https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-azure-functions> |
| Azure Cosmos DB + Azure Functions                   |                   <https://docs.microsoft.com/en-us/azure/cosmos-db/serverless-computing-database>                    |
| Continuous deployment of Azure Functions            |               <https://docs.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment>                |
| Code and test Azure Functions locally               |                     <https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local>                      |
