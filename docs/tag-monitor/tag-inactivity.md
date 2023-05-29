# Tag Inactivity Monitoring

## Product Description 

Tag Inactivity Monitoring is a solution designed to help users monitor important tags, such as conversion tags, and receive timely notifications when the tag does not fire for more than an hour. This solution is useful for ensuring that critical tags are working properly, and for quickly identifying issues that may be impacting business operations.

The Tag Inactivity Monitoring solution sends notifications to users via email or Slack, informing them that the tag has not fired and providing details on the last time the tag was fired. This allows users to easily spot and troubleshoot the issue. The solution is available for use from 8:00 AM to 8:00 PM, making it an ideal tool for businesses that operate during regular business hours.

Overall, the Tag Inactivity Monitoring solution provides an easy-to-use, convenient way for businesses to monitor critical tags and quickly identify issues that may be impacting their operations.

## Implementation

To implement the Tag Inactivity Monitoring solution, users must fill out a configuration form on the Code Cube portal. Once the form is submitted, we will take care of the rest, setting up the solution to monitor the specified tag and sending notifications as needed.


## Configuring Tag Inactivity Notifications

To enable Tag Inactivity notifications, you can access our portal and navigate to the tag monitor configuration page. From there, select your desired method of receiving notifications based on your subscription model, such as Email, Slack, or Teams. Fill in the required fields accordingly for each method.
To configure error monitoring notifications, follow the steps below:

#### **Email Notifications**
1. Go to our portal and access the tag monitor configuration page.
2. Activate the toggle switch to enable email updates.
3. Provide the email addresses where you wish to receive the notifications.


#### **Slack Notifications**
1. Go to our portal and access the tag monitor configuration page.
2. Activate the toggle switch to enable Slack updates.
3. Open your Slack Workspace and copy the workspace ID by clicking on the workspace name. 
![workspace ID](../images/workspace-id.png)
4. Paste the workspace ID into the corresponding field in the configuration page and save the form.
5. You will be prompted to log in to your workspace and authorize our Tag Monitor Alerts app.
6. After authorizing the app, add it to your workspace by clicking the **add apps** button and selecting the app.
7. Invite the app to the desired channel where you want to receive the notifications by clicking on the channel name, going to the integrations tab and, adding the app.


#### **Teams Notifications**
1. Go to our portal and access the tag monitor configuration page.
2. Activate the toggle switch to enable Teams updates.
3. Follow [these steps](https://learn.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook?tabs=dotnet){:target="_blank"} to create an incoming webhook for the channel where you want to receive the notifications.
4. Copy the generated Webhook URL and paste it into the corresoinding field and save the form.
