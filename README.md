# DrupalGovCon-Kiosk
This repository is intended for building the functionality in Drupal8 for the primary purpose of querying (in Drupal) the check-in report (XLSX) from AWS S3 for respective service providers (AWS -> Drupal)

## Pre-requisites:
Moderate or expert Drupal 8 knowledge involving experience with Drupal modules, PHP, Contenta API and React. This module will be built with Drupal 8 methods (all of the logic and functionality). 

## What is the goal of these tasks?
(1) To build functionality within the Drupal framework to retrieve the appropriate .xlsx file report from AWS S3 by interfacing with an established REST API
(2)

## Strategy
(1)
Set up a CRUD module which utilizes an input CSV file to create new user profiles, which exposes an API endpoint using Contenta.

(2)
Create a button for users whose authenticated role is ____, _____, or ______ and belong to a specific list of service providers.
Create functionality for the button to pass on Organization Name (?) as query input (eg: 'Arlington Free Clinic, VA.xlsx') to the established API endpoint
Allow for download of the xlsx file on pressing of the button

(3)
Create a button for users whose authenticated role is ____, _____, or ______ and belong to a specific list of service providers.
Create functionality for the button to (i) upload a file (XLSX/CSV/PDF), (ii) pass it on as a POST call to an established REST API endpoint, (iii) after a certain amount of time, retrieve a CSV file from an established GET API endpoint, and (iv) point the Appt|Reminder module to utilize this file, as opposed to the current text box.

## Environment
Any basic vanilla Drupal 8 environment is acceptable for development.
