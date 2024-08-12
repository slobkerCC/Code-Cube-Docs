## Cloud Run Monitoring and Error Logging Automation

This implementation is designed to set up Cloud Run monitoring and server-side error logging in your Google Cloud Platform (GCP) project. Below is an overview of how the process works and the resources it will create in your GCP project.

---

### Features               
#### Cloud Run Monitoring                   
- **CPU and Memory Alert Policies:** Alerts are set up to monitor CPU and memory usage of specified Cloud Run services for your tagging services.
- **Uptime Check:** Regular checks to ensure the Cloud Run services are operational.
- **SSL Certificate Expiration Alert:** Alerts for SSL certificate expiration of Cloud Run services.
#### Server-Side Error Logging                
- **Logging Sink:** Server logs are routed to BigQuery for detailed analysis and storage. The logs will be stored in a dataset in our GCP project for dashboarding and further analysis purposes.

---
### Resources Created in your GCP project
1. **Pub/Sub Topic and Subscription**      
    - A Pub/Sub topic.
    - A Pub/Sub subscription with push configuration for Cloud Functions.
2. **Notification Channel**
    - A notification channel linked to the Pub/Sub topic for alerting.
3. **Alert Policies**
    - **CPU Alert Policy:** Monitors CPU utilization of Cloud Run services.
    - **Memory Alert Policy:** Monitors memory utilization of Cloud Run services.
    - **Uptime Check Alert Policy:** Ensures Cloud Run services are up and running.
    - **SSL Certificate Expiration Alert Policy:** Monitors SSL certificate expiration.
4. **Service Account**
    - A service account `cloud-run-monitoring@{project_id}.iam.gserviceaccount.com` with appropriate IAM bindings.
5. **Logging Sink**
    - A logging sink named `codecube-serverside-logs` routing logs to BigQuery dataset in our GCP project.
6. **IAM Bindings**
    - IAM roles for the service account and Pub/Sub topic.
---

### How to Enable Cloud Run Monitoring

1. **Navigate to the Configuration Page:**
    - Go to the [Tag Monitor Configuration Page](https://portal.code-cube.io/tag_monitor_config){:target="_blank"} on our portal.
2. **Access the Monitoring Tab:**
    - Click on the `Monitoring via Google Cloud Platform` tab.  
3. **Enable Cloud Run Monitoring:**
    - Turn on the toggle for Cloud Run monitoring.
4. **Enter Project Information:**
    - In the project number field, enter your GCP project number.       
    ([Click here to learn how to find your project number](#find-project-number))
5. **Upload Service Account Key:**
    - Upload your service account key.               
    ([Click here to learn how to create the service account key?](#create-service-account-key))
    - **Note:** This service account key will not be stored in any of our systems for privacy and security purposes.
6. **Provide Cloud Run Details:**
    - Enter the name and the region of your Cloud Run resources for your tagging service.               
    ([Click here to learn how to find the Cloud Run Details](#spot-cloud-run-resources))
7. **Start Configuration:**
    - Click on `Start Configuration` to initiate the process.

---

### How to Enable Server-Side Error Logging

1. **Navigate to the Configuration Page:**
    - Go to the [Tag Monitor Configuration Page](https://portal.code-cube.io/tag_monitor_config){:target="_blank"} on our portal.
2. **Access the Monitoring Tab:**
    - Click on the `Monitoring via Google Cloud Platform` tab.
3. **Enable Server-Side Error Logging:**
    - Turn on the toggle for server-side error logging.
4. **Upload Service Account Key:**
    - Upload your service account key.            
    ([Click here to learn how to create the service account key?](#create-service-account-key))
    - **Note:** This service account key will not be stored in any of our systems for privacy and security purposes.
5. **Start Configuration:**
    - Click on `Start Configuration` to initiate the process.

---
### Enabling Both Configurations

If you wish to enable both Cloud Run monitoring and server-side error logging:

1. **Turn On Both Toggles:**
    - Enable the toggles for both Cloud Run monitoring and server-side error logging.
2. **Follow the Steps:**
    - Follow the respective steps for each configuration as outlined above.

---
### How to Find Your GCP Project Number {#find-project-number}

1. **Log in to the Google Cloud Console**:
    - Visit [Google Cloud Console](https://console.cloud.google.com/).
    - Sign in with your Google account if you're not already logged in.
2. **Select Your Project**:
    - In the top navigation bar, click on the project drop-down menu (typically displaying the name of your currently selected project).
    - If you have multiple projects, select the one you want from the list.
3. **Locate the Project Number**:
    - After selecting your project, the **Project Info** panel will appear on the dashboard.
    - Your **Project number** will be displayed in this panel, usually right below the project name. 
---
### Creating a Service Account and Generating a Key {#create-service-account-key}

To enable the automation of monitoring and management processes, you need to create a Google Cloud Service Account with specific permissions. Follow these steps to create the service account, assign the necessary roles, and generate a service account key for upload to our [portal](https://portal.code-cube.io/tag_monitor_config){:target="_blank"}.

#### Step 1: Create a Service Account

1. **Navigate to the Google Cloud Console**
    - Open the [Google Cloud Console](https://console.cloud.google.com/).
2. **Select Your Project:**
    - Ensure you have the correct project selected from the project selector dropdown at the top of the page.
3. **Go to the Service Accounts Page**
    - Navigate to `IAM & Admin` > `Service Accounts`.
4. **Create a New Service Account**
    - Click the `+ CREATE SERVICE ACCOUNT` button.
    - Enter a name, ID, and description for the service account.
    - Click `CREATE AND CONTINUE`.

#### Step 2: Assign Roles to the Service Account

Assign the following roles to the service account to grant it the necessary permissions:

1. **Pub/Sub Admin:**
    - Resource: `google_pubsub_topic`
    - Role: `roles/pubsub.admin`
2. **Monitoring Notification Channel Admin:**
    - Resource: `google_monitoring_notification_channel`
    - Role: `roles/monitoring.notificationChannelAdmin`
3. **Monitoring Alert Policy Admin:**
    - Resource: `google_monitoring_alert_policy`
    - Role: `roles/monitoring.alertPolicyAdmin`
4. **Service Account Admin:**
    - Resources: `google_pubsub_topic_iam_member`, `google_project_iam_binding`
    - Role: `roles/iam.serviceAccountAdmin`
5. **Pub/Sub Admin:**
    - Resource: `google_pubsub_subscription`
    - Role: `roles/pubsub.admin`
6. **Monitoring Uptime Check Admin:**
    - Resource: `google_monitoring_uptime_check_config`
    - Role: `roles/monitoring.uptimeCheckAdmin`
7. **Logging Admin:**
    - Resource: `google_logging_project_sink`
    - Role: `roles/logging.admin`
8. **Config Writer:**
    - Resource: `google_logging_project_sink`
    - Role: `roles/config.writer`
    - After adding all the roles, click `DONE`.  

**Note**: You can also set the **owner** role to include all above-mentioned permissions to the service account at once. 

#### Step 3: Create and Download the Service Account Key

1. **Generate a New Key:**
    - In the `Service Accounts` page, find the service account you created.
    - Click the `⋮` (three vertical dots) at the end of the service account row, then click `Manage keys`.
2. **Add Key:**
    - Click `ADD KEY` > `Create new key`.
3. **Select Key Type:**
    - Choose the `JSON` key type and click `CREATE`.
4. **Download Key:**
    - The key will automatically download to your computer. Keep this file secure, as it contains the credentials required to access the service account.

#### Step 4: Upload the Service Account Key to Our Portal

1. **Access Our Portal:**
    - Log in to our [portal](https://portal.code-cube.io/tag_monitor_config){:target="_blank"} where the key is required for upload.
2. **Upload the Key:**
    - Navigate to the section where the service account key upload is requested.
    - Click the `Upload` button and select the JSON key file you downloaded earlier.
    - Follow any additional instructions provided to complete the upload process.

By completing these steps, you will have successfully created a service account with the required permissions and provided the necessary credentials for our portal to automate and manage processes effectively.

---    
### Identifying Cloud Run Services and Their Regions {#locate-cloud-run-resources}

To manage and monitor your Cloud Run services, you need to know the name and region of each service used for your tagging service. Follow these steps to locate your Cloud Run services and identify their corresponding names and regions.

#### Step 1: Navigate to the Cloud Run Console

1. **Open the Google Cloud Console:**
    - Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. **Select Your Project:**
    - Ensure you have the correct project selected from the project selector dropdown at the top of the page.
3. **Access Cloud Run:**
    - From the navigation menu, go to `Cloud Run` under the `Serverless` section.

#### Step 2: View Cloud Run Services

1. **List of Services:**
    - On the Cloud Run page, you will see a list of all Cloud Run services deployed in your project.
2. **Service Details:**
    - Each row in the list represents a Cloud Run service. The primary details displayed include:
        - **Service Name:** The name of the Cloud Run service.
        - **Region:** The region where the service is deployed.

#### Step 3: Identify Service Name and Region

1. **Service Name:**
    - The service name is displayed in the `Service` column. This is the identifier you use to manage and reference the service within your project.
2. **Region:**
    - The region is displayed in the `Region` column. This indicates the geographical location where the service is deployed, which is crucial for understanding latency and data residency.

By following these steps, you will be able to easily locate all Cloud Run services within your project and identify their names and regions needed for the implementation.

---    
### Next Steps

By following these steps, Cloud Run monitoring and/or server-side error logging will be implemented and enabled for you. 

**What's Next?**          

**Enable Notification Methods**      
Set up your preferred notification methods (e.g., email or Slack) to receive alerts when an event occurs. 