---
hide:
  - toc
---

# The DataLayer Guard 
Code Cube's DataLayer Guard keeps a constant eye on your website's dataLayer. Any changes or errors within the dataLayer triggeLayer Guard to send a notification, based on preconfigured templates within the Code Cube portal. The DataLayer Guard conducts website monitoring hourly or daily, depending on your license.

The dataLayer contains all information used to pass data from your website to Tag Manager. A broken dataLayer causes the loss of valuable marketing- and analytics data and missing out on important insights.

**Quick links**

- [Configuration via scraper](https://docs.code-cube.io/datalayer-guard/scraped-events/)
- [Configuration via Tag Manager](https://docs.code-cube.io/datalayer-guard/scraped-events/).

## 🔎 How does it work?
At Code Cube, we use two methods for dataLayer monitoring: the DataLayer Guard Scraper and integration with (Google) Tag Manager.

### ⚒️ Monitoring via custom scraper
The DataLayer Guard acts as a scraper, continuously visiting your website, navigating through it, and performing various interactions based on predefined templates set up via the configuration page in the portal.

Most dataLayer events can be monitored with this setup, without the need for additional configurations via frontend or Tag Management systems. This autonomy from development and external scripts is one of the setup's significant advantages.

Within the scraper, two types of events are defined. 

**Page load events**: These events trigger directly upon page load, requiring no user interactions. Examples include pageview events. Once added to the configuration page, page load events are promptly inspected during the next DataLayer Guard run.

**Interaction events**: These events require performing actions on the page, such as clicking on elements, filling in input fields, selecting options from a list, adding a product to the cart. Interaction events may take up to a maximum of 24 hours to be fully inspected by the DataLayer Guard.

[How to configure :material-open-in-new:](https://docs.code-cube.io/datalayer-guard/scraped-events/){ .md-button .md-button--primary }

### ⚒️ Monitoring via (Google) Tag Manager
Certain events, like those requiring user authentication, email subscriptions, or completing purchases on the website, cannot be captured through scraping. For such scenarios, we've devised a fallback method via Google Tag Manager.

[How to configure :material-open-in-new:](https://docs.code-cube.io/datalayer-guard/events-tag-manager/){ .md-button .md-button--primary }
