# WhatNext Vision Motors - Salesforce

## Project Overview

**WhatNext Vision Motors** is a Salesforce-based vehicle management system designed to manage vehicles, dealers, customers, vehicle orders, test drives, and service requests.

The project uses **Salesforce Custom Objects, Record-Triggered Flows, Apex Triggers, Batch Apex, and Scheduled Apex** to automate important vehicle management processes.

## Objectives

* Manage vehicle and dealer information.
* Manage customer information.
* Create and track vehicle orders.
* Automatically assign dealers to vehicle orders.
* Manage test drive bookings.
* Send reminders for scheduled test drives.
* Manage vehicle service requests.
* Automatically process pending vehicle orders based on stock availability.
* Maintain vehicle stock automatically.

---

## Salesforce Custom Objects

The project contains the following custom objects:

1. **Vehicle__c** - Stores vehicle details and stock information.
2. **Vehicle_Dealer__c** - Stores dealer information.
3. **Vehicle_Customer__c** - Stores customer information.
4. **Vehicle_Order__c** - Stores vehicle purchase orders.
5. **Vehicle_Test_Drive__c** - Stores test drive bookings.
6. **Vehicle_Service_Request__c** - Stores vehicle service requests.

---

## Object Implementation

### 1. Vehicle__c

* **Before:** Vehicle details such as model, price, status, dealer, and stock quantity need to be stored and managed.
* **Code/Automation:** Vehicle stock is checked and updated through the Vehicle Order Trigger/Handler, Batch Apex, and Scheduled Apex.
* **After:** Vehicle information is maintained in Salesforce, and stock is automatically reduced when a confirmed order is processed.

### 2. Vehicle_Dealer__c

* **Before:** Dealer information needs to be maintained so that suitable dealers can be assigned to vehicle orders.
* **Code/Automation:** The Auto Assign Dealer Flow uses dealer information and dealer location to assign a suitable dealer to a vehicle order.
* **After:** Dealer information is centrally maintained and a suitable dealer can be assigned automatically.

### 3. Vehicle_Customer__c

* **Before:** Customer details need to be stored so customers can place orders and schedule test drives.
* **Code/Automation:** Customer information is used by the Auto Assign Dealer Flow and Test Drive Reminder Flow.
* **After:** Customer information is organized in Salesforce and can be associated with orders and test drives.

### 4. Vehicle_Order__c

* **Before:** Order is created with `Pending` status and vehicle stock is available or unavailable.
* **Code/Automation:** Trigger + Handler + Batch + Scheduler + Flow process the order.
* **After:** If stock is available, the order becomes `Confirmed` and stock decreases; if unavailable, the order remains `Pending`.

### 5. Vehicle_Test_Drive__c

* **Before:** A customer schedules a test drive for a selected vehicle.
* **Code/Automation:** The Test Drive Reminder Flow uses a Record-Triggered Flow with a Scheduled Path.
* **After:** The customer receives an email reminder one day before the scheduled test drive.

### 6. Vehicle_Service_Request__c

* **Before:** Customers may need vehicle servicing or report vehicle-related issues.
* **Code/Automation:** A custom Service Request object stores customer, vehicle, service date, and issue information.
* **After:** Service requests can be stored and tracked in a structured format.

---

## Automation

### Auto Assign Dealer

A **Record-Triggered Flow** is used to automatically assign a suitable dealer when a vehicle order is created with `Pending` status.

### Flow Process

1. A Vehicle Order is created.
2. The flow checks the order status.
3. The related Vehicle Customer is retrieved.
4. Customer address and dealer location are used for dealer matching.
5. A suitable dealer is identified.
6. The dealer is assigned to the Vehicle Order.

### Salesforce Feature

**Record-Triggered Flow**

---

### Test Drive Reminder

A **Record-Triggered Flow with a Scheduled Path** sends an email reminder to the customer one day before a scheduled test drive.

### Flow Process

1. A test drive is scheduled.
2. The flow checks whether the status is `Scheduled`.
3. A scheduled path runs one day before the test drive date.
4. The related customer is retrieved.
5. An email reminder is sent to the customer.

### Salesforce Feature

**Record-Triggered Flow with Scheduled Path**

---

## Apex Trigger

### VehicleOrderTrigger

The `VehicleOrderTrigger` runs on Vehicle Order records during:

* Before Insert
* Before Update
* After Insert
* After Update

It works with the `VehicleOrderTriggerHandler` class to validate vehicle stock and update vehicle stock when an order is confirmed.

---

## Apex Trigger Handler

### VehicleOrderTriggerHandler

The handler contains the main business logic for:

* Checking vehicle stock availability.
* Preventing orders when a vehicle is out of stock.
* Updating vehicle stock when an order is confirmed.

The handler keeps the main business logic separate from the trigger.

---

## Batch Apex

### VehicleOrderBatch

The `VehicleOrderBatch` processes Vehicle Orders with `Pending` status.

When stock is available:

1. The order status is changed to `Confirmed`.
2. Vehicle stock is reduced by one.

If stock is unavailable, the order remains `Pending`.

Batch Apex allows pending orders to be processed automatically in batches.

---

## Scheduled Apex

### VehicleOrderBatchScheduler

The `VehicleOrderBatchScheduler` starts the `VehicleOrderBatch` process automatically.

The intended schedule is a **daily execution at midnight**.

This allows pending vehicle orders to be checked automatically without requiring manual execution.

---

## Overall Order Processing

```text
Customer
   ↓
Vehicle Order Created
   ↓
Status = Pending
   ↓
Auto Assign Dealer Flow
   ↓
Vehicle Stock Check
   ↓
Stock Available?
   ├── No → Order remains Pending
   │
   └── Yes
        ↓
     Order Confirmed
        ↓
     Stock Reduced
```

---

## Test Drive Process

```text
Customer
   ↓
Test Drive Created
   ↓
Status = Scheduled
   ↓
Scheduled Path
   ↓
One Day Before Test Drive
   ↓
Reminder Email Sent
```

---

## Technology Stack

* **Salesforce Platform**
* **Apex**
* **SOQL**
* **Salesforce Flow**
* **Custom Objects**
* **Record-Triggered Flow**
* **Batch Apex**
* **Scheduled Apex**

---

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
```

---

## Key Features

* Vehicle inventory management
* Customer management
* Dealer management
* Vehicle order management
* Test drive management
* Service request management
* Automated dealer assignment
* Automated test drive reminders
* Vehicle stock validation
* Pending vehicle order processing
* Batch processing
* Scheduled automation

---

## Project Outcome

The project demonstrates how **Salesforce Custom Objects, Flow Automation, Apex Triggers, Batch Apex, and Scheduled Apex** can be combined to build a vehicle management system with automated business processes and inventory handling.

The system reduces manual processing by automating dealer assignment, stock validation, pending order processing, and test drive reminders.

---

## Future Enhancements

* Customer and dealer dashboards
* Advanced reporting and analytics
* Improved dealer matching using multiple parameters
* Automated service reminders
* Notification integration
* Lightning Web Components for enhanced user experience

---

## Author

**Bhanu Sri Thallapaneni**

**B.Tech - Artificial Intelligence and Data Science**
