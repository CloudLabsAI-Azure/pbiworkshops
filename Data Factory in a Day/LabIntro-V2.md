# Microsoft Fabric - Data Factory in a Day

### Overall Estimated Duration: 4 Hours

## Overview

The purpose of this lab is to explore various data ingestion and transformation experiences. This includes the orchestration of end-to-end projects with [data pipelines](https://learn.microsoft.com/fabric/data-factory/create-first-pipeline-with-sample-data) and an introduction to [dataflow gen2]() which represents the next generation of no-code/low-code data transformation that now support [data destinations](https://learn.microsoft.com/fabric/data-factory/dataflows-gen2-overview#data-destinations) and [fast copy](https://learn.microsoft.com/fabric/data-factory/dataflows-gen2-fast-copy) data ingestion, which enhances the efficiency of data movement.

## Architecture

The process starts with a data pipeline that brings raw data into the Lakehouse Bronze layer, which stores the unprocessed information. This data is then cleaned and organized through another pipeline and moved into the Lakehouse Silver layer. From there, Dataflows Gen2, supported by Copilot, helps further transform the data to make it ready for analysis. The final, processed data is loaded into the Data Warehouse Gold layer using either Dataflows Gen2 or a copy job. This curated data is then used in Power BI for dashboards, reports, and business insights.

## Architecture Diagram

![](./Media/23042025(1).png)

## Explanation of Components

The architecture for this lab involves the following key components:

1. **Data Pipeline:** Used for ingesting and moving data between different stages in the architecture. It automates the extraction, loading, and initial processing of data.

2. **Lakehouse (Bronze):** This is the first landing zone for raw data. It stores unprocessed or minimally processed data collected from various sources.

3. **Lakehouse (Silver):** The Silver layer contains data that has been cleaned, filtered, and structured. It serves as an intermediate stage, preparing data for advanced transformations.

4. **Dataflows Gen2:** A low-code/no-code transformation tool used to shape, enrich, and transform data from the Lakehouse. Integrated with **Copilot**, it allows users to build dataflows more intuitively and efficiently.

5. **Copy Job:** A tool or process used to transfer data from the Lakehouse Silver layer into the Data Warehouse Gold layer when needed.

6. **Data Warehouse (Gold):** The Gold layer is optimized for analytics. It stores fully transformed, business-ready data that supports reporting, dashboards, and decision-making.

7. **Power BI:** A business intelligence tool used to visualize and analyze data. It connects to the Data Warehouse to create interactive reports and dashboards for end users.

## Getting Started with the Lab
 
Welcome to your Data Factory in a Day with Microsoft Fabric workshop! We've prepared a seamless environment for you to explore and learn about Azure services. Let's begin by making the most of this experience:

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and lab guide will be right at your fingertips within your web browser.
 
![](./media/1.png)

### Virtual Machine & Lab Guide
 
Your virtual machine is your workhorse throughout the workshop. The lab guide is your roadmap to success.
 
## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.
 
![](./media/2.png)
 
## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the Top right corner.
 
![](./media/3.png)
 
## Managing Your Virtual Machine
 
Feel free to start, stop, or restart your virtual machine as needed from the **Resources** tab. Your experience is in your hands!
 
![](./media/4.png)

## Lab Guide Zoom In/Zoom Out

To adjust the zoom level for the environment page, click the **A↕ : 100%** icon located next to the timer in the lab environment.

   ![](media/labzoom-1.png)

## Let's Get Started with Power BI Portal
 
1. On your virtual machine, click on the Power BI Portal icon as shown below:
 
   ![](./media/7.png)

2. On the **Sign in to Microsoft Azure** tab you will see the login screen, in that enter the following email/username, and click on **Next**.
 
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>
 
     ![](./media/8.png)
 
3. Now enter the following password and click on **Sign in**.
 
   - **Password:** <inject key="AzureAdUserPassword"></inject>
 
     ![](./media/9.png)
 
1. If you see the pop-up Action Required, click Ask Later.

   ![](media/asklater.png)

   >**NOTE:** Do not enable MFA, select **Ask Later**.
     
1. If you see the pop-up **Stay Signed in?**, select **No**.

   ![](media/Sign-in-no.png)

1. If you see the pop-up **You have free Azure Advisor recommendations!**, close the window to continue the lab.

1. If a **Welcome to Microsoft Azure** popup window appears, select **Cancel** to skip the tour.
   
## Support Contact
 
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:
- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Now, click on **Next** from the lower right corner to move on to the next page.
 
   ![](./media/10.png)

### Happy Learning!!
