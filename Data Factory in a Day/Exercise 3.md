# **Microsoft Fabric - Data Factory in a Day - Lab 3**

![](./Media/main3lab.png)

## Contents
- Introduction
    - Task 1: Creating Golden data storage and a Dataflow Gen2
    - Task 2: Connecting to lakehouse tables
    - Task 3: Preparing data using Power Query Online
    - Task 4: Outputting data to the warehouse destination
    - Task 5: Group queries and save
    - Task 6: Further transform task flow
    - Task 7: Copy data into the warehouse
    - Task 8: End-to-end orchestration with pipelines
    - Task 9: Unlock the power of T-SQL, Power BI Direct Lake mode, Excel connectivity, and more with your data
- Summary

## Introduction
In this lab, you'll learn about how to shape and orchestrate your data using Data Factory experiences.

1. How to create a [Dataflow Gen2](https://docs.microsoft.com/power-bi/transform-model/dataflows/dataflows-introduction-self-service) to prepare and load data using Power Query Online.

1. Understanding the [storage and compute staging](https://blog.fabric.microsoft.com/blog/data-factory-spotlight-dataflows-gen2?ft=Data-factory:category) architecture for large scale data transformations.

1. Configuring [data destination outputs](https://learn.microsoft.com/fabric/data-factory/dataflow-gen2-data-destinations-and-managed-settings).

1. How to create and configure a [Copy job](https://learn.microsoft.com/fabric/data-factory/what-is-copy-job) for a streamlined and user-friendly data ingestion process from source to destination.


## Task 1: Creating Golden data storage and a Dataflow Gen2

1. In the Fabric portal, open the previously created workspace named **Data Factory in a Day_<inject key="Deployment ID" enableCopy="false"/>**.

1. Select the **+ New item** option on the **Gold data** from your task flow to add another storage item to your project. Within the **Item type** selection, select **Warehouse**.

    ![Golden data new item](./Media/task-flow-new-item-gold-data.png)

1. In the New warehouse window, set the warehouse name to **g_IADWarehouse** (shorthand for gold in a day) and then select **Create**.

    ![Golden data warehouse](./Media/new-warehouse-giad.png)

1. Within the warehouse item from the **Home** tab select **Get data** from **New Dataflow Gen2**.

    ![New dataflow gen2 from warehouse](./Media/new-dataflow-gen2-from-warehouse.png)

1. In the top-left corner of the **New Dataflow Gen2** window, rename the dataflow to **PrepContoso**, then press **Enter** to apply the change.
    
    ![Name the dataflow](./Media/23042025(55).png)

## Task 2: Connecting to lakehouse tables

1. Navigate to the **Home** tab, click on **Get data**, and then choose **More...** to access additional data source options.

    ![Name the dataflow](./Media/23042025(56).png)

1. Within the Get data explorer's search bar, type **s_iad** to locate the silver lakehouse item. Select the **s_IADLake** item within the OneLake catalog's returned results.

    ![Search for silver lakehouse](./Media/dataflow-choose-data-source.png)

1. From the **Get data** table navigator, select the specified tables to perform data transformation and merge operations for downstream business intelligence projects, then click **Create**.

    | Table Name |
    | :--- |
    | DimCustomer |
    | DimGeography |
    | DimProduct |
    | DimProductCategory |
    | DimProductSubcategory |
    | FactOnlineSales |

    ![Get data select tables](./Media/choose-data-dims.png)

## Task 3: Preparing data using Power Query Online

1. Select the **DimCustomer (1)** table and from the **Home (2)** tab, navigate to the **Combine (3) -> Merge queries (4)** option and select **Merge queries as new (5)**.

    ![Merge dim customer](./Media/23042025(57).png)

1. From the Merge query window, set the **Right table for merge** to **DimGeography**. In the top right corner, select the lightbulb which has detected a possible column match. In this example, both tables contain a column titled **GeographyKey**. Select this option to set the columns to be merged on. For the Join kind, select **Inner** and then **OK** to proceed.

    ![Merge dim customer](./Media/23042025(58).png)

1. On the right-hand side in the Query settings pane, update the **Name** of the query to be **DimCustomers**

    ![Merge dim customer](./Media/23042025(59).png)

1. Navigate to the far right for the **DimCustomers** table and select the joined **DimGeography** table column's top right corner to expand the table, from the avaialble column selections deselect **GeographyKey** since this column is what we used to merge on and already exists in the dataset before selecting **OK** to continue.

    ![Expand DimGeography](./Media/merge-dimcustomer-expand.png)

1. Next, select the **DimProduct** table and from the **Home** tab, navigate to the **Combine -> Merge queries** option and select **Merge queries as new**.

    ![Merge dim customer](./Media/23042025(60).png)

1. From the Merge query window, set the **Right table for merge** to **DimProductSubcategory**. In the top right corner, select the lightbulb which has detected a possible column match. In this example, both tables contain a column titled **ProductSubcategoryKey**. Select this option to set the columns to be merged on. For the Join kind, select **Inner** and then **OK** to proceed.

    ![Merge dim customer](./Media/23042025(61).png)

1. Navigate to the far right fo the **Merge** Queries and select the joined **DimProductSubcategory** table column's top right corner to expand the table, from the avaialble column selections **deselect** **ProductSubCategoryKey** since this column is what we used to merge on and already exists in the dataset before selecting **OK** to continue.

    ![Expand dimproductsubcategory](./Media/merge-dimproduct-expand-dimproductsubcategory.png)

1. Select the **Merge** query and from the **Home** tab, navigate to the **Combine -> Merge queries** option and select **Merge queries**.

    ![Merge dim customer](./Media/23042025(62).png)

1. From the Merge query window, set the **Right table for merge** to **DimProductCategory**. In the top right corner, select the lightbulb which has detected a possible column match. In this example, both tables contain a column titled **ProductCategoryKey**. Select this option to set the columns to be merged on. For the join kind, select **Inner** and then **OK** to proceed.

    ![Merge dim customer](./Media/23042025(65).png)

1. On the right-hand side in the Query settings pane, update the **Name** of the query to be **DimProducts**

    ![Updated query name to DimProducts](./Media/dimproducts-rename.png)

1. Navigate to the far right for the **DimProducts** table and select the joined **DimProductCategory** table column's top right corner to expand the table, from the avaialble column selections deselect **ProductCategoryKey** since this column is what we used to merge on and already exists in the dataset before selecting **OK** to continue.

    ![Expand dimproductcategory](./Media/merge-dimproduct-expand-dimproductcategory.png)

## Task 4: Outputting data to the warehouse destination

1. First, we need to remove the default data destination. Select the **FactOnlineSales (1)** query, on the **Home** tab, click on **Default data destination (2)**, and then select **Remove (3)**.

    ![Merge dim customer](./Media/23042025(64).png)

1. On Remove default data destination dialog opens. Select **Remove**.

    ![Merge dim customer](./Media/23042025(66).png)

1. Select the **FactOnlineSales** query again and from the **Home** tab, select **Add data destination** and then choose the **Warehouse** option.

    ![Add warehouse destination](./Media/add-warehouse-destination.png)

1. If a connection window asks you to authenticate, confirm your credentials. Otherwise, in the **Choose destination target** window, select **g_IADWarehouse** and then click **Next**.

    ![Choose destination target for FactOnlineSales](./Media/factonlinesales-data-destination.png)

1. In the **Choose destination settings** window, change the **Update method** to **Append** and click **Save settings**.

    ![Append FactOnlineSales](./Media/factonlinesales-append-destination.png)

1. In the bottom right-hand corner, hover above the **Data destination** field to view the configuration values of your queries at a glance.

    ![Confirm the destination configuration of FactOnlineSales](./Media/factonlinesales-destination-configured.png)

1. Select the **DimCustomers** query and from the **Home** tab, select **Add data destination** and then choose the **Warehouse** option.

    ![Add warehouse destination for DimCustomers](./Media/dimcustomers-add-destination.png)

1. If a connection window asks you to authenticate, confirm your credentials. Otherwise, in the **Choose destination target** window, select **g_IADWarehouse** and then click **Next**.

    ![Choose destination target for DimCustomers](./Media/dimcustomers-data-destination.png)

1. In the **Choose destination settings** window, ensure the **Update method** is set to the default **Replace** and then click **Save settings**. This will delete data from the table and replace the values after each refresh.

    ![Replace update method for DimCustomers](./Media/dimcustomers-replace-destination.png)

1. Select the **DimProducts** query and from the **Home** tab, select **Add data destination** and then choose the **Warehouse** option.

    ![Add warehouse destination for DimProducts](./Media/dimproducts-add-destination.png)

1. If a connection window asks you to authenticate, confirm your credentials. Otherwise, in the **Choose destination target** window, select **g_IADWarehouse** and then click **Next**.

    ![Choose destination target for DimProducts](./Media/dimproducts-data-destination.png)

1. In the **Choose destination settings** window, ensure the **Update method** is set to the default **Replace** and then click **Save settings**. This will delete data from the table and replace the values after each refresh.

    ![Replace update method for DimCustomers](./Media/dimproducts-replace-destination.png)

## Task 5: Group queries and save

1. Select the **DimCustomer**, **DimGeography**, **DimProduct**, **DimProductCategory** and **DimProductSubcategory** queries by holding the shift key, as they are all adjacent to each other. Right-click and select **Move to group**, then select **New group..**

    ![Data reference group](./Media/new-group-data-reference.png)

1. In the New group window, set the properties as needed below and select **OK**.

    | Name | Description |
    | :-- | :-- |
    | Data reference | Data used only as a source from the silver lakehouse |

    ![New data reference group](./Media/data-reference-group.png)

1. Select the **FactOnlineSales**, **DimCustomers** and **DimProducts** queries by holding the control key. Right-click and choose **Move to group**, then select **New group...**

    ![Create new data load group](./Media/new-group-data-load.png)

1. In the New group window, set the properties as needed below and select **OK**.

    | Name | Description |
    | :-- | :-- |
    | Data load | Data loaded to the gold warehouse |

    ![New group data load description](./Media/data-load-group.png)

1. Click **Publish** to save and apply the changes to the dataflow.

    ![New group data load description](./Media/23042025(67).png)

## Task 6: Further transform task flow

1. If you don't automatically return to the workspace upon closing the dataflow, select the workspace name on the left side-rail.

    ![](./Media/23042025(24).png)

1. From the task flow, select the **Further transform** task and click on the paper clip icon to assign a previously created item.

    ![Attach further transform](./Media/attach-further-transform.png)

1. Select the **PrepContoso** item and then press **Select**.

    ![Attach PrepContoso](./Media/attach-prepcontoso-item.png)

1. From the task flow, select the **Further transform** task and click on the **+ New item** option. Within the Create an item pane, display properties, change the toggle to the **All items** option.

    ![Further transform all items](./Media/further-transform-all-items.png)

1. From the list of available items, navigate to the Data Factory section and select the **Copy job** item.

    ![New copy job item](./Media/new-copy-job-item.png)

## Task 7: Copy data into the warehouse

1. In the New copy job window, set the copy job name to **CopyContoso** and then select **Create**.

    ![New the copy job](./Media/new-copy-job-name.png)

1. From the Copy job window, search for the data source starting with **s_IAD** in the search bar and then select **s_IADLake** from the OneLake catalog list.

    ![Copy job choose data source](./Media/copy-job-data-source.png)

1. Now that you're on the **Choose data** step, select the following tables:

    | Table Name |
    | :-- |
    | DimDate |
    | DimEmployee |
    | DimStore |

    ![Copy job choose table data](./Media/copy-job-choose-data.png)

1. The copy job also supports a limited set of transformations, such as column mapping, setting schema names, and renaming tables. Expand the **DimStore** table and then deselect the **GeoLocation** and **Geometry** columns. Once done, select **Next** to continue.

    ![Copy job choose columns](./Media/copy-job-choose-columns.png)

1. Within the Choose data destination step, search for the data source starting with **g_IAD** in the search bar and then select **g_IADWarehouse** from the OneLake catalog list.

    ![Copy job data destination](./Media/copy-job-data-destination.png)

1. Within the Map to destination step, you can review the added tables and update the schema or table names. Once done reviewing, select **Next** to continue.

    ![Copy job map to destination](./Media/copy-job-map-to-destination.png)

1. On the Settings step, review the Copy job mode options and then select **Next** to continue.

    ![Copy job mode](./Media/copy-job-mode.png)

1. On the Review + save step, **deselect** the **Start data transfer immediately** option and then select **Save** to continue.

    ![Copy job review and save](./Media/copy-job-review-save.png)

1. Now that you've reviewed the configuration, from the **Home** tab, select the **Run** option to begin copying data from the lakehouse into the warehouse.

    ![Copy job run](./Media/copy-job-run.png)

1. You can monitor the copy job in the **Results** tab at the bottom to confirm that it has successfully completed.

    ![Copy job succeeded](./Media/copy-job-succeeded.png)

1. Hover over the copy job on the left side-rail and select the **X** to close it.

    ![Copy job close](./Media/copy-job-close.png)

## Task 8: End-to-end orchestration with pipelines

1. Within the workspace, select the **Initial process** task flow item and from the filtered list, select the **createContosoTables** pipeline.

    ![Initial process task flow](./Media/create-contoso-tables-pipeline.png)

1. From the **Home** tab, add a new **Dataflow** activity to the pipeline.

    ![Add a dataflow activity](./Media/create-contoso-tables-dataflow.png)

1. Drag the **On success** conditional path between the **For each file** activity and the new **Dataflow1** activity. Next, go to the **Settings** section and within the Dataflow drop-down, select the **PrepContoso** dataflow.

    ![Dataflow settings configurations](./Media/create-contoso-tables-dataflow-settings.png)

1. With the dataflow activity still selected, go to the **General** tab and update the activity name to **PrepContoso**. Once complete, select the **Save** icon.

    ![Dataflow general settings](./Media/create-contoso-tables-dataflow-general.png)

1. On the left side-rail, select the **X** to close out of the **createContosoTables** pipeline.

    ![Close data pipeline](./Media/create-contoso-tables-close-pipeline.png)

1. Within the workspace, select the **High-volume data ingest** task flow item and from the filtered list, select the **getContosoSample** pipeline.

    ![Add the invoke pipeline activity](./Media/23042025(73).png)

1. From the **Home** tab, add the **Invoke Pipeline (Preview)** activity.

    ![Add the invoke pipeline activity](./Media/get-contoso-sample-invoke-pipeline.png)

1. Create a conditional **On success** path between the **Get and Unzip files** activity and the **Invoke pipeline1** activity. From the activity settings **Connection** option, select **More**.

    ![Add the invoke pipeline activity](./Media/23042025(68).png)

1. On the **Choose a data source to get started** dialog appears, select the **Fabric Data Pipelines** as your data source.

    ![Add the invoke pipeline activity](./Media/23042025(69).png)

1. Enter **FabricDataPipelines** as the connection name, then click **Sign in** to open the sign-in window. Enter the credentials provided below.

    - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

    - **Password:** <inject key="AzureAdUserPassword"></inject>

      ![Add the invoke pipeline activity](./Media/23042025(70).png)

1. After signing in successfully, click **Connect** to establish the connection.

    ![Add the invoke pipeline activity](./Media/23042025(71).png)

1. From the activity settings **Pipeline** option, select the **createContosoTables** pipeline.

    ![Add the invoke pipeline activity](./Media/23042025(72).png)

1. With the invoke pipeline activity still selected, go to the **General** tab and update the activity **Name** to **Invoke createContosoTables**. Once complete, select the **Save** icon and then **Run**.

    >**Note:** You can set a schedule from this first pipeline, and it will call the subsequent pipelines and its dataflow upon successful completion or have the pipeline triggered by events like when new files are added to the lakehouse.

    ![Invoke createContosoTables pipeline](./Media/get-contoso-sample-general-name-run.png)

1. From the **Output** pane monitor that the activities and **Succeedded** and once done close the pipeline by selecting the **X** on the left side-rail to return to the workspace.

    ![Invoke succeeded and close](./Media/get-contoso-sample-general-succeeded-close.png)

## Task 9: Unlock the power of T-SQL, Power BI Direct Lake mode, Excel connectivity, and more with your data

1. Within the workspace, select the **Golden data** task flow item and from the filtered list, select the **g_IADWarehouse** Warehouse.

    ![Task flow g_IADWarehouse selection](./Media/golden-data-g-iadwarehouse.png)

1. Now that your data ingestion processes are complete, using the Fabric warehouse as your gold layer simplifies data management and enhances the user experience in several ways:

    - The Fabric warehouse offers built-in [RLS, CLS, and OLS security](https://learn.microsoft.com/fabric/data-warehouse/security) and schemas, ensuring secure and organized data access. 
    - Users can write [T-SQL queries](https://learn.microsoft.com/fabric/data-warehouse/sql-query-editor), build [Direct Lake semantic models](https://learn.microsoft.com/fabric/fundamentals/direct-lake-develop) via the Reporting tab, and use Excel for direct connectivity to up-to-date information.
    - Additionally, [Power BI explorations](https://learn.microsoft.com/power-bi/consumer/explore-data-service) allow for instant visual creation, making data analysis and reporting more efficient and user-friendly.

        ![Start building your solutions](./Media/golden-data-g-iadwarehouse-interactions.png)

## Summary

In this lab, you explored the **medallion architecture** to manage and transform data efficiently across four layers: **Bronze** (raw), **Silver** (cleansed), **Gold** (curated), and **Platinum** (insight-ready via Power BI semantic models).

You worked with **dynamic pipelines**, **Copy activities**, and **Dataflow Gen2** to orchestrate data movement and transformation using low-code/no-code interfaces. These tools streamlined ingestion, optimized storage, and ensured that data was ready for analysis.

### You have successfully completed the lab.
