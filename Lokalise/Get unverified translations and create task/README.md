# Create a task with all unverified translations

## Overview

This Make.com workflow is designed to automate the process of retrieving unverified translations from Lkoalise, and creating a translation task for those translations. It efficiently handles API pagination in case you have a large # of keys or languages.

This workflow does consume a large volume of Make.com Operations, which are limited by subscription tier. In its current state, the workflow gets ALL unverified languages for each unique langauge and stores their associated key IDs for task creation. You can alter the workflow to consume less operations by filtering for the unverified translations of just one language if all languages are treated equally when the source langauge is updated. 

## Workflow Components

### 1. **Retrieve and Store Records with Pagination Support**
   - The workflow uses pagination to retrieve records from a multi-page API response. 
   - It keeps track of the current page and total page count, iterating through all available pages.
   - As each page is fetched, the records are stored in a datastore for easy access and reference. 
   - **Loop Breaking Condition**: The workflow stops making API requests when the current page matches the total number of pages, ensuring only necessary API calls are made.

### 2. **Create Lokalise Task**
   - After retrieving and storing all records, the workflow automatically creates a task in Lokalise.
   - Task details include:
      - **Title**: Contains the current date and execution ID for easy tracking.
      - **Languages**: Assigns the task to specific languages (e.g., Spanish) based on the retrieved records.
      - **Users/Teams**: Assigns translation tasks to specific users or teams in Lokalise.
      - **Source Language**: Defines the source language (e.g., English).
      - **Task Automation**: Enables settings for auto-closing languages, tasks, and items once translations are completed.

## Setup Notes

1. **Define Language and User Assignments in Lokalise**:
   - Specify the language codes, source language, and user or team assignments for all languages in your  the Lokalise task. You can modify these details in the workflow to match your project requirements.

