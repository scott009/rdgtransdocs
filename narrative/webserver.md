# Web Server Architecture Narrative (Draft)

**Status:** Narrative (non-authoritative)

This document captures the *intent, direction, and conceptual framing* of the web server architecture discussed in-session. It is **not authoritative** and does not define final implementation details. Its purpose is to serve as *gist material* for a later formal manifest and specification.

---

## Purpose

The immediate goal is to configure a **second VPS** using a **Caddy-first web server architecture** that is simple, stable, and flexible enough to support both static and dynamic workloads over time.

The emphasis is on:
- Architectural clarity
- Minimal ongoing operational burden
- DNS-driven flexibility
- Clean separation of concerns

This system is intended to replace ad-hoc hosting solutions (such as GitHub Pages) and become the long-term home for several related projects.

---

## Core Architectural Principles

### 1. Caddy as the Front Door

- Caddy is always the entry point
- HTTPS is automatic and assumed
- The Caddy configuration should be *rarely edited* once established

Caddy is treated as stable infrastructure, not an application surface.

---

### 2. Subdomain-Based Routing

Routing is **subdomain-based**, not path-based.

Examples:
- `app1.catbench.com`
- `app2.catbench.com`
- `app3.catbench.com`

Each subdomain represents a conceptual application or role, not just a deployment unit.

---

### 3. DNS-Driven App Switching

- DNS determines which application is active
- Caddy routes are predeclared
- Application changes are handled by DNS updates, not frequent Caddyfile edits

The design target is to predefine ~10 routes and then largely leave the Caddy configuration alone.

---

### 4. Cross-Server Reverse Proxying

The system must support routing to services running on *other servers*.

Example:
- `ic.catbench.com` → Inquiry Circle running on a different VPS

This allows services to move or scale independently without changing public-facing URLs.

---

## Hosting Strategy Shift

### Moving Away from GitHub Pages

- GitHub Pages is no longer sufficient for the translation project
- The new VPS becomes the primary home for static HTML + CSS
- Static-first, dynamic-later is the guiding principle

The goal is ownership, flexibility, and architectural consistency.

---

## Conceptual Application Roles

### app1 — Static Content

- Public-facing HTML and CSS
- Translation outputs
- Documentation and reference material

This layer is intentionally simple and robust.

---

### app2 — Persistence Layer

- Database-backed service
- Receives form input from static pages
- Acts as a durable data store

This separates user input and state from presentation.

---

### app3 — Transformation Layer

- Likely implemented in Python (e.g., Flask)
- Consumes data from the persistence layer
- Generates new documents or derived artifacts

This opens the door to **dynamic documents** built from controlled data sources.

---

## Directional Insight

This architecture naturally evolves toward:

- Composable document generation
- Dynamic publishing without abandoning static guarantees
- Clear separation of:
  - Presentation
  - Persistence
  - Transformation

The emphasis is on *maintaining option space* rather than locking into premature complexity.

---

## Closing Note

This document is **narrative only**. It records intent, intuition, and architectural direction. It is expected to inform—but not constrain—the creation of a future authoritative manifest and specification.

