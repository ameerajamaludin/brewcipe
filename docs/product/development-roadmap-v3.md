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

* [ ] Create `frontend/`
* [ ] Create `backend/`
* [ ] Create `scripts/enrichment/`
* [ ] Create `supabase/migrations/`
* [ ] Create and confirm `docs/` structure
* [ ] Remove obsolete scraper-related directories if present
* [ ] Remove local production-data directories from the public project structure if present

### Git and Repository Configuration

* [ ] Initialize Git repository
* [ ] Create public GitHub repository
* [ ] Connect local repository to GitHub
* [ ] Configure `.gitignore`
* [ ] Exclude environment files
* [ ] Exclude private datasets
* [ ] Exclude private data-preparation artifacts
* [ ] Confirm no credentials or production data are tracked by Git

### Frontend Foundation

* [ ] Initialize React + TypeScript application
* [ ] Configure Tailwind CSS
* [ ] Configure ESLint
* [ ] Configure application routing
* [ ] Establish frontend folder structure
* [ ] Confirm frontend development server runs successfully

### Backend Foundation

* [ ] Create Python virtual environment
* [ ] Initialize FastAPI application
* [ ] Establish backend folder structure
* [ ] Configure environment-variable loading
* [ ] Create basic health-check endpoint
* [ ] Confirm backend development server runs successfully

### Environment Configuration

* [ ] Create local environment templates
* [ ] Configure Supabase environment variables
* [ ] Document required environment variables without exposing secret values

## Exit Criteria

Phase 1 is complete when:

* frontend runs locally
* backend runs locally
* repository structure matches the current Brewcipe architecture
* GitHub repository is configured
* private data and credentials are excluded from version control

---

# 4. Phase 2 — Database Foundation

## Goal

Implement the canonical Brewcipe relational database in Supabase.

## Tasks

### Supabase Setup

* [ ] Create or configure Brewcipe Supabase project
* [ ] Configure local application connection to Supabase
* [ ] Confirm database connectivity

### Database Schema

Implement the schema defined in:

`docs/architecture/database-schema-v3.md`

* [ ] Create geography-related tables
* [ ] Create coffee/recipe-related tables
* [ ] Create ingredient-related tables
* [ ] Create instruction-related tables
* [ ] Create source/provenance-related tables
* [ ] Create required relationships
* [ ] Create primary keys
* [ ] Create foreign keys
* [ ] Create uniqueness constraints
* [ ] Create required indexes

### Database Migrations

* [ ] Create initial migration files
* [ ] Store migrations under `supabase/migrations/`
* [ ] Verify migrations can create the expected schema
* [ ] Confirm migration files contain schema changes rather than production recipe records

### Database Validation

* [ ] Verify required relationships
* [ ] Verify constraints
* [ ] Verify nullable fields match the data model
* [ ] Verify expected indexes
* [ ] Confirm database schema matches architecture documentation

## Exit Criteria

Phase 2 is complete when the Brewcipe production database structure can be created reproducibly from version-controlled migrations.

---

# 5. Phase 3 — Production Data Preparation & Import

## Goal

Prepare the privately maintained coffee dataset for the canonical Brewcipe relational model and import approved records into Supabase.

The production dataset itself remains outside the public repository.

## Tasks

### Canonical Mapping

* [ ] Map private curated dataset fields to the Brewcipe database schema
* [ ] Define mappings for coffee identity fields
* [ ] Define geographical mappings
* [ ] Define recipe mappings
* [ ] Define ingredient mappings
* [ ] Define instruction mappings
* [ ] Define source/provenance mappings
* [ ] Define handling for optional and missing values

### Data Review

* [ ] Review records requiring rechecking
* [ ] Review normalized or inferred values where necessary
* [ ] Verify source attribution required for production records
* [ ] Resolve duplicate or conflicting identifiers
* [ ] Confirm records satisfy the canonical model

### Validation Tooling

Where useful, create reproducible tooling under `scripts/enrichment/`.

Potential tooling may include:

* [ ] schema validation
* [ ] identifier validation
* [ ] source-field validation
* [ ] unit validation
* [ ] duplicate detection
* [ ] dataset statistics

Automation should support validation and preparation rather than imply that the production dataset was generated through automated scraping.

### Import Preparation

* [ ] Create private transformation/import workflow
* [ ] Transform curated records into relational entities
* [ ] validate transformed records before import
* [ ] ensure private import files are excluded from Git

### Supabase Import

* [ ] Import approved coffee records
* [ ] Import geographical relationships
* [ ] Import recipe data
* [ ] Import ingredients
* [ ] Import preparation instructions
* [ ] Import source/provenance relationships
* [ ] Verify imported relationships
* [ ] Verify representative records manually

## Exit Criteria

Phase 3 is complete when approved production coffee records are available through Supabase and correctly conform to the Brewcipe canonical database model.

---

# 6. Phase 4 — Backend API

## Goal

Build the FastAPI application layer between Brewcipe clients and Supabase.

## Tasks

### Backend Architecture

* [ ] Configure backend application structure
* [ ] Configure Supabase/database access
* [ ] Create shared configuration
* [ ] Create request/response models
* [ ] Establish error-handling approach

### Coffee APIs

* [ ] Implement coffee listing endpoint
* [ ] Implement coffee-detail endpoint
* [ ] Implement pagination where required
* [ ] Return appropriate not-found responses
* [ ] Handle database failures appropriately

### Recipe Data

* [ ] Retrieve recipe information
* [ ] Retrieve ingredients
* [ ] Retrieve instructions in sequence
* [ ] Retrieve geographical context
* [ ] Retrieve source information where required
* [ ] Handle optional recipe fields correctly

### API Validation

* [ ] Validate API response models
* [ ] Test representative coffee records
* [ ] Test missing records
* [ ] Test records containing optional/null fields
* [ ] Confirm privileged database credentials are not exposed to clients

## Exit Criteria

Phase 4 is complete when the frontend can retrieve canonical coffee and recipe information through documented backend endpoints.

---

# 7. Phase 5 — Core Frontend Experience

## Goal

Implement the primary Brewcipe coffee discovery and recipe experience.

## Tasks

### Application Shell

* [ ] Implement global navigation
* [ ] Implement page layout
* [ ] Implement responsive behavior
* [ ] Implement shared loading states
* [ ] Implement shared error states
* [ ] Implement empty states

### Coffee Discovery

* [ ] Build coffee discovery page
* [ ] Connect discovery page to backend
* [ ] Display coffee records
* [ ] Build reusable coffee-card component
* [ ] Implement navigation to recipe details

### Recipe Detail

* [ ] Build recipe-detail page
* [ ] Display English coffee name
* [ ] Display native name where available
* [ ] Display transliteration where available
* [ ] Display geographical information
* [ ] Display recipe type
* [ ] Display brewer/brewing method
* [ ] Display serving information
* [ ] Display temperature
* [ ] Display ingredients
* [ ] Display preparation instructions
* [ ] Display cultural context
* [ ] Display source attribution where required
* [ ] Handle missing optional fields gracefully
* [ ] Implement recipe not-found state

## Exit Criteria

Phase 5 is complete when users can browse Brewcipe and navigate from coffee discovery to usable structured recipe pages.

---

# 8. Phase 6 — Search & Geographic Discovery

## Goal

Implement the remaining Must Have discovery capabilities defined in the PRD.

## Tasks

### Search

* [ ] Implement backend coffee search
* [ ] Implement frontend search input
* [ ] Search by coffee name
* [ ] Display search results
* [ ] Implement zero-result state
* [ ] Implement search error state

Additional searchable attributes should follow the settled PRD and implementation feasibility.

### Geographic Discovery

* [ ] Implement geographical data retrieval
* [ ] Build geographic exploration interface
* [ ] Allow users to browse by relevant geographic hierarchy
* [ ] Display coffees associated with selected locations
* [ ] Link geographical results to recipe details
* [ ] Handle locations without available recipes

## Exit Criteria

Phase 6 is complete when users can discover Brewcipe recipes through both direct search and geographical exploration.

---

# 9. Phase 7 — Authentication & Favorites

## Goal

Implement the Should Have account and personalization capabilities defined in the PRD.

## Tasks

### Authentication

* [ ] Configure Supabase Auth
* [ ] Implement registration
* [ ] Implement login
* [ ] Implement logout
* [ ] Maintain authenticated session state
* [ ] Implement protected actions
* [ ] Handle authentication errors

### Favorites

* [ ] Create favorites database structure if not already included
* [ ] Configure appropriate Row Level Security policies
* [ ] Implement add-to-favorites operation
* [ ] Implement remove-from-favorites operation
* [ ] Build saved-favorites view
* [ ] Prevent duplicate favorites
* [ ] Verify users cannot modify another user's favorites
* [ ] Verify favorites persist across sessions

## Exit Criteria

Phase 7 is complete when authenticated users can securely maintain their own saved coffee collection.

---

# 10. Phase 8 — AI Coffee Sommelier

## Goal

Implement the Should Have conversational recommendation capability defined in the PRD.

## Tasks

### AI Foundation

* [ ] Select LLM provider
* [ ] Configure server-side API credentials
* [ ] Define AI request/response models
* [ ] Define recommendation boundaries
* [ ] Define grounding strategy using Brewcipe data

### Context Retrieval

* [ ] Determine how relevant Brewcipe records are selected
* [ ] Retrieve relevant database context
* [ ] Format context for LLM requests
* [ ] Prevent unnecessary exposure of production data

### Backend Integration

* [ ] Create AI Sommelier endpoint
* [ ] Construct LLM request
* [ ] Send request through backend
* [ ] Parse provider response
* [ ] Handle provider errors
* [ ] Handle timeouts
* [ ] Implement appropriate usage controls

### Frontend Experience

* [ ] Build AI Sommelier interface
* [ ] Submit user questions
* [ ] Display loading state
* [ ] Display recommendations
* [ ] Link relevant recommendations to Brewcipe recipes
* [ ] Display appropriate failure state

### Validation

* [ ] Test preference-based questions
* [ ] Test geographical questions
* [ ] Test brewing-constraint questions
* [ ] Test queries with no strong Brewcipe match
* [ ] Verify recommendations reference existing recipes where appropriate
* [ ] Verify the LLM does not become the canonical recipe source

## Exit Criteria

Phase 8 is complete when users can request conversational coffee recommendations grounded in Brewcipe's structured data.

---

# 11. Phase 9 — Testing & Quality Assurance

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

### Frontend Testing

* [ ] Test primary components
* [ ] Test loading states
* [ ] Test error states
* [ ] Test empty states
* [ ] Test recipe rendering with missing optional fields
* [ ] Test authentication flows
* [ ] Test favorites interactions
* [ ] Test AI Sommelier interactions

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

Phase 9 is complete when the MVP's primary journeys pass functional testing and no known critical security, privacy, or usability issue prevents release.

---

# 12. Phase 10 — Deployment & Portfolio Readiness

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

Phase 10 is complete when Brewcipe is deployed, documented, secure for public repository access, and understandable to a potential employer or client.

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
