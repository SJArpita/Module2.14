Q.Does SNS guarantee exactly once delivery to subscribers?
Ans.No, Amazon SNS (Simple Notification Service) does not guarantee exactly-once delivery to subscribers. It follows an "at-least-once" delivery model, meaning:
 Messages will be delivered at least once to each subscribed endpoint.However, duplicates may occur, so subscribers should handle idempotency.
Q.What is the purpose of the Dead-letter Queue (DLQ)? This is a feature available to SQS/SNS/EventBridge.
Ans.A Dead-Letter Queue (DLQ) is a special queue used to capture messages that cannot be successfully processed after multiple retry attempts. It helps in debugging, monitoring, and preventing message loss.
DLQ feature works following way in SQS/SNS/EvenBridge
SQS (Simple Queue Service)	Messages are moved to the DLQ after exceeding the maximum receive count.
SNS (Simple Notification Service)	Messages that cannot be successfully delivered to a subscriber (e.g., HTTP endpoint, Lambda) are sent to a DLQ.
EventBridge	Failed event deliveries (e.g., due to misconfigured targets) are stored in the DLQ for troubleshooting.
Q.How would you enable a notification to your email when messages are added to the DLQ?
Ans. To enable email notifications when messages are added to a Dead-Letter Queue (DLQ), we can integrate Amazon SNS with your DLQ and configure an SNS topic to send notifications. Here’s how to do it:
1. Create an SNS Topic
Go to the Amazon SNS console.
Click on Create topic and select Standard.
Enter a name for the topic, such as DLQ-Notification-Topic.
Click Create topic.
2. Subscribe Email to the SNS Topic
After creating the SNS topic, click on Create subscription.
Set the Protocol to Email.
Enter email address under Endpoint.
Click Create subscription.
Check inbox for a confirmation email and click Confirm subscription.
In the SNS topic configuration for original SNS notification system, configur the DLQ as a secondary SNS topic that receives messages that couldn't be delivered.
Then, configure the primary SNS subscription to notify via email when messages are placed in the DLQ.
