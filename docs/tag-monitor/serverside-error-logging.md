# Server-side GTM Logging

To provide additional information on error occurrences in the Tag Monitor, it is important to enable logging configurations to provision a table with available and relevant data. This document serves as a short implementation guide on setting up the necessary Logging Sink.

## Requirements
- Utilisation of the `logToConsole()` API within the sGTM container, messages passed to this method are outputted in the stdout stacktrace. This is where the server logs will be recorded.
- Access to the client’s cloud project.
- Writing permissions to the relevant Code Cube dataset for the client’s `logging.iam.gserviceaccount.com` service account.

## Log Router Setup
1. Navigate to the Log router page, found under Logging → Log router.

![Log Router](../images/log-router.jpg)

2. Click on Create sink.

![Create sink](../images/create-sink.jpg)

This will open a new interface, where the relevant destinations, services, and logging filters are submitted.

3. Give the router an appropriate name and description.
4. Configure the destination as a BigQuery dataset, and subsequently select Use a BigQuery dataset in another project.

![Sink destination](../images/sink-destination.jpg)


5. The service and destination will be converted to the format as seen in the image below. Make sure to add `[PROJECT_ID]` as **'code-cube'** and `[DATASET_ID]` is equal to the dataset name shown on the Tag Monitor configuration page.


6. In the log filters, input the following query:

    ```
    logName=~"stdout"
    AND textPayload!~"https://www.googletagmanager.com/sgtm/a"
    AND textPayload!~"Listening"
    ```

    - Explanation:
      - `logName=~"stdout"`: Filter logs based on stdout.
      - `textPayload!~"https://www.googletagmanager.com/sgtm/a"`: Exclude GTM analytics pings.
      - `textPayload!~"Listening"`: Exclude instance initializations.
    
7. __Keep in mind that further refinement is possible by adding more filters, however, be sure to test these in the logs explorer before applying. A faulty or unreturning filter will cause the sink to stop writing logs.__

## External Project Permissions
The creation of a logging sink generates a new service account in your GCP project. It is necessary for Code Cube to hav writing permissions on the BigQuery dataset, where the logs will be stored.
Please make sure to locate this service account and share the name with your contact at Code Cube.

How to find the service account;
- This service account is found under IAM and admin → IAM.
- On the Top right of this page, enable the inclusion of Google-provided role grants.
- Look for the service account that ends with `-logging.iam.gserviceaccount.com`.
- Copy the name of this service account, this will be assigned writing permissions on the relevant dataset.
