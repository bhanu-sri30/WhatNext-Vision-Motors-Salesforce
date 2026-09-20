# Auto Assign Dealer Flow

## Purpose
Automatically assigns a suitable dealer to a Vehicle Order.

## Trigger
- Object: Vehicle Order
- Trigger: When a record is created
- Condition: Status = Pending

## Flow Process
1. A new Vehicle Order is created.
2. The flow checks the order status.
3. The related Vehicle Customer record is retrieved.
4. The customer's address is compared with dealer location.
5. A matching dealer is identified.
6. The dealer is assigned to the Vehicle Order.

## Salesforce Feature
Record-Triggered Flow
