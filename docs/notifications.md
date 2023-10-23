# Enable Notifications

## Configuring Monitoring Notifications
To enable monitoring notifications for our products, you can access our portal and navigate to the configuration pages of each product such as Tag Monitor, Datalayer Guard or Sitespeed Monitor. From there, select your desired method of receiving notifications based on your subscription model, such as Email, Slack, or Teams. Fill in the required fields accordingly for each method.
Follow the steps below accoring to your desired method:

#### **Email Notifications**
1. Go to our portal and access the configuration page of the product for which you want to enable notifications.
2. Activate the toggle switch to enable email updates.
3. Provide the email addresses where you wish to receive the notifications.


#### **Slack Notifications**
1. Go to our portal and access the configuration page of the product for which you want to enable notifications.
2. Activate the toggle switch to enable Slack updates.
3. Open your Slack Workspace and copy the workspace ID by clicking on the workspace name. 
![workspace ID](./images/workspace-id.png)
4. Paste the workspace ID into the corresponding field in the configuration page and save the form.
5. You will be prompted to log in to your workspace and authorize our app.
6. After authorizing the app, add it to your workspace by clicking the **add apps** button and selecting the app.
7. Invite the app to the desired channel where you want to receive the notifications by clicking on the channel name, going to the integrations tab and, adding the app.


#### **Teams Notifications**
1. Go to our portal and access the configuration page of the product for which you want to enable notifications.
2. Activate the toggle switch to enable Teams updates.
3. Follow [these steps](https://learn.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook?tabs=dotnet){:target="_blank"} to create an incoming webhook for the channel where you want to receive the notifications.
4. Copy the generated Webhook URL and paste it into the corresoinding field and save the form.