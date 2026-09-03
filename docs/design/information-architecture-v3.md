# Brewcipe — Information Architecture

## 1. Overview

### 1.1 Purpose

This document defines the user-facing information architecture for the Brewcipe MVP.

It describes:

* the major content areas within Brewcipe
* the hierarchy between those areas
* the core page and view inventory
* how users move between coffee discovery experiences
* how geographical coffee information is organized
* which experiences are public or authenticated
* the relationship between search, discovery, recipes, favorites, and the AI Coffee Sommelier

This document defines **information structure and navigation relationships**, not detailed page layouts or visual styling.

---

### 1.2 Scope

This document covers the current Brewcipe MVP capabilities:

* coffee discovery
* structured recipe detail
* search
* geographical exploration
* authentication
* favorites
* AI Coffee Sommelier

Detailed visual presentation belongs in:

* `design-direction-v3.md`
* `design-system-v3.md`
* `wireframes-v3.md`

Detailed product scope remains governed by:

* `prd-v3.md`
* `requirements-v3.md`

Technical routes and implementation details belong in Brewcipe's frontend and technical architecture documentation.

---

# 2. Information Architecture Principles

## 2.1 Coffee First

Brewcipe should organize the application around coffee discovery and recipe information.

Supporting features such as accounts and favorites should not dominate the product structure.

---

## 2.2 Discovery Without Authentication

Users should be able to access Brewcipe's core public coffee content without creating an account.

Public experiences include:

* browsing available coffees
* searching for coffee
* geographical exploration
* opening recipe details
* using public discovery experiences

Authentication should only be required when functionality depends on persistent user-specific data.

---

## 2.3 Multiple Discovery Paths, One Coffee Library

Users may approach Brewcipe differently.

For example:

```text
"I want to browse."
        ↓
Coffee Discovery

"I know the coffee name."
        ↓
Search

"I want to explore somewhere."
        ↓
Geographical Exploration

"I don't know what I want."
        ↓
AI Coffee Sommelier
```

These experiences should lead back to the same canonical Brewcipe coffee and recipe library rather than behaving as separate content systems.

---

## 2.4 Structured Geography

Geographical discovery follows Brewcipe's established hierarchy:

```text
Continent
    ↓
Region
    ↓
Country
    ↓
Coffee
```

The interface should expose geographical relationships without requiring users to understand the underlying database structure.

---

## 2.5 Progressive Disclosure

Users should initially see the information required to make their next decision.

Detailed recipe, geographical, cultural, and provenance information should appear when relevant rather than overwhelming discovery views.

---

## 2.6 Optional Data Should Remain Optional

Not every coffee record contains every possible field.

The information architecture should allow unavailable optional information to disappear gracefully without creating empty or misleading content areas.

---

## 2.7 AI Is an Additional Discovery Path

The AI Coffee Sommelier should supplement normal discovery and search.

Core coffee content must remain accessible without using AI.

---

# 3. High-Level Product Structure

The Brewcipe MVP is organized around the following major areas:

```text
Brewcipe
│
├── Home
│
├── Discover
│   │
│   ├── Coffee Library
│   │   └── Coffee / Recipe Detail
│   │
│   └── Geographical Exploration
│       └── Continent
│           └── Region
│               └── Country
│                   └── Coffee / Recipe Detail
│
├── Search
│   └── Search Results
│       └── Coffee / Recipe Detail
│
├── AI Coffee Sommelier
│   └── Recommended Coffee
│       └── Coffee / Recipe Detail
│
├── Favorites
│   └── Coffee / Recipe Detail
│
└── Authentication
```

Authentication and Favorites are **Should Have** capabilities.

If they are deferred from the first MVP release, the core Coffee Discovery, Recipe Detail, Search, and Geographical Exploration structure remains intact.

---

# 4. Primary Content Model

At the user-facing level, Brewcipe's core information model can be represented as:

```text
Coffee
│
├── Names
│   ├── English name
│   ├── Native name
│   └── Transliteration
│
├── Geography
│   ├── Continent
│   ├── Region
│   └── Country
│
├── Recipe Information
│   ├── Recipe type
│   ├── Brewer / brewing method
│   ├── Servings
│   ├── Temperature
│   ├── Ingredients
│   └── Preparation instructions
│
├── Context
│   └── Cultural context
│
└── Provenance
    └── Source information
```

Not every coffee must contain every optional field.

---

# 5. Primary Navigation Model

The final navigation component and exact labels should be validated during wireframing.

At the information-architecture level, Brewcipe requires persistent access to the major product areas:

```text
Home
Discover
Search
AI Coffee Sommelier
Favorites
Account / Authentication
```

However:

* Favorites only requires prominent navigation if the feature is included in the release
* account access may be separated from the primary content navigation
* Search may be represented as a dedicated destination, a global action, or both
* the AI Coffee Sommelier may use a shorter interface label such as `Ask`

The exact mobile and desktop presentation should not be fixed by the IA document.

---

# 6. Home

## 6.1 Purpose

Home acts as Brewcipe's primary entry point.

It should help users begin discovering coffee without requiring them to understand the complete site structure.

---

## 6.2 Primary Entry Points

Home should provide clear access to the core discovery paths:

```text
Home
│
├── Browse Coffees
├── Search
├── Explore Geographically
└── Ask the AI Coffee Sommelier
```

If Favorites is implemented, authenticated users may also have a route back to saved coffees.

---

## 6.3 Content Priority

Home should prioritize useful discovery over general marketing content.

The exact homepage content modules and layout belong to `wireframes-v3.md`.

---

# 7. Discover

## 7.1 Purpose

Discover is the main browsing experience for users who do not have a specific coffee in mind.

---

## 7.2 Core Structure

```text
Discover
│
├── Coffee Library
│
└── Geographical Exploration
```

Coffee records may expose useful attributes such as:

* country
* region
* recipe type
* brewing method

where those attributes are available.

These attributes do not automatically require separate dedicated browsing hierarchies.

---

# 8. Coffee Library

## 8.1 Purpose

Allow users to browse available Brewcipe coffee records.

---

## 8.2 Discovery Items

Each coffee discovery item should provide enough information for users to distinguish it from other coffees.

Potential identifying information may include:

* English name
* native name where appropriate
* country
* relevant recipe or brewing information
* imagery where available

Exact card anatomy belongs to the design system and wireframes.

---

## 8.3 Navigation

```text
Coffee Library
        ↓
Coffee
        ↓
Recipe Detail
```

Selecting a coffee should lead to its structured recipe-detail experience.

---

# 9. Geographical Exploration

## 9.1 Purpose

Allow users to discover coffee through geographical relationships.

---

## 9.2 Geographic Hierarchy

Brewcipe uses:

```text
Continent
    ↓
Region
    ↓
Country
    ↓
Coffee
```

Example:

```text
Asia
    ↓
Southeast Asia
    ↓
Vietnam
    ↓
Cà phê vợt
```

Only geographical entities relevant to available Brewcipe content need to be surfaced.

---

## 9.3 Geographic Entry Experience

The initial geographical exploration experience should allow users to begin navigating Brewcipe's geography.

The exact presentation remains open.

It may eventually use:

* hierarchical lists
* visual geographic groups
* map-supported exploration
* another suitable navigation pattern

The IA defines the relationships, not the visualization technique.

---

# 10. Continent

## 10.1 Purpose

Represent the highest level of Brewcipe's user-facing geographical hierarchy.

---

## 10.2 Content

A Continent view may expose:

* continent identity
* available regions
* coffee content associated with the selected geography where appropriate

Example:

```text
Asia

Southeast Asia
East Asia
South Asia
...
```

Only regions represented by Brewcipe content need to appear.

---

# 11. Region

## 11.1 Purpose

Allow users to move from a broad geographical area toward represented countries.

Example:

```text
Southeast Asia

Vietnam
Thailand
Malaysia
Indonesia
Singapore
...
```

---

## 11.2 Navigation

```text
Continent
    ↓
Region
    ↓
Country
```

---

# 12. Country

## 12.1 Purpose

Allow users to discover coffees associated with a particular country.

Example:

```text
Vietnam

Cà phê vợt
Cà phê kho
...
```

Coffee names should preserve their native representation where available.

---

## 12.2 Navigation

```text
Country
    ↓
Coffee
    ↓
Recipe Detail
```

---

# 13. Coffee / Recipe Detail

## 13.1 Purpose

Provide the complete available structured information needed to understand and prepare a Brewcipe coffee.

This is one of Brewcipe's primary content destinations.

---

## 13.2 Information Hierarchy

The recipe detail experience may contain:

```text
Coffee Identity
│
├── English name
├── Native name
├── Transliteration
└── Geographical information

Recipe Information
│
├── Recipe type
├── Brewer / brewing method
├── Servings
└── Temperature

Ingredients

Preparation Instructions

Cultural Context

Source Attribution
```

Only available information should be displayed.

---

## 13.3 Optional Information

Missing optional fields should not produce:

* empty sections
* placeholder values such as `N/A`
* broken layouts
* misleading assumptions

The surrounding information hierarchy should adapt naturally.

---

## 13.4 Source Attribution

Brewcipe's data model supports source attribution.

Whether source attribution is visibly presented directly on the MVP recipe page remains subject to the current product-design decision.

The IA should preserve a place for provenance without prematurely deciding the exact interface treatment.

---

## 13.5 Related Actions

Depending on implemented scope, recipe detail may provide access to:

```text
Favorite
Geographical context
AI recommendation context
```

Related-coffee recommendations are not required for the current MVP.

---

# 14. Search

## 14.1 Purpose

Allow users who know what they are looking for to find relevant coffee without browsing the full library.

---

## 14.2 Core Search

MVP search must support coffee-name discovery.

Users should be able to submit a query such as:

```text
Café de olla
```

or another coffee name.

---

## 14.3 Additional Search Attributes

The PRD permits additional searchable attributes where available, but advanced search and filtering are not required for the core MVP.

Possible future or optional attributes may include:

* native name
* country
* region
* brewing method
* recipe type

The IA should not require dedicated filter interfaces until those capabilities are intentionally included.

---

# 15. Search Results

## 15.1 Purpose

Present coffee records relevant to a submitted query.

---

## 15.2 Result Structure

Each result should contain sufficient identifying information to distinguish it from other results.

Conceptually:

```text
Search Results

Coffee
Coffee
Coffee
...
```

Selecting a result opens the corresponding recipe detail.

---

## 15.3 Zero-Result State

When no coffee matches the query, the experience should provide:

* a clear explanation
* an opportunity to modify the search
* a route back to discovery where useful

Exact content belongs to the wireframes and content design.

---

# 16. AI Coffee Sommelier

## 16.1 Purpose

Provide conversational coffee discovery for users who do not know exactly what they want to search for.

---

## 16.2 Entry

Users should be able to submit a coffee-related natural-language request.

Examples may include:

```text
"I want something sweet and iced."

"What coffee should I try from Malaysia?"

"I like strong coffee but don't have an espresso machine."
```

---

## 16.3 Recommendation Structure

The AI Coffee Sommelier may return:

```text
Recommendation
│
├── Suggested coffee
├── Explanation
└── Route to Brewcipe recipe
```

When a relevant Brewcipe recipe exists, recommendations should provide a clear path to that canonical recipe.

---

## 16.4 IA Boundary

The AI response itself is not a separate source of canonical recipe content.

The structural relationship is:

```text
User Request
      ↓
AI Coffee Sommelier
      ↓
Recommendation
      ↓
Brewcipe Coffee / Recipe Detail
```

---

# 17. Authentication

## 17.1 Purpose

Support user-specific Brewcipe functionality.

Authentication is not required for basic coffee discovery.

---

## 17.2 Authentication Capabilities

The current product requirements support:

```text
Registration
Login
Logout
Authenticated Session
Protected Actions
```

The exact authentication provider interaction and interface flow belong to implementation and interaction design.

---

## 17.3 Authentication Trigger

Authentication should be introduced when a user attempts functionality that requires an authenticated identity.

For example:

```text
Unauthenticated User
        ↓
Attempts to Favorite Coffee
        ↓
Authentication Required
        ↓
Successful Authentication
        ↓
Return to Relevant Context
```

The exact post-authentication behavior should be confirmed during wireframing.

---

# 18. Favorites

## 18.1 Access

Authenticated users only.

---

## 18.2 Purpose

Provide access to coffees intentionally saved by the current user.

---

## 18.3 Structure

```text
Favorites
    ↓
Saved Coffee
    ↓
Recipe Detail
```

Favorites should reuse Brewcipe's standard coffee presentation rather than creating an unrelated dashboard-style experience.

---

## 18.4 Empty State

When a user has not saved any coffees, the page should:

* communicate that no favorites are currently saved
* provide a clear route back to coffee discovery

---

# 19. Account Access

Brewcipe requires a way for users to:

* authenticate
* understand whether they are authenticated
* log out

A dedicated profile-management page is **not currently required** by the MVP requirements.

If later product requirements introduce account settings or user-profile information, the IA can be expanded accordingly.

---

# 20. Page and View Inventory

The following represents the current Brewcipe MVP information architecture.

| ID    | Page / View               | Access              | Priority    | Primary Purpose                          |
| ----- | ------------------------- | ------------------- | ----------- | ---------------------------------------- |
| IA-01 | Home                      | Public              | Core        | Entry into Brewcipe discovery            |
| IA-02 | Discover / Coffee Library | Public              | Must Have   | Browse available coffees                 |
| IA-03 | Geographic Explore        | Public              | Must Have   | Enter geographical discovery             |
| IA-04 | Continent                 | Public              | Must Have   | Browse relevant regions                  |
| IA-05 | Region                    | Public              | Must Have   | Browse relevant countries                |
| IA-06 | Country                   | Public              | Must Have   | Browse coffees associated with a country |
| IA-07 | Coffee / Recipe Detail    | Public              | Must Have   | Understand and prepare a coffee          |
| IA-08 | Search                    | Public              | Must Have   | Submit a coffee search                   |
| IA-09 | Search Results            | Public              | Must Have   | View matching coffees                    |
| IA-10 | AI Coffee Sommelier       | Public              | Should Have | Conversational coffee discovery          |
| IA-11 | Favorites                 | Authenticated       | Should Have | View saved coffees                       |
| IA-12 | Authentication            | Public / Contextual | Should Have | Register or authenticate                 |

A single application route may support more than one IA state.

For example, Search and Search Results may be implemented within one route or interface.

The IA inventory describes conceptual user-facing states rather than requiring a one-to-one relationship with frontend files.

---

# 21. Dynamic Content Templates

Geographical entities and coffee records should use reusable templates rather than requiring separately designed pages for every database record.

Conceptually:

```text
Continent Template
        ↓
selected continent data

Region Template
        ↓
selected region data

Country Template
        ↓
selected country data

Recipe Template
        ↓
selected coffee data
```

This allows Brewcipe's content library to grow without creating new page designs for every coffee or location.

---

# 22. Content Hierarchy

At a high level:

```text
Brewcipe Coffee Library
│
├── General Discovery
│   └── Coffee
│       └── Recipe Detail
│
├── Search
│   └── Coffee
│       └── Recipe Detail
│
├── Geography
│   └── Continent
│       └── Region
│           └── Country
│               └── Coffee
│                   └── Recipe Detail
│
└── AI Coffee Sommelier
    └── Recommendation
        └── Coffee
            └── Recipe Detail
```

Favorites provide a user-specific return path to existing coffee records rather than creating duplicate recipe content.

---

# 23. Core User Journeys

## 23.1 Browse Coffee

```text
Home
    ↓
Discover
    ↓
Coffee
    ↓
Recipe Detail
```

---

## 23.2 Browse by Geography

```text
Home
    ↓
Geographic Explore
    ↓
Continent
    ↓
Region
    ↓
Country
    ↓
Coffee
    ↓
Recipe Detail
```

---

## 23.3 Search by Name

```text
Home / Search Entry
        ↓
Search
        ↓
Search Results
        ↓
Coffee
        ↓
Recipe Detail
```

---

## 23.4 Ask the Sommelier

```text
Home / Navigation
        ↓
AI Coffee Sommelier
        ↓
Recommendation
        ↓
Coffee
        ↓
Recipe Detail
```

---

## 23.5 Save a Coffee

```text
Recipe Detail
        ↓
Favorite
        ↓
Authentication
(if required)
        ↓
Saved
        ↓
Favorites
```

---

## 23.6 Return to a Saved Coffee

```text
Favorites
    ↓
Saved Coffee
    ↓
Recipe Detail
```

---

# 24. Navigation Rules

## NAV-001 — Core Navigation

Users should have a clear route to Brewcipe's primary discovery experiences.

---

## NAV-002 — Coffee Destination

Coffee discovery, search results, geographical results, favorites, and relevant AI recommendations should resolve to the canonical coffee / recipe detail experience.

---

## NAV-003 — Public Discovery

Users should not be required to authenticate before accessing core public coffee content.

---

## NAV-004 — AI Independence

Core coffee content should remain discoverable through normal browsing and search without requiring AI interaction.

---

## NAV-005 — Geographic Context

Where useful, recipe and geographical views should allow users to understand a coffee's location within Brewcipe's geographical hierarchy.

Conceptually:

```text
Asia
→ Southeast Asia
→ Vietnam
→ Cà phê vợt
```

The exact breadcrumb or navigation treatment belongs to interaction design.

---

## NAV-006 — Consistent Terminology

The same concept should use consistent product terminology throughout Brewcipe.

For example, if the canonical term is:

```text
Favorites
```

the product should not arbitrarily alternate between:

```text
Favorites
Saved
Bookmarks
My Coffees
```

unless those labels intentionally describe different concepts.

---

## NAV-007 — Preserve Context

When users move into temporary or supporting flows such as authentication, Brewcipe should preserve relevant context where practical so they can continue their original task.

---

# 25. URL and Routing Considerations

Information architecture should support predictable and human-readable navigation.

Conceptually, route families may correspond to:

```text
home

discover

coffee
    └── coffee identifier

geography
    ├── continent
    ├── region
    └── country

search

sommelier

favorites

authentication
```

Exact URL patterns, slugs, route parameters, and routing implementation belong to frontend and technical architecture decisions.

The IA should not prescribe implementation-specific paths unless those routes later become part of a deliberate product decision.

---

# 26. MVP IA Boundaries

The current information architecture does not require dedicated experiences for:

* brewing-method directories
* brewing-method detail pages
* equipment directories
* advanced filter pages
* related-coffee recommendation pages
* recipe comparison
* interactive coffee maps
* community recipes
* public recipe submission
* social feeds
* comments
* reviews
* ratings
* coffee journals
* brewing history
* interactive brewing timers
* smart recipe scaling
* shopping
* administrative content management
* extensive user profiles

Some of these may become future capabilities if the PRD is updated.

Brewing method remains valid recipe information and may support search or discovery where available without requiring a dedicated page hierarchy.

---

# 27. Open IA Decisions

The following product questions remain intentionally unresolved.

| Decision                                                            | Current Status         |
| ------------------------------------------------------------------- | ---------------------- |
| Exact primary navigation labels                                     | TBD during wireframing |
| Mobile navigation pattern                                           | TBD during wireframing |
| Desktop navigation pattern                                          | TBD during wireframing |
| Dedicated Search page versus integrated global search               | TBD                    |
| Geographic list versus richer visual/map exploration                | TBD                    |
| Which search attributes beyond coffee name belong in MVP            | TBD                    |
| How much cultural context appears in discovery versus recipe detail | TBD                    |
| Exact visible treatment of source attribution                       | TBD                    |
| Exact post-authentication return behavior                           | TBD                    |
| Final account/authentication presentation                           | TBD                    |

Open decisions should remain visible until intentionally resolved.

---

# 28. Relationship to Wireframes

This document defines **what information and destinations exist**.

The wireframes should determine:

* where navigation controls are placed
* how Home is composed
* how coffee cards are arranged
* how geographic hierarchy is presented
* whether Search occupies a page, overlay, field, or combination
* how recipe information is visually ordered
* how Favorites and Sommelier interactions work
* how mobile and desktop layouts differ

The wireframes should not introduce new product capabilities without corresponding product requirements.

---

# 29. Information Architecture Goal

Brewcipe should allow users to approach its coffee library through several natural entry points:

```text
"I want to browse."
        ↓
Discover


"I know what I'm looking for."
        ↓
Search


"I want to explore coffee from somewhere."
        ↓
Geographical Exploration


"I don't know what I want."
        ↓
AI Coffee Sommelier


"I want to return to something I liked."
        ↓
Favorites
```

Regardless of entry point, Brewcipe should guide users toward the same structured coffee and recipe information.

The architecture should remain understandable without requiring users to understand Brewcipe's database model, internal taxonomy, or AI implementation.
