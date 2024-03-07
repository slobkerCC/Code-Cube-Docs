# Manage access to raw Tag Manager data

### Manage access rights
We need to create a service account in your Google Cloud Platform project.

1. In the Google Cloud console, go to the Create [service account page](https://console.cloud.google.com/projectselector2/iam-admin/serviceaccounts/create?walkthrough_id=iam--create-service-account&_ga=2.256991880.228167773.1709798988-298617199.1684135176#step_index=1).

2. Select a Google Cloud Project.

3. Enter a service account name to display in the Google Cloud console.
_The Google Cloud console generates a service account ID based on this name. Edit the ID if necessary. You cannot change the ID later_.

4. Add the IAM role **BigQuery User**

5. Click Done to finish creating the service account.

### Create new dataset and table in BigQuery 
In your BigQuery environment, prepare the new dataset and table.

#### Create the dataset

1. Open the BigQuery page in the Google Cloud console.

2. In the Explorer panel, select the project where you want to create the dataset.

3. Expand the more_vert Actions option and click Create dataset.

4. On the 'Create dataset' page:

    - For Dataset ID, enter a unique dataset name. For example 'codecube-tagmonitor'.
    - Location type: Select **multi-region** and **EU**.

5. Click Create dataset.

### Create the table for the client-side monitor

1. Select the new dataset and click on **'Create table'**

2. On the 'Create table' page:

    - Create table from: Select 'Empty table'
    - Destination
        - Project: select your GCP project ID
        - Dataset: select your newly created dataset, for example 'codecube-tagmonitor'
        - Give the table a new, for example 'raw_data_client'
        - Add the following schema:
    

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


### Create the table for the server-side monitor

1. Select the new dataset and click on **'Create table'**

2. On the 'Create table' page:

    - Create table from: Select 'Empty table'
    - Destination
        - Project: select your GCP project ID
        - Dataset: select your newly created dataset, for example 'codecube-tagmonitor'
        - Give the table a new, for example 'raw_data_server'
        - Add the following schema:
    

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
 
### Create the query

#### Client-side data
SELECT  FROM `code-cube.clientname_313_tag_monitor.raw_data_client` WHERE DATE(timestamp) = DATE(DATE_ADD(CURRENT_TIMESTAMP(), INTERVAL -1 DAY))

#### Server-side data
SELECT  FROM `code-cube.clientname_313_tag_monitor.raw_data_server` WHERE DATE(timestamp) = DATE(DATE_ADD(CURRENT_TIMESTAMP(), INTERVAL -1 DAY))

### Create the scheduled query

1. Details and schedule: Give the scheduled query a name, for example 'codecube-tagmonitor-client'.

2. Add the schedule options:

    -  Repeat frequency: Days
    -  At: 6:00AM
    - Start and end dates can be added when relevant

3. Add destination details for query results:

    - Enable 'Set a destination table for query results'
    - Add the name of the dataset you just created
    - Add the table ID of the table you just created
    - Destination table write preference: Append to table
    - Location type: Multi-region, select EU

4. Add the service account
    - Select the service account that has been created.

5. Optional: Enable email notifications

6. Save the settings
