# DrupalGovCon-Kiosk
This repository is intended for building the functionalities in Drupal8 for three tracks- client registration, advancing the Appointment|Reminder tool, and advancing the Check-In tool.

## Architectural overview:
One of the systems involved in HopeOneSource is a Python app wrapping around various AWS modules, currently providing storage and data manipulation functionalities for data collected from Check-In Kiosks (survey on a tablet placed on a stand).

Two of the below tasks involve transporting data between AWS and Drupal:

(1) Transporting data of clients who are registering using the kiosk, from AWS to Drupal (POST -- only required when a client signs up)

(2) Transporting kiosk reports (Excel) stored in AWS S3 (data lake), from AWS to Drupal (GET -- only required when service provider clicks a button from within Drupal environment)

## Pre-requisites:
Moderate or expert Drupal 8 knowledge involving experience with Drupal modules, PHP, Contenta API and React. This module will be built with Drupal 8 methods (all of the logic and functionality). 

## What is the goal of these tasks?
(1) Migrate from Drupal 7 to Drupal 8, prioritizing the Service Provider, Client and additional roles

(2) Set up Contenta, to provide an API interface for frontend and external backend technologies outside of Drupal

(3) Build functionality within the Check-In tool to allow for the service provider to download the report file (Excel XLSX), by interacting with AWS S3 (Data Lake) through an API endpoint provided by AWS API Gateway (if provided pro-bono)

(4) Build functionality within the Drupal framework to register clients by reading from a CSV file provided by a Python app, by utilizing Contenta to expose a Drupal POST API

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
