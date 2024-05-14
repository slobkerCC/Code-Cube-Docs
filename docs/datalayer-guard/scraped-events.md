# Monitoring via scraped events

This guide will walk you through configuring dataLayer events to be monitored by DataLayer Guard. 

### Adding events

To add events for monitoring, follow these steps:

1. Navigate to the [DataLayer Guard configuration](https://portal.code-cube.io/datalayer_guard_config) page.             
    <img src="/../images/dlg-add-event/dlg-config-link.png"
        alt="DataLayer Guard configuration image"
        height=800
        width=800
        class="big-img"
          >                 
    

2. Prepare the list of events you want to be monitored.
3. Click on the `Monitoring via scraped events` tab.                
    <img src="/../images/dlg-add-event/monitoring-tab.png"
        alt="Monitoring via scraped events image"
        height=800
        width=800
        class="big-img"
          >

4. Click on the `Add event` button.              
    <img src="/../images/dlg-add-event/add-event-btn.png"
        alt="Add event image"
        height=800
        width=800
        class="big-img"
          >


5. Enter the event name in the corresponding field.
    <img src="/../images/dlg-add-event/event-name-field.png"
        alt="event name field"
        height=800
        width=800
        class="big-img"
          >       

6. For adding the events you have two options:          

   
    Add the entire event in valid JSON format:                        

      - Click on the `Add JSON` button and paste the entire event. The event will be displayed in the event table, enabling you to edit, add, and remove fields easily.

      <img src="/../images/dlg-add-event/add-json-btn.png"
        alt="Add JSON button"
        height=800
        width=800
        class="big-img"
          >


              
    Add events field by field:                      

      - Enter the parameter name in the "Parameter" field.
      <img src="/../images/dlg-add-event/param-name.png"
        alt="parameter name field"
        height=800
        width=800
        class="big-img"
        >

      - Select the type of value. Note: for nested arrays or objects, select the array or object type accordingly.
      <img src="/../images/dlg-add-event/type-drpdown.png"
        alt="type of value dropdown"
        height=800
        width=800
        class="big-img"
        >
      - Specify if the value is required or not.
      <img src="/../images/dlg-add-event/value-required-btn.png"
        alt="value required field"
        height=800
        width=800
        class="big-img"
        >
      - Determine if the value should match a specific value or if it can be dynamic.
      <img src="/../images/dlg-add-event/match-value-dropdown.png"
        alt="value match field"
        height=800
        width=800
        class="big-img"
        >
      - Enter the value or an example of the value (if dynamic) in the "Value" field.
      <img src="/../images/dlg-add-event/value-field.png"
        alt="value field"
        height=800
        width=800
        class="big-img"
        >
      - Click the add icon at the end of the row to add more parameters and rows.      
      <img src="/../images/dlg-add-event/add-icon.png"
        alt="add icon"
        height=800
        width=800
        class="big-img"
        >      


8. Define how the event is triggered from the `How does this event fire` dropdown.
  <img src="/../images/dlg-add-event/event-trigger-type.png"
    alt="event trigger"
    height=800
    width=800
    class="big-img"
    >
9. Specify the URL on which the event can be found.
  <img src="/../images/dlg-add-event/url-trigger.png"
    alt="URL field"
    height=800
    width=800
    class="big-img"
    >
10. If the event is an interaction event, define the trigger element for the event.
  <img src="/../images/dlg-add-event/click-element.png"
    alt="trigger element"
    height=800
    width=800
    class="big-img"
    >
11. Hit the save button to save the event.
  <img src="/../images/dlg-add-event/save-btn.png"
    alt="save button"
    height=800
    width=800
    class="big-img"
    >


### Watch the video below to learn how to add the events

<video width="2000" controls>
  <source src="https://storage.googleapis.com/portal_dev_bucket/docs-videos/add-dlg-events.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>
