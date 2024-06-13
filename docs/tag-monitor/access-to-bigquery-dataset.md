---
hide:
  - toc
---

# Access to Tag Monitor dataset(s) in BigQuery

➡️ This feature is exclusively available in the **premium package.**

➡️ This documentation presents the updated method of offloading BigQuery data to your own GCP environment. The old method involved using a scheduled query, with access managed via a service account. If you already have this setup and have questions about it, please contact [support@code-cube.io](mailto:support@code-cube.io).

## Introduction

BigQuery's Analytics Hub is used to share BigQuery data. This robust feature allows users to access and analyze shared datasets. It enables users to extract valuable insights from the data collected and shared by Code Cube. This feature is especially beneficial for data analysts and businesses looking to use shared data to make informed decisions about their tag or dataLayer insights and errors.

**Technical background**

The Analytics Hub operates on a publish and subscribe model for BigQuery datasets. Your Google Cloud Project serves as the subscriber, meaning the costs for running queries are charged to your own Google Cloud Platform. The data will be shared in real-time. You'll have read-only access to the BigQuery dataset, allowing you to read the data but not make any additions or updates to it. 

We can provide access to the following datasets:

   - Access to raw Tag Monitor client-side data
   - Access to raw Tag Monitor server-side data

## Steps to Follow

To access datasets shared by Code Cube, please follow these steps:

**1. Set up a Google Cloud Platform (GCP) project**

Navigate to the Google Cloud Platform project where you wish to store the data. If you do not already have a Google Cloud Project, create a new one (see [link](https://developers.google.com/workspace/guides/create-project)).

**2. Provide a Google email address**

Share the Google email address that should receive access to the shared dataset with your contact at Code Cube or via [support@code-cube.io](mailto:support@code-cube.io).

*We will add this account as a subscriber to the dataset listing within the Analytics Hub.*

**3. Access the shared dataset**

After granting the email address access to the dataset, you will receive a **data exchange link** from us. Open this link (via the specific Google account) to offload the data to your own environment. 

We will let you know as soon as your Google email address has been added as a subscriber. You will receive a link to the *data exchange* from us. Please open this link via the represented Google account and click here on the button ‘+ add data set to project’.

![https://docs.code-cube.io/images/shared-dataset.png](https://docs.code-cube.io/images/shared-dataset.png)

You will be redirected to the configuration page ‘Create linked dataset’. On this page two fields are required to fill in. 

   - **Project:** Select the project where the Code Cube data should be stored.
   - **Linked data set name:** Add the name of the dataset in BigQuery where the Code Cube data should be stored.

**4. Locate the dataset in BigQuery**

After adding the dataset to your project, you can find it in your BigQuery console. Navigate to BigQuery via the [Google Cloud Platform console](https://console.cloud.google.com/) to view and analyse the shared dataset.

If you encounter any issues or need further assistance, please feel free to contact us at [support@code-cube.io](mailto:support@code-cube.io).
