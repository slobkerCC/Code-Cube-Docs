# Monitoring via scraped events



## Configuring dataLayer Events for Monitoring

This guide will walk you through configuring dataLayer events to be monitored by DataLayer Guard. Before you begin, ensure you have access to our portal and have a list of events you want to monitor.

## Adding Events

To add events for monitoring, follow these steps:

1. Navigate to the [DataLayer Guard configuration](https://portal.code-cube.io/datalayer_guard_config) page.
2. Prepare the list of events you want to be monitored.
3. Click on the `Monitoring via scraped events` tab.
4. Click on the `Add event` button.
5. Enter the event name in the corresponding field.
6. For adding the events you have two options:
    - Add the entire event in valid JSON format:
        - Click on the `Add JSON` button and paste the entire event. The event will be displayed in the event table, enabling you to edit, add, and remove fields easily.
    - Add events field by field:
        - Enter the parameter name in the "Parameter" field.
        - Select the type of value. Note: for nested arrays or objects, select the array or object type accordingly.
        - Specify if the value is required or not.
        - Determine if the value should match a specific value or if it can be dynamic.
        - Enter the value or an example of the value (if dynamic) in the "Value" field.
        - Click the add icon at the end of the row to add more parameters and rows.

7. Define how the event is triggered from the `How does this event fire` dropdown.
8. Specify the URL on which the event can be found.
9. If the event is an interaction event, define the trigger element for the event.
10. Hit the save button to save the event.