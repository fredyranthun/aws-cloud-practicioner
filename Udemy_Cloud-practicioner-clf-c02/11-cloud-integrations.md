# Cloud Integrations

- Applications need to communicate with each other
- Two patterns for this communication:

  - Synchronous communications (application to application)
  - Aynchronous communications / Event Based (application to queue to application) -> services become more decoupled

- Synchronous between applications can be problematic if there sudden spikes of traffic
- Decouple can be done:
  - using SQS: queue model
  - using SNS: pub/sub model
  - using Kinesis: real-time data streaming model
- These services can scale independently from our application

# Amazon SQS

- Simple Queue Service
- Producers will send a message to a queue -> SQS queue
- Consumers will poll the queue (requesting messages from the queue) - one or multiple consumers
- when they finish, they will delete the message from the queue

## Standard Queue

- Oldest AWS offering (over 10 years old)
- fully managed service (serverless), use to decouple applications
- Scales from 1 message per second to 10,000s per second
- default retention of messages: 4 days, maximum of 14 days
- no limit to how many messages can be in the queue
- Messages are deleted after they are read by consumers
- low latency (<10 ms on publish and receive)
- consumers share the work to read messages and scale horizontally

## Use Cases

- decouple between application tiers
- Requests -> Web Servers (Auto scaling group) -> put messages -> SQS Queue -> Video Processing (Auto scaling group)
- Two ASG can scale independently

## FIFO Queue

- First In First Out (ordering of messages in the queue)
- Messages are processed in order by consumer

# Amazon Kinesis

- Kinesis -> real-time big data streaming
- Managed service to collect, process and analyze real-time streaming data at any scale

# Amazon SNS

- one message to many receivers
- Buying Service
  - email notification
  - fraud service
  - shipping service
- Pub Sub pattenr
  - We publich in a topic
  - the services will listen to that topic
- Simple Notification Services
- The **event publishers** only sends messages to one SNS Topic
- As many **event subscribers** as we want will listen to the SNS topic notifications
- each subscriber to the topic **will get all the messages**
- Up to 12,500,000 subscriptions per topic, 100,000 topics limit
- SNS can publish to
  - SQS
  - Lambda
  - Kinesis Data Firehose
  - emails
  - SMS and mobile notifications
  - send data to http endpoints

# Amazon MQ

- SQS and SNS are cloud native servies: proprietary protocols from AWS
- Traditional applications running from on-premises may use open protocols such as: MQTT, AMQP, STOMP, Openwire, WSS
- Instead of rewriting the application, we can use Amazon MQ
- Managed message broker service for:
  - RabbitMQ
  - ActiveMQ
- Amazon MQ does not scale as much as SQS/ SNS
- runs on servers, you can use Multi-AZ with failover
- has queue feature and topic features

# Summary

- SQS: queue service in AWS, multiple producers, messages are kept up to 14 days, decouple applications, multiple consumers share the read and delete messages when done
- SNS: notification service in AWS, subscribers: Email, lambda, SQS, HTTP, Mobile, multiple subscribers, send all messages to all of them, no message retention
- Kinesis: real-time data streaming persistence and analysis
- Amazon MQ: managed message broker for ActiveMQ and RabbitMQ in the cloud
