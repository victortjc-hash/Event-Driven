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

5. Test Dev Rule
6. 
