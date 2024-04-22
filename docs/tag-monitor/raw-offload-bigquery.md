# Manage access to raw Tag Monitoring data in BigQuery

To offload BigQuery data from one project to another, we'll create a scheduled query managed by a service account.

<div class="alert alert-info" role="alert">
This feature is only available in the <b> premium package </b>
</div>

## Granting access to raw Tag Monitoring data
This section explains how to set up access control for offloading BigQuery data using a service account. A service account is a special Google Cloud identity used by applications or services to access Google Cloud resources.

### Creating a Service Account for Code Cube

1. **Navigate to the Service Account Creation Page**: In the Google Cloud Console, locate the "IAM & Admin" section and navigate to the "Service Accounts" page. Alternatively, you can directly access the service account creation page using [this link] (https://cloud.google.com/iam/docs/service-account-overview).
2. **Select your Google Cloud Project**: From the dropdown menu, ensure you've selected the project containing the BigQuery dataset you want to share with Code Cube.
3. **Create a Service Account with a Descriptive Name**:  Enter a clear and descriptive name for the service account. This name helps identify the purpose of the account (e.g., "codecube-tagmonitor-access"). The Google Cloud Console will generate a unique service account ID based on this name. You can edit the ID if needed, but keep in mind that it cannot be changed later.
4. **Assign the **BigQuery User** IAM role**: Grant the service account the "BigQuery User" role. This role provides the necessary permissions to access and query BigQuery data.
5. **Finalize Service Account Creation**: Click the "Done" button to create the service account.
  
**Important Note**: After creating the service account, you'll need to share the service account ID securely with your contact at Code Cube. This ID will be used by Code Cube to establish access to your BigQuery data through the scheduled query. Remember to restrict access to the service account after granting access to Code Cube. You can manage access controls later by following the instructions in the Google Cloud documentation https://cloud.google.com/iam/docs/understanding-roles.

## Preparing the BigQuery datasets and tables
This section guides you through creating the BigQuery datasets and tables that will store your offloaded Tag Monitoring data.

### Create the BigQuery dataset</summary>
A BigQuery dataset is a container that organizes your tables. Here's how to create a new dataset for Code Cube's Tag Monitoring data:

1. **Open the BigQuery console**: In the Google Cloud Console, navigate to the BigQuery service.2. In the Explorer panel, select the project where you want to create the dataset.
2. **Select your project**: In the BigQuery console's left-hand navigation panel, locate the "Explorer" section.  Ensure you have selected the GCP project where you want to store the Tag Monitoring data.
3. **Create a new dataset**:  Within the "Explorer" panel, click the "Actions" dropdown menu and choose "Create dataset".
4. **Name your dataset**: Enter a unique and descriptive name for the dataset. A good example might be "codecube-tagmonitor". This name helps identify the purpose of the dataset.
5. **Set the location**:  BigQuery allows you to choose where your data is geographically stored. For this case, select "multi-region" and "EU" as the location type.
6. **Create the dataset**: Once you've filled in the details, click the "Create dataset" button to create the new dataset in BigQuery.

### Create the BigQuery table for client-side monitoring

1. **Select the new dataset and click 'Create table'**: In the BigQuery console, navigate to your newly created dataset and click the "Create table" button.
2. **Choose 'Empty table' as the table type**: Select "Empty table" to create a new table without referencing existing data.
3. **Provide a descriptive table name**: Enter a clear and descriptive name for the table, such as 'raw_data_client'. 
4. **Define the table schema as follows**: The table schema defines the structure and data types for each column. Here's a breakdown of the columns used to store client-side monitoring data:    

        | Field name        | Type          | Mode |
        | ----------------- | ------------- | --------
        | timestamp         | TIMESTAMP     |NULLABLE
        | initial_url       | STRING        | NULLABLE
        | url               | STRING        | NULLABLE
        | event_name        | STRING        | NULLABLE
        | event_timestamp   | STRING        | NULLABLE
        | container_version | STRING        | NULLABLE
        | container_id      | STRING        | NULLABLE
        | env_name          | STRING        | NULLABLE
        | tag               | RECORD        | REPEATED
        | id                | STRING        | NULLABLE
        | name              | STRING        | NULLABLE
        | status            | STRING        | NULLABLE
        | channel           | STRING        | NULLABLE
        | execution_time    | STRING        | NULLABLE

4. **Select 'No partitioning' for this table**: Partitioning is not required at this moment.
6. **Click Create table**: Once you've filled in the details, click the "Create table" button to create the table in BigQuery.

### Create the table for server-side monitoring</summary>

1. **Select the new dataset and click 'Create table'**: In the BigQuery console, navigate to your newly created dataset and click the "Create table" button.2. Choose 'Empty table' as the table type.
2. **Choose 'Empty table' as the table type**: Select "Empty table" to create a new table without referencing existing data.
3. **Provide a descriptive table name**: Enter a clear and descriptive name for the table, such as 'raw_data_server'. 
4. **Define the table schema as follows**: The table schema defines the structure and data types for each column. Here's a breakdown of the columns used to store server-side monitoring data:    


        | Field name        | Type      | Mode |
        | ----------------- | --------- | --------
        | timestamp         | TIMESTAMP | NULLABLE
        | url               | STRING    | NULLABLE
        | event_name        | STRING    | NULLABLE
        | event_timestamp   | INTEGER   | NULLABLE
        | client_name       | STRING    | NULLABLE
        | container_version | STRING    | NULLABLE
        | container_id      | STRING    | NULLABLE
        | env_name          | STRING    | NULLABLE
        | tag               | RECORD    | REPEATED
        | id                | STRING    | NULLABLE
        | name              | STRING    | NULLABLE
        | status            | STRING    | NULLABLE
        | execution_time    | STRING    | NULLABLE

4. **Select 'No partitioning' for this table**: Partitioning is not required at this moment.
6. **Click Create table**: Once you've filled in the details, click the "Create table" button to create the table in BigQuery.

### Creating the client- and server-side queries</summary>
This section explains how to write queries to extract client-side and server-side data from your BigQuery tables. These queries will be used later to set up scheduled data offloading to Code Cube.

#### Client-side data
The following SQL query retrieves all data from Code Cube's raw_data_client table for the previous day:

```sql
SELECT * FROM `code-cube.{{dataset_name}}.raw_data_client`
WHERE DATE(timestamp) = DATE(DATE_ADD(CURRENT_TIMESTAMP(), INTERVAL -1 DAY))
```

** Explanation:**

- SELECT *: This selects all columns from the table.
- FROM: This clause specifies the source table, which is code-cube.{{dataset_name}}.raw_data_client.
  - Replace {{dataset_name}} with the actual name of the dataset. The dataset name can be found in the portal under **client-side error monitoring settings** on the Tag Monitor configuration page.
- WHERE: This clause filters the results to include only data where the timestamp field falls on the previous day relative to the current time.
  - DATE(timestamp): Extracts the date portion from the timestamp field.
  - DATE(DATE_ADD(CURRENT_TIMESTAMP(), INTERVAL -1 DAY)): Calculates the date for one day before the current timestamp.

Note: You can modify this query to filter data for a specific date range or based on other criteria.

#### Server-side data
The query for server-side data retrieval is similar to the client-side query, but uses the raw_data_server table instead. Simply replace "client" with "server" throughout the query:

```sql
SELECT * FROM `code-cube.{{dataset_name}}.raw_data_server`
WHERE DATE(timestamp) = DATE(DATE_ADD(CURRENT_TIMESTAMP(), INTERVAL -1 DAY))
```
The {{dataset}} name is equal to the dataset name shown on the Tag Monitor configuration page.

### Create the scheduled query in your BigQuery environment
The next step involves creating scheduled queries in your BigQuery environment to automate this data retrieval process. This will ensure regular data offloading to Code Cube.

**1. Provide details and schedule for the query (once a day)**

- In the BigQuery console, navigate to the query editor.
- Paste your client-side or server-side query (refer to the previous section) into the editor window.
- Locate the "Schedule" section. This section allows you to define how often the query should run.
  - Set the "Frequency" to "Daily".
  - Optionally, you can define a specific time for the query to run each day.

**2. Add destination details for query results.**
In the "Destination" section, BigQuery offers various options for where to store the query results. Select here the tables created in the previous steps.

**3. Add the service account**

- In the "Job configuration" section, locate the "Service account" option.
- Select the service account you created and granted access to your BigQuery data.
  
**4. Save the settings**

- Once you've filled in all the details, review your query and configurations.
- Click the "Save" button to create and schedule the query.

Additional Notes:

- BigQuery allows you to preview the query results before saving the scheduled query. This can help ensure the query retrieves the expected data.
- Consider naming your scheduled queries descriptively to improve clarity and organization within your BigQuery environment.
