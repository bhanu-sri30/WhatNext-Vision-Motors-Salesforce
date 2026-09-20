# Salesforce Custom Objects

## 1. Vehicle__c
Stores vehicle information.

### Key Fields
- Vehicle_Name__c
- Vehicle_Model__c
- Stock_Quantity__c
- Price__c
- Dealer__c
- Status__c

## 2. Vehicle_Dealer__c
Stores dealer information.

### Key Fields
- Dealer_Name__c
- Dealer_Location__c
- Dealer_Code__c
- Phone__c
- Email__c

## 3. Vehicle_Customer__c
Stores customer information.

### Key Fields
- Customer_Name__c
- Email__c
- Phone__c
- Address__c
- Preferred_Vehicle_Type__c

## 4. Vehicle_Order__c
Stores vehicle purchase orders.

### Key Fields
- Customer__c
- Vehicle__c
- Order_Date__c
- Status__c

## 5. Vehicle_Test_Drive__c
Stores test drive bookings.

### Key Fields
- Customer__c
- Vehicle__c
- Test_Drive_Date__c
- Status__c

## 6. Vehicle_Service_Request__c
Stores vehicle service requests.

### Key Fields
- Customer__c
- Vehicle__c
- Service_Date__c
- Issue_Description__c
