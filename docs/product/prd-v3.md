# Brewcipe — Product Requirements Document

> **Documentation approach:** This PRD uses Atlassian's Product Requirements Document (PRD) guidance as a structural reference and has been adapted to suit Brewcipe as an independent portfolio product. The structure is therefore intentionally tailored rather than a direct reproduction of the Atlassian template.

---

## 1. PRD Overview

| Item            | Details                       |
| --------------- | ----------------------------- |
| Product         | Brewcipe                      |
| Document        | Product Requirements Document |
| Status          | In Development                |
| Product Type    | Web Application               |
| Owner           | Project Owner                 |
| Target Release  | MVP                           |
| Repository      | Public GitHub repository      |
| Production Data | Private, stored in Supabase   |

### Product Summary

Brewcipe is a global coffee recipe discovery platform that allows users to explore coffee drinks, brewing traditions, preparation methods, and cultural context from around the world.

The platform combines structured coffee recipe data, geographical discovery, search and filtering, user favorites, source attribution, and AI-assisted coffee discovery.

The application uses a React frontend, FastAPI backend, Supabase PostgreSQL database, and an LLM API for the AI Coffee Sommelier.

The production coffee dataset is privately maintained and stored in Supabase. The complete dataset and private data-preparation artifacts are intentionally excluded from the public repository.

---

# 2. Objective

Coffee recipe information is fragmented across websites, countries, languages, and formats.

Users interested in exploring global coffee culture may encounter:

* inconsistent recipe structures
* different naming conventions
* recipes available only in local languages
* inconsistent ingredient measurements
* limited geographical context
* limited cultural context
* difficulty discovering related coffee traditions
* recipe information distributed across multiple sources

Brewcipe aims to organize coffee recipes into a consistent data model and make them discoverable through search, geographical exploration, structured recipe pages, and AI-assisted recommendations.

The product should make global coffee exploration approachable to casual users while retaining enough structured information and provenance to remain useful to coffee enthusiasts.

---

# 3. Goals and Success Metrics

Because Brewcipe is currently an MVP portfolio project without production usage data, the initial success criteria focus primarily on functional completion and usability.

Quantitative product metrics can be established after deployment and real user testing.

| Goal                            | MVP Success Measure                                                                                     |
| ------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Enable global coffee discovery  | Users can browse coffee recipes stored in the production database                                       |
| Make recipes understandable     | Recipe pages consistently present available ingredients, instructions, brewing information, and context |
| Support direct discovery        | Users can search for coffee recipes                                                                     |
| Support geographical discovery  | Users can explore coffees through country or regional relationships                                     |
| Support personalization         | Authenticated users can save and remove favorites                                                       |
| Provide AI-assisted discovery   | Users can ask the AI Coffee Sommelier for recommendations grounded in Brewcipe data                     |
| Preserve provenance             | Coffee records can maintain source attribution where available                                          |
| Protect private product data    | Production datasets and credentials are excluded from the public repository                             |
| Provide a responsive experience | Core user journeys work across supported desktop and mobile layouts                                     |

### Post-Launch Metrics

Once Brewcipe has real users, potential metrics may include:

* search success rate
* recipe-detail views
* favorite-save rate
* AI recommendation engagement
* repeat visits
* geographic exploration usage
* failed or zero-result searches

These are candidate metrics and are not yet validated product KPIs.

---

# 4. Assumptions

The MVP is based on the following assumptions.

## User Assumptions

* Users may know the name of a coffee they want to find, but some will prefer browsing.
* Some users are interested in coffee based on country or cultural origin rather than brewing method alone.
* Users may encounter unfamiliar coffee terminology and therefore benefit from structured, approachable presentation.
* Users may want to save interesting recipes for later.
* Conversational recommendations may help users who do not know what coffee to search for.

## Data Assumptions

* Not every coffee record will contain every possible field.
* Coffee information from different sources varies in terminology, measurement systems, language, and structure.
* Source attribution is valuable for provenance.
* Some source information may require normalization before it can fit Brewcipe's canonical data model.
* The production coffee dataset can remain private without preventing the public repository from demonstrating Brewcipe's architecture and implementation.

## Technical Assumptions

* Supabase PostgreSQL can support the MVP's relational data requirements.
* Supabase Auth can support MVP authentication requirements.
* FastAPI can provide the application API and AI orchestration layer.
* React and TypeScript can support the required frontend experience.
* The LLM should receive relevant Brewcipe data through the backend rather than acting as the application's canonical coffee database.

These assumptions should be revisited as implementation and user testing provide evidence.

---

# 5. Target Users

## Coffee Enthusiasts

Users who actively explore different coffee drinks, brewing methods, and coffee cultures.

**Primary needs:**

* discover unfamiliar recipes
* understand preparation methods
* explore coffee geographically
* access cultural and source context

## Home Brewers

Users looking for coffee recipes they can prepare themselves.

**Primary needs:**

* clear ingredient quantities
* understandable instructions
* brewing equipment information
* serving and temperature information

## Coffee Explorers

Users particularly interested in the geographical and cultural dimensions of coffee.

**Primary needs:**

* browse by country or region
* understand local coffee names
* view transliterations where relevant
* learn cultural context
* discover related coffee traditions

## Casual Coffee Drinkers

Users with limited knowledge of coffee terminology.

**Primary needs:**

* approachable discovery
* simple search
* understandable recipe presentation
* recommendation assistance

---

# 6. Requirements and User Stories

Brewcipe uses the **MoSCoW prioritization method** to classify requirements for the MVP.

The prioritization approach is guided by the MoSCoW framework described in the referenced Atlassian Community article.

For this PRD:

| Priority        | Meaning in Brewcipe                                                                                               |
| --------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Must Have**   | Critical to the Brewcipe MVP. Without these requirements, the MVP would not meet its core purpose.                |
| **Should Have** | Important and high-value requirements, but the MVP can still function without them if they must be deferred.      |
| **Could Have**  | Desirable requirements that may be included when time and resources permit without affecting MVP success.         |
| **Won't Have**  | Requirements intentionally excluded from the current MVP delivery. They may be reconsidered for a future release. |

Priorities should be reviewed as the project evolves. A requirement may move between categories when implementation constraints, user feedback, or new information changes its relative importance.

The MVP should avoid treating every desirable feature as a **Must Have**. Must Have requirements are reserved for capabilities necessary for Brewcipe to deliver its core coffee discovery experience.

---

## 6.1 Coffee Discovery

**MoSCoW Priority:** Must Have

### User Story

As a coffee explorer, I want to browse available coffee recipes so that I can discover coffees I may not already know.

### Requirements

The system must:

* retrieve coffee records through the backend
* display relevant discovery information
* allow users to open individual coffee recipes
* provide loading states
* provide appropriate error and empty states
* support responsive presentation

### Acceptance Criteria

* available coffee records can be retrieved from Supabase through the backend
* users can browse available coffees
* users can navigate from discovery views to recipe details
* failed requests display appropriate feedback

---

## 6.2 Structured Recipe Detail

**MoSCoW Priority:** Must Have

### User Story

As a home brewer, I want recipe information presented consistently so that I can understand how a coffee is prepared even when the original sources use different formats.

### Recipe Information

A coffee record may include:

* English name
* native name
* transliteration
* country
* region
* recipe type
* brewing method or brewer
* servings
* temperature
* ingredients
* preparation instructions
* cultural context
* source attribution

Not every field is required for every coffee record.

### Requirements

The system must:

* retrieve recipes using stable identifiers
* present available ingredients clearly
* present preparation steps in the correct order
* support optional recipe fields
* display geographical and cultural information where available
* represent source attribution where appropriate

### Acceptance Criteria

* valid recipe identifiers return the appropriate recipe
* invalid identifiers return a not-found state
* missing optional fields do not break the interface
* ingredients and instructions maintain their expected order

---

## 6.3 Search

**MoSCoW Priority:** Must Have

### User Story

As a user who already has something in mind, I want to search the coffee library so that I can find relevant recipes without browsing the entire collection.

### Requirements

Search must support coffee-name discovery.

Search should additionally support relevant attributes where available, such as:

* native name
* country
* region
* brewing method
* recipe type

### Acceptance Criteria

* users can submit a search query
* relevant results are returned
* zero-result searches display an appropriate state
* frontend search does not require direct database access

---

## 6.4 Geographical Exploration

**MoSCoW Priority:** Must Have

### User Story

As a coffee explorer, I want to browse coffee geographically so that I can discover coffee traditions associated with different parts of the world.

### Geographical Model

```text
Continent
    ↓
Region
    ↓
Country
    ↓
Coffee
```

### Requirements

The system must:

* associate coffees with relevant geographical entities
* maintain geographical relationships in the database
* allow users to discover coffees through geographical information

### Acceptance Criteria

* coffee records can be associated with countries
* geographical relationships can be retrieved
* geographical navigation leads users to relevant coffee records

---

## 6.5 Authentication

**MoSCoW Priority:** Should Have

### User Story

As a returning user, I want an account so that Brewcipe can provide user-specific functionality such as saved favorites.

### Requirements

The system should support:

* registration
* login
* logout
* authenticated sessions
* protected user-specific operations

### Acceptance Criteria

* users can create an account
* valid users can authenticate
* authenticated state can be determined by the application
* protected actions require authentication

---

## 6.6 Favorites

**MoSCoW Priority:** Should Have

### User Story

As an authenticated user, I want to save coffees that interest me so that I can return to them later.

### Requirements

Authenticated users should be able to:

* add a coffee to favorites
* remove a coffee from favorites
* view saved coffees
* retain favorites across sessions

### Acceptance Criteria

* favorites belong to the authenticated user
* duplicate favorite relationships are prevented
* users cannot modify another user's favorites
* favorites persist in the database

---

## 6.7 AI Coffee Sommelier

**MoSCoW Priority:** Should Have

### User Story

As a user who does not know exactly what to search for, I want to describe my coffee preferences conversationally so that Brewcipe can recommend relevant coffees.

Example queries may include:

* "I want something sweet and iced."
* "What coffee should I try from Malaysia?"
* "I like strong coffee but don't have an espresso machine."
* "Recommend something similar to Vietnamese coffee."

### Requirements

The system should:

* accept coffee-related natural-language queries
* retrieve relevant Brewcipe data
* send relevant context to the LLM through the backend
* return understandable recommendations
* reference Brewcipe recipes where relevant
* handle provider failures gracefully

The LLM must not function as Brewcipe's canonical coffee database.

### Acceptance Criteria

* users can submit coffee-related questions
* AI requests are processed through the backend
* relevant Brewcipe data can be provided as grounding context
* recommendations can reference existing Brewcipe recipes
* API credentials remain server-side
* provider errors return an appropriate response

---

## 6.8 Could Have Requirements

No requirements are currently classified as **Could Have** for the Brewcipe MVP.

Requirements may be moved into this category during future prioritization if they are considered desirable for the MVP but are not necessary for its success.

---

## 6.9 Won't Have for MVP

**MoSCoW Priority:** Won't Have

Brewcipe recognizes additional capabilities that may provide value but are intentionally excluded from the current MVP delivery.

Under the MoSCoW prioritization used in this PRD, **Won't Have** does not necessarily mean that a requirement is permanently rejected. It means that the requirement is not planned for the current MVP and may be reconsidered for a future release.

The complete MVP exclusions and scope boundaries are defined in **Section 11 — Out of Scope for MVP**.

This keeps the MoSCoW prioritization aligned with the PRD's scope definition without maintaining duplicate requirement lists.

---

# 7. Data Requirements

## 7.1 Canonical Application Data

Supabase PostgreSQL serves as Brewcipe's canonical production data store.

The relational model should support application entities including:

* coffee recipes
* geographical entities
* ingredients
* preparation instructions
* sources
* users
* favorites

Detailed implementation is defined separately in the database architecture documentation.

---

## 7.2 Data Provenance

Where applicable, coffee records should retain source information.

Normalized or interpreted information should not be represented as though it were necessarily stated directly by an original source.

---

## 7.3 Initial Data Preparation

The initial Brewcipe coffee library was created through manual research, extraction, normalization, and curation using publicly available coffee recipe sources.

Source information varied in terminology, measurement systems, recipe structure, language, geographical specificity, and cultural context.

The initial preparation process therefore prioritized consistency, provenance, and reviewability.

Private research, preparation, and intermediate data artifacts are outside the public application repository.

---

## 7.4 Public Repository Data Boundary

The public repository may contain:

* database migrations
* schema definitions
* application data models
* validation and enrichment logic
* API models
* technical documentation
* synthetic example records where required

The public repository should not contain:

* the complete production coffee dataset
* private research notes
* intermediate curation artifacts
* private data-import files
* credentials or privileged configuration

Production coffee records are maintained privately and stored in Supabase.

---

# 8. Technical Constraints

The current MVP is designed around the following technology choices.

| Layer          | Technology                      | Responsibility                                        |
| -------------- | ------------------------------- | ----------------------------------------------------- |
| Frontend       | React, TypeScript, Tailwind CSS | Interface, navigation and user interactions           |
| Backend        | FastAPI, Python                 | APIs, validation, business logic and AI orchestration |
| Database       | Supabase PostgreSQL             | Canonical application data and relational integrity   |
| Authentication | Supabase Auth                   | User authentication                                   |
| AI             | LLM API via backend             | Conversational recommendations                        |

### Security Constraints

The application must:

* keep secrets outside version control
* use environment variables for credentials
* prevent privileged credentials from reaching frontend code
* validate backend requests
* enforce authorization for user-specific resources
* use Row Level Security where appropriate
* exclude private production datasets from the public repository

---

# 9. User Experience and Supporting Design

Detailed UX and interface decisions are maintained separately to prevent the PRD from duplicating design documentation.

Supporting documentation includes:

* `docs/design/information-architecture.md`
* `docs/design/wireframes.md`
* `docs/design/design-direction.md`
* `docs/design/design-system.md`

Technical implementation details are maintained in:

* `docs/architecture/technical-architecture.md`
* `docs/architecture/database-schema.md`
* `docs/architecture/coffee-data-schema.md`

Implementation sequencing is maintained in:

* `docs/product/development-roadmap.md`

These documents should remain consistent with the requirements defined in this PRD.

---

# 10. Open Questions

Open questions should be recorded rather than silently converted into requirements before a decision has been made.

| Question                                                                                             | Status | Decision |
| ---------------------------------------------------------------------------------------------------- | ------ | -------- |
| Which search filters are necessary beyond basic text search for MVP?                                 | Open   | TBD      |
| Should geographical exploration use an interactive map in MVP or a simpler region/country interface? | Open   | TBD      |
| How much cultural context should appear directly on recipe cards versus recipe-detail pages?         | Open   | TBD      |
| Which LLM provider will be used for the AI Coffee Sommelier?                                         | Open   | TBD      |
| What amount of Brewcipe context should be supplied to the LLM for each recommendation request?       | Open   | TBD      |
| Should source attribution be visible directly on recipe pages in MVP?                                | Open   | TBD      |

Questions should be updated with their decision when resolved.

---

# 11. Out of Scope for MVP

The following capabilities are intentionally excluded from the current Brewcipe MVP.

Under the MoSCoW prioritization defined in **Section 6 — Requirements and User Stories**, these items are classified as **Won't Have** for the current delivery.

* unrestricted public recipe submissions
* community moderation workflows
* social networking features
* e-commerce functionality
* payment processing
* professional coffee certification
* automated web scraping as a production ingestion pipeline
* automated publication of externally collected recipes
* public distribution of Brewcipe's complete production coffee dataset
* public access to private research, curation, or data-preparation artifacts

These exclusions define the boundary of the current MVP rather than the permanent scope of Brewcipe.


---

# 12. Future Considerations

The following capabilities may be considered after the Brewcipe MVP has been implemented and evaluated.

Their inclusion in this section does not represent a committed requirement or delivery timeline. Future capabilities should be evaluated based on user needs, product evidence, technical feasibility, and their contribution to Brewcipe's product goals.

* advanced search and filtering
* richer geographical visualization
* related coffee recommendations
* recipe comparison
* multilingual interfaces
* personalized recommendation profiles
* recommendation signals based on user preferences and interactions
* community recipe contributions
* admin moderation workflows
* brewing equipment recommendations
* richer educational coffee content
* administrative content-management interfaces
* assisted data enrichment
* automated data validation
* candidate recipe discovery
* improved provenance management
* source-monitoring workflows
* improved contextual recommendations
* personalization of AI Coffee Sommelier responses
* richer integration between structured Brewcipe data and conversational discovery

Future automation may support data-management workflows where it improves efficiency without bypassing Brewcipe's requirements for normalization, provenance, review, and data quality.

---

# 13. References

This PRD uses Atlassian's Product Requirements Document guidance as a structural reference and adapts it to Brewcipe's scope as an independently developed portfolio product.

Requirement prioritization uses the **MoSCoW method**, guided by the referenced Atlassian Community article. The prioritization categories have been applied specifically to Brewcipe's MVP requirements and may be reviewed as the project evolves.

## PRD Guidance

**Atlassian — Product requirements document (PRD) template**
https://www.atlassian.com/software/confluence/templates/product-requirements

**Atlassian — What is a Product Requirements Document (PRD)?**
https://www.atlassian.com/agile/product-management/requirements

## Prioritization Guidance

**Atlassian Community — Understanding the MoSCoW prioritization | How to implement it into your project**
Author: Lucas / DevSamurai
Published: August 30, 2023
https://community.atlassian.com/forums/App-Central-articles/Understanding-the-MoSCoW-prioritization-How-to-implement-it-into/ba-p/2463999

