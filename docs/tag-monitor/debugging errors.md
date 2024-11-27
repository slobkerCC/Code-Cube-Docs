# Debugging errors in the Tag Monitor

*These guidelines are constantly updated based on best practices we find along the way. Do you have any specific findings? Please let us know and help us getting this docs as complete as possible.*

Before diving into the specifics, there are some tips on debugging Tag Manager errors in general:

1. Check which **container version** gave the error. Google Tag Manager has quite a thorough cache and therefore some older container versions might still give errors as these versions are some quite persistent.
2. Check when the error started; did a change took place in tracking around that time?
3. Analyse on which page the error was encountered. Is there a **specific page** or **page type** that triggers the error?*

## Google Tag Manager client-side

Below some tips and tricks on debugging errors in your Google Tag Manager client-side environment. In most cases debugging errors in your client-side container are a trial and error, but these tips might help you along the way.

For more specific insights on the Code Cube errors you can enable the BigQuery offload (premium+ feature). Please contact us if you require more information.

### Microsoft Ads

1. Make sure the ‘UET config’ tag is installed and fires on every page.
    
    ![image.png](image.png)
    
2. Make sure to add the right variable for the parameter ‘UETQ variable ID’. This is for example ‘uetq’.
    
    ![image.png](image%201.png)
    
3. Make sure Microsoft Consent Mode is configured correctly.

### LinkedIn Insight

1. The LinkedIn tag gives an error when you try to fire the event before a consent update has been send. Try and send it a bit later.

## Google Tag Manager server-side

Below some tips and tricks on debugging errors in your Google Tag Manager server-side environment. 

GTM server-side container gives more insights on the errors then the client-side container. Do you encounter a high percentage of failed tags (+ 75%)? Make sure to open the preview mode and look into the tab ‘Console’. The changes are quite high more information on the specific error can be found here.

For more specific insights on the Code Cube errors you can enable the BigQuery offload (premium+ feature) or retrieve detailed insights via the server-side error logs (premium+ feature). Please contact us if you require more information.

### General tips

1. Use the trigger type ‘Custom’ as less as possible. This one is to generic and therefore causes quite often a lot of triggers.
    - Do you want to fire on all events? It is better to use trigger type ‘Custom Event’ with a wildcard.
2. Check if the client handling the event is implemented correctly.

### Google Ads

1. Conversion Linker failing? Make sure the region specific settings are added in your server-side instance (Cloud Run for example).

![image.png](image%202.png)

### **Facebook Conversion API**

1. Facebook is very strict on all event parameters. When a Facebook tag fails, this is mostly caused by an event parameter not having the right value. 
    - Using a variable to fill in the value of the event parameter? Make sure to always at a default value to send.
2. Check the trigger added to the tag. Is the trigger specific enough? It might be the trigger fires on events where you don’t want it to fire, so it can’t fill in all parameters and throw an error.
    1. Make sure to also check our general tips on setting up triggers in the server-side environment.

### **TikTok Conversion API**

1. TikTok is very strict on all event parameters. When a Facebook tag fails, this is mostly caused by an event parameter not having the right value. 
    - Using a variable to fill in the value of the event parameter? Make sure to always at a default value to send.

### Criteo

1. Make sure to check if all parameters are configured correctly. 
    - Using a variable to fill in the value of the event parameter? Make sure to always at a default value to send.