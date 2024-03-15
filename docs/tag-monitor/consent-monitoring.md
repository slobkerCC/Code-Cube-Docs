# Enable Consent Monitoring

!!! warning This feauture is only available for the Tag Monitor Premium, Enterprise or Agency licenses.


## Changes in Google Tag Manager

### Retrieve variables to retrieve the consent status
1. Install the variable template ['GTM Consent State'](https://tagmanager.google.com/gallery/#/owners/Ayudante/templates/gtm-consent-state) in your GTM container.

2. Create new variables, one for each consent status to monitor. Often two variables for 'analytics_storage' and 'ad_storage' are enough.

### Add parameters to the tags where consent should be monitored.
1. **Google Analytics**: Add a parameter value and key to every GA4 event (tip: add these parameters via a standard 'Event settings variable'). 

- The parameter name should be 'consent_ad_storage' or 'consent_analytics_storage'.
- The parameter value should be the matching variables that you've just added to the container.

2. **Google Ads**: In the Remarketing tag custom parameters can be added via the option 'Manually Specify'

- The parameter key should be 'consent_ad_storage' or 'consent_analytics_storage'.
- The parameter value should be the matching variables that you've just added to the container.

3. **Microsoft Ads**: All event tracking tags give the opportunity to add extra event data via the table option. 

- The name should be 'consent_ad_storage' or 'consent_analytics_storage'.
- The value should be the matching variables that you've just added to the container.

### Link the tags and parameters to the Code Cube Tag Monitor template.
1. When you open a tag in a new tab, the **Tag ID** will be available in the url, after /tags/.
For example, **4175** is the tag ID in the example URL below.

https://tagmanager.google.com/#/container/accounts/112031/containers/126673/workspaces/1000716/tags/4175

2. In the Code Cube Tag Monitor tag (premium template) add the list of tag ID's with the consent variable and the given label (consent_analytics_storaga) for example.
