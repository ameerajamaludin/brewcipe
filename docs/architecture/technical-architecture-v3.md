# Brewcipe — Technical Architecture

## 1. Purpose

This document defines the high-level technical architecture for the Brewcipe MVP.

It describes:

* major system components
* component responsibilities
* system and trust boundaries
* frontend and backend responsibilities
* application data flow
* database access
* authentication and authorization boundaries
* private data-preparation and import boundaries
* AI Coffee Sommelier integration
* configuration and secrets
* deployment boundaries
* repository structure
* testing boundaries
* architectural decisions and unresolved questions

This document intentionally remains at the architectural level.

Detailed data definitions and relational implementation belong in:

```text
docs/architecture/coffee-data-schema-v3.md
docs/architecture/database-schema-v3.md
```

Product behavior and scope remain governed by:

```text
docs/product/prd-v3.md
docs/product/requirements-v3.md
```

Implementation sequencing belongs in:

```text
docs/product/development-roadmap-v3.md
```

---

# 2. Architecture Context

Brewcipe is a web application for discovering structured coffee recipes and coffee traditions from around the world.

The MVP supports the following core product capabilities:

```text
Coffee Discovery
Structured Recipe Detail
Search
Geographical Exploration
```

The following are Should Have capabilities:

```text
Authentication
Favorites
Taste Profile & Personalization
AI Coffee Sommelier
```

The architecture should support these capabilities without introducing infrastructure for features that are outside the current MVP.

The production coffee dataset is privately maintained and stored in Supabase PostgreSQL.

The complete production dataset, private research material, intermediate curation artifacts, and private import files are not part of the public Brewcipe repository.

---

# 3. Architecture Goals

The Brewcipe architecture should:

* support the current MVP product requirements
* maintain clear separation between frontend, backend, database, data-preparation, and AI responsibilities
* keep Supabase PostgreSQL as the canonical production application data store
* prevent privileged credentials from reaching the browser
* support public coffee discovery without requiring authentication
* support authenticated user-specific functionality where implemented
* support structured and optional coffee data
* support geographical coffee relationships
* support AI recommendations grounded in Brewcipe data
* preserve the distinction between canonical application data and AI-generated content
* keep private production datasets outside the public repository
* support reproducible database changes through migrations
* remain understandable and maintainable as a portfolio project
* avoid unnecessary infrastructure before product requirements justify it

The architecture should favor clear boundaries and simple implementation over premature scalability.

---

# 4. Architecture Style

Brewcipe uses a separated frontend/backend architecture.

At a high level:

```text
┌──────────────────────────────┐
│         Web Browser          │
│                              │
│  React + TypeScript          │
│  Tailwind CSS                │
└──────────────┬───────────────┘
               │
               │ HTTPS / JSON
               ▼
┌──────────────────────────────┐
│       Brewcipe Backend       │
│                              │
│  Python + FastAPI            │
│                              │
│  API                         │
│  Validation                  │
│  Application Logic           │
│  Authorization               │
│  AI Orchestration            │
└───────────┬───────────┬──────┘
            │           │
            │           │
            ▼           ▼
┌──────────────────┐  ┌──────────────────┐
│     Supabase     │  │   LLM Provider   │
│                  │  │                  │
│ PostgreSQL       │  │ AI Coffee        │
│ Auth             │  │ Sommelier        │
└──────────────────┘  └──────────────────┘
```

Private data preparation exists outside the live application request path:

```text
┌──────────────────────────────┐
│ Private Coffee Dataset       │
│ and Curation Artifacts       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Validation / Transformation  │
│ / Import Workflow            │
│                              │
│ Optional reusable tooling:   │
│ scripts/enrichment/          │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│    Supabase PostgreSQL       │
│                              │
│ Canonical Production Data    │
└──────────────────────────────┘
```

The private data-preparation workflow is administrative and does not participate in normal user requests.

---

# 5. Major Technical Areas

Brewcipe consists of five primary technical areas:

```text
1. Frontend Application
2. Backend Application API
3. Supabase Database and Authentication
4. Private Data Preparation and Import
5. AI Coffee Sommelier Integration
```

Supporting concerns include:

```text
Configuration
Security
Database Migrations
Testing
Logging
Deployment
```

---

# 6. Frontend Application

## 6.1 Technology

The current frontend technology choices are:

```text
React
TypeScript
Tailwind CSS
```

The frontend build tooling and supporting libraries should remain implementation decisions unless they become architectural constraints.

Reusable UI should follow the principles defined in:

```text
docs/design/design-system-v3.md
```

The architecture does not require a specific third-party component library.

---

## 6.2 Responsibilities

The frontend is responsible for:

* rendering Brewcipe's user interface
* responsive layouts
* application navigation
* displaying coffee discovery results
* displaying structured recipe information
* search interactions
* geographical exploration interactions
* authentication interfaces where implemented
* favorites interactions where implemented
* AI Coffee Sommelier presentation where implemented
* loading states
* empty states
* error states
* accessible client-side interaction
* local presentation and interaction state
* communicating with the Brewcipe backend

The frontend should not be responsible for:

* privileged database access
* Supabase service-role credentials
* LLM provider credentials
* canonical coffee-data validation
* private dataset transformation
* private import workflows
* server-side authorization decisions
* constructing privileged AI-provider requests

---

# 7. Frontend Architecture

The exact folder structure may evolve during implementation.

A suitable conceptual structure is:

```text
frontend/
│
├── public/
│
└── src/
    ├── assets/
    ├── components/
    │   ├── ui/
    │   ├── layout/
    │   └── common/
    │
    ├── features/
    │   ├── coffee/
    │   ├── search/
    │   ├── geography/
    │   ├── auth/
    │   ├── favorites/
    │   └── sommelier/
    │
    ├── pages/
    ├── hooks/
    ├── services/
    ├── lib/
    ├── types/
    └── utils/
```

This structure is illustrative rather than mandatory.

Folders should be introduced when implementation requires them rather than created solely to satisfy the diagram.

---

# 8. Frontend Dependency Direction

The frontend should favor reusable layers.

Conceptually:

```text
Pages
  ↓
Feature Components
  ↓
Brewcipe Product Components
  ↓
Shared UI Components
  ↓
UI Primitives
```

Data access should generally follow:

```text
Page / Feature
      ↓
Service / Hook
      ↓
Backend API
```

API requests should not be independently scattered throughout low-level visual components.

---

# 9. Frontend Data Access Boundary

Application coffee data should be accessed through the Brewcipe backend where required by the architecture.

Conceptually:

```text
React
  ↓
Frontend Service Layer
  ↓
FastAPI
  ↓
Application Service
  ↓
Database Access
```

Example:

```text
RecipeDetailPage
      ↓
coffeeService.getCoffee(identifier)
      ↓
Brewcipe API
      ↓
FastAPI
      ↓
Supabase PostgreSQL
```

This keeps database-specific access patterns out of the presentation layer and provides a stable application boundary for validation, response shaping, and future backend changes.

Supabase client-side functionality may still be used where specifically required for supported authentication flows.

---

# 10. Backend Application

## 10.1 Technology

```text
Python
FastAPI
```

FastAPI serves as Brewcipe's request-serving application backend.

---

## 10.2 Responsibilities

The backend is responsible for:

* retrieving coffee records
* retrieving structured recipe information
* search
* geographical data retrieval
* request validation
* response shaping
* application-level error handling
* authentication validation for protected operations
* authorization for user-specific operations
* favorites operations where implemented
* AI Coffee Sommelier orchestration where implemented
* retrieving Brewcipe data for AI grounding
* communicating with the configured LLM provider
* protecting privileged credentials

The backend provides the primary application boundary between browser clients and protected services.

---

# 11. Backend Architecture

A suitable conceptual structure is:

```text
backend/
│
├── app/
│   ├── api/
│   ├── schemas/
│   ├── services/
│   ├── repositories/
│   ├── core/
│   └── main.py
│
└── tests/
```

Additional folders should only be introduced where implementation complexity justifies them.

---

# 12. Backend Layer Responsibilities

## 12.1 API Layer

The API layer defines HTTP interfaces.

Potential route families include:

```text
/coffees
/search
/geography
/favorites
/auth-related protected operations
/sommelier
```

Exact endpoint paths and contracts should be finalized during backend implementation.

API routes should remain relatively thin and delegate reusable application logic to appropriate services.

---

## 12.2 Schemas

Schemas define validated request and response structures.

Potential examples include:

```text
CoffeeSummaryResponse
CoffeeDetailResponse
SearchResponse
GeographyResponse
FavoriteResponse
SommelierRequest
SommelierResponse
```

These structures should align with the canonical coffee-data and database models while remaining focused on application needs.

Database rows do not need to be exposed directly as API responses.

---

## 12.3 Services

Services contain reusable application logic.

Potential examples include:

```text
CoffeeService
SearchService
GeographyService
FavoriteService
SommelierService
```

A service may coordinate multiple repositories or external providers when required.

---

## 12.4 Repositories

Repositories isolate database interaction where that separation improves maintainability.

Potential examples include:

```text
CoffeeRepository
GeographyRepository
FavoriteRepository
```

Repository logic should prevent database queries from becoming scattered throughout API route handlers.

The architecture does not require unnecessary repository abstraction for trivial operations if it provides no practical value.

---

## 12.5 Core

Shared backend infrastructure may include:

```text
configuration
authentication
authorization helpers
logging
database/client initialization
shared dependencies
```

---

# 13. Backend Dependency Direction

Backend dependencies should generally follow:

```text
API Routes
    ↓
Services
    ↓
Repositories
    ↓
Supabase PostgreSQL
```

External services follow a parallel controlled path:

```text
API Route
    ↓
Sommelier Service
    ↓
LLM Provider
```

Avoid placing substantial database or AI-provider logic directly inside route handlers when that logic belongs to a reusable application layer.

---

# 14. Canonical Database

## 14.1 Technology

```text
Supabase PostgreSQL
```

Supabase PostgreSQL is Brewcipe's canonical production application data store.

The production application should operate against canonical database records rather than private research or intermediate preparation artifacts.

---

## 14.2 Database Responsibilities

The relational model must support the data required by the current MVP.

Conceptually, this includes entities or relationships for:

```text
Coffee / Recipe
Geography
Ingredients
Preparation Instructions
Sources / Provenance
Users
Favorites
```

The exact relational structure belongs in:

```text
docs/architecture/database-schema-v3.md
```

---

# 15. Canonical Coffee Data

The canonical coffee-data model defines the information Brewcipe recognizes as application-ready coffee data.

It should support the fields required by the product, including where applicable:

```text
English name
Native name
Transliteration
Geography
Recipe type
Brewer / brewing method
Servings
Temperature
Ingredients
Preparation instructions
Cultural context
Source attribution
```

Optional values must remain optional where permitted by the canonical model.

Detailed field definitions, normalization rules, data types, and provenance representation belong in:

```text
docs/architecture/coffee-data-schema-v3.md
```

---

# 16. Canonical Data Boundary

Brewcipe distinguishes between:

```text
Private Research / Curation Data
```

and:

```text
Canonical Production Application Data
```

Conceptually:

```text
Private Curated Dataset
        ↓
Review
        ↓
Transformation
        ↓
Canonical Validation
        ↓
Relational Import
        ↓
Supabase PostgreSQL
        ↓
Brewcipe Application
```

Private research or preparation artifacts must not become application data merely because they exist in the source dataset.

Records should conform to the canonical Brewcipe data model before being made available to the production application.

---

# 17. Private Data Preparation and Import

The initial Brewcipe coffee library was created through manual research, extraction, normalization, and curation.

The production dataset is maintained privately.

Therefore, private data preparation is treated as an administrative workflow rather than a public application subsystem.

Potential activities include:

```text
research
review
normalization
translation where required
geographical mapping
duplicate resolution
source verification
canonical transformation
validation
database import
```

The exact private working files do not form part of the public repository architecture.

---

# 18. Public Data Tooling Boundary

Reusable tooling may be created under:

```text
scripts/enrichment/
```

when it supports reproducible technical processes such as:

```text
schema validation
identifier validation
unit validation
source-field validation
duplicate detection
dataset statistics
transformation utilities
```

Such tooling should demonstrate application engineering without requiring the private production dataset to be committed publicly.

Private input files, intermediate artifacts, and production import files remain excluded from Git.

---

# 19. Scraper Boundary

The repository may retain:

```text
scripts/scraper/
```

for scraper-related experimentation or supporting tooling.

However, automated web scraping is not part of Brewcipe's production ingestion architecture for the current MVP.

The live application does not depend on scraping.

Conceptually:

```text
scripts/scraper/
      ≠
Production Request Path
```

and:

```text
scripts/scraper/
      ≠
Required Production Ingestion Pipeline
```

Scraper failures, blocked websites, extraction changes, or external-site availability must not affect Brewcipe's live coffee discovery experience.

If future product requirements introduce assisted candidate discovery or source-monitoring workflows, the architecture should be reviewed before those capabilities become production dependencies.

---

# 20. Application Coffee Data Flow

The live application data flow is:

```text
User
  ↓
React Frontend
  ↓
FastAPI Backend
  ↓
Supabase PostgreSQL
  ↓
Canonical Coffee Data
  ↓
FastAPI Response
  ↓
React Interface
```

Private data preparation follows a separate flow:

```text
Private Curated Data
        ↓
Review / Transformation
        ↓
Canonical Validation
        ↓
Private Import Workflow
        ↓
Supabase PostgreSQL
```

These two flows should remain architecturally distinct.

---

# 21. Provenance

Brewcipe's data model supports source attribution and provenance.

Source information required by the canonical model should remain associated with the corresponding production coffee data.

Normalized or interpreted information should not be represented as though it were necessarily stated directly by the original source.

Detailed provenance fields and relationships belong in:

```text
coffee-data-schema-v3.md
database-schema-v3.md
```

Private processing metadata does not automatically need to be exposed through the application API or user interface.

---

# 22. Search Architecture

MVP search should operate against Brewcipe's canonical application data.

Conceptually:

```text
User Query
    ↓
Frontend
    ↓
Search API
    ↓
Backend Search Logic
    ↓
Supabase PostgreSQL
    ↓
Matching Coffee Records
    ↓
Frontend
```

Coffee-name search is required for the MVP.

Additional searchable attributes may be introduced according to the settled PRD and implementation feasibility.

AI is not required for standard search.

---

# 23. Search Infrastructure

The default MVP architecture should use PostgreSQL-supported querying and search capabilities unless implementation evidence demonstrates that additional infrastructure is necessary.

The MVP does not currently require:

```text
Elasticsearch
OpenSearch
Algolia
Dedicated search clusters
Vector search
```

Advanced search infrastructure should only be introduced when justified by future product requirements.

---

# 24. Geographical Exploration Architecture

Brewcipe's user-facing geographical hierarchy is:

```text
Continent
    ↓
Region
    ↓
Country
    ↓
Coffee
```

The database should represent the relationships required to support this hierarchy.

The frontend should retrieve geographical information dynamically rather than hard-coding separate pages for every location.

Conceptually:

```text
Geographical Selection
        ↓
Frontend
        ↓
FastAPI
        ↓
Geographical Query
        ↓
Supabase
        ↓
Relevant Geography / Coffees
```

The exact relational implementation belongs in `database-schema-v3.md`.

The exact visual presentation belongs in Brewcipe's design documentation.

---

# 25. Recipe Detail Architecture

Recipe detail requests should resolve through a stable coffee or recipe identifier.

Conceptually:

```text
Recipe Route
    ↓
Stable Identifier
    ↓
FastAPI
    ↓
Coffee / Recipe Retrieval
    ↓
Related Structured Data
    │
    ├── Geography
    ├── Ingredients
    ├── Instructions
    └── Source Information
    ↓
Application Response
```

The backend should return an appropriate not-found response when the identifier does not correspond to an available record.

Optional recipe information should remain nullable or absent without preventing valid recipe data from being returned.

---

# 26. Authentication

## 26.1 Technology

```text
Supabase Auth
```

Authentication is a Should Have capability for the current MVP.

The exact authentication methods offered to users should be selected during implementation and should not be assumed by the architecture before that decision is made.

---

## 26.2 Public Access

Core coffee discovery does not require authentication.

Public functionality includes:

```text
browse coffees
view recipe details
search
geographical exploration
```

The AI Coffee Sommelier may also remain public according to the current product requirements, subject to appropriate usage controls if implemented.

---

## 26.3 Protected Access

Authentication is required for persistent user-specific functionality such as:

```text
add favorite
remove favorite
view user's favorites
```

---

# 27. Protected Request Flow

Conceptually:

```text
Authenticated User
        ↓
Frontend
        ↓
Authenticated Request
        ↓
FastAPI
        ↓
Validate Authentication
        ↓
Determine Authenticated User
        ↓
Authorize Requested Operation
        ↓
Supabase
```

The backend must not trust a client-provided user identifier as proof of ownership.

User-specific operations should derive identity from validated authentication context.

---

# 28. Favorites Architecture

Favorites represent a relationship between an authenticated user and a coffee.

Conceptually:

```text
User
  │
  └──── Favorite ──── Coffee
```

The system should:

* prevent duplicate favorite relationships
* associate favorites with the authenticated user
* prevent users from modifying another user's favorites
* persist favorites across authenticated sessions

Supabase Row Level Security should be used where appropriate to reinforce user-specific data protection.

The exact table structure belongs in:

```text
database-schema-v3.md
```

---

# 29. Supabase Access Boundaries

Different application contexts may use different Supabase capabilities and credentials.

## Frontend-Safe Configuration

Where required for supported Supabase client-side authentication functionality, the frontend may use public/publishable project configuration.

Examples may include:

```text
Supabase project URL
Supabase publishable key
```

These credentials must not provide privileged database access.

---

## Server-Only Configuration

Privileged configuration must remain outside frontend source code.

Examples include:

```text
Supabase service-role credentials
LLM provider credentials
```

Privileged credentials must be supplied through secure environment configuration.

---

# 30. Personalization Architecture

Brewcipe's Taste Profile Mechanic is implemented as deterministic application logic that combines explicit user preferences with observed recipe interactions.

Conceptually:

```text
                    Taste Model
                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
     Saved Coffees   Coffee History  User Signals
          │              │              │
          └──────────────┼──────────────┘
                         ↓
                Recommendation Engine
                         │
              ┌──────────┴──────────┐
              ↓                     ↓
      Personalized Home       Sommelier Context
```

## 30.1 Deterministic Recommendation Layer

The recommendation engine should remain independent of the LLM provider.

It uses:

* taste-profile preferences
* brewer preferences
* discovery style
* derived recipe-intelligence signals
* tried-history affinity
* skipped-recipe exclusions

The current implementation derives qualitative recipe-intelligence signals from structured recipe data. These signals are application features and do not modify canonical recipe records.

## 30.2 User-Specific Data

User taste profiles and recipe interactions are stored in Supabase and associated with the authenticated user's UUID.

Current interaction types are:

```text
tried
skipped
```

Favorites remain the saved-coffee relationship. Favorite weighting in recommendation ranking is a planned continuation of the mechanic.

## 30.3 Sommelier Boundary

The Sommelier receives the current personalization context through the backend. Gemini provides conversational recommendation and explanation, but it does not calculate or own the canonical taste model.

The detailed product mechanic is defined in `docs/product/taste-profile-mechanic-v1.md`.

---

# 30. AI Coffee Sommelier

The AI Coffee Sommelier is a Should Have capability.

It provides conversational coffee recommendations grounded in Brewcipe's canonical structured data.

The AI feature is not Brewcipe's canonical data source.

Conceptually:

```text
Canonical Brewcipe Data
        ↓
Relevant Context Retrieval
        ↓
AI Coffee Sommelier
        ↓
Recommendation
        ↓
Existing Brewcipe Recipe
```

where a relevant Brewcipe recipe exists.

---

## 31. LLM Provider

## Status

**Implemented — Google Gemini**

The specific LLM provider and model have not yet been finalized.

The architecture should therefore avoid coupling application-wide behavior to a provider-specific implementation.

Provider credentials and provider requests must remain server-side.

Configuration should allow the selected model or provider settings to change without requiring frontend redesign.

---

# 32. AI Request Flow

Conceptually:

```text
User
  ↓
React Frontend
  ↓
Sommelier API Request
  ↓
FastAPI
  ↓
Sommelier Service
  │
  ├── Retrieve Personalized User Context
  │
  ├── Retrieve Relevant Brewcipe Data
  │
  ├── Construct Controlled AI Request
  │
  └── Call Configured LLM Provider
  ↓
Parse / Validate Response
  ↓
FastAPI
  ↓
React Frontend
```

The frontend must not call a privileged LLM API directly using a private provider credential.

---

# 33. Why AI Requests Use the Backend

The backend boundary allows Brewcipe to:

* protect provider credentials
* validate user input
* control context retrieval
* control prompt construction
* avoid exposing unnecessary production data
* handle provider failures
* handle timeouts
* introduce usage controls where required
* normalize provider responses
* change provider or model implementation with minimal frontend impact

---

# 34. AI Grounding Boundary

The LLM should receive only the Brewcipe context relevant to the user's request where practical.

The architecture should avoid sending the complete production coffee dataset to the provider for every query.

A likely conceptual flow is:

```text
User Question
      ↓
Backend
      ↓
Retrieve Relevant Brewcipe Records
      ↓
Construct Grounding Context
      ↓
LLM Provider
      ↓
Recommendation
```

The exact retrieval strategy remains unresolved.

Potential future implementation should be selected based on actual data size, query requirements, quality, cost, and implementation complexity.

A vector database is not an assumed MVP requirement.

---

# 35. AI Canonical-Data Boundary

AI-generated output must not become canonical Brewcipe data automatically.

The relationship is:

```text
Supabase Coffee Data
        =
Canonical Application Data
```

while:

```text
LLM Response
        =
Generated Recommendation Content
```

AI-generated responses must not directly create or modify canonical production coffee records.

---

# 36. AI Failure Boundary

The AI Coffee Sommelier should fail independently from Brewcipe's core coffee functionality.

Conceptually:

```text
LLM Provider Failure
        ≠
Coffee Library Failure
```

If the AI provider is unavailable, users should still be able to:

```text
browse coffee
search
explore geographically
open recipes
use implemented non-AI functionality
```

The frontend should provide an understandable AI failure state.

---

# 37. API Boundary

Backend responses should represent application needs rather than exposing raw database structures or private preparation metadata.

For example, application responses may contain:

```text
coffee identity
geographical information
recipe information
ingredients
ordered instructions
cultural context
source attribution where required
```

They should not expose irrelevant private preparation fields or privileged internal metadata.

The exact response contracts should be defined during backend implementation and kept consistent with the canonical data model.

---

# 38. Error Boundaries

Different architectural components should fail independently where practical.

Examples:

```text
Private import workflow failure
        ≠
Production API failure
```

```text
LLM provider failure
        ≠
Coffee discovery failure
```

```text
Authentication failure
        ≠
Public recipe access failure
```

The backend should return appropriate error responses without exposing sensitive configuration or internal credentials.

---

# 39. Configuration

Environment-specific configuration should use environment variables or an equivalent secure configuration mechanism.

Conceptually:

```text
frontend/.env
backend/.env
```

Example files may document required variable names without containing secret values.

Actual environment files containing credentials must not be committed to Git.

---

# 40. Frontend Configuration

Potential frontend-safe configuration may include:

```text
Backend API base URL
Supabase project URL
Supabase publishable key
```

Exact variable names should be finalized during frontend setup.

The frontend must not contain:

```text
Supabase service-role credentials
LLM provider private API keys
other privileged server credentials
```

---

# 41. Backend Configuration

Potential server-side configuration may include:

```text
Supabase URL
Supabase privileged credentials where required

LLM provider API key
LLM provider/model configuration

Allowed frontend origin
Environment identifier
```

Exact variable names should be finalized during implementation.

Only configuration actually required by the application should be introduced.

---

# 42. Repository Structure

The current Brewcipe repository structure is:

```text
brewcipe/
│
├── frontend/
├── backend/
│
├── scripts/
│   ├── scraper/
│   └── enrichment/
│
├── data/
│
├── supabase/
│   └── migrations/
│
└── docs/
    ├── product/
    │   ├── product-idea-v3.md
    │   ├── prd-v3.md
    │   ├── requirements-v3.md
    │   └── development-roadmap-v3.md
    │
    ├── design/
    │   ├── design-direction-v3.md
    │   ├── design-system-v3.md
    │   ├── information-architecture-v3.md
    │   └── wireframes-v3.md
    │
    └── architecture/
        ├── technical-architecture-v3.md
        ├── database-schema-v3.md
        └── coffee-data-schema-v3.md
```

The existence of `scripts/` and `data/` does not mean private production data should be committed to the repository.

Private datasets and private preparation/import artifacts must remain excluded from Git.

---

# 43. Directory Responsibilities

## `frontend/`

Contains the browser-based Brewcipe application.

---

## `backend/`

Contains the FastAPI request-serving application.

---

## `scripts/scraper/`

Contains scraper-related experimental or supporting tooling.

It is not part of the current production request or required production-ingestion path.

---

## `scripts/enrichment/`

Contains reusable validation, transformation, enrichment, or preparation utilities where appropriate.

Private production data should not be committed alongside these tools.

---

## `data/`

May be used for local development artifacts, synthetic examples, or other intentionally permitted data.

The complete production coffee dataset and private data-preparation artifacts must not be committed.

The exact contents of this directory should remain consistent with Brewcipe's repository privacy boundary.

---

## `supabase/migrations/`

Contains version-controlled database schema migrations.

Migration files should describe schema changes rather than contain the complete production coffee dataset.

---

## `docs/`

Contains Brewcipe product, design, and architecture documentation.

---

# 44. Database Migrations

Database schema changes should be reproducible through version-controlled migrations.

Conceptually:

```text
database-schema-v3.md
        ↓
Supabase Migration
        ↓
PostgreSQL Schema
```

Schema changes should not depend solely on undocumented manual changes in the production database.

Migration files belong in:

```text
supabase/migrations/
```

The complete production coffee dataset must not be embedded into public migrations.

---

# 45. Development Environment

Brewcipe is developed as a separated frontend/backend application.

Conceptually, local development runs:

```text
React Frontend
      +
FastAPI Backend
      +
Supabase Project / Services
```

Private data-preparation utilities run separately when required.

---

# 46. Frontend Development Flow

Conceptually:

```text
Browser
  ↓
Frontend Development Server
  ↓
React Application
  ↓
Configured FastAPI Base URL
  ↓
FastAPI Development Server
```

The frontend should not hard-code production API addresses throughout application components.

---

# 47. Backend Development Flow

Conceptually:

```text
FastAPI
  ↓
Application Services
  ↓
Repositories / Data Access
  ↓
Supabase PostgreSQL
```

AI requests follow a separate external-service path:

```text
FastAPI
  ↓
Sommelier Service
  ↓
Configured LLM Provider
```

---

# 48. Deployment Architecture

## Status

**Frontend and backend hosting providers are TBD.**

The architecture should support separate deployment of:

```text
Frontend
Backend
Database / Authentication
```

Supabase provides the managed PostgreSQL and authentication layer.

The frontend and FastAPI backend may be hosted independently.

Provider selection should be documented when deployment requirements are evaluated.

---

# 49. Production Network Flow

Conceptually:

```text
User Browser
     │
     ▼
Frontend Hosting
     │
     │ HTTPS
     ▼
FastAPI Backend Hosting
     │
     ├──────────► Supabase PostgreSQL
     │
     └──────────► LLM Provider
```

Authentication may additionally involve supported Supabase Auth client flows.

Private data import occurs separately:

```text
Private Import Workflow
        ↓
Supabase PostgreSQL
```

---

# 50. Security Principles

Brewcipe should follow these baseline principles:

* secrets must not be committed to Git
* privileged Supabase credentials must remain server-side
* LLM provider credentials must remain server-side
* protected operations must validate authentication
* authorization must enforce resource ownership
* user-controlled backend input must be validated
* Row Level Security should protect user-specific Supabase data where appropriate
* production datasets must remain outside the public repository
* private preparation and import artifacts must remain outside the public repository
* production traffic should use HTTPS
* backend errors must not expose credentials or privileged configuration
* AI-generated content must not be treated as trusted canonical data
* external or privately curated source content should be treated as data rather than executable instructions

---

# 51. Trust Boundaries

Conceptually:

```text
UNTRUSTED / EXTERNAL
────────────────────────────────

Browser input
External source material
AI-generated responses

            ↓ validation / controlled handling

BREWCIPE APPLICATION BOUNDARY
────────────────────────────────

FastAPI application logic
Validation
Authorization
Response shaping
AI orchestration

            ↓ controlled access

PROTECTED SERVICES / DATA
────────────────────────────────

Supabase PostgreSQL
User-specific records
Privileged Supabase credentials
LLM provider credentials
Private production dataset
```

The exact degree of trust differs by component, but crossing a boundary should involve appropriate validation or authorization.

---

# 52. AI Security Boundary

User input and Brewcipe data supplied to an LLM should be treated as contextual data rather than privileged system instructions.

The AI integration should maintain a distinction between:

```text
Brewcipe-controlled instructions
```

and:

```text
user-controlled or retrieved contextual content
```

The exact prompt construction and provider-specific security controls should be defined when the AI Coffee Sommelier is implemented.

AI output should be treated as generated content and validated or constrained where application behavior depends on its structure.

---

# 53. Logging and Observability

For MVP development, backend logging should provide enough information to diagnose:

```text
API errors
database failures
authentication failures
authorization failures
validation failures
LLM provider failures
```

Logs must not contain:

```text
passwords
authentication tokens
private API keys
service-role credentials
unnecessary sensitive configuration
```

Advanced observability infrastructure is not required until deployment or operational needs justify it.

---

# 54. Testing Boundaries

Testing should reflect the architecture's major responsibilities.

## Frontend

Potential coverage includes:

```text
shared components
feature components
page behavior
loading states
error states
empty states
service interactions
primary user journeys
```

---

## Backend

Potential coverage includes:

```text
API endpoints
request validation
response models
services
database access
authentication
authorization
error handling
AI integration boundaries
```

---

## Data Preparation

Potential coverage includes:

```text
canonical validation
field transformation
identifier validation
duplicate detection
unit handling
relational transformation
```

---

## Database

Potential verification includes:

```text
migrations
constraints
relationships
nullable fields
indexes
Row Level Security policies
```

The detailed implementation and testing sequence remains governed by `development-roadmap-v3.md`.

---

# 55. Accessibility Boundary

Accessibility is primarily expressed through frontend implementation, but architecture should not create barriers that make accessible behavior difficult.

The application should support the requirements defined by Brewcipe's design system and system requirements, including:

```text
semantic HTML
keyboard-operable interactions
accessible form naming
visible state feedback
responsive interfaces
understandable loading/error states
```

Brewcipe targets WCAG 2.2 Level AA for the web interface.

---

# 56. Scaling Philosophy

Brewcipe should begin with the simplest architecture that satisfies the current product requirements.

The MVP does not currently require:

```text
microservices
Kubernetes
message queues
event buses
distributed caches
multiple application databases
dedicated search clusters
vector databases
complex event-driven architecture
```

These technologies should not be introduced merely to make the portfolio architecture appear more sophisticated.

Future architecture should evolve in response to actual product requirements, performance evidence, operational constraints, or scale.

---

# 57. Future Architecture Possibilities

Future product requirements may eventually justify additional architecture for capabilities such as:

```text
advanced search and filtering
richer geographical visualization
related recommendations
multilingual interfaces
community contributions
administrative content management
larger data-management workflows
source monitoring
personalized recommendation systems
richer AI retrieval
background processing
```

These are not assumed parts of the current MVP architecture.

Future architecture should be introduced only after corresponding product requirements are established.

---

# 58. Architectural Decisions

## TA-DECISION-001 — Frontend Framework

Use React for the Brewcipe web frontend.

---

## TA-DECISION-002 — Frontend Language

Use TypeScript for frontend development.

---

## TA-DECISION-003 — Styling

Use Tailwind CSS for frontend styling.

---

## TA-DECISION-004 — Backend Framework

Use Python and FastAPI for the Brewcipe backend API.

---

## TA-DECISION-005 — Canonical Database

Use Supabase PostgreSQL as Brewcipe's canonical production application data store.

---

## TA-DECISION-006 — Authentication Platform

Use Supabase Auth for authentication when the Should Have authentication capability is implemented.

---

## TA-DECISION-007 — Backend Application Boundary

Use FastAPI as the primary application boundary between the frontend and protected database or external-service operations.

---

## TA-DECISION-008 — Private Production Dataset

Keep the complete production coffee dataset outside the public Brewcipe repository.

---

## TA-DECISION-009 — Private Data Preparation

Keep private research, curation, transformation, and import artifacts outside the public repository.

---

## TA-DECISION-010 — Canonical Data Validation

Require production coffee records to conform to Brewcipe's canonical data model before being made available to the application.

---

## TA-DECISION-011 — Scraper Separation

Keep scraper-related tooling separate from the live backend.

Automated web scraping is not a required production ingestion pipeline for the current MVP.

---

## TA-DECISION-012 — Database Migrations

Represent database schema changes through version-controlled migrations under:

```text
supabase/migrations/
```

---

## TA-DECISION-013 — AI Backend Boundary

Send privileged AI-provider requests through the FastAPI backend rather than exposing provider credentials to the frontend.

---

## TA-DECISION-014 — AI Canonical Boundary

Do not treat the LLM as Brewcipe's canonical coffee-data source.

---

## TA-DECISION-015 — AI Write Boundary

AI-generated responses must not directly create or modify canonical production coffee records.

---

## TA-DECISION-016 — Configuration

Use environment variables or equivalent secure configuration for environment-specific settings and secrets.

---

## TA-DECISION-017 — MVP Infrastructure

Do not introduce additional infrastructure such as microservices, dedicated search clusters, or vector databases unless implementation evidence or product requirements justify them.

---

# 59. Open Architecture Decisions

The following architectural decisions remain unresolved.

## TA-TBD-001 — Frontend Build Tooling

Which frontend build tooling and project initialization approach will be used?

The decision should remain compatible with the settled React + TypeScript architecture.

---

## TA-TBD-002 — Frontend Hosting

Where will the Brewcipe frontend be hosted in production?

---

## TA-TBD-003 — Backend Hosting

Where will the FastAPI backend run in production?

---

## TA-TBD-004 — Authentication Methods

Which Supabase Auth methods will Brewcipe expose to users?

Examples could include email/password or supported OAuth providers, but no specific method is currently required by the product requirements.

---

## TA-TBD-005 — LLM Provider

**Resolved:** Google Gemini is the current LLM provider and is called through the backend.

---

## TA-TBD-006 — Sommelier Retrieval

**Current implementation:** the backend retrieves a limited candidate set and supplies structured recipe summaries plus personalized user context to Gemini. Further retrieval improvements remain open.

---

## TA-TBD-007 — Search Implementation Details

Which PostgreSQL search capabilities will be sufficient for MVP coffee-name search and any additional intentionally supported attributes?

The default direction is to avoid dedicated search infrastructure unless evidence demonstrates a need.

---

## TA-TBD-008 — Image Architecture

How will coffee imagery be sourced, attributed, stored, optimized, and delivered?

---

## TA-TBD-009 — Public Data Directory

What, if any, non-private data artifacts should be maintained under the repository's `data/` directory?

The production dataset and private preparation/import artifacts must remain excluded regardless of this decision.

---

## TA-TBD-010 — Backend Database Access Implementation

Which Supabase/PostgreSQL client approach will the FastAPI backend use for application data access?

The choice should preserve the security and application boundaries defined in this document.

---

# 60. Relationship to Brewcipe Documentation

Brewcipe's architecture documentation should maintain clear responsibilities.

```text
technical-architecture-v3.md
```

Defines:

> How do Brewcipe's technical systems fit together, and where are their boundaries?

---

```text
coffee-data-schema-v3.md
```

Defines:

> What information represents canonical Brewcipe coffee and recipe data?

---

```text
database-schema-v3.md
```

Defines:

> How is canonical Brewcipe data stored and related in PostgreSQL?

---

Product requirements remain defined in:

```text
prd-v3.md
requirements-v3.md
```

Design decisions remain defined in:

```text
design-direction-v3.md
design-system-v3.md
information-architecture-v3.md
wireframes-v3.md
```

Implementation sequencing remains defined in:

```text
development-roadmap-v3.md
```

---

# 61. Architecture Traceability

The technical architecture should exist to support product and system requirements rather than introduce independent product scope.

Conceptually:

```text
Product Idea
      ↓
PRD
      ↓
System Requirements
      ↓
Technical Architecture
      ↓
Coffee Data Schema
      ↓
Database Schema
      ↓
Development Roadmap
      ↓
Implementation and Testing
```

Where architecture decisions reveal a conflict with product requirements, the relevant source document should be reviewed rather than silently redefining product behavior inside the architecture.

---

# 62. Architecture Summary

The Brewcipe MVP architecture can be summarized as:

```text
                       ┌──────────────────┐
                       │       User       │
                       └────────┬─────────┘
                                │
                                ▼
                    ┌───────────────────────┐
                    │   React + TypeScript  │
                    │       Frontend        │
                    │                       │
                    │     Tailwind CSS      │
                    └───────────┬───────────┘
                                │
                                │ HTTPS / JSON
                                ▼
                    ┌───────────────────────┐
                    │       FastAPI         │
                    │        Backend        │
                    │                       │
                    │ Validation            │
                    │ Application Logic     │
                    │ Authorization         │
                    │ AI Orchestration      │
                    └────────┬───────┬──────┘
                             │       │
                             │       │
                             ▼       ▼
                   ┌──────────────┐ ┌──────────────┐
                   │   Supabase   │ │     LLM      │
                   │              │ │   Provider   │
                   │ PostgreSQL   │ │              │
                   │ Auth         │ │  Sommelier   │
                   └──────────────┘ └──────────────┘


       PRIVATE / ADMINISTRATIVE DATA FLOW

       ┌──────────────────────────────┐
       │   Private Curated Dataset    │
       │   + Preparation Artifacts    │
       └──────────────┬───────────────┘
                      │
                      ▼
       ┌──────────────────────────────┐
       │ Review / Transformation /    │
       │ Canonical Validation         │
       │                              │
       │ Optional reusable tooling    │
       │ under scripts/enrichment/    │
       └──────────────┬───────────────┘
                      │
                      ▼
              ┌──────────────┐
              │   Supabase   │
              │  PostgreSQL  │
              └──────────────┘
```

The architecture intentionally separates:

```text
User Interface
Application API
Canonical Data Storage
Authentication
AI Integration
Private Data Preparation
```

while keeping the MVP technically straightforward.

Brewcipe should demonstrate deliberate product and engineering decisions without adding infrastructure simply for architectural complexity.

The goal is a system that is understandable, secure, maintainable, appropriate for the current product scope, and capable of evolving when future requirements provide a reason to do so.
