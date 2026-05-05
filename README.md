<div align="center">
  <h1>Lookitry | Architecture & Engineering Showcase</h1>
  <h3>High-Concurrency B2B SaaS Platform</h3>
  
  <p>
    <i>A technical overview demonstrating the architecture, infrastructure, and engineering challenges resolved during the development of <a href="https://lookitry.com">Lookitry.com</a>. Proprietary source code and core algorithms remain strictly confidential.</i>
  </p>
</div>

<br/>

## Executive Summary

Lookitry is a scalable B2B SaaS platform providing an AI-driven virtual fitting room for retail e-commerce. The system allows end-users to upload a selfie and visualize clothing items on themselves.

The engineering focus of this project revolves around multi-tenant data isolation, self-hosted storage infrastructure, complex AI workflow orchestration, and frictionless integration via a zero-impact embeddable widget.

---

## Technical Architecture

The platform architecture enforces a strict separation of concerns, ensuring that the frontend never interacts directly with AI models or database secrets.

### 1. Frontend & Client Integration
* **Core Application:** Built on Next.js 14 (App Router) and React 18 using TypeScript. Styled with Tailwind CSS under a custom Premium/Dark design system.
* **Embeddable Integration:** Delivered to clients via a lightweight, vanilla JavaScript script (`/widget.js`) injected into storefronts, or through dynamic customizable mini-landing pages. 
* **Performance:** Assets are deferred and isolated to maintain a zero-impact footprint on the host's Core Web Vitals.

### 2. Backend API & Infrastructure
* **API Gateway:** A robust Node.js / Express backend written in TypeScript. It acts as a secure proxy that orchestrates payments, handles custom JWT authentication, and dispatches AI jobs.
* **Rate Limiting & Security:** Cloudflare Turnstile integrated natively to prevent spam and abuse.
* **Database:** Supabase (PostgreSQL) utilizing Service Role keys at the backend level for secure, bypassed RLS data management.
* **Storage Infrastructure:** Self-hosted **MinIO** storage clusters, handling ephemeral storage of user images and generation outputs.

### 3. AI Processing & Workflow Orchestration
* **Workflow Engine:** **n8n** is deployed as the central orchestrator, managing complex logic for image generation, inpainting, and MinIO insertion.
* **AI Inference:** Integrated with **OpenRouter** and custom GPU workers (`idm-vton-api`) handling the heavy lifting of Virtual Try-On generation.
* **Asynchronous Communication:** n8n communicates back to the Node.js backend via secure webhooks once asynchronous image processing is completed.

### 4. Billing & Subscriptions
* **Dual Gateway System:** Integrated with **Wompi** for local currency processing (COP) and **PayPal** for international processing (USD).
* **Automated Logic:** Includes dynamic currency conversion based on configurable exchange rates (TRM) and automated prorated billing for subscription upgrades.

---

## Key Engineering Challenges Solved

### 1. Secure AI Orchestration
To prevent frontend exploitation of expensive AI generation endpoints, all requests are securely marshaled through the Express backend, validated via custom JWT, and offloaded to n8n. This decoupling ensures the AI models and the core database are completely air-gapped from public access.

### 2. Self-Hosted High-Volume Storage
Instead of relying on costly managed storage for millions of temporary generations, a self-hosted MinIO cluster was implemented. This drastically reduced cloud storage costs while maintaining S3-compatible APIs for seamless backend integration.

### 3. Conflict-Free E-commerce Embedding
The client-facing widget was engineered to avoid CSS/JS collisions with the infinite variety of themes and frameworks used by client stores.

---

## Technology Stack

<div align="center">
  <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js" />
  <img src="https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white" alt="Express" />
  <img src="https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Node.js-43853D?style=flat-square&logo=node.js&logoColor=white" alt="Node.js" />
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=flat-square&logo=supabase&logoColor=white" alt="Supabase" />
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=flat-square&logo=n8n&logoColor=white" alt="n8n" />
  <img src="https://img.shields.io/badge/MinIO-C7202C?style=flat-square&logo=minio&logoColor=white" alt="MinIO" />
</div>

<br/>

---
*Maintained by [Sam Wilkie](https://sam.wilkiedevs.com) - Full Stack Developer & System Architect.*