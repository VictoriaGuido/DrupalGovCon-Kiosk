# DrupalGovCon-Kiosk
This repository is intended for building the functionalities in Drupal8 for three tracks- client registration, advancing the Appointment|Reminder tool, and advancing the Check-In tool

## Pre-requisites:
Moderate or expert Drupal 8 knowledge involving experience with Drupal modules, PHP, Contenta API and React. This module will be built with Drupal 8 methods (all of the logic and functionality). 

## What is the goal of these tasks?
(1) Migrate from Drupal 7 to Drupal 8, prioritizing the Service Provider, Client and additional roles

(2) Set up Contenta, to provide an API interface for frontend and external backend technologies outside of Drupal

(3) Build functionality within the Drupal framework to register clients by reading from a CSV file provided by a Python app, by utilizing Contenta to expose a Drupal POST API

(4) Build functionality within the Check-In tool to allow for the service provider to download the report file (Excel XLSX), by interacting with AWS S3 (Data Lake) through an API endpoint provided by AWS API Gateway (if provided pro-bono)

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
