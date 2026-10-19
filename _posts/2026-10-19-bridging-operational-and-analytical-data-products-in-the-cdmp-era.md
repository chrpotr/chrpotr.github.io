---
layout: post
title: "Bridging Operational and Analytical: Data Products in the CDMP Era"
excerpt: "How Confluent's Shift Left Approach Enables Data Products for Converged Data Management Platforms"
---

*How Confluent's Shift Left Approach Enables Data Products for Converged Data Management Platforms*

> I wrote this paper at Confluent in mid-2025 for industry analysts, and Confluent subject-matter experts reviewed it at the time. This edited edition holds only public information; product details are as of July 2025.<br>
> This paper is not a Confluent or IBM publication.

[PDF version](/assets/bridging-operational-and-analytical-data-products-in-the-cdmp-era.pdf)

## Executive Summary

Chief Data Officers face pressure to democratize data while maintaining governance standards. As enterprises shift from point solutions to converged data management platforms (CDMPs), they seek **integrated technology environments where multiple vendors' tools work together seamlessly**. Confluent serves as the real-time data nervous system within these **interconnected technology stacks**, adding value to existing data management investments without replacing them.

Confluent serves as the nervous system connecting all CDMP components through streaming data, providing:

- **Stream Governance** - The industry's only fully managed governance suite for data in motion, with Schema Registry, Stream Catalog, and Stream Lineage providing near real-time visibility into data flows

- **Universal Data Products** - Data assets that bridge operational and analytical systems, enabling the same event to drive real-time fraud detection (sub-second) AND update data warehouses (minutes)

- **120+ pre-built connectors** - Including 80+ fully-managed connectors that connect legacy systems, cloud services, and modern applications without custom coding

- **Proven scale** - Managing 30k+ clusters processing 3+ trillion messages daily across 4,800+ customers with 99.99% uptime SLA

Confluent's Data Streaming Platform (DSP) enables business domains to create, manage, and share their own data products **within their unified CDMP**, serving multiple use cases and teams across the enterprise. Frequently data product strategies fail because they firstly only address a small set of batch oriented analytical consumers, and secondly because domain teams cannot create data products in practice because they lack self-service infrastructure for building, managing, and governing data pipelines across operational and analytical systems. Confluent solves this through self-service infrastructure, strong governance in the operational layer, powerful stream processing made easy, and native integration with 50+ analytical destinations spanning lakehouse platforms, real-time analytics databases, time series systems, and traditional data warehouses[^1].

## The Promise and Peril of Data Democratization

Chief Data Officers face an impossible tension: business teams need data within hours to launch campaigns and make product decisions, but central data teams processing thousands of requests from every domain create multi-week backlogs that grind innovation to a halt. This mismatch costs dearly because analysts waste their time searching for data, executives make decisions on outdated information, and companies with slow data access underperform their competitors. The traditional centralized approach, where a small team tries to serve all domains' data needs, has become the very bottleneck preventing data-driven innovation.

The pressure to deliver quickly collides with governance needs. Without controls, teams create duplicate data sets (e.g., different customer datasets across marketing, sales, and support). Each bespoke version contains different calculations for revenue, churn, and lifetime value.

Compliance compounds the problem. Financial transactions must meet PCI DSS requirements, including immutable audit trails. Healthcare systems must be HIPAA-compliant and track Protected Health Information (PHI) through every transformation. To meet GDPR’s requirement for granular consent, many European operations have to implement row-level or attribute-level consent controls. Implementing these compliance measures in post-processing rather than during construction can lead to rework, delays, and disruptions.

### Causes of Failure

**Most domain teams weren’t created with data engineering and infrastructure expertise in mind**. For instance, a full stack developer building an app probably understands SQL but cannot configure Kafka clusters and build stream processors to curate data products in real-time.

**Governance operates reactively**. When data validation only happens after data lands in warehouses or lakes, downstream systems have already consumed malformed records. Machine learning models trained on this flawed historical data learn incorrect patterns, producing unreliable predictions. Dashboards display incorrect metrics. By the time quality issues are discovered, the damage cascades through every system that touched the data.

**Operational and analytical systems are disconnected**. The same payment transaction must block for fraud scoring (sub-100ms latency), update personalized offers (1-2 second tolerance), and flow into Snowflake for analytics (5-minute micro-batches). Each system demands different data formats, delivery guarantees, and processing semantics forcing teams to build custom integrations for every connection.

**Organizations cannot implement balanced governance**. Centralized platforms require approval for every schema change, blocking many deployments daily. Federated approaches allow teams to define incompatible date formats, duplicate customer identifiers, and conflicting business logic. The solution to localized divergence is selective centralization: enforce encryption for PII, standardize customer identifiers, mandate schema registration—while allowing domains to define product categories, calculate local metrics, and manage release schedules.

## Confluent Enables Data Products Across Operational and Analytical Systems

Confluent abstracts distributed systems complexity through three layers that enable domain teams to create, govern, and share data products independently.

1/**Confluent accelerates and simplifies data product creation**[^2]. 120+ pre-built connectors that help domain teams to instantly connect data sources without writing generic integration code. Domain teams can use Change Data Capture (CDC) to automatically stream updates from operational databases, employing patterns like the outbox table to isolate internal data models from external data product schemas. For complex data products spanning multiple sources, Confluent's fully managed Apache Flink service lets teams join, enrich, and curate data using SQL while removing the operational complexity and burden of running distributed processing infrastructure. For example, teams can join data from PostgreSQL, MongoDB, and existing event streams using simple Flink SQL statements to create enriched data products from three separate sources.

2/**[Stream Governance](https://www.confluent.io/product/stream-governance/) enforces [data contracts](https://docs.confluent.io/cloud/current/sr/fundamentals/data-contracts.html) between producers and consumers**[^3]. Domains define data contracts through UI or API, specifying field names, types, defaults, and validation rules. The registry maintains all schema versions with compatibility checks that prevent breaking changes. When producers attempt to write messages, schema validation occurs at the client level during serialization. If the data doesn’t adhere to the schema, the Kafka client throws an exception and prevents the non-conforming data from being sent to the broker. This shifts data quality enforcement from consumers to producers, eliminating bad data at the source.

**3/[Data Portal](https://docs.confluent.io/cloud/current/stream-governance/data-portal.html) provides data product management without exposing Kafka internals**. Teams publish data products by defining business metadata, ownership, and access policies[^4]. The [Stream Catalog](https://docs.confluent.io/cloud/current/stream-governance/stream-catalog.html) indexes all data products with searchable tags for domain, data classification, and business purpose. Discovery happens through keyword search, metadata filters, or browsing domain hierarchies. Access requests route directly to data owners, enabling self-service.

### Automated Governance

[Stream Governance](https://docs.confluent.io/cloud/current/sr/fundamentals/index.html) implements federated control through three mechanisms operating at data production time:

**1/[Stream Quality](https://docs.confluent.io/cloud/current/stream-governance/index.html#cloud-stream-quality) enforces data integrity through Schema Registry and Data Quality Rules**[^5]. Beyond basic type validation, rules enforce field-level constraints: customer IDs must match regex patterns, amounts must fall within ranges, timestamps must use UTC. Schema Linking replicates schemas across regions and clouds, maintaining consistency in global deployments.

**2/**[**Stream Catalog**](https://docs.confluent.io/cloud/current/stream-governance/stream-catalog.html) **enables self-service through automated metadata management**[^6]. When teams create data products, the catalog extracts schema information, samples data, and builds searchable indexes. Business metadata—data owner, SLA, refresh frequency, business purpose—augments technical metadata. GraphQL endpoints enable custom discovery interfaces. Data enrichment happens through stream processing, allowing teams to create derived products without new infrastructure.

**3/[Stream Lineage](https://docs.confluent.io/cloud/current/stream-governance/stream-lineage.html) tracks data flow through** **Confluent’s DSP**[^7]. The lineage graph captures producer-to-topic-to-consumer relationships automatically. Teams query lineage to understand dependencies before making changes. Impact analysis shows which downstream applications consume specific topics. When investigating data quality issues, teams trace data backward from problematic outputs to original sources. Historical lineage enables root-cause analysis of past incidents.

### Reusability Through Trust and Understanding

Data products are much more likely to achieve reuse when teams trust data quality and understand semantics without searching through documentation. Both streaming lineage and data contracts are two-way doors to build trust. Just as streaming lineage allows a producer to know who is consuming their product for better management, consumers are able to see what other consumers are using a data product. Data contracts serve the purpose of both enforcing data quality but also enabling consumers to fundamentally understand the data they are using.

**Metadata drives understanding**. Each data product includes machine-readable tags: domain ownership, data classification (PII, financial, operational), quality SLAs, and business definitions. Usage analytics show which teams consume each product, peak access times, and data volumes.

**Data contracts enable evolution**[^8]. Schema evolution follows compatibility rules: producers can add optional fields (backward compatible), consumers can ignore unknown fields (forward compatible), and major versions support parallel deployment. The registry manages version transitions: old consumers continue reading old versions while new consumers adopt new schemas. Automatic version bridging translates between schema versions in real-time. Breaking changes follow migration paths: create new version, dual-write period, consumer migration, deprecate old version.

### Business Impact

Confluent’s DSP transforms data from technical assets requiring specialized skills into business products any team can discover, understand, trust, and use. These technical capabilities directly impact business metrics like:

**1/Time-to-market drops**[^9]**.** Marketing teams launch campaigns using real-time customer data products without waiting for IT. Product teams A/B test features using transaction streams. Operations monitors supply chains through IoT data products.

**2/Data quality improves through shift-left enforcement.** Bad data never enters the system. Quality rules catch errors at creation. Downstream teams trust upstream data. Reconciliation efforts disappear.

**3/Governance scales without bottlenecks.** Each domain manages its data products. Central policies propagate automatically. End-to-end visibility and traceability helps meet compliance requirements. Audit trails capture every access.

**4/Innovation accelerates through composition.** Teams combine existing data products into new offerings. Derived products build on trusted foundations. Network effects multiply value as more domains participate.

## Real-World Success: Detailed Customer Journeys

### SumUp: From Centralized Bottleneck to Federated Innovation

SumUp's fintech platform processes payments for 4M merchants across 36 markets. The centralized data platform team had become a bottleneck as the volume of requests for reports, analytics tools, and data access grew steadily. Internal stakeholders who needed data had to go through the data platform team, which could only prioritize a handful of projects per quarter, meaning valuable use cases were often delayed repeatedly, impacting product launches and business decisions[^10].

SumUp adopted Confluent Cloud to enable domain teams to create and manage their own data products. The architecture shifts from centralized pipeline management to federated ownership where domains publish data directly to Kafka topics with enforced schemas. Over the last two years, Confluent Cloud has become integral to SumUp's data mesh implementation. The platform now enables more than 20 teams to manage their own data products independently. Teams can build and share data products without waiting for the data platform team. When teams need data access, they submit requests directly to data owners who publish to Confluent Cloud, allowing responsible teams to build reusable data products.

The platform uses Schema Registry for data contracts between producers and consumers. Each domain owns schemas for their data products. Confluent Cloud handles infrastructure scaling, partition management, and replication. The platform integrates seamlessly with SumUp's microservices architecture.

By implementing data mesh principles with Confluent Cloud, the data platform team removed the data management bottleneck. Teams now have self-service access to build and share data products. Three teams demonstrate the transformation:

- Global Bank tribe: This cross-functional team operates SumUp’s banking and merchant payment services. They use Confluent Cloud to update transaction records in real-time, enabling improved resilience for use cases processing massive daily data volumes—including 24/7 monitoring, fraud detection, and personalized merchant recommendations.

- CRM team: Moving from batch processing to real-time streaming, the CRM team now provides customer and product information to operational teams instantly, enabling a more seamless customer experience while sharing streaming data across the organization.

- Risk data and ML platform team: This team manages connections between near-real-time streaming aggregation processes and the SumUp feature store. They've standardized data pipelines feeding their machine learning models, allowing models to make decisions based on the latest data.

### BMW Group: Manufacturing Data Products at Global Scale

BMW operates 31 plants across 15 countries, with a global sales network spanning 140 countries. The company generates massive volumes of IoT data from sensors, machines, and production equipment, producing over one billion events daily across dozens of Kafka clusters supporting hundreds of applications. BMW transitioned from batch processing to real-time streaming with Confluent Cloud on Microsoft Azure. Initially using self-managed Apache Kafka on Red Hat OpenShift, BMW found the operational burden costly and challenging to maintain 24/7/365 reliability with limited internal Kafka expertise[^11].

The implementation connects industrial IoT protocols like OPC UA with SAP systems and cloud applications. Confluent serves as a central hub, enabling streaming ETL to continuously transform, filter, and enrich data. Confluent's Infinite Storage feature automatically tiers older data to cost-effective cloud object storage while maintaining access, enabling BMW to replay historical manufacturing data. This architecture eliminated manual provisioning and infrastructure management through Confluent's fully managed service. Teams across the organization now have ubiquitous access to real-time data, enabling operational applications that streamline factory production and support R&D innovation. The platform operates with zero downtime, providing the reliability required for business-critical use cases.

BMW continues to expand use cases weekly, with the vision of creating a fully integrated, transparent, and centralized approach to data exchange across their global operations.

### Financial Services: Trust Through Governance

Financial institutions implement federated governance to satisfy four concurrent requirements: weekly product launches require rapid data provisioning; regulatory mandates demand complete transaction lineage; fraud detection systems need sub-100ms response times; privacy regulations (GDPR, CCPA) require field-level encryption and consent tracking.

An example in the financial services space is EVO Banco. Their implementation shows federated governance in action[^13]. Pattern matches trigger automated responses through the same streaming infrastructure. Result: 99% reduction in fraud losses.

The architecture pattern repeats across financial services: domain teams own data product creation and quality; central teams define policies and models; the streaming platform enforces governance rules at data production time; consumers receive governed data products without knowing the underlying complexity. This separation enables both domain autonomy and enterprise compliance.

## Ecosystem Integration for Federated Governance

Rather than positioning against other platforms, Confluent focuses on creating partnerships where all parties benefit from joint customer success. This approach recognizes that customers seek integrated solutions, not isolated technologies. Confluent implements federated governance through three integration patterns:

**1/Streaming-to-Lakehouse Integration.** [Tableflow](https://docs.confluent.io/cloud/current/topics/tableflow/overview.html) converts data products flowing in Kafka topics into Apache Iceberg tables (generally available) and Delta Lake tables (currently in preview). The system integrates with AWS Glue Data Catalog and Apache Polaris (via Snowflake Open Catalog) today[^14]. This simplifies architecture, reduces latency, and enables analytical technologies like Trino, Presto, and Snowflake to access continuously updated data products. Currently available on AWS.

**2/Cloud Platform Integration.** Confluent offers 120+ pre-built [connectors](https://www.confluent.io/product/confluent-connectors/), including 80+ fully-managed connectors that require no infrastructure setup, enabling seamless integration with services across AWS, Azure, and GCP. On AWS, Confluent’s managed connectors provide bidirectional data flow for S3 and DynamoDB, Redshift and Lambda as sink destinations, Kinesis as a source, and CDC from RDS via Debezium MySQL, PostgreSQL, or SQL Server CDC Source connectors. In Azure, you can stream data in and out of Blob Storage, deliver data to Data Lake Storage Gen2, and push to Synapse Analytics, while consuming from Event Hubs and Cosmos DB or capturing CDC from Azure SQL Database with the SQL Server CDC connector. On GCP, Confluent supports BigQuery as a sink, Cloud Storage for both sourcing and sinking data, Pub/Sub as a source, CDC from Cloud SQL using Debezium MySQL/PostgreSQL connectors, and Bigtable as a sink.

Each connector is purpose-built: source connectors ingest real-time changes and automatically register schemas in Schema Registry, while sink connectors deliver validated data products to analytical targets such as Snowflake, BigQuery, or Redshift, preserving schema evolution and offering at-least-once delivery guarantees. Schema Registry serves as the central governance layer across these integrations, ensuring that data contracts (incl. schemas, quality rules, and metadata) remain consistent throughout your pipelines, though maintaining this consistency requires proper configuration rather than happening by default. This architecture helps organizations enforce unified governance policies such as field-level encryption, data masking, and role-based access control across multi-cloud deployments, with the understanding that achieving end-to-end governance still demands careful setup of Schema Registry, security policies, and access controls within each cloud environment.

**3/** **Open Format Standardization.** Confluent's Tableflow supports Apache Iceberg (GA) and Delta Lake (Open Preview), enabling integration from Kafka into a broad ecosystem of data platforms including Snowflake, BigQuery, Amazon Athena, Databricks, and many others. Through native catalog integrations with AWS Glue and Snowflake Open Catalog, changes to Kafka data streams automatically propagate to the corresponding Iceberg or Delta tables. Once configured, downstream analytics engines can query these tables directly through their native interfaces, eliminating the need for custom ETL pipelines or sink connectors.

This architecture enables domain ownership while data flows across platform boundaries with consistent governance. Key capabilities include:

- **Proactive Data Quality:** Data contracts with quality rules execute during producer serialization and consumer deserialization, ensuring downstream platforms receive pre-validated, compliant data. This client-side enforcement prevents bad data from entering the system at the source.

- **Managed Schema Evolution:** Backward-compatible schema changes (adding optional fields, widening types) automatically propagate to Iceberg tables without disrupting consumers. Breaking changes require manual intervention and coordinated migration strategies, as Tableflow suspends materialization when encountering non-conforming data.

- **Multi-Catalog Integration:** Stream Catalog provides discovery for Kafka topics and schemas, while Tableflow synchronizes metadata with external catalogs like AWS Glue and Polaris. Each catalog maintains its own query interface, with business metadata preserved across synchronization boundaries. Organizations can leverage existing catalog investments while adding streaming capabilities.

- **Secure Kafka-to-Kafka Sharing:** For cross-organizational data sharing, Confluent provides stream sharing (topic-level access controls), cluster linking (inter-cluster replication), and authenticated API access. These patterns require network configuration (VPC peering, PrivateLink) but enable controlled data distribution between Kafka environments.

This approach establishes Confluent as the real-time foundation for modern data stacks, bridging operational systems with analytical platforms.

## Conclusion: Enabling Data Products in the Converged Data Management Era

Confluent provides the real-time layer that unifies operational and analytical systems, enabling organizations to deliver on the promise of democratized, trusted, and immediately actionable data. Traditional approaches fail when domain teams need specialized infrastructure expertise to build data products, and when governance only catches problems after data lands in downstream systems. Confluent's Data Streaming Platform addresses these challenges in 3 ways: First, Stream Governance combines broker-level schema validation with configurable data quality rules, creating multiple checkpoints to prevent bad data from propagating through the system. Second, self-service interfaces like Data Portal enable business users to discover, understand, and request access to existing data products without navigating Kafka's operational complexity. Third, Tableflow bridges streaming and analytical worlds through continuous near real-time materialization, making the same data available for both millisecond fraud detection and minute-level warehouse analytics. Within converged data management platforms, Confluent serves as the real-time foundation where engineering teams transform raw operational data into trusted, reusable data products. A single transaction can simultaneously feed real-time fraud detection systems (with millisecond latency) and analytical warehouses (with minute-level batch processing), all while maintaining consistent governance. This shift from reactive data fixing to proactive data quality (when properly configured and implemented) makes domain-driven data products technically achievable rather than organizationally aspirational.

## Appendices

### Appendix A: What are “Universal Data Products”?

Data products in Confluent are NOT proprietary objects locked in a vendor platform. They are open, governed streams of data that any system can consume from real-time applications to data warehouses.

Unlike vendor-specific data products locked within proprietary platforms, Confluent enables **Universal Data Products** - streaming data assets that:

- **Serve multiple consumers simultaneously**: The same product feeds real-time applications AND analytical warehouses

- **Use open standards**: Based on Apache Kafka with portable schemas (Avro, JSON Schema, Protobuf)

- **Include built-in governance**: Schema evolution, data quality rules, and lineage travel with the data

- **Enable domain ownership**: Business teams can create and manage their own data products without central IT bottlenecks

For example, a 'customer-events' data product can simultaneously:

- Trigger real-time personalization (milliseconds)

- Update fraud detection models (seconds)

- Flow into Snowflake for analytics (minutes)

- Archive to S3 for compliance (hours)

This contrasts with traditional data products that are either trapped in proprietary systems (SAP, Salesforce) or exist only for batch analytics (data warehouse tables).

[^1]: Confluent's analytical integrations include lakehouse platforms (Databricks, Snowflake, BigQuery, Redshift), real-time OLAP engines (Apache Druid, ClickHouse, Apache Pinot), time series databases (InfluxDB, TimescaleDB), search platforms (Elasticsearch, Splunk), and traditional data warehouses (Teradata, Oracle, IBM Db2). This breadth ensures data products can serve any analytical workload from sub-second operational intelligence to complex historical analysis.

[^2]: [Data Products, Data Contracts, and Change Data Capture](https://www.confluent.io/blog/implementing-streaming-data-products/)

[^3]: [How to Keep Bad Data Out of Apache Kafka with Stream Quality](https://www.confluent.io/blog/streaming-data-quality-keep-bad-data-out-of-apache-kafka/)

[^4]: [Data Products, Data Contracts, and Change Data Capture](https://www.confluent.io/blog/implementing-streaming-data-products/)

[^5]: [How to Keep Bad Data Out of Apache Kafka with Stream Quality](https://www.confluent.io/blog/streaming-data-quality-keep-bad-data-out-of-apache-kafka/)

[^6]: [How to Find, Share, and Organize Your Data Streams with Stream Catalog \| Confluent](https://www.confluent.io/blog/share-find-understand-data-streams-stream-catalog/)

[^7]: [How to Visualize Your Apache Kafka Data the Easy Way with Stream Lineage \| Confluent](https://www.confluent.io/blog/visualize-apache-kafka-data-easily-with-stream-lineage/)

[^8]: [Schema Evolution and Compatibility for Schema Registry on Confluent Cloud](https://docs.confluent.io/cloud/current/sr/fundamentals/schema-evolution.html)

[^9]: [The Business Value of the DSP: Part 2 – A Framework for Measuring Impact](https://www.confluent.io/blog/business-value-of-data-streaming-platform-part-2/#:~:text=Before%20the%20DSP,to%20%2425M%20savings)

    [Conquer Your Data Mess With Universal Data Products (Confluent ebook)](https://www.confluent.io/resources/ebook/conquer-your-data-mess-with-universal-data-products/)

[^10]: [SumUp Scales for Success with a Data Mesh Built on Confluent Cloud](https://www.confluent.io/customers/sumup/)

[^11]: [How BMW Group Streams Data on Global Scale with Confluent](https://www.confluent.io/customers/bmw-group/)

[^13]: [How EVO Banco Is Reinventing Fraud Prevention with Data Streaming & Machine Learning (Confluent blog, 2023-04-26)](https://www.confluent.io/blog/fraud-prevention/)

[^14]: [Delta Lake & Unity Catalog Now Integrate With Tableflow](https://www.confluent.io/blog/tableflow-databricks-delta-lake-unity-catalog/)
