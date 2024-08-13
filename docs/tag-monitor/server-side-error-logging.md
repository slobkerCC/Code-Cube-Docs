## Feature description

❕This feature is only available with the Tag Monitor's premium and enterprise licenses.

Logs play an essential role in monitoring your server-side tagging. They assist in troubleshooting request issues, identifying missing data, and understanding how a vendor processed a request.

Logs are available for all tags that support the "logging to console" option in the server-side GTM container. However, it's important to note that you **can not** retrieve log data for Google Analytics and Google Ads tags, as these default templates do not support the logging option.

The logging will be configured in the Google Cloud Project where your GTM server-side container operates in a Cloud Run instance. From this instance, you can connect the logs to the Code Cube environment. These logs will then be paired with other error information and integrated into dashboarding and notifications.

---
## How it works

Our system works by setting up a log monitoring mechanism within your Google Cloud Project. It starts by configuring a router log that collects logs from your GTM server-side container, specifically targeting logs that meet certain criteria.

The filtering logic is applied to ensure only relevant logs are captured, with the filter being: logName=~"stdout" AND textPayload!~"https://www.googletagmanager.com/sgtm/a" AND textPayload!~"Listening". 

Filter explanation:
logName=~"stdout": Filter logs based on stdout.
textPayload!~"https://www.googletagmanager.com/sgtm/a": Exclude GTM analytics pings.
textPayload!~"Listening": Excludes instance initializations.

Once the relevant logs are collected, they are sent to a dataset in our Google Cloud Project. This dataset serves as a repository for the logs, which can then be used to create insights, create dashboards, and track various metrics.

---
### Resources Created in your GCP project {#GCP-respurces}  

1. **Logging Sink**
    - A logging sink named codecube-serverside-logs routing logs to BigQuery dataset in our GCP project.

---

### How to Enable server-side error logging
To enable the feature you need to take the steps below:

1. **Navigate to the Configuration Page:**
    - Go to the [Tag Monitor Configuration Page](https://portal.code-cube.io/tag_monitor_config){:target="_blank"} on our portal.
2. **Access the Monitoring Tab:**
    - Click on the `Monitoring via Google Cloud Platform` tab.                            
    <img src="/../images/GCP-monitoring/monitoring-tab.png"
    alt="Monitoring via GCP tab"
    height=800
    width=800
    class="big-img"
        >
3. **Enable server-side error logging:**
    - Turn on the toggle for server-side error logging.                   
    <img src="/../images/GCP-monitoring/server-side-toggle.png"
    alt="Enabling toggle for server-side error logging"
    height=800
    width=800
    class="big-img"
        >                     
4. **Upload Service Account Key:**
    - Upload your service account key.               
    [How to create the service account key?](#create-service-account-key)
    - **Note:** This service account key will not be stored in any of our systems for privacy and security purposes.  Find more about 
        the security Measures and Implementation safeguards [here](#security-measures-and-implementation-safeguards).                     
    <img src="/../images/GCP-monitoring/upload-key-ss-logs.png"
    alt="Field of upload service account key"
    height=800
    width=800
    class="big-img"
        >            
5. **Start Configuration:**
    - Click on `Start Configuration` to initiate the process.              
    <img src="/../images/GCP-monitoring/start-config-ss-logs.png"
    alt="Start configuration button"
    height=800
    width=800
    class="big-img"
        >

8. **Confirm the implementation:**
    - Once the following message appears on your screen, you can confirm that the implementation was successful.                   
    <img src="/../images/GCP-monitoring/success-msg-ss-log.png" 
    alt="Success message"
    height=800
    width=800
    class="big-img"
            >

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
    <img src="/../images/GCP-monitoring/service-account.png"
    alt="Service Accounts Page in GCP"
    height=900
    width=900
    class="big-img"
        >
4. **Create a New Service Account**
    - Click the `+ CREATE SERVICE ACCOUNT` button.
    <img src="/../images/GCP-monitoring/create-service-account.png"
    alt="CREATE SERVICE ACCOUNT Button"
    height=900
    width=900
    class="big-img"
        >
    - Enter a name, ID, and description for the service account.
    - Click `CREATE AND CONTINUE`.
    - Copy the service account email into your clipboard for the next step.


#### Step 2: Assign Roles to the Service Account

- Navigate to `IAM & Admin` > `IAM`.                     
    <img src="/../images/GCP-monitoring/IAM-tab.png"
        alt="IAM page in GCP"
        height=900
        width=900
        class="big-img"
        >
- Click on `GRANT ACCESS` button.              
    <img src="/../images/GCP-monitoring/grant-access-btn.png"
        alt="Grant access Button"
        height=900
        width=900
        class="big-img"
        >
- Paste your service account email from the previous step into the `New principals` field.             
    <img src="/../images/GCP-monitoring/add-principals.png"
        alt="Add principals Button"
        height=900
        width=900
        class="big-img"
        >
- Assign the following roles to the service account to grant it the necessary permissions:
    <img src="/../images/GCP-monitoring/add-role.png"
        alt="Add role Button"
        height=900
        width=900
        class="big-img"
        >

1. **Logging Admin:**
    - Resource: `google_logging_project_sink`
    - Role: `roles/logging.admin`
2. **Config Writer:**
    - Resource: `google_logging_project_sink`
    - Role: `roles/config.writer`
    - After adding all the roles, click `DONE`.  

**Note:** You can set the **owner** role to grant all of the permissions mentioned above to the service account in one step. However, be aware that this will also grant full access to the service account.

#### Step 3: Create and Download the Service Account Key

1. **Generate a New Key:**
    - In the `Service Accounts` page, find the service account you created.
    - Click the `⋮` (three vertical dots) at the end of the service account row, then click `Manage keys`.
    <img src="/../images/GCP-monitoring/manage-key-btn.png"
    alt="Manage key Button"
    height=900
    width=900
    class="big-img"
        >
2. **Add Key:**
    - Click `ADD KEY` > `Create new key`.
    <img src="/../images/GCP-monitoring/add-key-btn.png"
    alt="Add key Button"
    height=900
    width=900
    class="big-img"
        >
3. **Select Key Type:**
    - Choose the `JSON` key type and click `CREATE`.
    <img src="/../images/GCP-monitoring/create-json-key.png"
    alt="Create JSON key Button"
    height=900
    width=900
    class="big-img"
        >
4. **Download Key:**
    - The key will automatically download to your computer. Keep this file secure, as it contains the credentials required to access the service account.


---

### Security Measures and Implementation Safeguards {#security-measures-and-implementation-safeguards}

Our implementation process is built around a strong security framework that safeguards user data and blocks unauthorized access. Here's how we maintain top-level security throughout the process:

1. **One-Time Use of Service Account Key:**
    - We keep your service account key secure by using it only once. The service account key, necessary for implementation, is never stored in our databases. This means that after the initial implementation, the key is discarded. Should you need to update your setup, you will be required to upload the key again. This approach eliminates any potential vulnerabilities associated with key storage.
2. **Strict Separation of Front-End and Back-End Processing:**
    - To minimize risk, the service account key file is never handled on the front-end. Instead, when you upload the key, it is sent as a binary file via secure HTTPS requests directly to our servers. By processing the key exclusively on the back-end, we prevent any exposure of sensitive information in the front-end environment, adding an extra layer of protection against potential security breaches.
3. **No Credentials Stored:**
    - In the event of a security breach, your credentials remain safe. Since we do not store the service account key or any sensitive credentials in our system, even a successful hack would yield no access to your Google Cloud resources. This ensures that your data and accounts remain secure, regardless of external threats.
4. **Limited Scope of Resource Creation:**
    - Our implementation is highly targeted and precise. We only create the resources explicitly required for the project within your Google Cloud environment, and nothing more. This controlled and minimalistic approach ensures that there are no unnecessary permissions or resources that could be exploited, further tightening security.            
    [See the list of resources that will be created in your GCP project](#GCP-respurces)

By following these strict security practices, we secure your implementation, reducing risk and protecting your Google Cloud environment.

