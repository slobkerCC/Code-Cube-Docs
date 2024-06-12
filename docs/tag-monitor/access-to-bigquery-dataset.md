# Access to Tag Monitor dataset(s) in BigQuery

➡️ This feature is exclusively available in the **premium package.**
➡️ This documentation presents the updated method of offloading BigQuery data to your own GCP environment. The old method involved using a scheduled query, with access managed via a service account. If you already have this setup and have questions about it, please contact [support@code-cube.io](mailto:support@code-cube.io).

## Introduction

To share the BigQuery datasets, we use the functionalities of the Analytics Hub in BigQuery. The Analytics Hub is a powerful feature that allows users to access and analyse shared datasets. With this feature, users can gain valuable insights from the data collected and shared by Code Cube. This functionality is particularly useful for data analysts and businesses who want to leverage shared data to make informed decisions on there tag or dataLayer insights and errors.

We can provide access to the following datasets:

- **Tag Monitor**
    - Access to raw client-side data
    - Access to raw server-side data

## Steps to Follow

To access datasets shared by Code Cube, please follow these steps:

### **Set up a Google Cloud Platform (GCP) project**

Navigate to the Google Cloud Platform project where you wish to store the data. If you do not already have a Google Cloud Project, create a new one (see [link](https://developers.google.com/workspace/guides/create-project)).

### **Provide a Google email address**

Share the Google email address that should receive access to the shared dataset with your contact at Code Cube or via [support@code-cube.io](mailto:support@code-cube.io).

*We will add this account as a subscriber to the dataset listing within the Analytics Hub.*

### **Access the shared dataset**

After granting the email address access to the dataset, you will receive a **data exchange link** from us. Open this link (via the specific Google account) to offload the data to your own environment. 

We will let you know as soon as your Google email address has been added as a subscriber. You will receive a link to the *data exchange* from us. Please open this link via the represented Google account and click here on the button ‘+ add data set to project’.

![https://docs.code-cube.io/images/shared-dataset.png](https://docs.code-cube.io/images/shared-dataset.png)

**Create linked data set**

You will be redirected to the configuration page ‘Create linked dataset’. On this page two fields are required to fill in. 

- **Project:** Select the project where the Code Cube data should be stored.
- **Linked data set name:** Add the name of the dataset in BigQuery where the Code Cube data should be stored.

**Locate the dataset in BigQuery**

After adding the dataset to your project, you can find it in your BigQuery console. Navigate to BigQuery via the [Google Cloud Platform console](https://console.cloud.google.com/) to view and analyse the shared dataset.

If you encounter any issues or need further assistance, please feel free to contact us at [support@code-cube.io](mailto:support@code-cube.io).
