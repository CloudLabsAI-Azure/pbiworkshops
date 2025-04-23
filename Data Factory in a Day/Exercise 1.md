# Microsoft Fabric - Data Factory in a Day - Lab 1


## Contents
- Introduction
- Task 1: Getting Started with Microsoft Fabric: Activate Trial and Set Up a Workspace
    - Task 1.1: Medallion task flow
    - Task 1.2: Copy activity
- Task 2: Authoring canvas 
    - Task 2.1: Pipeline expression builder


## Introduction
In this lab, you will learn how to create a project task flow and understand the basics of Data Factory experiences. This workshop is designed to provide you with hands-on experience in building and managing your solution using Microsoft Fabric. By the end of this lab, you will have a foundational understanding of key concepts and tools that are essential for efficient data management and transformation.

1. First, you will learn how to create a medallion architecture [task flow](https://learn.microsoft.com/fabric/get-started/task-flow-overview) within a workspace. The medallion architecture is a design pattern that organizes data into different layers, such as bronze, silver, and gold, to improve data quality and accessibility. This task flow will help you understand how to structure and manage your data effectively.

1. Next, you will create a [lakehouse](https://learn.microsoft.com/fabric/data-engineering/lakehouse-overview) item for data storage. A lakehouse combines the best features of data lakes and data warehouses, providing a unified platform for storing and analyzing large volumes of data. This step is crucial for setting up a scalable and efficient data solution that supports various data processing and analytics tasks.

1. Finally, you will create a data pipeline to ingest sample data using the [copy activity](https://learn.microsoft.com/fabric/data-factory/copy-data-activity) within a data pipeline. Data pipelines are essential for automating the movement and transformation of data from various sources to destinations. The copy activity is a powerful tool that allows you to efficiently transfer data between different storage systems, ensuring that your data is always up-to-date and ready for analysis.

## Task 1: Getting Started with Microsoft Fabric: Activate Trial and Set Up a Workspace

1. In the top-right corner of Power BI, click the **User icon**, then select **Free trial** from the menu.

    ![](./Media/23042025(14).png)

1. On Activate your 60-day free Fabric trial capacity dialog opens. Select **Activate**.

    ![](./Media/23042025(12).png)

1. Successfully upgraded to Microsoft Fabric dialog opens. Select **Fabric Home Page**.

    ![](./Media/23042025(13).png)

1. You will be navigated to the **Microsoft** **Fabric Home page**.

    ![](./Media/23042025(15).png)

1. Now let's create a workspace with a Fabric license. Select **Workspaces** **(1)** from the left navigation bar. A dialog opens.

2. Click **+ New workspace** **(2)** found at the bottom of the pop-out menu.

    ![](./Media/23042025(16).png)

3. **Create a workspace** dialog opens on the right side of the browser.

4. In the **Name** field enter **Data Factory in a Day_<inject key="Deployment ID" enableCopy="false"/>**

    >**Note:** The workspace name must be unique. Make sure a green check mark with "This name is available" is displayed below the Name field.

5. If you choose, you can enter a Description for the workspace. This is an optional field.

6. Click on **Advanced** to expand the section.

   ![](./Media/23042025(17).png)

7. Under **License mode**, make sure **Trial** is selected. (It should be selected by default.)

8. Select **Apply** to create a new workspace.

    ![](./Media/23042025(18).png)

## Task 1.1: Medallion task flow

