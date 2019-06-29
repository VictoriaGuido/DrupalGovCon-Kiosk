# DrupalGovCon-Kiosk
This repository is intended for building the functionalities in Drupal8 for three tracks- client registration, advancing the Appointment|Reminder tool, and advancing the Check-In tool

## Pre-requisites:
Moderate or expert Drupal 8 knowledge involving experience with Drupal modules, PHP, Contenta API and React. This module will be built with Drupal 8 methods (all of the logic and functionality). 

## What is the goal of these tasks?
(1) To build functionality within the Drupal framework to register clients using a file using Contenta API

(2) To build functionality within the Appt|Event Reminder tool to allow the service provider to upload and process a file

(3) To build functionality within the Check-In tool to allow for the service provider to download a file, by interacting with an API endpoint

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
