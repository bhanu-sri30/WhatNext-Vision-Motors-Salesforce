# WhatNext Vision Motors - Salesforce

## Project Overview

WhatNext Vision Motors is a Salesforce-based vehicle management system designed to manage vehicles, dealers, customers, vehicle orders, test drives, and service requests.

The project uses Salesforce custom objects, Record-Triggered Flows, Apex Triggers, Batch Apex, and Scheduled Apex to automate important vehicle management processes.

## Objectives

- Manage vehicle and dealer information.
- Manage customer information.
- Create and track vehicle orders.
- Automatically assign dealers to vehicle orders.
- Manage test drive bookings.
- Send reminders for scheduled test drives.
- Manage vehicle service requests.
- Automatically process pending vehicle orders based on stock availability.
- Maintain vehicle stock automatically.

## Salesforce Custom Objects

The project contains the following custom objects:

1. **Vehicle__c** - Stores vehicle details and stock information.
2. **Vehicle_Dealer__c** - Stores dealer information.
3. **Vehicle_Customer__c** - Stores customer information.
4. **Vehicle_Order__c** - Stores vehicle purchase orders.
5. **Vehicle_Test_Drive__c** - Stores test drive bookings.
6. **Vehicle_Service_Request__c** - Stores vehicle service requests.

## Automation

### Auto Assign Dealer

A Record-Triggered Flow is used to automatically assign a suitable dealer when a vehicle order is created with Pending status.

### Test Drive Reminder

A Record-Triggered Flow with a Scheduled Path sends an email reminder to the customer one day before a scheduled test drive.

## Apex Trigger

### VehicleOrderTrigger

The trigger runs on Vehicle Order records during:

- Before Insert
- Before Update
- After Insert
- After Update

It works with the `VehicleOrderTriggerHandler` class to validate stock and update vehicle stock when an order is confirmed.

## Apex Trigger Handler

### VehicleOrderTriggerHandler

The handler contains the main business logic for:

- Checking vehicle stock availability.
- Preventing orders when a vehicle is out of stock.
- Updating vehicle stock when an order is confirmed.

## Batch Apex

### VehicleOrderBatch

The batch job processes Vehicle Orders with Pending status.

When stock is available:

1. The order status is changed to Confirmed.
2. Vehicle stock is reduced by one.

If stock is unavailable, the order remains Pending.

## Scheduled Apex

### VehicleOrderBatchScheduler

The scheduler starts the `VehicleOrderBatch` process automatically.

The intended schedule is a daily execution at midnight.

## Technology Stack

- Salesforce Platform
- Apex
- SOQL
- Salesforce Flow
- Custom Objects
- Record-Triggered Flow
- Batch Apex
- Scheduled Apex

## Project Structure

```text
WhatNext-Vision-Motors-Salesforce
│
├── appex
│   ├── VehicleOrderTriggerHandler.cls
│   ├── VehicleOrderBatch.cls
│   └── VehicleOrderBatchScheduler.cls
│
├── triggers
│   └── VehicleOrderTrigger.trigger
│
├── automation
│   ├── AutoAssignDealer.md
│   └── TestDriveReminder.md
│
├── objects
│   └── CustomObjects.md
│
├── screenshots
│   └── README.md
│
└── README.md
