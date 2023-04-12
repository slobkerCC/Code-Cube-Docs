# Product Description

## Product Description
This repository contains the DataLayer Guard source code and terraform documents. DataLayer Guard crawls through the provided pages and collect dataLayer objects. Then those objects are compared with the provided templates and checked for errors. After the script ends its work all the dataLayer snapshots together with checked URLs are saved to the BigQuery tables so as errors. If there's any errors found the client receive a message next morning with detailed description of the error and all the checkup information.

## How it works
The main point of DataLayer Guard work is to get the dataLayer object from the page after page loading or imitating the potential user actions on the page. To perform those actions DataLayer Guard using the advanced page crawling algorythms.

To set the configuration user must fill out the configuration form on **Code Cube Portal** for customers.

**Steps needed for complete the implementation:**
1. Select the checkup frequency (how many times per day should we run checkups)
2. Set the list of emails which should be notified about the errors
3. Turn on the slack alerts as well if it's needed
4. Fill the dataLayer events: custom event name, URL and JSON-object of the dataLayer template which would be used to check the page dataLayer