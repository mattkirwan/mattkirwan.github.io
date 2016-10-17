---
layout: post
title: "Apache Kafka - An Introduction"
date: "2016-10-17 22:00:00"
categories: apache kafka
---
It's a common occurrence in our industry to have heard of a technology, glean a vague idea of "what it is" but never have the opportunity to actually explore the technology any further.

This introductory article has been specifically designed for anyone with zero knowledge of Apache Kafka to get up-to-speed quickly with the fundamentals. 

So, whether preparing yourself to delve further into this technology or you are just trying to keep up with the Jones' in preparation for your next conference you should finish reading this article feeling confident, somewhat more knowledgeable and hopefully inspired to explore Apache Kafka further.

# So What Is Apache Kafka?

It's a streaming/messaging platform.

# Ok, that's great. But, _what_ is it?

Think of Apache Kafka as a mashup of a transaction log and publish/subscribe platform.

1. You _produce_ a **message** onto kafka.
2. That **message** is appended onto a **topic**.
3. You then _consume_ that **message**.

![Right now Apache Kafka is a black box to us](/assets/2016-10-17/apache_kafka_black_box.png)

# Well, that was easy. Is that it?

Of course not. Like most technology today kafka takes a brilliantly simple concept and masks its true power through layers of abstraction.

I want to explore each layer throughout this series, but for now lets stick with the fundamentals.

# What can I use Apache Kafka for?

Kafka has an amazingly wide remit of applications of use, I like to phrase it like this:

>If you want to move and transform large volumes of data in real-time between disparate systems then Apache Kafka might just be what you need.

The official website provides some good [use cases kafka](https://kafka.apache.org/uses).

## High Level Concepts

# Kafka Brokers

The heart of the Apache Kafka ecosystem. A kafka broker runs as a single instance on a machine. Running multiple brokers across multiple machines creates a Kafka cluster.

To give you some idea of throughput, a single Kafka broker is capable of reading and writing hundreds of megabytes of data per second.

![An Apache Kafka cluster containing multiple brokers](/assets/2016-10-17/apache_kafka_cluster_and_brokers.png)

# Apache Zookeeper

Zookeeper is a centralised service for coordinating distributed systems. Kafka is designed as a distributed system and for this reason it intentionally offloads the common problems associated with coordinating these distributed systems.

It has a hard depenency on Zookeeper. This is a great thing. It allows Kafka to what it's good at without re-inventing the wheel and trying to solve problems it shouldn't be concerned with.

Kafka hands off several things to Zookeeper for management and coordination - namely broker, partition and topic management.

# Messages

It wouldn't be much of an introduction to Kafka if we didn't discuss messages. 

Messages are the blood cells moving through our circulatory system, without the we have nothing and our shiny new Kafka cluster will sit there without a byte to process.

At this high level we should just think of messages made up of three main components:

* A header
* A Key (optional) [byte array]
* A Value [byte array]

These messages are published onto a topic of our choosing.

All messages that are published to the cluster persist regardless of if they are consumed or not until the retention period for the server expires. For example, if the message retention period is set to 7 days any number of consumers can read and re-read those messages and any number of producers can publish more and more messages, only after the 7 days are up will the messages start dropping from the cluster.

# Topics

A kafka topic is how we categorise or group messages.

Upon creation of a topic we must decide its **name**, the number of **partitions** it should have and its **replication** factor.

When we produce a message it must be **published to a topic and partition**. That message will then be appended to that partition within that topic.

At its most basic level, if we were to produce a message onto a topic with a single partition that message would simply be placed onto the end of the topic.

![Kafka topic with a single partition](/assets/2016-10-17/apache_kafka_topic_partition_simple.png)

Some crucial points to note:

* Messages within a partition are **immutable**.
* Messages within a partition are **ordered**.
* Messages within a partition get an identifier known as the **offset**

Topics, partitions and replication factors are incredibly important concepts within Apache Kafka and each subject would require far too much detail for this introductory article.

# Producers

A Kafka producer is a straight forward concept. We have some data that we would like to persist in a Kafka cluster, we simply take that data and publish that message to any given partition within a Kafka topic.

We can choose to produce messages onto topics in a round-robin fashion for simple load-balancing or publish to a specific partition based on an arbritary hashing function.

# Consumers

Responsible for consuming messages from a given topic, Kafka consumers send a fetch request to a topic containing the offset from which they would like to consume and the message at that offset is sent to the consumer.

When creating a consumer you must define a **consumer group** to which the consumer belongs. The Kafka cluster uses this label to balance the message delivery to the consumers.

A message published to a topic will be delivered to _one_ consumer within each _consumer group_.

Breaking it down to a really simple (and unrealistic) example below, we can see that messages from a single partition can only be sent to a single instance (**consumer 1**) from a single consumer group (**mygroup**). Consumer 2 will never receive any messages from the topic **anintrotokafka** while there is only one partition and consumer 1 is up and running:

![Multiple consumers with the same consumer group and a single partition](/assets/2016-10-17/apache_kafka_consumer_group_simple.png)

# A Summary & tldr Video

Having covered at a very high level some of the core concepts of Apache Kafka hopefully some of which have clarified some questions or even piqued your interest for further exploration.

I've created the following video to hopefully act as an anchor and a much easier way to digest the learnings from this article in a more visual format.

<iframe width="560" height="315" src="https://www.youtube.com/embed/CyZP8hvHbM8" frameborder="0" allowfullscreen></iframe>





