---
title: Elasticsearch for Java Developers hosted on Azure Overview
description: Integrating Elasticsearch Service on Microsoft Azure for Java developers.
author: Aaron Schifman (Elastic)
manager: Craig Griffin (Elastic)
ms.topic: Overview
ms.date: August 2020
---
# Elasticsearch Service for Java developers running on Microsoft Azure

This document presents an overview of Elasticsearch Service hosted on Microsoft Azure, focused on the Java developer audience.

Expect to understand what Elasticsearch is and why deploying it on Microsoft Azure is the quickest way of spinning up an Elasticsearch cluster, rather than deploying a self-managed environment. This should matter to a Java developer because Java developers are more interested in spending their time developing and enhancing their applications, rather than on infrastructure management.

If you are already familiar with deploying an Elasticsearch cluster, keep reading, you will certainly find it very useful. This overview identifies and articulates various benefits applicable for Java developers. At various times, details around the various out-of-the-box solutions are discussed, such as ingesting data and how powerful Kibana is, providing critical insight into the environment both during development and at run-time.

## Elastic’s products and features

Elasticsearch is a distributed, RESTful search and analytics engine providing Java developers running on Azure with rich features and services. Open source solutions optimized for your use cases, including industry-leading service, monitoring, and support from both Elastic and Azure. Get automatic backups, upgrades and the latest security patches with little downtime or disruptions.

Some of the core Elastic products include:

- [Elastic Stack](https://www.elastic.co/elastic-stack) - The core products: Elasticsearch, Kibana, Beats, and Logstash.
- [Elastic Enterprise Search](https://www.elastic.co/enterprise-search) - Search everything, anywhere.
- [Elastic Observability](https://www.elastic.co/observability) - Unified visibility across your entire ecosystem.
- [Elastic Security](https://www.elastic.co/security) - Unified protection for everyone (combined SEIM and Elastic Endpoint Security).
- [Machine learning](https://www.elastic.co/what-is/elasticsearch-machine-learning) - Find anomalies, forecast trends, and identify areas of interest.

Some of the more applicable features includes monitoring, alerting and reporting, log and metric collection by using [Elastic Beats](https://www.elastic.co/beats) - Elastic’s lightweight data shippers.

Beats sit on the edge and are the collectors for all good and bad things. Beats include:

- Audit data using [Auditbeat](https://www.elastic.co/products/beats/auditbeat)  
- Log files using [Filebeat](https://www.elastic.co/products/beats/filebeat)  
- Cloud data using [Functionbeat](https://www.elastic.co/products/beats/functionbeat)  
- Availability using [Heartbeat](https://www.elastic.co/products/beats/heartbeat)  
- Systemd journals using [Journalbeat](https://www.elastic.co/downloads/beats/journalbeat)  
- Metrics using [Metricbeat](https://www.elastic.co/products/beats/metricbeat)  
- Network traffic using [Packetbeat](https://www.elastic.co/products/beats/packetbeat)  
- Windows event logs using [Winlogbeat](https://www.elastic.co/products/beats/winlogbeat)  

Need a single, unified way to add monitoring for logs, metrics, and other types of data to each host? Look at ingest management using [Elastic Agent](https://www.elastic.co/guide/en/ingest-management/7.9/ingest-management-overview.html).

> [!div class="nextstepaction"]
> [Check out all of the Elastic features.](https://www.elastic.co/elasticsearch/features)

> [!TIP]
> Refer to the official Elastic [Hosted Elasticsearch on Microsoft Azure](https://www.elastic.co/azure) landing page for more details and be sure to check out all the [free training](https://www.elastic.co/training) opportunities!

## Create deployments in just minutes on Microsoft Azure

Getting started with Elasticsearch is no further than executing a few simple clicks from the [Azure Marketplace](https://azuremarketplace.microsoft.com). Just run a search for **Elasticsearch Service**, and within a few clicks you will be signed up with your [free Elasticsearch Service trial](https://www.elastic.co/azure). The Elasticsearch Service Azure Marketplace listing contains a great deal of useful **Key Features**, offering a great starting point for those wishing to plunge into Elasticsearch.

## Choosing the right deployment type

Deployment templates are what Elastic Cloud managed services provides you, to get up and running on the Elastic Cloud quickly. To get started, there is no need to determine how many nodes are needed, nor how much memory or storage each instance should have.

Every deployment template includes a set of components called **instances** which are appropriately sized based on the type of workload selected. These instances include Elasticsearch data, ingest, as well as Kibana for every deployment, but there are additional instances one can include at the time of deployment, or later, such as a machine learning (ML) node, dedicated monitoring nodes, an Application Performance Monitoring (APM) server, or when ingesting data from an expansive environment, a coordinating node. Instance configurations map to [Azure instance types](https://www.elastic.co/guide/en/cloud/current/ec-reference-hardware.html#ec_azure).

At Elastic, we understand there is never a one-size-fits all deployment type, and that is why we provide various templates which have customization options, if you should choose. Elasticsearch Service on Microsoft Azure provides stability, consistent performance, and greater flexibility, ensuring you always have whatever resources you need, where and when you need them.

For most general search use cases, the **I/O Template** is recommended, however, for more specific uses cases, there are other templates which may be more suitable. For example, **hot-warm** templates are typically used for logging use cases. [Hot-Warm Architecture](https://www.elastic.co/guide/en/cloud/current/ec-getting-started-templates-hot-warm.html) configures different tiers of data nodes, with hot data nodes optimized for indexing and high search throughput and warm data nodes optimized for cost effective storage. Index Lifecycle Management Policies ensure that the numerous logs that no longer need to be frequently queried get moved to the **warm data nodes**.

> [!div class="nextstepaction"]
> [Read more about deployment templates.](https://www.elastic.co/guide/en/cloud/current/ec-getting-started-templates.html)

## Visualize in Kibana

[Kibana](https://www.elastic.co/kibana) is your window into the Elastic Stack, where building and exploring dashboards gives you the ability, and freedom, to bring insights into the hands who need them. Remember the age old saying, “a picture says a thousand words?” Kibana is that same picture, “worth a thousand log lines.”

Getting started looking at real world data is as simple as clicking **Try our sample data**, which not only loads the sample data, but also sample dashboards and more. This option is great to get familiar with Kibana and its features, immediately seeing and controlling the power of Kibana - using and customizing the amazing dashboards containing histograms, graphs, pie charts, maps and more!

> [!div class="nextstepaction"]
> [Check out this wonderful Getting Started with Kibana video!](https://www.elastic.co/webinars/getting-started-kibana)

## Ingesting your data into Elasticsearch

What types of data matters most to you? Performance metrics for the application, JVM, container, or cloud platform monitoring? Do you need to analyze thousands of lines of log files from many different kinds of sources, all in one location to find out why an app is running slow, or worst, not running at all, or perhaps just monitoring the ecosystem health and user access?

You can find answers to these questions and more in Kibana where prepackaged content like dashboards, data transformation pipeline, etc, and let you go from data to insight in literally minutes.

![Kibana Web Traffic Dashboard](media/es-for-java-developers-overview/kibana-overview.png)

### Ingest manager

Elastic version 7.9 has made it easy to collect logs, metrics, endpoint security data and other types of data with a unified agent that gets installed on your edge machines. Elastic’s consolidated ingest management approach uses the [Elastic Agent](https://www.elastic.co/blog/introducing-elastic-agent-and-ingest-manager) and offers centralized configuration management with [Fleet mode](https://www.elastic.co/guide/en/ingest-management/current/ingest-management-getting-started.html#agent-fleet-mode), where defining and managing the configuration happens within Kibana using the convenient Configuration Editor.

[![Elastic Agent](media/es-for-java-developers-overview/elastic-agent.png)](https://www.elastic.co/guide/en/ingest-management/current/ingest-management-getting-started.html).

You can still take a more traditional approach with Elastic Agent by configuring YAML files on the systems running it using [standalone mode](https://www.elastic.co/guide/en/ingest-management/current/ingest-management-getting-started.html#agent-standalone-mode).

> [!IMPORTANT]
> Make sure and first read the [limitations with Ingest Manager](https://www.elastic.co/guide/en/ingest-management/current/ingest-management-limitations.html).  

### Filebeat

Throughout your environment, we can assume there are thousands of threads in logs, spread across many different applications, servers, and locations with different format types and even possibly languages that a person in your position must analyze. It is not practical, nor scalable, to try and analyze them by logging onto each system and to parse through those 10s of thousands of lines of text. Rather, there is a much more efficient method to analyze such large amounts of log file data, provided at no additional cost. One in particular is [Filebeat](https://www.elastic.co/beats/filebeat), Elastic’s lightweight data shippers for logs.

![Logs Analysis ](media/es-for-java-developers-overview/log-analysis.png)

Filebeat is one of the many open platform [Beats](https://www.elastic.co/beats) Elastic offers out-of-the-box, ready to help ingesting logs and are [container](https://www.elastic.co/docker-kubernetes-container-monitoring) and cloud-ready. Beats are designed by Elastic to understand your applications, sending relevant data directly into Elasticsearch in a pattern that is understood.

Configuring Filebeat begins within Kibana, where clear instructions are depicted. The setup depends on your system, but essentially consists of downloading, configuring the **filebeat.yml** file, which consists of setting what to collect, and where they need to go, and then running the setup commands. The process generally takes under five minutes.

Additionally, you may want to enable modules relevant to your environment, such as if you are running Nginx or MySQL. There is also a **Systems Logs module**, which you can enable upon installing Filebeat. Check out all the out-of-the-box types of [Elastic Integrations](https://www.elastic.co/integrations). Many come with predefined dashboards and visualizations, getting you up and running even faster!

For more detailed instructions, please visit the [Getting Started with Filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation-configuration.html) reference guide.

> [!NOTE]
> Filebeat guarantees at-least-once delivery and from then on keeps track of the last lines sent by utilizing [harvesters](https://www.elastic.co/guide/en/beats/filebeat/current/how-filebeat-works.html#harvester). There is a *registry* that rebuilds the state should Filebeat get restarted. If that registry gets corrupted or deleted, then all the logs will need to be re-sent to Elasticsearch.

#### Enabling additional Filebeat modules

Don’t stop there! Install the [Azure Filebeat module](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-module-azure.html) which collects the following types of logging activities using [Azure Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about). Predefined dashboards come packaged in this Filebeat module, like many others.

> [!div class="checklist"]
> * Azure activity - Azure Resource Manager resources providing insight into the operations performed on your subscription resources.
> * Active Directory sign-in logs - reports on application usage and sign-in activities.
> * Active Directory audit logs -  providing tracing statistics on changes made within AD such as changing permissions on resources, or adding or removing users, apps, etc.

> [!TIP]
> Read more about [Azure exported fields](https://www.elastic.co/guide/en/beats/filebeat/current/exported-fields-azure.html).
> Check out all the [out-of the-box modules](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-modules.html). Most come with visualizations and predefined dashboards.

> [!div class="nextstepaction"]
> [Launch a Logging Quick Start Course for free!](https://www.elastic.co/training/logging-quick-start)

### Metricbeat

Metricbeat tailgates Filebeat in our Elasticsearch journey, using Kibana for gaining a holistic point of view of the entire ecosystem. The [Metricbeat System module](https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-module-system.html) sends into Elasticsearch: `cpu`, `memory`, `load`, `network` and `processes`, all ready to be visualized in Kibana with predefined dashboards. Metrics can sit alongside log data providing visibility across your entire ecosystem known as [Elastic Observability](https://www.elastic.co/observability).  

The [Metricbeat Azure module](https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-module-azure.html) offers features that aggregates logs and metrics from any, or all, Azure accounts/subscriptions. Usage details, forecasting information, all in predefined dashboards.  

Using Azure Active Directory authentication, users are able to collect metrics from virtual machines, storage, container instances, registries and services, database account details, billing, and application insights including collecting APM data from applications in Azure.

> [!TIP]
> Don’t forget that the Azure module, as with all other Beats, customizations are just an idea away.

> [!div class="nextstepaction"]
> [Launch a Metrics Quick Start course for free!](https://www.elastic.co/training/metrics-quick-start)

## Elastic Observability

Elastic Observability is not just for the development perspective, nor just for helping with break-fix scenarios. Elastic Observability drives intelligent operational decisions based on gaining an insight as to whom may have been impacted, how they may have reacted, how much money may have been lost, and more. Utilizing machine learning, an optionally enabled service offered through the Platinum [Elastic Cloud managed service pricing plan](https://www.elastic.co/pricing), detecting anomalies can also help prevent unforeseen circumstances in a more proactive manner.

The APM Server ingests data from agents, the open source libraries that sit on your application host which instrument the code and collect performance data and errors at run-time. The APM Java Agent can help Java developers by capturing data to help determine the root cause for perhaps a web transaction timing out because a server has run out of cache, a result of seeing anomalies in the heap usage.

This is possible because Kibana brings together the relevant logs and metrics, into one centralized location. The various APM agents capture [instrumented application events](https://www.elastic.co/guide/en/apm/get-started/current/apm-data-model.html) such as spans, transactions, errors and metrics.

The [Elastic Observability](https://www.elastic.co/observability) solution includes:

> [!div class="checklist"]
> * [Elastic APM](https://www.elastic.co/apm) - Open source application performance monitoring
> * [Elastic Logs](https://www.elastic.co/log-monitoring) - Open source log monitoring
> * [Elastic Metrics](https://www.elastic.co/infrastructure-monitoring) - Open source infrastructure monitoring
> * [Elastic Uptime](https://www.elastic.co/uptime-monitoring) - Open source uptime monitoring

> [!div class="nextstepaction"]
> [Read more about Elastic’s APM system.](https://www.elastic.co/guide/en/apm/get-started/current/overview.html)

## Viewing in Kibana

### Dashboards

Kibana dashboards drive insights into the data you need. There are many relevant out-of-the-box dashboards, made from predefined visualizations, which can be customized for whatever use case you desire, whether it be for root cause analysis to building a compelling business decision.

Logs and metrics from applications, systems, containers, cloud resources, and more, are all brought together under one roof. From Syslog analysis, determining what Sudo commands and what SSH logins have been attempted by whom, to understanding why an application is hanging at a certain point, the answers are just a few clicks away within the same interface.

### Kibana Lens

[Kibana Lens](https://www.elastic.co/what-is/kibana-lens) is all about **shaping** your data with an intuitive UI. Lens is a feature of Kibana that allows you to build rich visualizations by using a simple drag-n-drop method. Lens is also very intelligent in that it understands the data you are trying to work with and offers suggestive input, greatly increasing your productivity and efficiency.

There are many different kinds of visualizations that you can create, such as area, bar and line graphs, data tables, heat maps, pie charts and more!

![Kibana Lens](media/es-for-java-developers-overview/kibana-lens.png)

> [!div class="nextstepaction"]
> [Get started with Lens!](https://www.elastic.co/guide/en/kibana/current/lens.html)

### Discover

Discover offers users the ability to create relevant visualizations representing the message data, which alone in its raw format cannot easily be interpreted.

Before using Discover an [index pattern](https://www.elastic.co/guide/en/kibana/current/index-patterns.html) must be created. Fortunately for us, Filebeat provides a basic index pattern we can build off of, so we are not having to start from scratch, but the process is very straightforward. [Our user guides provide more info on creating index patterns](https://www.elastic.co/guide/en/kibana/current/index-patterns.html).

Take advantage of the [sample data set](https://www.elastic.co/guide/en/kibana/current/getting-started.html#get-data-in) that comes with predefined index patterns, visualizations and dashboards. They are a wonderful way to get started with Elasticsearch without worrying about other types of configurations.

![Adding sample data](media/es-for-java-developers-overview/add-sample-data.png)

Within Discover you can see an ingest of data. Use the [time filter](https://www.elastic.co/guide/en/kibana/current/set-time-filter.html) to expand or narrow the time range and notice the various fields one can filter. Those fields one can filter on have to do with index patters, which can be fully customized based on the type of data being ingested.

### Logs

Developers are very interested in data log analysis, during the development process as well as during run-time. Stream logs live and execute query terms resulting in highly relevant results. Use the [Kibana Query Language](https://www.elastic.co/guide/en/kibana/current/kuery-query.html) or plain text English, and filter by every different type of index available.  

Filebeat provides a default index pattern, a definition table Elasticsearch uses within Kibana for the data as it is ingested and indexed to be searched by field types. Modules are used not only to collect, but to interpret that ingested data. If there are no modules for the types of logs you are ingesting, and you want to manipulate the data before ingesting with Elasticsearch, you can use an [ingest node](https://www.elastic.co/guide/en/beats/filebeat/current/configuring-ingest-node.html) to parse the data.

![Streaming Logs in Kibana](media/es-for-java-developers-overview/logs-logline-details.png)

## Next Steps

> [!div class="nextstepaction"]
> [Take advantage of Free Fundamentals training](https://www.elastic.co/training/free#quick-starts)
