# Product Description

## Product Description
This repository contains the Tag Monitor source code and terraform documents. Tag Monitor uses [Google Tag Management](https://tagmanager.google.com/#/home) which is a tag delivery system that allows you to quickly and easily update measurement codes and related code fragments (collectively known as tags) on a website or mobile app. Tag monitoring will allow you to understand if important tags are actually firing for real users and see when they break down in a well formatted table. 

## How it works
The key deliverable of Tag monitor is a BigQuery view that collects data from a website. This is supported by a Cloud Function that collects the pixel and stores it into BigQuery. The data will be sent by way of a new Google Tag Manager custom template, and it will comprise statistics of all the tags (or a random portion of it) that have fired on the website for any given dataLayer event.

![image](../images/product-desc.png)

The basic setup of the monitor collects the following metadata from each dataLayer event:
- Event name and timestamp (to uniquely distinguish events with the same name from each other).
- Tag ID, name, firing status, and execution time for every tag that fired for that event (or null if no tags fired for the event).

This solution can be easily extended to include other metadata, like container ID, domain etc.