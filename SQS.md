Amazon Simple Queue Service (SQS) is a fully managed message queuing service provided by AWS. It enables you to decouple and scale microservices, distributed systems, and serverless applications by allowing components to communicate through messages without requiring direct integration. SQS offers reliable and scalable message queuing, ensuring that messages are delivered and processed.

Key Features
Decoupling:

SQS allows you to decouple the components of your applications. Producers send messages to the queue, and consumers process those messages, enabling independent scaling and fault tolerance.
Scalability:

SQS automatically scales to handle any volume of messages, ensuring that your application can handle varying workloads without manual intervention.
Reliability:

Messages are stored redundantly across multiple servers and data centers, ensuring high availability and durability.
Security:

SQS provides features such as encryption at rest, access control policies, and VPC endpoints to secure message data and control access.
Dead-Letter Queues (DLQs):

Allows you to handle messages that cannot be processed successfully after multiple attempts. These messages are moved to a separate DLQ for further investigation.
Visibility Timeout:

Ensures that messages are not processed more than once by hiding messages from other consumers while they are being processed.
Types of SQS Queues
Standard Queues:

Description: Standard queues offer maximum throughput, at-least-once delivery, and best-effort ordering. They are ideal for applications where the order of messages is not critical, and you need high throughput and scalability.
Features:
At-Least-Once Delivery: Messages are delivered at least once, but there might be occasional duplicates.
Best-Effort Ordering: Messages are generally delivered in the order they are sent, but this is not guaranteed.
Unlimited Throughput: Supports a nearly unlimited number of transactions per second.

FIFO Queues (First-In-First-Out):

Description: FIFO queues are designed to ensure that messages are processed exactly once and in the exact order that they are sent. They are suitable for applications that require strict ordering and exactly-once message processing.
Features:
Exactly-Once Processing: Guarantees that each message is processed exactly once and that duplicates are eliminated.
Strict Ordering: Ensures that messages are processed in the order they are sent.
Limited Throughput: Provides a maximum of 300 transactions per second (TPS) for standard FIFO queues. You can increase throughput by enabling batching.
Key Concepts
Messages:

Messages are the basic units of communication in SQS. They consist of a body and optional attributes. Messages can be up to 256 KB in size.
Queue:

A queue is a temporary storage location for messages. Producers send messages to the queue, and consumers receive and process them.

Visibility Timeout:

When a consumer receives a message, the message is hidden from other consumers for a specified visibility timeout period. If the message is not deleted or its processing is not completed within the timeout, it becomes visible again for other consumers.

Message Retention:
SQS allows you to configure the retention period for messages, ranging from 1 minute to 14 days. Messages are automatically deleted once they reach the end of the retention period.
Dead-Letter Queue (DLQ):

A DLQ is used to handle messages that cannot be processed successfully after multiple attempts. It helps in isolating problematic messages for further analysis.
Batch Operations:

SQS supports batch operations for sending and receiving multiple messages at once, reducing the number of API calls and improving performance.
Use Cases
Decoupling Microservices:

SQS can decouple microservices, allowing them to communicate asynchronously and handle varying workloads independently.
Order Processing:

FIFO queues can be used for order processing systems where maintaining the order of transactions is crucial.
Event Notification:

SQS can be used to send notifications or trigger events in response to specific actions or changes in your application.
Message Buffering:

SQS can act as a buffer to handle burst loads or traffic spikes, ensuring that your application can handle temporary surges in activity.
Job Queuing:

Use SQS to manage and process background jobs or tasks, ensuring that they are handled asynchronously and reliably.
Summary
Amazon SQS is a powerful message queuing service that provides reliable and scalable communication between components of a distributed system. With its two types of queues—Standard and FIFO—SQS offers flexibility to meet different application requirements, from high-throughput scenarios to those requiring strict message ordering and exactly-once processing.

# Auto scaling

Scenario Overview
Use Case: The scenario involves a web application that allows users to upload images, which need to be resized and encoded before being published. This app uses EC2 instances in an Auto Scaling group to handle the processing of images.
Current Setup: Each image upload generates a task that is queued in an Amazon SQS queue. The app processes these tasks on EC2 instances.

Problem: The existing architecture is suitable for a stable rate of uploads but struggles when the upload rate varies significantly. This necessitates dynamic scaling of the Auto Scaling group to match the processing demand.

Dynamic Scaling with Target Tracking
Target Tracking Policy: A target tracking scaling policy is used, which scales the number of instances based on a custom metric related to the SQS queue.
Backlog Per Instance Metric: This custom metric measures the number of messages in the SQS queue relative to the number of active instances in the Auto Scaling group. The formula is: Backlog per instance = ApproximateNumberOfMessages / Number of instances.
Acceptable Backlog: The target value for scaling is based on the acceptable processing latency, which is determined by dividing the maximum allowable latency by the average processing time per message.
Example Calculation

Given Data: If you have 10 instances and 1,500 messages in the queue, with each message taking 0.1 seconds to process and a maximum allowable latency of 10 seconds:
Acceptable backlog per instance = 10 seconds / 0.1 seconds = 100 messages.
Since the backlog per instance is 150 (1,500 messages / 10 instances), the Auto Scaling group will scale out by five instances to maintain the desired target value.
Implementation Steps

Custom Metric Publication: Use the AWS CLI or an SDK to publish the custom metric to Amazon CloudWatch.
Target Tracking Policy Setup: Configure the Auto Scaling group to use the custom metric and define the target value through a target tracking policy.

CloudWatch Integration: CloudWatch alarms trigger the scaling actions based on the metric values.
Limitations and Requirements

AWS CLI or SDK Use: The custom metric must be published using the AWS CLI or an SDK; it cannot be directly configured through the EC2 Auto Scaling console.
Prerequisites: An existing Amazon SQS queue, Auto Scaling group, and EC2 instances are required to implement this scaling solution.
Instance Scale-In Protection

Handling Terminations: When instances are terminated, unprocessed messages are returned to the SQS queue for reassignment.
Scale-In Protection: Applications that handle long-running tasks can use scale-in protection to control which instances are terminated during a scale-in event.


# SNS vs SQS

Comparison
SNS is more about broadcasting messages to multiple endpoints (subscribers) simultaneously. Each subscriber gets a copy of the message, and the messages are not removed from SNS until they are successfully delivered to all endpoints.
SQS is more about queuing messages and having multiple consumers process those messages. Each message in a queue is processed by only one consumer, but multiple consumers can work in parallel to process the queue's messages.

# Message Deletion Process
Message Retrieval: When a consumer retrieves a message from an SQS queue, the message is not immediately removed from the queue. Instead, it becomes invisible to other consumers for a specified period known as the visibility timeout.

Processing: The consumer processes the message during this visibility timeout period. If the processing is successful, the consumer needs to explicitly delete the message from the queue.

Message Deletion:

API Call: The consumer application makes an API call to Amazon SQS to delete the message. This is done using the DeleteMessage API call. The consumer needs to provide the ReceiptHandle of the message, which is obtained when the message was retrieved from the queue.
Successful Deletion: Once the DeleteMessage API call is successfully processed, the message is removed from the queue and will no longer be available for retrieval.
Failure to Delete:

Visibility Timeout Expiry: If the message is not deleted within the visibility timeout period, it becomes visible again in the queue and can be retrieved by the same or different consumers.
Retries: If the consumer fails to process the message (e.g., due to an error) and does not delete it, the message will be retried based on the queue’s configuration and the visibility timeout.

