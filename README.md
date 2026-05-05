<div align="center">
  <h1>Lookitry | Architecture & Engineering Showcase</h1>
  <h3>High-Concurrency B2B SaaS Platform</h3>
  
  <p>
    <i>A technical overview demonstrating the architecture, infrastructure, and engineering challenges resolved during the development of <a href="https://lookitry.com">Lookitry.com</a>. Proprietary source code and core algorithms remain strictly confidential.</i>
  </p>
</div>

<br/>

## Executive Summary

Lookitry is a scalable B2B SaaS platform providing an AI-driven virtual fitting room for retail e-commerce. The system is currently deployed and trusted by over 500 retail stores across Latin America, processing thousands of concurrent generation requests daily.

The engineering focus of this project revolves around multi-tenant data isolation, high-availability AI pipelines, and frictionless integration via a zero-impact embeddable widget.

---

## Technical Architecture

The platform architecture is designed to manage heavy asynchronous workloads while maintaining sub-second response times for the host applications.

### 1. Frontend & Client Integration
* **Core Application:** Built on Next.js (App Router) and React 18, ensuring optimal Server-Side Rendering (SSR) and SEO performance for the main platform.
* **Embeddable Widget:** A framework-agnostic, vanilla JavaScript script injected into client storefronts. 
* **Performance Optimization:** Utilizes the Shadow DOM to guarantee strict CSS isolation, preventing style leakage into the host site. Assets are deferred to maintain a zero-impact footprint on the host's Core Web Vitals (Lighthouse).

### 2. Backend & Infrastructure
* **Infrastructure:** Deployed on highly optimized Virtual Private Servers (VPS) tuned for compute-intensive AI operations.
* **Database Architecture:** PostgreSQL implemented with a strict multi-tenant schema. This isolates data, usage quotas, and analytics per retail store while allowing aggregated reporting for administrative oversight.
* **API Gateway:** Node.js / Next.js API Routes expose RESTful endpoints consumed by the client widgets and third-party plugins.

### 3. AI Processing Pipeline
* **Processing Engine:** Custom image processing pipeline integrating Google Cloud Vertex AI infrastructure.
* **Queue Management:** Implemented a robust asynchronous message queuing system to handle traffic spikes, manage API rate limits, and prevent timeout failures during high-demand periods.
* **Data Security:** Strict adherence to data privacy protocols. Ephemeral storage is utilized for user-uploaded images, which are processed in memory and immediately purged upon task completion.

---

## Key Engineering Challenges Solved

### 1. Multi-Tenant Scalability
Designing a centralized system capable of handling 500+ independent stores required a robust authentication and routing mechanism. Each tenant operates under unique API scopes and strict quota limits, enforced at the API Gateway level to prevent noisy-neighbor issues.

### 2. Seamless E-commerce Integration
To reduce onboarding friction, a native WooCommerce Plugin was developed. This integration automates catalog synchronization and dynamically injects the fitting room widget into the Product Detail Pages (PDP) without requiring technical intervention from the store owner.

### 3. Tier-Based Subscription Lifecycle
Engineered an automated billing and provisioning lifecycle integrated with localized payment gateways (Wompi, PSE, Nequi). The system handles downgrades, upgrades, and automated teardown of services based on real-time webhook events.

---

## Technology Stack

<div align="center">
  <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js" />
  <img src="https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Node.js-43853D?style=flat-square&logo=node.js&logoColor=white" alt="Node.js" />
  <img src="https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL" />
  <img src="https://img.shields.io/badge/Vertex_AI-4285F4?style=flat-square&logo=google-cloud&logoColor=white" alt="Vertex AI" />
  <img src="https://img.shields.io/badge/VPS-673AB7?style=flat-square&logo=hostinger&logoColor=white" alt="VPS" />
</div>

<br/>

---
*Maintained by [Sam Wilkie](https://sam.wilkiedevs.com) - Full Stack Developer & System Architect.*