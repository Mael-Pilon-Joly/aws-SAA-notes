# Metrics

Remember that by default, CloudWatch doesn't monitor memory usage but only the CPU utilization, Network utilization, Disk performance, and Disk Reads/Writes.

# Unified agent

Amazon CloudWatch Unified Agent is a unified logging and monitoring agent designed to collect metrics and logs from your Amazon EC2 instances, on-premises servers, and other sources. It simplifies the process of monitoring your infrastructure by consolidating the collection and sending of both metrics and logs to Amazon CloudWatch, AWS's monitoring and observability service.

Key Features of CloudWatch Unified Agent
Unified Data Collection:

Metrics and Logs: The agent can collect both custom metrics and log data from your servers, making it easier to monitor your resources without needing separate agents for different data types.
Ease of Deployment:

Single Agent: Instead of deploying multiple agents for different types of data, you use a single agent to handle both logs and metrics.
Configuration: You configure the agent using a single configuration file, simplifying management.
Support for Various Data Sources:

EC2 Instances: The agent can be installed on Amazon EC2 instances to collect metrics and logs.
On-Premises Servers: You can also use it to monitor on-premises servers, providing flexibility for hybrid environments.
Centralized Management:

Configuration Management: You can manage the configuration of the agent centrally, making it easier to deploy and update across multiple instances or servers.
AWS Systems Manager Integration: The agent can be managed using AWS Systems Manager, which allows for easy configuration and deployment through Systems Manager Run Command.
Rich Monitoring Capabilities:

Custom Metrics: The agent can be configured to collect custom metrics from applications or system performance metrics.
Log Collection: It supports collecting and forwarding log data to CloudWatch Logs, where you can set up alerts, visualize logs, and perform analysis.

While it's commonly used for collecting metrics and logs, it also allows for configuration to tailor its behavior to specific needs. Here are a few key aspects of configuring the CloudWatch Unified Agent:

Configuration Capabilities
Custom Metrics:

You can configure the agent to collect custom metrics beyond the default ones, such as memory usage, disk space, or application-specific metrics. This helps in monitoring aspects that are crucial for your specific applications or infrastructure.
Log Collection:

The agent can be configured to collect logs from various sources, including application logs, system logs, and custom log files. You can specify which log files to monitor and how to format the log data.
Configuration File:

The configuration is typically done using a JSON or YAML file where you specify the metrics and logs to be collected. This configuration file can be centrally managed and distributed using tools like AWS Systems Manager Parameter Store or AWS Secrets Manager.
Integration with CloudWatch:

The agent sends collected data to Amazon CloudWatch, where you can create dashboards, set up alarms, and analyze the data. Configuration options include defining how often metrics are sent, the granularity of logs, and more.
Automatic Updates:

Using AWS Systems Manager, you can automate the deployment and update of the agent's configuration across multiple instances, making it easier to manage large-scale environments.

# Event-Bridge

Amazon EventBridge is a serverless event bus service provided by AWS that makes it easier to build event-driven applications. It helps you connect different services, applications, and components using events, allowing them to react to changes in real time. Here’s a detailed overview of Amazon EventBridge:

Key Features
Event Buses:

Default Event Bus: Handles events from AWS services.
Custom Event Buses: You can create your own event buses to handle events from your applications or external sources.
Partner Event Buses: Provides integration with AWS partner services that can send events to EventBridge.
Event Sources and Targets:

Event Sources: Can be AWS services, custom applications, or SaaS applications that publish events to EventBridge.
Event Targets: Define where events should be sent. Targets can include AWS Lambda functions, Step Functions, Amazon SNS, Amazon SQS, AWS Kinesis Data Streams, and more.
Event Routing:

Event Rules: Rules help filter and route events to the appropriate targets based on the event content. Rules can match event patterns and trigger specific actions.
Event Patterns: Specify the criteria that events must meet to trigger a rule. Patterns can include various fields of the event data to make routing decisions.
Schema Registry and Discovery:

Schema Registry: Automatically discovers and registers the schemas of events sent to EventBridge, making it easier to manage and use event data.
Schema Discovery: Helps discover the structure of events and store schemas for easier integration with other services.
Integration with AWS Services:

Direct Integration: Many AWS services can directly send events to EventBridge, such as Amazon EC2, Amazon RDS, AWS CodePipeline, and more.
Service Integration: EventBridge integrates with various AWS services, allowing you to build complex event-driven workflows.
Use Cases
Application Integration:

Integrate different components of your application by using events to trigger actions in response to changes or specific conditions.
Real-Time Data Processing:

Process data in real time by routing events to Lambda functions or other processing services as they occur.
Microservices Architecture:

Facilitate communication between microservices by using events to decouple components and handle interactions asynchronously.
Monitoring and Automation:

Automate responses to system events or changes by triggering automated workflows or notifications based on event patterns.
Third-Party Integrations:

Connect with SaaS applications and external systems that can send events to EventBridge for processing or integration.
Example Workflow
Event Generation: An application or AWS service generates an event (e.g., a new file uploaded to S3).
Event Publication: The event is published to an EventBridge event bus.
Event Matching: EventBridge evaluates the event against defined rules.
Event Routing: If the event matches a rule, EventBridge routes it to the specified target (e.g., triggering a Lambda function).
Event Processing: The target processes the event, performing the desired action (e.g., processing the uploaded file).