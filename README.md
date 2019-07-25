# DrupalGovCon-Kiosk
This repository is intended for building the functionalities in Drupal8 for two tracks- kiosk report rendering and client registration

## Pre-requisites:
Moderate or expert Drupal 8 knowledge involving experience with Drupal modules, PHP, Drupal API and React. This module will be built with Drupal 8 methods (all of the logic and functionality). 

## Architectural Overview
HopeOneSource consists of many technological systems, among which are the Drupal and Python app running on AWS (Cloud). Currently, these systems operate independently:
- The Drupal environment handles user profiles (Service Providers/Clients/others) and functionality modules
- The Python app handles the check-in kiosk operations, including data ingestion, manipulation, reporting and file sharing.

The interactivity between these systems is key to achieving multiple important functionalities -

1. Rendering the report for service providers- At present, the kiosk reports are created using the Python app deployed in EC2, and are stored in S3 (Data lake). These reports are accessed by the service providers via a URL link provided by AWS API Gateway. Going forward, it is desired to provide a download functionality within Drupal. This is to be achieved by creating a download button on a Drupal 8 page, and directing the action of the button to request Excel payload from AWS API Gateway by providing the name of the service provider in question based on their role within Drupal and their marching account name. 

2. Adding registration capability from the kiosk- At present, user profiles are created in Drupal only through registration on a Drupal 7 form. Going forward, it is desired to set up a means for new clients to register through the kiosk, which is handled by the Python App running on AWS. To achieve this, we intend to set up an API with Drupal, connecting to the module in Drupal 8 to manage CRUD functionalities. The API will act as an endpoint for incoming JSON payloads containing registration information of new clients , which are provided from the Python app interacting with AWS elements. This payload should be imported and utilized to create new user (client) profiles.

In both situations, data would be encrypted in transit and at rest. Authentication would be managed using user profile information managed by Drupal.

## Current and Future Architecture Diagram
Please view 'Architectural Diagram.png' in repo

## What is the goal of these tasks?

### Kiosk Interfacing:
One of the main systems involved in HopeOneSource is the Check-In Kiosk, which is simply through a survey on a tablet placed at service provider locations. A Python app has been built, which wraps around various AWS modules, currently providing storage and data manipulation functionalities for data collected from the kiosk.

(1) Build functionality within the Drupal environment to allow for the service provider to download the report file (Excel XLSX) by clicking a button. This would be achieved by interacting with an API endpoint provided by AWS API Gateway (if provided pro-bono), fetching the appropriate file from AWS S3 (Data Lake).

(2) Build functionality within the Drupal environment to register clients by reading from a CSV/JSON payload provided by the Python app, internally utilizing API with Drupal to expose a Drupal POST API.

## Strategy
(1)
Create a button for users whose authenticated role is Standard Service Provider, Advanced Service Provider or Premium Service Provider, and belong to a specific list of service providers. Create functionality for the button to pass on Organization Name as query input (eg: 'Sample Service Provider Check-in Report.xlsx') to the established API endpoint. Allow for download of the xlsx file on pressing of the button

(2)
Set up a CRUD module which utilizes an input CSV file to create new user profiles, while exposing a POST API endpoint using API with Drupal.

## Environment
Any basic vanilla Drupal 8 environment is acceptable for development.

## AWS API Configuration
### 1. Rendering kiosk reports (GET)
Endpoint- Provided in Slack

Authorization-
Access key: Provided in Slack
Secret key: Provided in Slack
Region: us-east-1
Service: execute-api

Headers-
Host: 6i64lmzix2.execute-api.us-east-1.amazonaws.com
Content-Type: application/json
Accept: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet

X-Amz-Date: 20190725T094809Z
Authorization: AWS4-HMAC-SHA256 Credential=AKIAVTUU6QLUHXJOHW6U/20190725/us-east-1/execute-api/aws4_request, SignedHeaders=accept;cache-control;content-type;host;postman-token;x-amz-date, Signature=5c5cb92b3691c0bb068f7257249dd3a6015b6ea5d8e1cae0172fc37ca8c16bd1

#### Sample code:
require 'vendor/autoload.php';

use Aws\Credentials\Credentials;
use GuzzleHttp\Client;
use GuzzleHttp\Psr7\Request;
use Aws\Signature\SignatureV4;

$access_key = '<access_key>';
$secret_key = '<secret_key>';
$url = <endpoint_url>;
$region = 'us-east-1';

$credentials = new Credentials($access_key, $secret_key);
var_dump($credentials);

$client = new Client();
$request = new Request('GET', $url);
var_dump($request);

$s4 = new SignatureV4("execute-api", $region);
$signedrequest = $s4->signRequest($request, $credentials);

$response = $client->send($signedrequest);

## API Schema
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

