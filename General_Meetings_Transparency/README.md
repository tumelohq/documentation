# General Meetings Transparency

## Overview

This guide explains how to obtain a set of general meetings from a set of instrument ISINs. This may be used for example to show any upcoming general meetings related to a particular instrument. 

## Pre-requisites

* Must have signed up with Tumelo and obtained the credentials for your service user account (see [Getting Started](../Getting_Started/README.md) for further details)

### Organizations

Organizations represent public companies and other institutions such as governments that issue shares or bonds which are then traded on the world's financial markets.

### General Meetings

General meetings are either an annual general meeting (AGM) or an extraordinary general meeting (EGM). An organization will have 0 or more general meetings that can be listed. The API allows filtering of general meetings by the meeting date. This allows you to only retrieve meetings that have not yet ocurred for example.

## API Request Flow

### Step 1 - Authenticate

Authenticate with the Tumelo system

### Step 2 - Listing organizations

List the organizations, queried by issued ISINs.

| Tumelo API Documentation Link | [List organizations](https://docs.tumelo.com/#operation/listOrganizations) |
|-------------------------------|---------------------------------------------------------------------------------|

### Step 3 - Listing general meetings for each organization

For each organization returned by step 2, list the general meetings for that organization.

| Tumelo API Documentation Link | [List General Meetings](https://docs.tumelo.com/#operation/listGeneralMeetings) |
|-------------------------------|---------------------------------------------------------------------------------|
