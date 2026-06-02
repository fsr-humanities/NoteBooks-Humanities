# NoteBooks-Humanities

> A modern, structured knowledge management system for the Humanities Administration Department
> Designed by the **Federation of Socialist Republics (FSR)** to centralize, organize, and democratize academic study materials

---

## Table of Contents

1. [Overview](#overview)
2. [What is NoteBooks-Humanities](#what-is-notebooks-humanities)
3. [Core Features](#core-features)
4. [Technical Architecture](#technical-architecture)
5. [Authentication System](#authentication-system)
6. [Project Structure](#project-structure)
7. [Getting Started](#getting-started)
8. [Team &amp; Credits](#team--credits)

---

## Overview

**NoteBooks-Humanities** is the Humanities Administration Department's official study material platform. It replaces fragmented note-sharing workflows with a centralized, professionally managed repository that ensures:

* **Quality Control** — All materials pass through administrative review
* **Accessibility** — Students and educators can easily find, download, and reference materials
* **Organization** — Structured hierarchy following the standard NCERT curriculum structure
* **Scalability** — Built to grow with the department's academic needs

### The Problem We Solve

Humanities students face a critical challenge: study materials are scattered across personal collections, messaging apps, and informal shares. This leads to:

* Inconsistent material quality
* Difficulty finding reliable sources
* No official reference point for curriculum-aligned content
* Repeated manual file distribution

NoteBooks-Humanities provides the solution.

---

## What is NoteBooks-Humanities

NoteBooks-Humanities is a **domain-specific knowledge platform** that functions as:

1. **A Centralized Repository** — One authoritative source for all Humanities curriculum materials
2. **A Document Management System** — Organized filing system with granular categorization
3. **An Anonymous Submission Interface** — Users can contribute without revealing their identity
4. **A Moderation Workflow** — Administrators review and approve all content before publication
5. **A Learning Hub** — Integrated discussion forums for doubt resolution and collaborative learning

### Key Capabilities

#### Structured Note Publishing

* **Curriculum-Aligned Organization** — NCERT-based hierarchy (History, Political Science, Geography, Economics, Sociology, Psychology)
* **Multi-Format Support** — Markdown (.md), PDF, spreadsheets, presentations
* **Rich Categorization** — Each chapter organized into:
  * **NOTES** — Comprehensive study material
  * **GLOSSARY** — Key terms and definitions
  * **PQs** — Previous questions with solutions
  * **REVISION_MINDMAPS** — Visual revision aids

#### Anonymous Upload System

* Users submit materials without revealing their identity
* All submissions appear in an admin review queue
* Admins evaluate for accuracy, relevance, and quality
* Approved materials become publicly available

#### Moderated Content Delivery

* Only vetted materials appear on the platform
* Maintains high academic standards
* Prevents misinformation and low-quality content
* Ensures all resources align with curriculum

#### Integrated Discussion Layers (NotePad Forums)

* Topic-based discussion threads tied to specific materials
* Doubt resolution workflows with moderator support
* Collaborative answer building from community
* Persistent academic dialogue preserved for future reference

---

## Core Features

### Document Management

* Browse by subject, chapter, and content type
* Search functionality across all materials
* Download multiple formats
* Material version history and updates

### User Experience

* Clean, intuitive interface using Markdown rendering
* Fast navigation and retrieval
* LaTeX/MathJax support for mathematical and economic notation
* Diagram rendering (TikZ, Mermaid)
* Syntax-highlighted code blocks

### Content Support

* **Markdown Support** — Full markdown + academic extensions
* **Mathematical Notation** — MathJax with LaTeX/AMS support
* **Diagrams** — TikZ and Mermaid diagram rendering
* **Code Syntax** — Highlight.js with multiple language support
* **Graphing** — Desmos graphing calculator integration

### Admin Panel

* Submission review interface
* Content approval/rejection workflows
* User role management
* Analytics and usage tracking

---

## Technical Architecture

NoteBooks-Humanities is built with modern web technologies designed for performance and reliability.

### Frontend Stack

* **HTML5** — Semantic markup
* **CSS** — Custom styling with design tokens and CSS variables
* **Vanilla JavaScript** — No framework overhead, full control
* **Markdown-it** — Markdown parsing with plugin ecosystem
* **MathJax 3** — LaTeX mathematical rendering
* **TikZJax** — TikZ diagram rendering
* **Mermaid** — Flowchart and diagram support
* **Highlight.js** — Code syntax highlighting
* **Desmos API** — Interactive graphing calculator

### Backend Infrastructure

* **Upstash Redis** — Distributed session and data storage
* **Resend** — Email service for password reset notifications
* **Google reCAPTCHA v3** — Bot protection on authentication forms

### Security Features

* **JWT Tokens** — Secure session management
* **bcrypt Hashing** — Industry-standard password hashing (10-round salting)
* **CAPTCHA Protection** — Google reCAPTCHA v3 on all forms
* **Cooldown Periods** — 15-minute cooldown on password reset requests
* **Redis Storage** — Distributed session management with fallback to in-memory storage

### Data Flow

1. User submits form (with reCAPTCHA token)
2. CAPTCHA validated server-side before processing
3. Credentials hashed and stored in Redis
4. JWT issued for session management
5. Each request validated against stored session

---

## Authentication System

### Modern Email + Password System (v2.0)

**Old System** — SSH key-based authentication (deprecated and removed)

**New System** — Email + password with industry-standard security:

#### Login

* Email and password input
* reCAPTCHA v3 bot detection
* JWT token issued on success
* Session persists for 30 days

#### Registration

* Email validation
* Password requirements (minimum 8 characters)
* reCAPTCHA v3 bot detection
* Automatic account creation

#### Forgot Password

* Email-based password recovery
* reCAPTCHA protection
* 15-minute cooldown between requests (prevents abuse)
* Secure token-based reset link
* Password reset via email link

### Security Specifications

* **Password Hashing** — bcrypt with 10 salt rounds
* **Session Tokens** — JWT with 30-day expiration
* **CAPTCHA** — Google reCAPTCHA v3 (invisible, doesn't interfere with UX)
* **Rate Limiting** — 15-minute cooldown on password reset
* **Storage** — Upstash Redis with automatic fallback
* **Email Service** — Resend for secure email delivery

---

## Project Structure

```
NoteBooks-Humanities/
├── index.html                 # Main application entry point
├── package.json              # Project dependencies
├── README.md                 # This file
├── files.json                # Content hierarchy definition
├── api/
│   ├── auth.js              # Authentication backend (login, register, forgot password)
│   ├── desmos.js            # Desmos graphing calculator API proxy
│   └── [admin-endpoints]    # Admin submission review handlers
├── bin/
│   ├── auth.js              # Frontend session/user management
│   ├── modern-auth.js       # Modern email+password UI controllers
│   ├── md-init.js           # Markdown rendering initialization
│   ├── obsidian-markdown-it.js  # Obsidian syntax compatibility
│   ├── style.css            # Design tokens and styling
│   ├── tikzjax/             # TikZ rendering engine
│   └── [utilities]          # Helper scripts
├── AI-NOTES/
│   ├── HISTORY/             # History chapter hierarchy (NCERT aligned)
│   │   ├── HISTORY01-BRICKS_BEADS_AND_BONES/
│   │   │   ├── NOTES.md
│   │   │   ├── GLOSSARY.md
│   │   │   ├── PQs.md
│   │   │   └── REVISION_MINDMAPS.md
│   │   ├── HISTORY02-KINGS_FARMERS_AND_TOWNS/
│   │   └── ... [chapters total]
│   ├── POLITICAL_SCIENCE/   # Political Science content (similar structure)
│   ├── GEOGRAPHY/           # Geography content (similar structure)
│   ├── ECONOMICS/           # Economics content (similar structure)
│   ├── SOCIOLOGY/           # Sociology content (similar structure)
│   ├── PSYCHOLOGY/          # Psychology content (similar structure)
│   └── ...
├── public/
│   ├── favicon.png          # Application icon
│   └── manifest.json        # PWA manifest
└── .git/                    # Git repository with version history
```

### Content Organization

Materials are organized following the  **NCERT curriculum structure** :

```
HISTORY
├── HISTORY01: Bricks, Beads and Bones
├── HISTORY02: Kings, Farmers and Towns
├── HISTORY03: Kinship, Caste and Class
├── HISTORY04: Thinkers, Beliefs and Buildings
├── HISTORY05: Through the Eyes of Travellers
├── HISTORY06: Bhakti-Sufi Traditions
├── HISTORY07: An Imperial Capital: Vijayanagara
├── HISTORY08: Peasants, Zamindars and the State
├── HISTORY09: Kings and Chronicles
├── HISTORY10: Colonialism and the Countryside
├── HISTORY11: Rebels and the Raj
├── HISTORY12: Colonial Cities
└── ... [more chapters]

POLITICAL SCIENCE
├── POLSCI01: Constitution — Why and How?
├── POLSCI02: Rights in the Indian Constitution
├── POLSCI03: Election and Representation
└── ... [more chapters]

GEOGRAPHY
├── GEO01: Geography as a Social Science
├── GEO02: The Earth and its Geological History
└── ... [more chapters]

ECONOMICS
├── ECO01: Indian Economy on the Eve of Independence
├── ECO02: Indian Economy 1950–1990
└── ... [more chapters]
```

Each chapter contains 4 standard sections:

* **NOTES** — Main study material
* **GLOSSARY** — Key terms and concepts
* **PQs** — Previous exam questions with detailed solutions
* **REVISION_MINDMAPS** — Visual summaries for quick revision

---

## Getting Started

### Prerequisites

* Node.js 18+
* npm or yarn
* Environment variables configured (see below)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/fsr-humanities/NoteBooks-Humanities.git
   cd NoteBooks-Humanities
   ```
2. **Install dependencies**

   ```bash
   npm install
   ```
3. **Configure environment variables**
   Create a `.env.local` file in the project root:

   ```
   RECAPTCHA_SITE_KEY=your_google_recaptcha_v3_site_key
   RECAPTCHA_SECRET_KEY=your_google_recaptcha_v3_secret_key
   RESEND_API_KEY=your_resend_email_api_key
   JWT_SECRET=your_jwt_secret_key
   APP_URL=http://localhost:3000
   UPSTASH_REDIS_REST_URL=your_upstash_redis_url
   UPSTASH_REDIS_REST_TOKEN=your_upstash_redis_token
   ```

   **Getting the Keys:**

   * **reCAPTCHA Keys** — [Google reCAPTCHA Console](https://www.google.com/recaptcha/admin)
   * **Resend API Key** — [Resend Dashboard](https://resend.com)
   * **JWT Secret** — Generate with `openssl rand -base64 32`
   * **Upstash Redis** — [Upstash Console](https://console.upstash.com/)
4. **Start development server**

   ```bash
   npm run dev
   ```

   The application will be available at `http://localhost:3000`

### Building for Production

```bash
npm run build
npm run start
```

---

## Team & Credits

### Project Leadership

* **Harshit Saha** — Founder of NoteBooks-X (UBSR), Project Creator and Maintainer
  * *Science Administration Department (Head)*
  * Just your average fella
* **Rishiraj Adhikari** — President (FSR)
  * President of whole Operation
  * Federation-wide Coordination
* **Pratyush Chanda** — Project Founder of NoteBooks-Project (FSR)
  * *Science Administration Department*
  * Main Upgrader and Project Maintainer
* **Smayan** — Humanities Administration Department (Head)
  * *Humanities Administration Department*
  * Humanities stream lead and content oversight

### Technology Acknowledgments

**Frontend Technologies**

* Markdown-it team for markdown parsing
* MathJax community for LaTeX rendering
* TikZJax developers for diagram support
* Mermaid team for flowchart rendering
* Highlight.js for syntax highlighting
* Desmos team for graphing calculator

**Security & Infrastructure**

* Google reCAPTCHA team
* Upstash team for Redis hosting
* Resend team for email service
* Vercel for deployment platform

### Contributors

We welcome contributions from the FSR community. See [CONTRIBUTING.md]() for guidelines.

---

## Project Status

* **Version** — 1.0 (Modern Authentication System)
* **Status** — Active Development
* **Last Updated** — June 2026
* **Maintenance** — Humanities Administration Department

### Recent Changes (v1.0)

* ✅ Replaced SSH authentication with modern email + password system
* ✅ Integrated Google reCAPTCHA v3 for bot protection
* ✅ Added password reset via email (Resend)
* ✅ Implemented JWT-based session management
* ✅ Added bcrypt password hashing
* ✅ Created modern, user-friendly login/register UI
* ✅ Removed legacy SSH auth files

### Roadmap

* [ ] Discussion forums (NotePad integration)
* [ ] Content moderation dashboard
* [ ] Advanced search and filtering
* [ ] Progress tracking and bookmarks
* [ ] Offline mode support
* [ ] Mobile app (React Native)

---

## License

NoteBooks-Humanities is developed by the **Federation of Socialist Republics (FSR)** for the Humanities Administration Department. All materials are curated for educational use within the institution.

For questions or contributions, contact: **fsr-humanities@gmail.com**

---

**Made with dedication by the FSR community** 📜🏛️
