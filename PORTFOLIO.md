# Portfolio — David Sugianto

## 1. Predictive Capacity Planning System

**Context:** Tokopedia's peak campaigns (e.g., Harbolnas, Ramadan sale) required infrastructure provisioning weeks in advance. Teams relied on manual, assumption-based estimates — often over-provisioning (wasted cost) or under-provisioning (outage risk).

**Solution:** Designed a forecasting pipeline using Facebook Prophet that ingests business GMV targets, models historical QPS traffic patterns, and outputs per-service machine CPU spec recommendations. The system accounts for seasonality, growth trends, and campaign multipliers to produce infrastructure plans aligned with actual demand.

**Stack:** Go, Python, Prophet, ClickHouse, RocketMQ, ByteCloud APIs

**Impact:**

- Eliminated guesswork in capacity planning — all provisioning backed by data-driven forecasts
- Enabled cost-optimized scaling: right-sized infrastructure for each campaign window
- Zero capacity-related outages during peak campaigns post-adoption

---

## 2. Unified Service Metadata Platform

**Context:** Tokopedia's service topology was scattered across 10+ disconnected systems — CMDB, monitoring tools, deployment pipelines, and resource inventories each held partial views. No single source of truth existed for what services ran where, their dependencies, or their criticality.

**Solution:** Architected a centralized platform that ingests metadata from TCE, Redis, RDS, and other infrastructure systems in real time, normalizing and correlating records into a unified service graph. The platform tracks ownership, dependencies, SLO compliance, and multi-VDC placement for every service.

**Stack:** Go, ClickHouse, Redis, PostgreSQL, RocketMQ, ByteCloud APIs

**Impact:**

- Consolidated 10+ fragmented systems into one authoritative source
- Achieved 99% high-availability coverage and 100% multi-VDC resilience for P0/P1 services
- Enabled proactive risk assessment — teams could see blast radius and dependency chains before changes

---

## 3. SDLC Analytics Platform

**Context:** Engineering leadership lacked visibility into the software delivery lifecycle across business lines. Metrics like lead time, deployment frequency, and change failure rate were compiled manually in spreadsheets — slow, error-prone, and often stale by the time they reached decision-makers.

**Solution:** Built an analytics platform that instruments CI/CD pipelines, version control, and incident management tools to compute DORA metrics and quality indicators in near real-time. Dashboards surface trends by team, service, and business line, with drill-down into specific bottlenecks.

**Stack:** Go, PostgreSQL, ClickHouse, RocketMQ, ByteCloud APIs

**Impact:**

- Eliminated manual reporting — metrics available live instead of weekly spreadsheets
- Leadership gained real-time quality insights, accelerating data-driven decisions
- Bottleneck visibility drove targeted process improvements across teams

---

## 4. Cloud Migration Automation & Observability

**Context:** Tokopedia's migration to ByteCloud involved hundreds of online applications. Manual validation of migration readiness, infrastructure health checks, and cutover monitoring would have required an unsustainable amount of SRE toil.

**Solution:** Engineered automation tooling that validates pre-migration prerequisites (resource mappings, network policies, security groups), orchestrates staged cutovers, and provides real-time dashboards tracking migration progress, service health, and rollback readiness.

**Stack:** Go, PostgreSQL, BigQuery, NewRelic, Prometheus, GCP APIs, AWS APIs, ByteCloud APIs

**Impact:**

- Reduced manual migration effort by 90%
- Real-time visibility into infrastructure health and cutover readiness
- Supported cross-functional teams through validation and post-migration monitoring

---

## 5. Ephemeral Port Monitoring

**Context:** During Tokopedia's cloud migration to ByteCloud, some services experienced intermittent failures calling other services. Root cause analysis traced the issue to ephemeral port exhaustion on proxy servers — when all available ephemeral ports were consumed, new outbound connections failed, causing cascading service disruptions.

**Solution:** Initiated and led an ad-hoc project to build an Ephemeral Port Exporter that scrapes Linux kernel port usage metrics (`/proc/net/tcp`, `/proc/net/udp`) and exposes them as Prometheus metrics. Collaborated with the team to design dashboards in Grafana that track port utilization trends, connection states, and saturation thresholds, giving early warning before exhaustion occurs.

**Stack:** Go, Prometheus, Grafana, Linux kernel (/proc/net), ByteCloud

**Impact:**
- Proactive detection of port exhaustion before it caused service disruptions
- Eliminated repeated outages linked to ephemeral port depletion on transit proxies
- Improved overall system reliability during cloud migration with proper monitoring coverage

---

## 6. Cloud Cost Platform (FinOps)

**Context:** Tokopedia's multi-cloud (GCP, AWS, Alibaba Cloud) footprint made cost attribution difficult. Engineering teams had no visibility into their own infrastructure spend, and finance relied on monthly cloud provider invoices with minimal granularity.

**Solution:** Built a cost intelligence platform that ingests billing data from GCP and other providers into BigQuery, enriches it with organizational metadata (team, service, environment), and surfaces it through Looker Studio dashboards. Teams can drill into their spend by service, region, and resource type. Budget alerts and anomaly detection flag unexpected cost spikes.

**Stack:** Go, Redis, BigQuery, Apache Superset, Google Looker Studio, GCP APIs, AWS APIs, Alibaba Cloud APIs

**Impact:**

- Unified cost reporting across cloud providers
- Enabled team-level budgeting and resource planning
- Anomaly detection caught cost spikes before they became billing surprises

---

## 7. Distributed Cloud Infrastructure Event Platform

**Context:** Cloud infrastructure changes (instance provisioning, disk snapshots, network ACL updates) happened across multiple providers and regions, with no unified audit trail or automation trigger mechanism.

**Solution:** Designed an event-driven platform using GCP Pub/Sub and Go microservices that captures infrastructure lifecycle events from cloud provider APIs and webhooks, normalizes them into a common schema, and fans out to downstream automation workflows (compliance checks, cost tagging, inventory updates).

**Stack:** Go, GCP Pub/Sub, BigQuery

**Impact:**

- Full audit trail of infrastructure changes across cloud providers
- Enabled automated compliance and tagging workflows triggered by real-time events
- Foundation for future self-healing and auto-remediation automation

---

## 8. Containerized Infrastructure & CI/CD (Halalnode)

**Context:** Halalnode's deployments were manual — SSH into servers, pull code, restart services. No pipeline, no containerization, no repeatability.

**Solution:** Containerized all applications with Docker behind Nginx reverse proxies. Built GitLab CI/CD pipelines that run tests, build images, and deploy to staging/production. Automated server provisioning with Ansible, reducing setup time from hours to minutes.

**Stack:** Docker, Nginx, GitLab CI, Ansible, Prometheus, Grafana, PostgreSQL, MySQL, DigitalOcean Cloud

**Impact:**

- Deployment reliability: every release followed the same tested pipeline
- Reduced manual effort by 90% through Ansible automation
- Monitoring stack (Prometheus/Grafana)
