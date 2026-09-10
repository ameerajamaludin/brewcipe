# Brewcipe — Development Roadmap

## 1. Purpose

This roadmap translates the Brewcipe Product Requirements Document (PRD) into an implementation sequence for the MVP.

The roadmap focuses on building the current Brewcipe application from a clean project baseline.

Previous Brewcipe experiments, coffee scraping work, and data-preparation projects are not treated as completed implementation work in this roadmap.

Therefore, all implementation tasks begin as incomplete:

```text
[ ] Not started / incomplete
[x] Completed in the current Brewcipe project
```

A task should only be marked `[x]` when it has been completed and verified within the current Brewcipe project.

---

# 2. Development Approach

Brewcipe will be developed incrementally.

The general implementation sequence is:

```text
Project Foundation
        ↓
Database
        ↓
Private Data Preparation & Import
        ↓
Backend API
        ↓
Core Frontend
        ↓
Search & Geographic Discovery
        ↓
Authentication & Favorites
        ↓
AI Coffee Sommelier
        ↓
Testing & Quality
        ↓
Deployment & Portfolio Readiness
```

The production coffee dataset is maintained privately and is not committed to the public GitHub repository.

Supabase PostgreSQL serves as the production application data store.

---

# 3. Phase 1 — Project Foundation

## Goal

Establish the Brewcipe repository, development environments, project structure, and baseline configuration.

## Tasks

### Repository Structure

- [x] Create `frontend/`
- [x] Create `backend/`
- [x] Create `scripts/enrichment/`
- [x] Create `supabase/migrations/`
- [x] Create and confirm `docs/` structure
- [x] Remove obsolete scraper-related directories if present
- [x] Remove local production-data directories from public project structure if present

### Git and Repository Configuration

- [x] Initialize Git repository
- [x] Create GitHub repository
- [x] Connect local repository to GitHub
- [x] Configure `.gitignore`
- [x] Exclude environment files
- [x] Exclude private datasets
- [x] Exclude private data-preparation artifacts
- [x] Confirm no credentials or production data are tracked by Git

### Frontend Foundation

- [x] Initialize React + TypeScript application
- [x] Configure Tailwind CSS
- [x] Configure ESLint
- [x] Configure application routing
- [x] Establish frontend folder structure
- [x] Confirm frontend development server runs successfully

### Backend Foundation

- [x] Create Python virtual environment
- [x] Initialize FastAPI application
- [x] Establish backend folder structure
- [x] Configure environment-variable loading
- [x] Create basic health-check endpoint
- [x] Confirm backend development server runs successfully

### Environment Configuration

- [x] Create local environment templates
- [x] Configure Supabase environment variables
- [x] Document required environment variables without exposing secret values

## Phase 1 — Project Foundation

### Exit Criteria

- [x] Frontend runs locally
- [x] Backend runs locally
- [x] Repository structure matches the current Brewcipe architecture
- [x] GitHub repository is configured
- [x] Private data and credentials are excluded from version control

✅ Phase 1 complete

---

# 4. Phase 2 — Database Foundation

## Goal

Implement the canonical Brewcipe relational database in Supabase.

## Tasks

### Supabase Setup

[x] Create/configure Brewcipe Supabase project
[x] Configure local application/Supabase setup
[x] Confirm database connectivity

### Database Schema

Implement the schema defined in:

`docs/architecture/database-schema-v3.md`

[x] Create geography-related tables
[x] Create coffee/recipe-related tables
[x] Create ingredient-related tables
[x] Create instruction-related tables
[x] Create source/provenance-related tables
[x] Create required relationships
[x] Create primary keys
[x] Create foreign keys
[x] Create uniqueness constraints
[x] Create required indexes

### Database Migrations

[x] Create initial migration files
[x] Store migrations under supabase/migrations/
[x] Verify migrations recreate the schema
[x] Confirm migrations contain schema/reference data, not production coffee records

### Database Validation

[x] Verify required relationships
[x] Verify constraints
[x] Verify nullable fields
[x] Verify expected indexes
[x] Confirm schema matches database-schema-v3.md

## Exit Criteria

[x] Migration files exist in supabase/migrations
[x] Migration files are tracked by Git
[x] npx supabase db reset succeeds
[x] Fresh database rebuild creates the expected Brewcipe tables
[x] npx supabase db diff shows no unintended schema drift

✅ Phase 2 complete

---

# 5. Phase 3 — Production Data Preparation & Import

## Goal

[x] Approved production coffee records exist in Supabase
[x] 194 approved recipes are present
[x] Every recipe has verification metadata
[x] Canonical foreign-key relationships are valid
[x] Ingredient ordering conforms to the model
[x] Instruction sequencing conforms to the model
[x] Representative production records can be retrieved through their canonical relationships

The production dataset itself remains outside the public repository.

## Tasks

### Canonical Mapping

* [x] Map private curated dataset fields to the Brewcipe database schema
* [x] Define mappings for coffee identity fields
* [x] Define geographical mappings
* [x] Define recipe mappings
* [x] Define ingredient mappings
* [x] Define instruction mappings
* [x] Define source/provenance mappings
* [x] Define handling for optional and missing values

### Data Review

* [x] Review records requiring rechecking
* [x] Review normalized or inferred values where necessary
* [x] Verify source attribution required for production records
* [x] Resolve duplicate or conflicting identifiers
* [x] Confirm records satisfy the canonical model

### Validation Tooling

Where useful, create reproducible tooling under `scripts/enrichment/`.

Potential tooling may include:

* [x] schema validation
* [x] identifier validation
* [x] source-field validation
* [ ] unit validation
* [x] duplicate detection
* [x] dataset statistics

Automation should support validation and preparation rather than imply that the production dataset was generated through automated scraping.

### Import Preparation

* [x] Create private transformation/import workflow
* [x] Transform curated records into relational entities
* [x] validate transformed records before import
* [x] ensure private import files are excluded from Git

### Supabase Import

* [x] Import approved coffee records
* [x] Import geographical relationships
* [x] Import recipe data
* [x] Import ingredients
* [x] Import preparation instructions
* [x] Import source/provenance relationships
* [x] Verify imported relationships
* [x] Verify representative records manually

## Exit Criteria

[x] Phase 3 is complete when approved production coffee records are available through Supabase and correctly conform to the Brewcipe canonical database model.

✅ Phase 3 complete

---

# 6. Phase 4 — Backend API

## Goal

Build the FastAPI application layer between Brewcipe clients and Supabase.

## Tasks

### Backend Architecture

[x] Configure backend application structure
[x] Configure Supabase/database access
[x] Create shared configuration
[x] Create request/response models
[x] Establish error-handling approach

### Coffee APIs

[x] Implement coffee listing endpoint
[x] Implement coffee-detail endpoint
[x] Implement pagination where required
[x] Return appropriate not-found responses
[x] Handle database failures appropriately

### Recipe Data

[x] Retrieve recipe information
[x] Retrieve ingredients
[x] Retrieve instructions in sequence
[x] Retrieve geographical context
[x] Retrieve source information where required
[x] Handle optional recipe fields correctly

### API Validation

[x] Validate API response models
[x] Test representative coffee records
[x] Test missing records
[x] Test records containing optional/null fields
[x] Confirm privileged database credentials are not exposed to clients

## Exit Criteria

[x] Frontend can retrieve canonical coffee information
[x] Frontend can retrieve canonical recipe information
[x] Retrieval occurs through FastAPI backend endpoints
[x] Backend endpoints are documented through FastAPI/OpenAPI
[x] Browser CORS access is configured

✅ Phase 4 complete

---

# 7. Phase 5 — Core Frontend Experience

## Goal

Implement the primary Brewcipe coffee discovery and recipe experience.

## Tasks

### Application Shell

- [x] Global navigation
- [x] Page layout
- [x] Responsive behavior
- [x] Shared loading states
- [x] Shared error states
- [x] Empty states

### Coffee Discovery

- [x] Coffee discovery page
- [x] Backend integration
- [x] Coffee records displayed
- [x] Reusable CoffeeCard
- [x] Navigation to recipe details


### Recipe Detail

- [x] Recipe-detail page
- [x] English coffee name
- [x] Native name
- [x] Transliteration
- [x] Geographical information
- [x] Recipe type
- [x] Brewer / brewing method
- [x] Serving information
- [x] Temperature
- [x] Ingredients
- [x] Preparation instructions
- [x] Cultural context
- [x] Source attribution
- [x] Graceful optional-field handling
- [x] Recipe not-found state

## Exit Criteria

[x] Users can browse production coffee records
[x] Discovery page retrieves backend data
[x] Coffee cards navigate to recipe detail
[x] Recipe detail retrieves canonical backend data
[x] Recipe pages present structured, usable information
[x] Optional fields are handled gracefully
[x] Loading/error/not-found states work
[x] Responsive layouts remain usable

✅ Phase 5 complete

---

# 8. Phase 6 — Search & Geographic Discovery

## Goal

Implement the remaining Must Have discovery capabilities defined in the PRD.

## Tasks

### Search

* [x] Implement backend coffee search
* [x] Implement frontend search input
* [x] Search by coffee name
* [x] Display search results
* [x] Implement zero-result state
* [x] Implement search error state

Additional searchable attributes should follow the settled PRD and implementation feasibility.

### Geographic Discovery

* [x] Implement geographical data retrieval
* [x] Build geographic exploration interface
* [x] Allow users to browse by relevant geographic hierarchy
* [x] Display coffees associated with selected locations
* [x] Link geographical results to recipe details
* [x] Handle locations without available recipes

## Exit Criteria

[x] Users can discover recipes through direct search
[x] Search returns relevant production coffee records
[x] Search results navigate to recipe detail
[x] No-result search state is handled gracefully
[x] Users can explore recipes by geography
[x] Continent / region / country navigation works
[x] Geographical filtering returns appropriate recipes
[x] Geography results navigate to recipe detail
[x] Search and geography both retrieve backend production data
[x] Search and geography flows work without CORS/API/console errors
[x] Back navigation remains usable during discovery
[x] Search and geographical exploration remain usable on responsive layouts

✅ Phase 6 complete
---

# 9. Phase 7 — Authentication & Favorites

## Goal

Implement the Should Have account and personalization capabilities defined in the PRD.

## Tasks

### Authentication

* [x] Configure Supabase Auth
* [x] Configure email/password authentication
* [x] Configure Google OAuth provider in Supabase
* [x] Configure Google OAuth credentials and authorized redirect URLs
* [x] Implement registration using email and password
* [x] Implement email/password login
* [x] Implement Sign in with Google
* [x] Handle OAuth callback/session establishment
* [x] Implement logout
* [x] Maintain authenticated session state
* [x] Restore authenticated session after page refresh
* [x] Implement protected actions
* [x] Handle authentication errors
* [x] Handle cancelled or failed Google authentication

### Favorites

* [x] Create favorites database structure if not already included
* [x] Configure appropriate Row Level Security policies
* [x] Implement add-to-favorites operation
* [x] Implement remove-from-favorites operation
* [x] Build saved-favorites view
* [x] Prevent duplicate favorites
* [x] Verify users cannot modify another user's favorites
* [x] Verify favorites persist across sessions

## Exit Criteria

[x] Users can register using supported account methods
[x] Users can log in using email and password
[x] Users can authenticate using Google
[x] Authenticated sessions persist appropriately
[x] Users can log out
[x] Protected actions require authentication
[x] Authenticated users can add and remove favorites
[x] Authenticated users can view their saved coffee collection
[x] Duplicate favorites are prevented
[x] Users cannot access or modify another user's favorites
[x] Favorites persist across authenticated sessions
[x] Failed authentication flows are handled gracefully

✅ Phase 7 complete

---

# 10. Phase 8 — AI Coffee Sommelier

## Goal

Implement the Should Have conversational recommendation capability defined in the PRD.

## Tasks

### AI Foundation

* [x] Select LLM provider — Google Gemini
* [x] Configure server-side API credentials
* [x] Define AI request/response models
* [x] Define recommendation boundaries
* [x] Define grounding strategy using Brewcipe data

### Context Retrieval

* [x] Determine how relevant Brewcipe records are selected
* [x] Retrieve relevant database context
* [x] Format context for LLM requests
* [x] Prevent unnecessary exposure of production data

### Backend Integration

* [x] Create AI Sommelier endpoint
* [x] Construct LLM request
* [x] Send request through backend
* [x] Parse provider response
* [x] Handle provider errors
[x] Limit Sommelier input size
[x] Rate-limit AI Sommelier requests
[x] Implement appropriate usage controls

### Frontend Experience

* [x] Build AI Sommelier interface
* [x] Submit user questions
* [x] Display loading state
* [x] Display recommendations
* [x] Link relevant recommendations to Brewcipe recipes
* [x] Display appropriate failure state

### Validation

* [x] Test preference-based questions
* [x] Test geographical questions
* [x] Test brewing-constraint questions
* [ ] Test queries with no strong Brewcipe match
* [ ] Verify recommendations reference existing recipes where appropriate
* [ ] Verify the LLM does not become the canonical recipe source

## Exit Criteria

Phase 8 is complete when users can request conversational coffee recommendations grounded in Brewcipe's structured data.

# Phase 9 — UI/UX Refinement & Visual Polish

## Goal

Refine Brewcipe's complete frontend experience into a cohesive, responsive, accessible, and portfolio-ready product aligned with the updated Brewcipe design direction:

> **a dark, warm, editorial coffee experience combined with the clarity and efficiency of a modern coffee application.**

The Phase 9 UI refresh should incorporate the approved reference-driven direction documented in `design-direction-v3.md` while preserving Brewcipe's own identity, content hierarchy, dark-first visual system, and product scope.

## Tasks

### Visual Foundation

* [x] Apply the Brewcipe color palette consistently
* [x] Refine typography hierarchy
* [x] Standardize spacing and layout
* [x] Standardize border radius, shadows, borders, and surfaces
* [x] Refine buttons and interactive controls
* [x] Establish consistent content widths and page spacing
* [x] Establish compact, standard, and reading-oriented interface density where appropriate
* [ ] Verify the visual foundation preserves Brewcipe's dark, warm, editorial identity

### Reference-Driven UI Direction

* [x] Apply the approved AeroPress Recipe and iBrew references as directional inspiration
* [x] Translate reference qualities into Brewcipe-specific interface patterns rather than reproducing layouts literally
* [x] Introduce clearer application-oriented structure while preserving Brewcipe's editorial character
* [x] Improve interface density and scanability where appropriate
* [x] Ensure reference-driven changes do not copy external branding, typography, color systems, proprietary icons, exact navigation hierarchies, or feature sets
* [ ] Verify the resulting interface remains recognizably Brewcipe

### Global Application UI

* [x] Implement/refine the responsive primary navigation system
* [x] Implement/refine persistent mobile bottom navigation
* [x] Implement/refine adaptive tablet navigation
* [x] Implement/refine desktop and wide-desktop navigation
* [x] Ensure primary destinations remain consistent across responsive navigation patterns
* [x] Refine application headers and contextual page headers
* [x] Standardize back navigation and contextual header actions
* [x] Refine page containers and responsive layouts
* [x] Ensure persistent navigation does not obscure page content
* [ ] Add/refine footer only where appropriate

### Iconography

* [x] Select and apply a consistent icon family
* [x] Standardize icon sizing and visual weight
* [x] Implement icons for primary navigation
* [x] Refine icon-led actions such as search, favorite, back, close, clear, account, and contextual controls
* [x] Define consistent default, hover, focus, pressed, and selected icon states
* [x] Ensure primary mobile navigation uses clear icon-and-label combinations
* [x] Ensure icon-only actions provide accessible names and adequate interaction targets
* [x] Avoid decorative or inconsistent icon usage

### Shared Application Patterns

* [x] Implement/refine reusable App Header patterns
* [x] Implement/refine Bottom Navigation
* [x] Implement/refine Desktop Navigation
* [x] Implement/refine Navigation Item states
* [x] Implement/refine Search Input patterns
* [x] Implement/refine Section Header patterns
* [x] Implement/refine compact List Row patterns
* [x] Implement/refine Information Row patterns where appropriate
* [ ] Implement/refine tabs or segmented controls only where justified by the information architecture
* [x] Ensure shared application patterns adapt consistently across supported screen sizes

### Coffee Discovery

* [x] Refine the discovery page around the updated application-oriented design direction
* [x] Refine Coffee Card presentation
* [x] Implement/refine compact Coffee Row presentation
* [x] Define when Coffee Cards versus Coffee Rows should be used
* [x] Improve coffee-name, geography, native-name, and metadata hierarchy
* [x] Improve scanability without overusing cards or badges
* [x] Refine search entry points
* [x] Refine search interface
* [x] Refine search results using an appropriate compact or visual presentation
* [x] Refine empty/no-results states
* [x] Verify Coffee Card and Coffee Row variants represent the same canonical coffee entity consistently

### Geographic Discovery

* [x] Refine geographical exploration interface
* [x] Refine Continent pages
* [x] Refine Region pages
* [x] Refine Country pages
* [x] Implement/refine compact geographic row patterns
* [x] Improve navigation between Continent → Region → Country → Coffee
* [x] Preserve visible geographical context where useful
* [x] Avoid unnecessary large-card presentation where compact hierarchical navigation is clearer
* [ ] Verify geographical navigation remains usable across mobile, tablet, and desktop layouts

### Recipe Detail

* [x] Refine the recipe-detail page
* [x] Improve recipe information hierarchy
* [x] Refine recipe-header composition
* [x] Refine recipe metadata presentation
* [x] Refine ingredient presentation
* [x] Refine preparation instructions
* [x] Refine cultural-context presentation
* [x] Refine geographical-context presentation
* [x] Refine source attribution
* [x] Improve readability for long recipe content
* [x] Ensure missing optional data collapses cleanly
* [ ] Establish appropriate desktop/tablet split layouts without compromising reading width
* [x] Ensure recipe-detail layouts remain more spacious than compact application UI where appropriate

### Authentication & Favorites

* [x] Refine registration interface
* [x] Refine login interface
* [x] Refine Google Sign-In presentation
* [x] Refine authenticated-user states
* [x] Refine lightweight Account access
* [x] Refine Favorites page
* [x] Refine Favorite controls and feedback
* [x] Use Coffee Row or Coffee Card presentation according to available space and scanning needs
* [ ] Ensure authentication preserves originating coffee context where practical
* [x] Ensure Favorites remain accessible through the responsive navigation system when included in the release

### AI Sommelier

* [x] Refine AI Coffee Sommelier interface
* [x] Ensure the Sommelier feels like a Brewcipe discovery tool rather than a generic chatbot
* [x] Improve user-prompt layout
* [x] Refine recommendation presentation
* [x] Use Brewcipe-standard Coffee Card or Coffee Row patterns where appropriate
* [x] Preserve clear routes from recommendations to canonical Recipe Detail pages
* [x] Refine loading and failure states
* [x] Ensure AI presentation remains visually secondary to Brewcipe's coffee content

### Interaction & Feedback

* [x] Standardize hover states
* [x] Standardize focus states
* [x] Standardize pressed states
* [x] Standardize active/selected states
* [x] Standardize navigation selected states
* [ ] Standardize tabs/segmented-control selected states where implemented
* [x] Refine loading states
* [x] Refine error states
* [x] Refine empty states
* [x] Add subtle transitions where appropriate
* [x] Ensure selection and state are not communicated through color alone

### Responsive Refinement

* [ ] Review narrow-mobile layouts
* [ ] Review standard-mobile layouts
* [ ] Review tablet layouts
* [x] Review desktop layouts
* [x] Review wide-desktop layouts
* [ ] Verify mobile bottom navigation behavior
* [ ] Verify tablet navigation adaptation
* [x] Verify desktop navigation replacement
* [x] Verify app/header behavior across responsive layouts
* [ ] Verify Coffee Card and Coffee Row responsive behavior
* [ ] Verify discovery grid column changes
* [ ] Verify recipe-detail responsive composition
* [x] Fix overflow and spacing issues
* [x] Verify readable content widths
* [x] Verify wide-screen content remains intentionally bounded
* [x] Verify touch-target usability
* [ ] Verify keyboard usability on larger-screen interfaces
* [ ] Ensure primary actions and destinations remain accessible at all supported screen sizes

### Design Consistency Review

* [x] Compare implementation against `design-direction-v3.md`
* [x] Compare implementation against `design-system-v3.md`
* [x] Compare implementation against `information-architecture-v3.md`
* [x] Compare implementation against `wireframes-v3.md`
* [x] Verify reusable components follow the design system
* [x] Verify navigation follows the approved responsive hierarchy
* [x] Verify iconography is consistent across the application
* [x] Verify Coffee Card and Coffee Row usage is intentional
* [x] Remove inconsistent one-off styling
* [x] Remove unnecessary nested cards and floating surfaces
* [x] Verify visual hierarchy across primary pages
* [x] Verify compact application UI does not compromise recipe readability
* [ ] Verify the interface reflects Brewcipe's intended dark, warm, editorial, modern, application-oriented, and approachable direction
* [ ] Verify reference-driven changes strengthen usability without making Brewcipe resemble a copied third-party application

## Exit Criteria

Phase 9 is complete when:

* [ ] all primary Brewcipe pages follow a consistent visual and interaction system
* [ ] the updated reference-driven UI direction is implemented without compromising Brewcipe's visual identity
* [ ] mobile uses a coherent persistent primary-navigation pattern
* [ ] tablet navigation adapts appropriately to available space
* [ ] desktop and wide-desktop layouts provide equivalent persistent primary navigation
* [ ] application headers and contextual page headers are consistently implemented
* [ ] iconography follows one consistent family, size system, and interaction treatment
* [ ] Coffee Cards, Coffee Rows, geographic rows, and other shared patterns are used consistently and intentionally
* [ ] discovery, search, geography, recipes, authentication, favorites, and AI experiences have been visually refined
* [ ] mobile, tablet, desktop, and wide-desktop layouts are visually usable and coherent
* [ ] reading-heavy content remains comfortably constrained on larger displays
* [ ] loading, error, empty, hover, focus, pressed, selected, and active states are consistently styled
* [ ] reusable components are visually and behaviorally consistent
* [ ] primary navigation destinations remain accessible across responsive layouts
* [ ] the implemented interface aligns with Brewcipe's documented design direction, design system, information architecture, and wireframes
* [ ] no obvious placeholder, prototype, inconsistent, or legacy UI styling remains
* [ ] Brewcipe feels like a dark, warm, editorial coffee product with the clarity and efficiency of a modern coffee application

### Phase 9 Status

Phase 9 implementation complete; manual responsive, authenticated, live-data, and external-service validation remains. See `docs/reports/phase-9-ui-ux-refinement-report.md`.

---

# 10A. Personalization & Recommendation Intelligence

## Goal

Implement the Brewcipe 2.0 Taste Profile Mechanic so that explicit taste preferences and observed coffee interactions can improve future recommendations and Sommelier context.

The mechanic is defined in `taste-profile-mechanic-v1.md`.

## Tasks

### Taste Model

* [x] Define explicit taste preferences: sweet, milky, strong, spiced, simple
* [x] Support brewer preferences
* [x] Support discovery style
* [x] Persist authenticated user taste profiles

### Recipe Intelligence

* [x] Derive qualitative recipe-intelligence signals from structured recipe data
* [x] Support sweet, milky, strong, spiced, chocolate, nutty, citrus, fruity, herbal, hot, iced, simple, and dessert-like signals
* [x] Keep derived signals separate from canonical recipe data
* [x] Avoid unsupported numeric taste scores

### Interaction Learning

* [x] Persist `tried` recipe interactions
* [x] Persist `skipped` recipe interactions
* [x] Translate stored recipe UUIDs to stable Brewcipe recipe identifiers where required by application logic
* [x] Derive learned affinity from tried recipe signals
* [x] Exclude skipped recipes from the Sommelier candidate pool
* [ ] Integrate saved/favorite coffees as an explicit recommendation signal
* [ ] Demonstrate visible recommendation changes after save/try/skip interactions

### Recommendation Engine

* [x] Use taste profile as a primary recommendation input
* [x] Use brewer and discovery preferences in ranking
* [x] Use tried-history affinity in ranking
* [x] Keep recommendation ranking deterministic and testable
* [ ] Complete the Personalized Home recommendation surface

### Sommelier Integration

* [x] Retrieve taste profile for authenticated Sommelier requests
* [x] Retrieve tried and skipped history
* [x] Supply personalized context to Gemini
* [x] Exclude skipped recipes before Gemini candidate selection
* [x] Instruct Gemini to use taste profile and interaction history as personalization context
* [ ] Validate the complete personalized loop with a real authenticated user and live Gemini request

## Current Status

The core personalization backend is implemented and covered by automated tests. The remaining work is to connect saved/favorite behavior into recommendation weighting, expose the recommendation loop through Personalized Home, and verify that user interactions produce observable recommendation changes end to end.

---

# 11. Phase 10 — Testing & Quality Assurance

## Goal

Verify Brewcipe's MVP functionality, security, usability, and reliability.

## Tasks

### Backend Testing

* [ ] Test coffee-list endpoints
* [ ] Test coffee-detail endpoints
* [ ] Test search
* [ ] Test invalid identifiers
* [ ] Test validation failures
* [ ] Test authentication-related operations
* [ ] Test favorites
* [ ] Test AI endpoint behavior
* [ ] register with email/password → save favorite
* [ ] login with email/password → access favorites
* [ ] sign in with Google → save favorite
* [ ] refresh authenticated session → favorites remain accessible
* [ ] logout → protected favorite actions become unavailable

### Frontend Testing

* [ ] Test primary components
* [ ] Test loading states
* [ ] Test error states
* [ ] Test empty states
* [ ] Test recipe rendering with missing optional fields
* [ ] Test authentication flows
* [ ] Test favorites interactions
* [ ] Test AI Sommelier interactions
* [ ] Test email/password authentication flows
* [ ] Test Google authentication flow
* [ ] Test OAuth callback/session restoration

### End-to-End Testing

Test the primary user journeys:

* [ ] browse coffee → open recipe
* [ ] search → open recipe
* [ ] geographic exploration → open recipe
* [ ] register/login → save favorite
* [ ] open favorites → return to recipe
* [ ] ask AI Sommelier → open recommended recipe

### Security and Repository Review

* [ ] Verify secrets are excluded from Git
* [ ] Verify production dataset is excluded from Git
* [ ] Verify private data-preparation artifacts are excluded
* [ ] Verify privileged credentials are server-side
* [ ] Verify authorization rules
* [ ] Verify Row Level Security policies where applicable
* [ ] Review Git history for accidentally committed secrets or private datasets

### UX and Accessibility Review

* [ ] Test responsive layouts
* [ ] Test keyboard navigation
* [ ] Review semantic HTML
* [ ] Review accessible labels
* [ ] Review contrast and readability
* [ ] Test primary journeys on supported screen sizes

## Exit Criteria

Phase 10 is complete when the MVP's primary journeys pass functional testing and no known critical security, privacy, or usability issue prevents release.

---

# 12. Phase 11 — Deployment & Portfolio Readiness

## Goal

Deploy Brewcipe and prepare the public repository for portfolio review.

## Tasks

### Deployment

* [ ] Configure production frontend deployment
* [ ] Configure production backend deployment
* [ ] Configure production environment variables
* [ ] Configure production Supabase connection
* [ ] Verify production application connectivity
* [ ] Verify production authentication
* [ ] Verify AI integration where included in release
* [ ] Perform production smoke test

### Public Repository Review

* [ ] Confirm repository contains no production dataset
* [ ] Confirm repository contains no private research artifacts
* [ ] Confirm repository contains no credentials
* [ ] Confirm `.gitignore` is correct
* [ ] Confirm database migrations are present
* [ ] Confirm repository structure matches documentation
* [ ] Remove obsolete experimental files
* [ ] Remove unused dependencies

### Documentation Review

* [ ] Review `product-idea-v3.md`
* [ ] Review `prd-v3.md`
* [ ] Review `requirementsv-3.md`
* [ ] Review design documentation
* [ ] Review architecture documentation
* [ ] Review database documentation
* [ ] Update development roadmap completion status
* [ ] Create/update root `README.md`

### Portfolio Presentation

* [ ] Write concise project overview
* [ ] Document technology stack
* [ ] Document architecture
* [ ] Document major product decisions
* [ ] Document data privacy boundary
* [ ] Document AI architecture
* [ ] Add application screenshots
* [ ] Add setup instructions
* [ ] Add deployed application link
* [ ] Verify repository can be understood by an external reviewer

## Exit Criteria

Phase 11 is complete when Brewcipe is deployed, documented, secure for public repository access, and understandable to a potential employer or client.

---

# 13. MVP Completion Definition

Brewcipe MVP development is complete when all **Must Have** requirements defined in the PRD have been implemented and verified.

Should Have requirements should be completed according to the project's available capacity and release priorities.

A Should Have requirement that is not completed does not automatically prevent MVP release, but its status should be documented accurately.

Future Considerations defined in the PRD are not part of this roadmap unless they are explicitly reprioritized into the MVP.

---

# 14. Roadmap Maintenance

This roadmap is a living implementation document.

Tasks should be updated as development progresses.

Use:

```text
[ ] Not started / incomplete
[x] Completed and verified
```

Tasks inherited from previous Brewcipe experiments or related coffee projects should not be marked complete unless they have been implemented and verified within the current Brewcipe project.

If implementation reveals that the architecture, requirements, or scope must change, the relevant source documentation should be updated before the roadmap is treated as the new source of truth.
