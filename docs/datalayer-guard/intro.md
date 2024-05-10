---
hide:
  - toc
---


# Code Cube's DataLayer Guard 
The DataLayer Guard **continously monitors the dataLayer on your website**. Changes or errors in the dataLayer are signaled based on a preconfigured template within the Code Cube portal. The DataLayer Guard monitors the website every hour or every day (based on the license).

The dataLayer contains all information used to pass data from your website to Tag Manager. A broken dataLayer causes the loss of valuable marketing- and analytics data and missing out on important insights.

**Quick links**
- [Configuration via scraper](https://docs.code-cube.io/datalayer-guard/scraped-events/)
- [Configuratiion via Tag Manager](https://docs.code-cube.io/datalayer-guard/scraped-events/).


## How does the monitoring work? 🔎
At Code Cube, two methods are used for dataLayer monitoring: using the DataLayer Guard scraper or integrate monitoring via (Google) Tag Manager.

### Monitoring via custom scraper
The DataLayer Guard acts as a scraper, continuously visiting your website, navigating through it, and performing various interactions based on predefined templates set up via the configuration page in the portal.

Most dataLayer evnts can be montiored following this configuration. No additional configuration via front-end or Tag Management systems is required. Which is one of the biggest advantages of this set-up: there are no dependencies on development and on external scripts.

Within the scraper, two types of events are defined. 

**Page load events**: These events trigger directly upon page load, requiring no user interactions. Examples include pageview events. Once added to the configuration page, page load events are promptly inspected during the next DataLayer Guard run.

**Interaction events**: These events require performing actions on the page, such as clicking on elements, filling in input fields, selecting options from a list, adding a product to the cart. Interaction events may take up to a maximum of 24 hours to be fully inspected by the DataLayer Guard.

[How to configure :material-open-in-new:](https://docs.code-cube.io/datalayer-guard/scraped-events/){ .md-button .md-button--primary }


### Monitoring via (Google) Tag Manager
Some events cannot be captured through scraping, such as those requiring user authentication, email subscriptions, or completing a purchase on the website. For such scenarios, we've developed a fallback method via Google Tag Manager.

#### How to configure ⚒️
For comprehensive implementation guidance, please visit [this link](https://docs.code-cube.io/datalayer-guard/events-tag-manager/).
