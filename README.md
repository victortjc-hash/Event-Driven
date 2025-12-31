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


Step Functions Challenge
In this module, I will implement add a new rule to existing event bus Orders that will only process orders coming from EU using an AWS Step function.

1. Create a new rule (EUOrdersRule) in EventBus (Orders)
 <img width="1710" height="709" alt="Screenshot 2025-12-31 at 10 19 26 AM" src="https://github.com/user-attachments/assets/306a1ead-e4e9-4260-9fbe-d28acf6c4e31" />
With Target: Step Function
<img width="1696" height="736" alt="Screenshot 2025-12-31 at 10 20 15 AM" src="https://github.com/user-attachments/assets/49b9d9c1-43da-492e-8e21-ae626395592b" />


Test Send Event - Success
Using test event - 
```
{ "category": "office-supplies", "value": 300, "location": "eu-west" }
```
<img width="1585" height="772" alt="Screenshot 2025-12-31 at 10 18 55 AM" src="https://github.com/user-attachments/assets/b95c336a-a429-41c8-adc3-c087a2a11ad2" />

SNS Challenge

In this module, I will add another rule to Orders event bus with the name USLocationSupplyRule.
This event pattern is to amtch detail locations in US (East/West) and category "lab-supplies".

Created a new rule as below: 
<img width="1634" height="733" alt="Screenshot 2025-12-31 at 10 30 40 AM" src="https://github.com/user-attachments/assets/889a9fc6-2530-4ff6-bea1-54e34bfd3b13" />

Target: SNS Topic
<img width="1739" height="719" alt="Screenshot 2025-12-31 at 10 33 59 AM" src="https://github.com/user-attachments/assets/2054a8c3-79d3-42f6-b7b2-970e5ac4f0cb" />

Test: 
Send Event using:
```
{ "category": "lab-supplies", "value": 415, "location": "us-east" }
```
<img width="1751" height="710" alt="Screenshot 2025-12-31 at 10 39 20 AM" src="https://github.com/user-attachments/assets/dc5b98c3-062a-4c55-baa4-dbdc494d870a" />

Confirmation:
<img width="1735" height="746" alt="Screenshot 2025-12-31 at 10 39 40 AM" src="https://github.com/user-attachments/assets/1b5b8a45-2f14-4be5-93e5-97b8d96228b1" />


Scheduling Expressions for rules.

This is for rules that self-trigger on an automated schedule in EventBridge. 
1. Create a schedule in EventBridge Scheduler.

Parameters as below:

<img width="1632" height="776" alt="Screenshot 2025-12-31 at 2 26 20 PM" src="https://github.com/user-attachments/assets/4c2f8edb-ac80-4aa3-b49c-416f43341744" />
<img width="1735" height="746" alt="Screenshot 2025-12-31 at 10 39 40 AM" src="https://github.com/user-attachments/assets/16443989-e709-4041-94ba-b44a749cc235" />

2. Verify Scheduled Message Delivery
Using Cloud Watch > Logs
<img width="1695" height="646" alt="Screenshot 2025-12-31 at 2 29 51 PM" src="https://github.com/user-attachments/assets/0ffbb436-5328-4a39-a6c9-0646a2fbe8a9" />

The log shows success triggers every minute as scheduled. 

Success. 



