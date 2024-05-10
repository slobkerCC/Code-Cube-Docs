---
hide:
  - navigation
---


# DataLayer Guard
The DataLayer Guard monitors the dataLayer on your website. Changes or errors in the dataLayer are signaled based on a preconfigured template. The DataLayer Guard monitors the website every hour or every day (based on the license).

**Why monitor the dataLayer?**
The dataLayer contains all information used to pass data from your website to Tag Manager. A broken dataLayer causes the loss of valuable marketing- and analytics data and missing out on important insights.

## How do we set-up the monitoring?
There are two methods available for dataLayer monitoring: using the DataLayer Guard scraper or integrating via (Google) Tag Manager.

### Monitoring via scraped events
Code Cube's DataLayer Guard can automatically monitor most dataLayer events without the need for additional functionality like adding scripts in Tag Manager or on the website's frontend.

The DataLayer Guard acts as a scraper, continuously visiting your website, navigating through it, and performing various interactions based on predefined templates set up via the configuration page in the portal.

Within the scraper, we classify events into two types:

**Page load events**

These events trigger directly upon page load, requiring no user interactions. Examples include page_view or item view events.

Once added to the configuration page, page load events are promptly inspected during the next DataLayer Guard run.

**Interaction events**

These events require performing actions on the page, such as clicking on elements, filling in input fields, selecting options from a list, adding a product to the cart. Interaction events may take up to a maximum of 24 hours to be fully inspected by the DataLayer Guard.

### How to configure
More information on implementation can be found [here](https://docs.code-cube.io/datalayer-guard/scraped-events/).

### Monitoring via (Google) Tag Manager
Some events cannot be captured through scraping, such as those requiring user authentication, email subscriptions, or completing a purchase on the website. For such scenarios, we've developed a fallback method via Google Tag Manager.

# DataLayer Guard

DataLayer Guard keeps a watchful eye on your website's dataLayer, alerting you to any changes or errors based on a predefined template. Depending on your license, it diligently monitors your website either hourly or daily.

**Why Monitor the dataLayer?**

The dataLayer holds all the crucial information for passing data from your website to Tag Manager. A malfunctioning dataLayer can lead to the loss of valuable marketing and analytics data, depriving you of essential insights.

## How to Set Up Monitoring?

There are two methods available for dataLayer monitoring: using the DataLayer Guard scraper or integrating with (Google) Tag Manager.

### Monitoring via Scraped Events

Code Cube's DataLayer Guard can automatically monitor most dataLayer events without the need for additional functionality like adding scripts in Tag Manager or on the website's frontend.

The DataLayer Guard acts as a scraper, continuously visiting your website, navigating through it, and performing various interactions based on predefined templates set up via the configuration page in the portal.

Within the scraper, we classify events into two types:

**Page Load Events**

These events trigger directly upon page load, requiring no user interactions. Examples include page_view or item view events.

Once added to the configuration page, page load events are promptly inspected during the next DataLayer Guard run.

**Interaction Events**

These events necessitate actions on the page, such as clicking on elements, filling in input fields, selecting options from a list, or adding a product to the cart. Interaction events may take up to a maximum of 24 hours to be fully inspected by the DataLayer Guard.

For detailed implementation instructions, refer to [this guide](https://docs.code-cube.io/datalayer-guard/scraped-events/).

### Monitoring via (Google) Tag Manager

Some events cannot be captured through scraping, such as those requiring user authentication, email subscriptions, or completing a purchase on the website. For such scenarios, we've developed a fallback method via Google Tag Manager.

For comprehensive implementation guidance, please visit [this link](https://docs.code-cube.io/datalayer-guard/events-tag-manager/).
