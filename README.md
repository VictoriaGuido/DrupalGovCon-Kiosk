# DrupalGovCon-Kiosk
This repository is intended for building the functionalities in Drupal8 for three tracks- client registration, advancing the Appointment|Reminder tool, and advancing the Check-In tool.

## Pre-requisites:
Moderate or expert Drupal 8 knowledge involving experience with Drupal modules, PHP, Contenta API and React. This module will be built with Drupal 8 methods (all of the logic and functionality). 

## Architectural Overview
HopeOneSource consists of many technological systems, among which are the Drupal 7 and Python app running on AWS (Cloud). Currently, these systems operate independently:
- The Drupal environment handles user profiles (Service Providers/Clients/others) and functionality modules
- The Python app handles the check-in kiosk operations, including data ingestion, manipulation, reporting and file sharing.

The interactivity between these systems is key to achieving multiple important functionalities -

1. Adding registration capability from the kiosk- At present, user profiles are created in Drupal only through registration on a Drupal 7 form. Going forward, it is desired to set up a means for new clients to register through the kiosk, which is handled by the Python App running on AWS. To achieve this, we intend to set up an API using Contenta, connecting to the module in Drupal 8 to manage CRUD functionalities. The API will act as an endpoint for incoming JSON payloads containing registration information of new clients , which are provided from the Python app interacting with AWS elements. This payload should be imported and utilized to create new user (client) profiles.

2. Rendering the report for service providers- At present, the kiosk reports are created using the Python app deployed in EC2, and are stored in S3 (Data lake). These reports are accessed by the service providers via a URL link provided by AWS API Gateway. Going forward, it is desired to provide a download functionality within Drupal. This is to be achieved by creating a download button on a Drupal 8 page, and directing the action of the button to request Excel payload from AWS API Gateway by providing the name of the service provider in question based on their role within Drupal and their marching account name. 

In both situations, data would be encrypted in transit and at rest. Authentication would be managed using user profile information managed by Drupal.

## Current and Future Architecture Diagram
Please view 'Architectural Diagram.png' in repo

## What is the goal of these tasks?
### Drupal Migration:
(1) Migrate from Drupal 7 to Drupal 8 (using Drupal Migrate -- https://www.drupal.org/project/migrate), prioritizing the Service Provider, Client and additional roles

### Contenta:
(2) Set up Contenta, to provide an API interface for frontend and external backend technologies outside of Drupal

### Kiosk Interfacing:
One of the main systems involved in HopeOneSource is the Check-In Kiosk, which is simply through a survey on a tablet placed at service provider locations. A Python app has been built, which wraps around various AWS modules, currently providing storage and data manipulation functionalities for data collected from the kiosk.

(3) Build functionality within the Drupal environment to allow for the service provider to download the report file (Excel XLSX) by clicking a button. This would be achieved by interacting with an API endpoint provided by AWS API Gateway (if provided pro-bono), fetching the appropriate file from AWS S3 (Data Lake).

(4) Build functionality within the Drupal environment to register clients by reading from a CSV/JSON payload provided by the Python app, internally utilizing Contenta to expose a Drupal POST API.

## Strategy
(1)
Prepare the site for Drupal 8 (https://www.drupal.org/docs/8/upgrade/preparing-a-site-for-upgrade-to-drupal-8). Identify the key modules (that include javascript) that impact the content, and are critical to proper interaction with the users.  Then check to see if it is on the latest version and if a D8 version exists. Then catalog the content types and views and prioritize what must get moved, which is almost a data cleaning process.

(2)
Set up ContentaCMS, and then manually re-create content on the Contenta Site.

(3)
Create a button for users whose authenticated role is ____, _____, or ______ and belong to a specific list of service providers.
Create functionality for the button to pass on Organization Name (?) as query input (eg: 'Arlington Free Clinic, VA.xlsx') to the established API endpoint
Allow for download of the xlsx file on pressing of the button

(4)
Set up a CRUD module which utilizes an input CSV file to create new user profiles, which exposes an API endpoint using Contenta.

## Environment
Any basic vanilla Drupal 8 environment is acceptable for development.

## API Schemas
### 1. Retrieval of check-in reports from AWS (Cloud)
{\
	"title": "Kiosk Report",\
   "description": "Report File",\
   "type": "object",\
   "properties":\
   {\
      "name":\
      {\
         "description": "Service Provider",\
         "type": "string"
      }                                              
   },\
   "required": ["name"]\
}

### 2. Registration of clients in Drupal
{\
   "title": "Client",\
   "description": "Client Record",\
   "type": "object",\
   "properties":\
   {\
      "name":\
      {\
         "description": "Client Name",\
         "type": "string"\
      },\
      "phone":\
      {\
         "description": "Client Phone Number",\
         "type": "number"\
      },\
      "birthday":\
      {\
         "description": "Client Birthdate [MM,DD,YYYY]",\
         "type": "array"\
      },\
      "gender":\
      {\
         "description": "Client Gender",\
         "type": "string"\
      },\
      "registering_org":\
      {\
         "description": "Organization which registered client",\
         "type": "string"\
      },\
      "location":\
      {\
         "description": "Location coordinates [lat,lon]",\
         "type": "array"\
      },\
      "services":\
      {\
         "description": "Desired services",\
         "type": "array"\
      },\
      "demographics":\
      {\
         "description": "Client Demographics",\
         "type": "array"\
      },\
      "sleep_loc":\
      {\
         "description": "Sleep Location",\
         "type": "string"\
      },\
      "unstably_housed":\
      {\
         "description": "Whether client is unstably housed",\
         "type": "boolean"\
      }                             
   },\
   "required": ["name","phone","birthday","gender","registering_org","location","services","demographics","sleep_loc","unstably_housed"]\
}

