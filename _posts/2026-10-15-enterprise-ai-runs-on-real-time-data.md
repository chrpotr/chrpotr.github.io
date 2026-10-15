---
layout: post
title: "Enterprise AI Runs on Real-Time Data"
excerpt: "I wrote this paper at Confluent in mid-2025 for industry analysts, and Confluent subject-matter experts reviewed it at the time."
---

> I wrote this paper at Confluent in mid-2025 for industry analysts, and Confluent subject-matter experts reviewed it at the time. This edited edition holds only public information; product details are as of July 2025.<br>
> This paper is not a Confluent or IBM publication.

[PDF version](/assets/enterprise-ai-runs-on-real-time-data.pdf)

## Executive Summary

AI workloads require continuous data fitness validation, which converged data management platforms (CDMPs) must support through ongoing contextual validation. This represents a shift from one-time data preparation to ongoing contextual validation. Confluent helps address the gap between data availability and AI readiness; a universal challenge that becomes even more complex for organizations pursuing platform convergence.

## The AI-Ready Data Challenge

The challenge intensifies with generative AI (GenAI). Without fresh, contextual data, AI models suffer from hallucinations, outdated insights, and poor decision making; problems that batch processing fundamentally cannot solve.

The rigid boundaries between transactional systems and analytical platforms create data silos that prevent AI from accessing the complete picture. This operational-analytical divide forces organizations into complex and brittle integration patterns that increase latency and reduce data freshness. While organizations invest heavily in AI infrastructure, many don't realize that batch data processing fundamentally limits AI effectiveness. Many sophisticated enterprises don't automatically connect the need for streaming, real-time data with their AI initiatives. However, according to Confluent's 2024 Data Streaming Report[^1], 90% of IT leaders say data streaming platforms lead to greater innovation in AI and ML development[^2]. Data can be unlocked from a source system and made available continuously in real-time in a decoupled fashion that means anyone who has proper permissions can discover and use it with no additional impact to the source system. As Mercedes-Benz R&D North America shared, time to market to use their real-time data product went from 4-6 months to 4-6 weeks while enabling them to implement real-time inferencing.[^3] Even if customers claim they don’t need “real-time”, AI-ready data needs to be complete and delivered continuously from sources.

## How Real-Time Data Streaming Enables AI-Ready Data

### Real-Time Data Contextualization

Confluent’s stream processing capabilities enable data sets to be analyzed, merged, joined, transformed, and filtered as it flows continuously from sources in real-time. This means that data can be curated specifically for the AI use case and continuously examined to detect drift. Advanced implementations will leverage data streaming to help implement continuous training (CT) methods by using the same data streams being inferenced in production to also feed incremental training or by sending it to a lake so that more regular batch retraining can be triggered by data/concept drift. Data streaming is well suited for this because additional consumers have very little to no impact. Outliers can be detected but passed through for model training if desired for representativeness.

When Optimove implemented their real-time customer 360 solution, they used Confluent to align disparate customer interactions (web, purchase history, support tickets) into a unified stream that helped ML models receive representative, contextually complete customer data.[^4] Their VP of Product said that this event-driven architecture enables “real-time self-optimizing journeys, which use AI to maximize uplift by identifying the optimal campaign for each individual customer.”

Mercedes R&D uses stream processing to transform heterogeneous vehicle telemetry from 180 billion events a day into semantically consistent data products with lineage tracking.[^5]

While Confluent doesn’t enforce statistical representativeness or detect bias directly, our streaming-first approach provides advantages batch processing cannot: unfiltered access to every event as it occurs, an intrinsic log of state changes, and the ability to discover and act more rapidly. Organizations must still validate that their data meets specific AI technique requirements but with streaming they’re working from a complete foundation rather than a sampled subset.

### Continuous Validation in Motion

Real-time qualification happens through Stream Governance that uses data contracts to validate data correctness and completeness. Stream Processing can then be used to compute confidence levels, transform, and enrich data to meet requirements before it reaches AI models. Stream Governance not only validates source data but can also be applied to model outputs before they flow to downstream systems.

### Unified Lineage Across Ecosystems

Confluent's Stream Governance enables the continuous governance practices needed for AI-ready data. **Stream Lineage** provides transparency for data flows and transformations[^7]; **Stream Quality** enforces data contracts[^8], and validation rules on streaming data; **Stream Catalog** and **Data Portal**[^9] enable data sharing and discovery of trusted data products across teams; **Schema Registry** stores data contracts along with their field level controls, versioning, and metadata tagging. Confluent provides client-side field level encryption (CSFLE) that supports encryption of PII and other fields. These controls (along with RBAC and audit logs) help customers stay in compliance with GDPR and the EU AI Act[^10].

## What Does Real-Time Data Do for the Business?

Most enterprises process data for AI in batches. This creates fundamental gaps between data availability and AI-readiness that limit model effectiveness. The following table demonstrates how streaming complements rather than replaces batch investments across common AI challenges. For each challenge, we show 1/where batch processing provides baseline capability, 2/how streaming enhances that capability, and 3/the quantifiable business impact from real customer implementations.

### Feature Staleness

**How Batch Processing Addresses It:** Computes features nightly/hourly/minutes, stores in feature stores for model training and inference

**How Confluent Enhances the Solution:** Alleviates pressure on operational systems by continuously computing features as events occur, streaming fresh features to both training and serving

**Business Impact of Real-Time Enhancement:**

- Improvement in model accuracy for time-sensitive predictions
- Captures behavioral patterns invisible in hourly aggregations
- Enables real-time personalization use cases
- Reduces AI pressure on business critical operational systems

### Temporal Model Training & Agent Testing

**How Batch Processing Addresses It:** Captures periodic snapshots requiring complex modeling to infer state changes between snapshots

**How Confluent Enhances the Solution:** Maintains immutable log of all state changes and current state enabling models to train on transitions; replayability for agent testing

**Business Impact of Real-Time Enhancement:**

- Faster agent deployments
- Decreased data prep costs (no temporal reconstruction required)
- Models can also learn from state transitions not interpolated changes

### Representative Data Capture

**How Batch Processing Addresses It:** Collects comprehensive datasets including errors and outliers for periodic model retraining

**How Confluent Enhances the Solution:** Streams every event including anomalies and edge cases as they occur, preserving temporal relationships

**Business Impact of Real-Time Enhancement:**

- Models trained on complete event sequences, not sampling
- Better fraud detection by capturing attack pattern evolution
- Reduced blind spots in model coverage

### Data Drift Detection

**How Batch Processing Addresses It:** Runs daily/weekly validation jobs comparing current data distributions to training baselines

**How Confluent Enhances the Solution:** Continuously monitors data distributions, detecting drift within minutes

**Business Impact of Real-Time Enhancement:**

- Prevents model degradation before business impact
- Reduced false positive rates
- Proactive model retraining triggers

### Governance and Lineage

**How Batch Processing Addresses It:** Tracks data lineage through ETL jobs, applies governance policies post-ingestion

**How Confluent Enhances the Solution:** Enforces governance policies in-flight immediately adjacent to source operational system, captures lineage as data flows all the way through consumers

**Business Impact of Real-Time Enhancement:**

- Real-time compliance for regulated industries
- Instant traceability for AI decision auditing
- Prevents policy violations before data lands

### Model Feedback Loops

**How Batch Processing Addresses It:** Batches prediction results and outcomes for periodic model evaluation and retraining

**How Confluent Enhances the Solution:** Streams predictions and outcomes back to training systems immediately

**Business Impact of Real-Time Enhancement:**

- Faster response to emerging threats

### Context for RAG/GenAI

**How Batch Processing Addresses It:** Periodically updates vector stores and knowledge bases with batch embeddings

**How Confluent Enhances the Solution:** Continuously streams fresh context to RAG applications (incl. real-time embeddings, event streams, transaction updates, and enriched metadata) to ensure GenAI apps operate on current info.

**Business Impact of Real-Time Enhancement:**

- Improvement in GenAI response relevance

### Cross-System Synchronization

**How Batch Processing Addresses It:** Coordinates batch jobs across systems, dealing with timing and consistency issues

**How Confluent Enhances the Solution:** Maintains continuous consistency through event-driven architecture

**Business Impact of Real-Time Enhancement:**

- Reduces operational complexity
- Enables real-time data sharing between AI agents, supporting coordination, context sharing, and collaborative decision-making

## Customer Evidence

### Notion: AI-powered Collaboration at Scale

Notion used data streaming to overcome scaling limitations, optimize costs, and unlock new product capabilities. They used Confluent to stream real-time data for AI powered search and content generation (RAG)[^11].

- real-time synchronization of workspace changes to vector database, ensuring AI tools always access the latest documents and content

- Continuous validation of data streams processing 100M users’ real-time messages.

### Agent Taskflow: Multi-agent Orchestration Platform

Agent Taskflow used Confluent to coordinate AI agents in real-time[^12].

- RAG implementation vectorizes events in Kafka topics and injects relevant memories into agent context windows ensuring data meets AI technique requirements

- Real-time observability with replayable agent executions and thought processes across operational planes

- **Business Impact**: Enabled healthcare client to sanitize medical transcripts in real-time without human handoffs

### Airy: Agentic AI Platform

Airy's use of Confluent for building enterprise AI copilots shows the cutting edge of AI-ready data[^13]:

- Enriches streaming data with context and metadata before ML processing

- Flink is used to filter out noise and cross reference LLM results with data sets for reducing hallucination risks.

- Data contracts provide structure and metadata to guide LLMs in generating data processing queries.

## The Ecosystem Advantage

Confluent accelerates the CDMP journey from platform to ecosystem. Our streaming infrastructure bridges this gap through 120+ pre-built connectors and native integrations with Databricks[^14], Snowflake[^15], and major cloud providers. Tableflow materializes Kafka topics to Apache Iceberg or Delta Lake tables in minutes, enabling organizations to choose best-in-class CDMP components without architectural lock-in.

Organizations can achieve lower TCO while gaining the flexibility to evolve their CDMP strategy. This matters because CDMPs *must* balance pre-integration benefits with openness; Confluent’s neutrality provides the real-time data foundation that makes this balance achievable, enabling continuous AI-readiness across heterogeneous systems without forcing architectural choices that limit future options.

## Conclusion

AI workloads require continuous access to fresh, validated data from across the enterprise. While batch processing provides the foundation for volume and governance, it cannot address the temporal challenges of AI-ready data.

Confluent’s DSP ensures context and data consistency across operational and analytical systems, eliminating the traditional divide that forces AI models to work with incomplete or outdated information. By maintaining an immutable log of all state changes and streaming validated data to both training and serving environments, organizations achieve the continuous AI-readiness that CDMPs promise but batch processing alone cannot deliver.

As organizations consolidate their data management tools, Confluent provides the real-time foundation that makes these unified platforms work, not by replacing existing investments, but by *connecting* them with governed, continuously validated data streams.

## Appendix: Frequently Asked Questions

**Q: How does Confluent fit within our existing lakehouse architecture?** A: Confluent complements rather than replaces lakehouse investments[^17]. Tableflow enables seamless streaming into Delta Lake or Iceberg formats, while maintaining compatibility with Unity Catalog for governance. Think of Confluent as the real-time data highway that feeds your lakehouse with fresh, pre-processed data[^18].

**Q: What about semantic layer capabilities for GenAI applications?** A: While Confluent focuses on technical schema management and real-time data flow, semantic business definitions typically reside in analytical platforms like Snowflake or Databricks. Confluent ensures data arrives with consistent schemas and can be enriched in-flight, enabling downstream semantic interpretation. This separation allows each platform to excel at what it does best.

**Q: Can we start small or do we need to transform everything at once?** A: Successful implementations start with focused, high-value use cases. Our recommended approach begins with a single critical pipeline—often fraud detection or personalization—to prove value quickly before expanding.

**Q: How does this help with the "shift-left" approach to data quality?** A: Confluent enables data quality checks, enrichment, and governance to happen at the point of creation rather than after data lands at destinations. This shift-left approach prevents bad data from propagating through your systems, reduces the cost of remediation, and reduces duplicative processing.[^19]

**Q: Can Confluent track lineage across systems?**

Confluent tracks lineage up to the boundaries of external systems. Stream Lineage visualizes data flow from source to destination within the Confluent Data Streaming Platform and shows connections to external systems through connectors. However, Confluent cannot track what happened to data before it entered the DSP or after it exits.

**Q: What cross system visibility does Stream Lineage provide?**

- which external systems received data from Confluent topics

- which external systems send data into Confluent topics

- the connectors that bridge Confluent with external systems

- metrics about data flow to/from external systems

**Q: What's the learning curve for our teams?** A: Teams familiar with SQL can be productive immediately using Flink SQL. The Confluent for VS Code extension provides familiar development experiences. Most organizations report developers achieving productivity within weeks, not months.

[^1]: [Confluent, 2024 Data Streaming Report (PDF)](https://assets.confluent.io/m/7c5e4f5fa3b9d6e2/original/20240531-DS-Data_Streaming_Report.pdf)

[^2]: [New Confluent Global Report Finds Data Streaming Accelerates AI Development and Cuts Costs (press release, 2024-06-05)](https://www.confluent.io/press-release/new-confluent-global-report-finds-data-streaming-accelerates-ai-development/)

[^3]: [Current 2024 Keynote Day 1 - Data Streaming in the Age of AI (Seema Acharya, Mercedes-Benz R&D North America, at 36:38)](https://youtu.be/Sn6fVsOzrSU?t=2198)

[^4]: [Optimove Builds Real-time Data Platform with Up-To-Date Customer Views using Confluent Cloud](https://www.confluent.io/customers/optimove/)

[^5]: [Current 2024 Keynote Day 1 - Data Streaming in the Age of AI (at 33:52)](https://youtu.be/Sn6fVsOzrSU?t=2032)

[^7]: [How to Visualize Your Apache Kafka Data the Easy Way with Stream Lineage \| Confluent](https://www.confluent.io/blog/visualize-apache-kafka-data-easily-with-stream-lineage/)

[^8]: [How to Keep Bad Data Out of Apache Kafka with Stream Quality](https://www.confluent.io/blog/streaming-data-quality-keep-bad-data-out-of-apache-kafka/)

[^9]: [Data Portal for Confluent Stream Governance](https://www.confluent.io/blog/data-portal-stream-governance/)

[^10]: [Enterprise-Grade Kafka Security & Compliance - Confluent](https://www.confluent.io/product/confluent-platform/enterprise-grade-security/)

[^11]: [How Notion Scales its AI and Lowers Operations Costs With Confluent](https://www.confluent.io/customers/notion/)

[^12]: [From Reactive to Orchestrated: Building Real-Time Multi-Agent AI With Confluent](https://www.confluent.io/blog/building-real-time-multi-agent-ai/)

[^13]: [Building AI Agents and Copilots with Confluent, Airy, and Apache Flink](https://www.confluent.io/blog/building-ai-agents-and-copilots/)

[^14]: [Shift Left Architecture for AI and Analytics with Confluent and Databricks - Kai Waehner](https://www.kai-waehner.de/blog/2025/05/09/shift-left-architecture-for-ai-and-analytics-with-confluent-and-databricks/)

[^15]: [Unlocking Real-Time Analytics With Confluent Tableflow, Apache Iceberg™, and Snowflake](https://www.confluent.io/blog/tableflow-ga-kafka-snowflake-iceberg/)

[^17]: [Technical Playbook for Optimizing Lakehouse & Warehouse Data Ingestion (Confluent white paper)](https://www.confluent.io/resources/white-paper/playbook-optimizing-ingestion-shift-left/)

[^18]: [Delta Lake & Unity Catalog Now Integrate With Tableflow](https://www.confluent.io/blog/tableflow-databricks-delta-lake-unity-catalog/)

[^19]: [Shift Left Processing & Governance \| Confluent](https://www.confluent.io/shift-left/processing-governance/)
