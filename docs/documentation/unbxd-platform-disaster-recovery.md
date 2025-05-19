---
title: Unbxd Platform & Disaster Recovery
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Unbxd AI-powered hosted search solution is supported by a highly performant infrastructure that scales to handle a wide range of traffic. Our architecture is designed for offering enterprise-grade security and reliability to avoid service disruptions. We maintain redundancy at multiple levels across the technology stack to eliminate the risk of downtimes due to a single point of failure.

## Global Coverage & Content Delivery

Unbxd products are deployed using a distributed architecture with clusters available on all major continents. The performance of our products is further accelerated by Cloudflare’s content delivery network coverage which also comes with advanced security measures including DDoS protection. The response time is a critical factor influencing shopper’s experience on your website and we are committed to offering the best performance in addition to highly relevant search results.

Unbxd infrastructure is hosted on Amazon Web Services (AWS) in the following regions :

1. United States (US)
2. United Kingdom (UK)
3. Singapore (SG)
4. Australia and New Zealand (ANZ)

<Image align="center" border={true} caption="AWS Regions" src="https://files.readme.io/b0a4b31e8e3faa77460521a1386b1f2a0ad504b32eec69a03331c87734b9bee0-image.png" width="80% " />

## Scalability

We understand that the traffic on your website varies with time so the infrastructure supporting the product discovery should be elastic enough to accommodate a surge in demand. We have built many options in our services to offer scalability

Spare capacity maintained during normal operations: Our services are configured with extra capacity to accommodate any sudden surge in traffic.

* **Auto-scaling Microservices**: Our cloud infrastructure scales automatically in accordance with the resource requirements to offer a stable performance irrespective of the traffic volume. The autoscaling is achieved by using Kubernetes for all micro-services that enables horizontal scaling of services depending upon the demand.
* **Caching**: Unbxd maintains an extensive cache capable of serving requests. During peak loads, the cache is used to serve some requests in order to reduce the load on downstream services and allow the autoscaling of services.
* **Monitoring & Proactive actions**: In addition to these, our platform stability team has built an extensive monitoring capability to measure system performance and take proactive action.

## Redundancy & Data backup

Our architecture is designed to provide enterprise-grade reliability and eliminate single points of failure.

* **Redundancy maintained across multiple availability zones**: Within a cluster ( AWS region) all the micro-services are distributed across multiple AWS availability zones to avoid service disruption due to ones happening in a single availability zone (physical data center location).
* **Automated recovery**: All microservices in our system are designed to automatically recover from unexpected failures with the help of a monitoring system that identifies & isolates the unresponsive nodes/servers. Services are maintained at low utilization levels under normal operations to reduce the impact on performance & availability when the load is re-distributed.
* **Multiple index replicas**: We also ensure redundancy at the index level by maintaining multiple replicas of the search index along with some failover index replicas which are utilized when the primary index is unavailable.
* **Data backup**: Data uploaded on our platform (including catalog data, merchandising rules) is stored in data centers distributed across multiple regions to achieve redundancy.

<Image align="center" border={true} caption="Search Request Flow" src="https://files.readme.io/faa0863845289698915716f56a389ec96a2c69f88ef13c1b138441fc6b869fbd-image.png" width="80% " />

The figure above is a simplified representation of the **feed/catalog upload** and \*\*search request \*\*lifecycle.

**Feed Upload Request**:\
You can upload your entire product catalog in one go (full feed) or only update the changed records (delta feed). All feed uploads require authentication via a secret key. Our feed indexing process runs independently from the request system to ensure uninterrupted service during updates.

**Search/Category Request**:\
When a shopper submits a search or category request, our advanced technology processes the query to understand the shopper's intent, applies relevant business rules, and expands the query. The system then retrieves and ranks products from the index to optimize the shopping experience and increase conversions.

<br />

## Disaster Recovery

Our architecture is robust and resilient by design and can handle a wide range of traffic and catalog sizes. However, there are certain factors which are outside our control that can impact the availability of services. Downtimes, especially during the peak sale times, can be costly for your business as it may lead to loss of potential revenue. For instance, Costco lost $11 Mn in sales due to downtime in 2019, effectively losing \~$11,000 in revenue every minute due to the incident.

The disaster recovery solution offers a mechanism to resume operations in an alternate data center (present in a different geographical location) if the primary data center becomes unavailable. The disaster recovery solution offers a quick failover mechanism to fallback to a secondary data center if the primary data center becomes unavailable.

### How does the DR solution offer higher availability?

The DR solution mitigates the risk of a wide-scale outage due to the unavailability of CDN service providers or cloud infrastructure providers (data center). The DR solution has the following systems in place to mitigate these risks:

* **Option to bypass CDN**: The DR solution offers an option to directly communicate with Unbxd clusters by bypassing the CDN.
* **Circuit break & Caching layer**: Circuit breaker detects unavailability of downstream services and routes the request to the failover cluster or allows our system to use cached data to provide a response to incoming requests. Unbxd maintains 2 layers of cache to minimize disruption of services while traffic is routed to the failover cluster.
* **Failover to DR cluster:** All data from the primary cluster is replicated to a secondary cluster at regular intervals. The secondary cluster acts as a standby cluster capable of handling live traffic when the primary cluster is unavailable.

### Salient Features of the DR solution

* **Quickly scale-up the DR cluster**: DR solution is built using the Spotinst platform to scale up services within minutes. A few stateless services will be autoscaled to maintain latency & SLA.
* **Fully managed by Unbxd**: Unbxd manages the data replication and failover to the DR solution. The traffic will be automatically switched to the failover/DR cluster when the primary cluster is unavailable. No intervention needed from the customers’ end.
* **New Endpoints**: The DR solution offers new endpoints for bypassing Cloudflare or directly hitting the DR cluster. These endpoints can be used by customers for testing the DR offering or routing production traffic to the DR solution.

### SLA

* **Recovery point objective (RPO)** : The RPO for DR solution is 2 hours. RPO represents the maximum time to backup.
* **Recovery time objective (RTO)**: The RTP for DR solution is automated by Unbxd.

### Instructions & DR Endpoint

The replication lag in the DR cluster can be up to 2 hours which means the feed data & merchandising rules may not be the most recent data. Hence, the DR end-point must only be used when the primary end-point is not available.

<Image align="center" border={true} caption="End Points" src="https://files.readme.io/02656973cc6f6611e5785480f15475bf603a2e50f7d3d5f11fa225371650b9ae-image.png" width="80% " />

Automated DR Routing Unbxd systems are designed to automatically detect failures in the primary search cluster and route the requests to the DR cluster. A circuit breaker is placed in the request flow to detect failures in the primary search cluster and automatically routes the request to a failover mechanism that servers the request from cache (if available) or DR cluster.

> 📘 Note
>
> Unbxd products (including the DR endpoint) will continue to use Cloudflare’s DNS service for domain name resolution. However, the DR end-point will not use Cloudflare’s proxy service which has been the factor behind most of the Cloudflare related outages experienced by us.