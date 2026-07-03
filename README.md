<p align="center">
  <img src="https://lookitry.com/logo.svg" alt="Lookitry Logo" height="80"/>
</p>

# Lookitry | Architecture & Engineering Showcase

### AI-Powered B2B SaaS — Virtual Try-On for Fashion E-Commerce

[![AWS Activate](https://img.shields.io/badge/AWS-Activate-FF9900?style=flat-square&logo=amazon-web-services&logoColor=white)](https://aws.amazon.com/activate/)
[![Google Cloud for Startups](https://img.shields.io/badge/Google_Cloud-Startups-4285F4?style=flat-square&logo=google-cloud&logoColor=white)](https://cloud.google.com/startup)
[![Built with Kiro](https://img.shields.io/badge/Built_with-Kiro_IDE-blue?style=flat-square)](https://kiro.dev)
[![Spec-Driven Development](https://img.shields.io/badge/Methodology-SDD-purple?style=flat-square)](https://kiro.dev/docs/)

A technical overview demonstrating the architecture, infrastructure, and engineering challenges resolved during the development of [Lookitry.com](https://lookitry.com/). Proprietary source code and core algorithms remain strictly confidential.

---

## Executive Summary

Lookitry is a scalable B2B SaaS platform providing an AI-driven virtual fitting room for retail e-commerce in Latin America. End-users upload a selfie and instantly visualize how clothing items look on them — directly from the brand's store.

The engineering focus revolves around:
- Multi-tenant data isolation with per-brand analytics
- Self-hosted high-volume storage infrastructure
- Asynchronous AI pipeline orchestration with sub-15s latency
- Frictionless integration via a zero-impact embeddable widget
- Automated billing with dual-currency support (COP/USD)

**Selected by AWS Activate and Google Cloud for Startups** for infrastructure and innovation standards.

---

## Development Methodology

This project was built entirely using **Spec-Driven Development (SDD)** in [Kiro IDE](https://kiro.dev):

1. **Requirements** — Acceptance criteria defined in Given/When/Then format before any code
2. **Design** — Architecture decisions documented with rationale
3. **Tasks** — Numbered implementation checklists grouped by phase
4. **Implementation** — Agent-assisted coding with full spec context
5. **Verification** — Automated checks against spec scenarios

This methodology reduced feature development time by approximately 50% compared to traditional approaches and ensured architectural consistency across the platform.

---

## Technical Architecture

The platform enforces strict separation of concerns. The frontend never interacts directly with AI models or database secrets.

```
┌──────────────────────────────────────────────────────────┐
│                     CLIENT LAYER                          │
│  Next.js 14 App Router · TypeScript · Tailwind CSS       │
│  Embeddable Widget (vanilla JS) · Mini-Landings          │
└─────────────────────────┬────────────────────────────────┘
                          │ REST API (Dual JWT Auth)
┌─────────────────────────▼────────────────────────────────┐
│                     API LAYER                             │
│  Express · Node.js · Redis Cache · Rate Limiting         │
│  Cloudflare Turnstile · JWT Rotation                     │
└────┬──────────┬──────────┬──────────┬────────────────────┘
     │          │          │          │
     ▼          ▼          ▼          ▼
 Database    Storage    AI Pipeline  Payments
 (Postgres)  (S3-compat) (Async)    (Dual Gateway)
```

### 1. Frontend & Client Integration

- **Core Application**: Next.js 14 (App Router), React 18, TypeScript. Custom Premium/Dark design system with Tailwind CSS.
- **Embeddable Integration**: Lightweight vanilla JS widget (`/widget.js`) for storefronts + dynamic customizable mini-landing pages for social media traffic.
- **Performance**: Zero-impact footprint on host's Core Web Vitals. Assets deferred and CSS isolated.

### 2. Backend API & Infrastructure

- **API Gateway**: Express/TypeScript backend acting as secure proxy — orchestrates payments, manages auth, dispatches AI jobs.
- **Security**: Dual JWT (access + refresh in HTTP-only cookies), distributed rate limiting, Cloudflare Turnstile anti-spam.
- **Database**: Supabase (PostgreSQL) with Service Role keys for secure RLS-bypassed operations.
- **Storage**: Self-hosted S3-compatible clusters for high-volume ephemeral image storage.

### 3. AI Processing

- **Architecture**: Fully asynchronous pipeline decoupled from the main API. AI models are air-gapped from public access.
- **Latency**: Sub-15 second generation time from upload to result.
- **Reliability**: Queue-based with automatic retry, graceful degradation on provider outages.
- **Details**: Proprietary — model selection, segmentation approach, and orchestration logic are confidential.

### 4. Billing & Subscriptions

- **Dual Gateway**: Wompi (COP, Colombian market) + PayPal (USD, international).
- **Automation**: Dynamic currency conversion (TRM-based), prorated billing for plan upgrades, automated subscription lifecycle management.

---

## Key Engineering Challenges Solved

### 1. Secure AI Orchestration

All AI requests are marshaled through the backend, validated via JWT, and dispatched asynchronously. This decoupling ensures AI models and the database are completely air-gapped from public access — preventing frontend exploitation of expensive generation endpoints.

### 2. Cost-Optimized High-Volume Storage

Self-hosted S3-compatible storage instead of managed cloud services. This handles millions of temporary generations at a fraction of the cost while maintaining standard APIs for seamless integration.

### 3. Conflict-Free E-commerce Embedding

The widget is engineered to avoid CSS/JS collisions with the infinite variety of themes and frameworks on client storefronts — working on Shopify, WooCommerce, Wix, and custom builds without configuration.

### 4. Multi-Tenant Isolation

Each brand operates in a fully isolated data environment with per-tenant analytics, credit management, and configuration. No data leakage between brands at any layer.

---

## Technology Stack

![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-43853D?style=flat-square&logo=node.js&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat-square&logo=supabase&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

---

## Programs & Recognition

<p align="center">
  <img src="https://sam.wilkiedevs.com/assets/Activate-Logo_color-white-e1601561941855.png" alt="AWS Activate" height="40"/>
  &nbsp;&nbsp;&nbsp;&nbsp;
  <img src="https://sam.wilkiedevs.com/assets/Logo_for_Google_for_Startups_page.png" alt="Google Cloud for Startups" height="40"/>
</p>

- **AWS Activate** — Startup Founders tier
- **Google Cloud for Startups** — Cloud credits program

---

## Links

- 🌐 **Product**: [lookitry.com](https://lookitry.com)
- 👤 **Author**: [Sam Wilkie](https://sam.wilkiedevs.com/) — Full Stack Developer & System Architect
- 🛠️ **Built with**: [Kiro IDE](https://kiro.dev) using Spec-Driven Development

---

*Proprietary source code and AI algorithms remain strictly confidential. This showcase is for portfolio and technical discussion purposes only.*
