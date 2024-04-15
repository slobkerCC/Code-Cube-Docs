---
hide:
  - toc
---

# Manage access to raw Tag Monitoring data in BigQuery
To offload BigQuery data from one project to another, we'll create a scheduled query managed by a service account.

## Managing access to the data

<details>
<summary>Create a service account </summary>

1. In the Google Cloud console, go to the Create [service account page](https://console.cloud.google.com/projectselector2/iam-admin/serviceaccounts/create?walkthrough_id=iam--create-service-account&_ga=2.256991880.228167773.1709798988-298617199.1684135176#step_index=1).

2. Select your Google Cloud Project.

3. Enter a name for the service account.
_The Google Cloud console generates a service account ID based on this name. Edit the ID if necessary. You cannot change the ID later_.

4. Assign the **BigQuery User** IAM role.

5. Click Done to finish creating the service account.
</details>

<details>
<summary>Managing access rights</summary>
  
Share the service account ID with your contact at Code Cube to confirm proper access rights management.
</details>

<details>
<summary>Create the BigQuery dataset</summary>

1. Open the BigQuery page in the Google Cloud console.
2. In the Explorer panel, select the project where you want to create the dataset.
3. Expand the Actions option and select 'Create dataset'.
4. Enter a unique dataset name (e.g., 'codecube-tagmonitor').
5. Select **multi-region** and **EU** for the location type.
6. Click **Create dataset**.
</details>
<details>
<summary>Create the BigQuery table for client-side monitoring</summary>

1. Select the new dataset and click **'Create table'**
2. Choose 'Empty table' as the table type.
3. Select your GCP project and newly created dataset, gave it an descriptive name like 'raw_data_client'.
4. Define the table schema as follows:    

        | Field name        | Type      | Mode |
        | :---------------- | --------- | --------
        | timestamp         | Title     |
        | initial_url       | STRING    | NULLABLE
        | url               | STRING    | NULLABLE
        | event_name        | STRING    | NULLABLE
        | event_timestamp   | STRING    | NULLABLE
        | container_version | STRING    | NULLABLE
        | container_id      | STRING    | NULLABLE
        | tag               | RECORD    | REPEATED
        | id                | STRING    | NULLABLE
        | name              | STRING    | NULLABLE
        | status            | STRING    | NULLABLE
        | channel           | STRING    | NULLABLE
        | execution_time    | STRING    | NULLABLE
        | parameters        | STRING    | REPEATED
        | key               | STRING    | NULLABLE
        | value               | STRING    | NULLABLE

4. Partitioning: Select 'No partitioning'
5. Click on **Create table**
</details>

<details>
<summary>Create the table for server-side monitoring</summary>

1. Select the new dataset and click **'Create table'**
2. Choose 'Empty table' as the table type.
3. Select your GCP project and newly created dataset, gave it an descriptive name like 'raw_data_server'.
4. Define the table schema as follows:    
    

        | Field name        | Type      | Mode |
        | :---------------- | --------- | --------
        | timestamp         | Title     |
        | url               | STRING    | NULLABLE
        | event_name        | STRING    | NULLABLE
        | event_timestamp   | STRING    | NULLABLE
        | client_name       | STRING    | NULLABLE
        | container_version | STRING    | NULLABLE
        | container_id      | STRING    | NULLABLE
        | env_name          | STRING    | NULLABLE
        | tag               | RECORD    | REPEATED
        | id                | STRING    | NULLABLE
        | name              | STRING    | NULLABLE
        | status            | STRING    | NULLABLE
        | execution_time    | STRING    | NULLABLE
        | parameters        | STRING    | REPEATED
        | key               | STRING    | NULLABLE
        | value               | STRING    | NULLABLE

4. Partitioning: Select 'No partitioning'
5. Click on **Create table**
</details> 

<details>
<summary>1. Creating Queries</summary>
Write queries to retrieve client-side and server-side data.

#### Client-side data
```sql
SELECT * FROM `code-cube.{{dataset_name}}.raw_data_client`
WHERE DATE(timestamp) = DATE(DATE_ADD(CURRENT_TIMESTAMP(), INTERVAL -1 DAY))
```

#### Server-side data

```sql
SELECT * FROM `code-cube.{{dataset_name}}.raw_data_server`
WHERE DATE(timestamp) = DATE(DATE_ADD(CURRENT_TIMESTAMP(), INTERVAL -1 DAY))
```
The {{dataset}} name is equal to the dataset name shown on the Tag Monitor configuration page.
</details>

<details>
<summary>2. Create the scheduled query </summary>
Set up scheduled queries to automate data retrieval.

1. Provide details and schedule for the query (once a day)
2. Add destination details for query results.
4. Add the service account
5. Save the settings
</details>

</details>
