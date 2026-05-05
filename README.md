<div align="center">
  <h1>Lookitry - AI Virtual Fitting Room (Architecture Showcase)</h1>
  <h3>High-Performance B2B SaaS Architecture</h3>
  
  <p>
    <i>This is a public showcase repository demonstrating the architecture and technical challenges solved while building <a href="https://lookitry.com">Lookitry.com</a>. The core source code, proprietary algorithms, and business logic remain strictly private.</i>
  </p>
</div>

<br/>

## 📌 Overview

**Lookitry** is a scalable B2B SaaS platform that empowers retail stores with an AI-driven virtual fitting room. It allows end-users to visualize clothing items on themselves before purchasing, significantly reducing return rates and increasing conversion for e-commerce brands.

Currently trusted by **500+ retail stores** across Colombia and Latin America.

---

## 🏗️ Technical Architecture

The system is designed to handle high concurrency, processing thousands of AI image generations daily across hundreds of e-commerce tenants without latency bottlenecks.

### 1. Frontend Architecture
* **Framework:** Next.js (App Router) + React 18
* **Styling:** Tailwind CSS + custom UI components.
* **Embeddable Widgets:** A lightweight, vanilla JS script injected into client websites. Designed to have **zero impact** on the host site's Lighthouse performance score (using Shadow DOM and deferred loading).
* **State Management:** Optimized for fast rendering and asynchronous polling while the AI processes heavy requests.

### 2. Backend & Infrastructure
* **Environment:** Hosted on dedicated VPS infrastructure optimized for compute-heavy workloads.
* **Database:** PostgreSQL (structured for multi-tenancy, isolating data, quotas, and analytics per store).
* **API Layer:** Node.js / Next.js API Routes serving REST endpoints for client widgets and external plugins.
* **Automation & Webhooks:** Automated internal microservices orchestration, subscription management, and asynchronous task queues.

### 3. AI Processing Pipeline (Abstracted)
* **Core Engine:** Custom AI pipeline integrated with Google Cloud (Vertex AI) for robust, scalable image processing.
* **Queue System:** AI generation requests are handled via a robust queuing mechanism to prevent timeout failures and manage API rate limits efficiently under heavy load.
* **Security & Privacy:** Ephemeral storage processing ensuring user data (uploaded images) is securely handled, processed, and immediately purged according to strict privacy standards.

---

## 🚀 Technical Challenges Solved

### Multi-Tenant Scalability
Managing 500+ distinct e-commerce stores required a strict multi-tenant database design. Each store generates unique API keys and scopes, ensuring complete data isolation while allowing aggregated platform-wide analytics.

### Third-Party Integrations (WooCommerce)
Developed a native **WooCommerce Plugin** that allows stores to integrate the Virtual Fitting Room with a single click. The plugin syncs product catalogs asynchronously and injects the widget directly into the product detail pages (PDP).

### Zero-Friction Embebding
The client-facing widget was engineered to be ultra-lightweight and conflict-free. It uses Shadow DOM to completely isolate CSS, ensuring that the widget's styles never clash with the host website's theme, regardless of their tech stack.

### Tier-based Subscription Engine
Implemented secure, localized payment gateways handling tier-based subscriptions (Basic, Pro, Enterprise) with automated provisioning, usage quotas, and teardown of services.

---

## 🛠️ Tech Stack Summary

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
*Created by **[Sam Wilkie](https://sam.wilkiedevs.com)** - Full Stack Developer & System Architect.*