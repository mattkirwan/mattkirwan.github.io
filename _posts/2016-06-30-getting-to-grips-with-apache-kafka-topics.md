---
layout: post
title: "Getting to Grips with Apache Kafka Basics"
date: "2016-06-30 18:53:17"
categories: apache kafka,
---

Recently I've spent a big chunk of time wrapping my brain around Apache Kafka topics, partitions, messages and how it's all related to brokers.

I'm fully aware that grasping this fundamental concept is crucial to me expanding my knowledge of Kafka. At the very least I want this post to solidify and validate my thoughts but maybe it will also help someone clarify their musings on this baffling (at first) erm...topic.

Starting at the top.

A Cluster - is a group of 1 or more Brokers.
A Broker - is a single instance/process/server running Apache Kafka.
A Topic - is a 'category' or means of grouping multiple, related messages.
A Message - is a byte array which can store pretty much anything. A message can also optionally have a key assigned to it.

I'm going to use a simple but (almost) believeable scenario to run through the structure around kafka.

The topic is

Topics

 

Kafka topics are subjectively interesting because of two things:

1. When you cre











A kafka message 