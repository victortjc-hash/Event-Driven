# Event-Driven
Event driven order system - EventBridge, Lambda, SQS, SNS 


In this workshop, I am building event-driven architecture on AWS, using the below workshop

https://catalog.us-east-1.prod.workshops.aws/workshops/63320e83-6abc-493d-83d8-f822584fb3cb/en-US/eventbridge

<img width="868" height="201" alt="Screenshot 2025-12-30 at 11 28 06 AM" src="https://github.com/user-attachments/assets/079e5420-4e7d-41e4-895d-86193b516aeb" />

I will create a custom EventBridge event bus, Orders and and Eventbridge Rule, OrderDevRule, which matches the order event bus and send events to a CloudWatch Logs log group 

1. Create an EventBus named Orders
<img width="1769" height="715" alt="Screenshot 2025-12-30 at 12 05 42 PM" src="https://github.com/user-attachments/assets/45f1846e-fe9c-4bd4-ba14-0523442ec90e" />


2. Setup Amazon Cloudwatch Target.

Within Orders event bus, I created a new rule named OrdersDevRule 
Parameters:
Rule Type : "Rule with an Event"
Event Pattern: "Other"
Event Pattern > Creation Method : "Custom Pattern JSON Editor" (To capture al events from com.aws.orders)
```
{
  "source": ["com.aws.orders"]
}
```

3. Select Targets

Parameters:
Target types: "AWS Service"
Select a target "Cloud log group"
Log Group: "/aws/events/orders

4. Create Rule.

5. Test Dev Rule (as below)
<img width="1580" height="695" alt="Screenshot 2025-12-30 at 1 54 55 PM" src="https://github.com/user-attachments/assets/ce6ba715-7918-46a6-8607-5a68ff48dbb8" />
-Send

7. Check Cloudwatch Log to see event is received: 
<img width="1604" height="712" alt="Screenshot 2025-12-30 at 1 56 01 PM" src="https://github.com/user-attachments/assets/e883be7b-3b8b-4dd4-a836-51df4460f69a" />

Working with EventBridge Rules.
The next steps of the workshop is to Rules match incoming events and routes them to targets for processing.
<img width="1079" height="393" alt="Screenshot 2025-12-30 at 1 58 05 PM" src="https://github.com/user-attachments/assets/e084f077-bd1e-42d1-8c22-28c7af317c03" />

From the diagram, I will create an Orders event Bus rule to match an event with a com.aws.orders source to an API Gateway endpoint, Invoke a AWS Step function and send events to an Amazon SNS (Simple Nofication Service) 

API Destination Challenge

1. Create an API Destination
<img width="1579" height="767" alt="Screenshot 2025-12-30 at 2 29 01 PM" src="https://github.com/user-attachments/assets/5ada67a7-c538-4254-b74d-91db332ccec1" />

2. Configure an Eventbridge Rule to target Event
 <img width="1599" height="721" alt="Screenshot 2025-12-30 at 2 41 58 PM" src="https://github.com/user-attachments/assets/8c6b06d6-207d-4e5a-8294-4af650f60191" />
ridge API Destination.

3. Sent test orders Event.
I will send Order Notifcation for testing: 
```
{ "category": "lab-supplies", "value": 415, "location": "us-east" }
```
<img width="1565" height="775" alt="Screenshot 2025-12-30 at 4 42 52 PM" src="https://github.com/user-attachments/assets/abaed6f6-795d-4a4c-99d1-1def20b9ed18" />
<img width="1223" height="763" alt="Screenshot 2025-12-30 at 4 44 39 PM" src="https://github.com/user-attachments/assets/bd9f2720-c682-46f2-aefb-5dc3e376702e" />
