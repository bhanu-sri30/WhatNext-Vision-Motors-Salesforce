# Test Drive Reminder Flow

## Purpose
Sends an email reminder to the customer before a scheduled test drive.

## Trigger
- Object: Vehicle Test Drive
- Trigger: When a record is created or updated
- Condition: Status = Scheduled

## Flow Process
1. A test drive is scheduled.
2. The flow checks whether the status is Scheduled.
3. A scheduled path runs one day before the test drive date.
4. The related customer record is retrieved.
5. An email reminder is sent to the customer.

## Salesforce Feature
Record-Triggered Flow with Scheduled Path
