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
* the relationship between search, discovery, recipes, favorites, account access, and the AI Coffee Sommelier
* the hierarchy of primary, secondary, and contextual navigation
* how navigation relationships remain consistent across responsive layouts

This document defines **information structure, destination hierarchy, and navigation relationships**, not detailed page layouts or visual styling.

---

### 1.2 Scope

This document covers the current Brewcipe MVP capabilities:

* coffee discovery
* structured recipe detail
* search
* geographical exploration
* authentication
* favorites
* account access
* AI Coffee Sommelier

Detailed visual presentation and responsive component behavior belong in:

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

Supporting features such as accounts, authentication, and favorites should not dominate the product structure.

Primary navigation should make Brewcipe's main coffee-discovery paths easy to reach.

---

## 2.2 Discovery Without Authentication

Users should be able to access Brewcipe's core public coffee content without creating an account.

Public experiences include:

* browsing available coffees
* searching for coffee
* geographical exploration
* opening recipe details
* using public discovery experiences
* using the AI Coffee Sommelier where included in the release

Authentication should only be required when functionality depends on persistent user-specific data.

---

## 2.3 Multiple Discovery Paths, One Coffee Library

Users may approach Brewcipe differently.

For example:

```text
"I want to browse."
        ↓
Discover

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

AI recommendations should lead users back into Brewcipe's canonical coffee and recipe content wherever a relevant Brewcipe coffee exists.

---

## 2.8 Navigation Should Preserve the User's Mental Model

Brewcipe may present navigation differently across mobile, tablet, desktop, and wide desktop layouts.

The underlying destination hierarchy should remain consistent.

A destination should not change meaning merely because its icon, position, or responsive presentation changes.

---

## 2.9 Primary and Contextual Navigation Should Remain Distinct

Primary navigation should provide access to Brewcipe's major product areas.

Contextual navigation should help users move within a specific hierarchy, task, or content relationship.

Examples of contextual navigation include:

* back navigation
* geographical hierarchy
* breadcrumbs
* tabs
* section navigation
* links between related geographic entities

Contextual navigation should not compete with or unnecessarily duplicate primary navigation.

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
├── Account Access
│   ├── Authentication
│   └── Logout
│
└── Authentication
    ├── Registration
    └── Login
```

Authentication and Favorites are **Should Have** capabilities.

If they are deferred from the first MVP release, the core Coffee Discovery, Recipe Detail, Search, and Geographical Exploration structure remains intact.

Account Access should remain lightweight for the MVP and should not imply a full user-profile system.

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

The information architecture should not require unavailable fields to be represented in the interface.

---

# 5. Navigation Architecture

## 5.1 Navigation Hierarchy

Brewcipe should distinguish between three navigation levels:

```text
Primary Navigation
        ↓
Major Brewcipe destinations

Secondary Navigation
        ↓
Entry points and related areas within a destination

Contextual Navigation
        ↓
Movement within a hierarchy, detail view, or task
```

This distinction should remain consistent even when the visual presentation changes across screen sizes.

---

## 5.2 Primary Product Destinations

At the information-architecture level, Brewcipe's major product destinations are:

```text
Home
Discover
Search
AI Coffee Sommelier
Favorites
Account / Authentication
```

These represent product destinations rather than a requirement that all six appear with equal visual prominence in every navigation component.

---

## 5.3 Primary Navigation Priority

The strongest navigation priority should remain coffee discovery.

Conceptually:

```text
Primary Coffee Experiences

Home
Discover
Search
AI Coffee Sommelier
```

User-specific destinations include:

```text
Favorites
Account / Authentication
```

Favorites should become prominently accessible when the feature is included in the release.

Account access may remain visually separate from coffee-oriented navigation.

---

## 5.4 Mobile Navigation Model

The preferred mobile navigation model is persistent bottom navigation for a restrained set of Brewcipe's most important destinations.

The IA does not prescribe the exact visual component, icon family, spacing, or styling.

The mobile navigation should prioritize destinations that users need to move between frequently.

A working hierarchy is:

```text
Home
Discover
Search
Sommelier
Favorites
```

where the corresponding capabilities are included in the release.

`AI Coffee Sommelier` may use the shorter navigation label:

```text
Ask
```

if that terminology is validated and used consistently.

Account / Authentication does not need to consume one of the primary mobile navigation positions if it remains clearly accessible through the application header or another persistent account entry point.

If Favorites is not included in a release, it should be removed rather than replaced with an unrelated destination merely to preserve a fixed number of navigation items.

---

## 5.5 Tablet Navigation Model

Tablet should preserve the same destination hierarchy.

Smaller tablet layouts may continue using the mobile primary-navigation model.

Larger tablet layouts may transition to the desktop navigation presentation when sufficient space is available.

This transition should change presentation rather than information hierarchy.

---

## 5.6 Desktop Navigation Model

Desktop and wide-desktop layouts should expose Brewcipe's primary destinations through persistent larger-screen navigation.

Conceptually:

```text
Brewcipe

Home
Discover
Search
Sommelier
Favorites

Account / Authentication
```

Account access may remain visually separated from the primary coffee-oriented destinations.

The exact desktop presentation belongs to the design system and wireframes.

The IA does not require a particular header, navigation rail, icon treatment, or responsive breakpoint.

---

## 5.7 Search in Navigation

Search is a core Brewcipe discovery path.

It should remain directly accessible through primary navigation or an equivalently prominent global search action.

Search may therefore exist as:

```text
Dedicated Search Destination

and/or

Persistent Global Search Action
```

These presentations may coexist if they lead into the same underlying search experience.

Search should not become a separate content system.

---

## 5.8 Account Access

Account / Authentication should remain accessible without competing with Brewcipe's primary coffee-discovery destinations.

Depending on authentication state:

```text
Unauthenticated
        ↓
Sign In / Authentication

Authenticated
        ↓
Account Access
        ├── Favorites where appropriate
        └── Logout
```

A full profile-management destination is not required for the MVP.

---

# 6. Home

## 6.1 Purpose

Home acts as Brewcipe's primary entry point.

It should help users begin discovering coffee without requiring them to understand the complete application structure.

---

## 6.2 Primary Entry Points

Home should provide clear access to the core discovery paths:

```text
Home
│
├── Personalized Recommendations (authenticated, when available)
├── Browse Coffees
├── Search
├── Explore Geographically
└── Ask the AI Coffee Sommelier
```

If Favorites is implemented, authenticated users should also have a clear route back to saved coffees through the application's navigation system.

Home does not need to duplicate every persistent navigation destination as a dedicated content module.

---

## 6.3 Content Priority

Home should prioritize useful discovery over general marketing content.

The exact homepage content modules and layout belong to `wireframes-v3.md`.

---

# 6A. Personalized Discovery

## 6A.1 Purpose

Personalized discovery is the user-facing expression of Brewcipe's Taste Profile Mechanic.

It connects the user's taste model and interaction history to ranked coffee discovery without creating a separate content library.

## 6A.2 Relationship

```text
Taste Model
     ↓
Saved Coffees + Coffee History + User Signals
     ↓
Recommendation Engine
     ↓
Personalized Home
     ↓
User interaction
     ↓
Taste model evolves
```

The same personalization context may also be supplied to the AI Coffee Sommelier.

## 6A.3 Navigation Boundary

Personalized recommendations should be presented within Home and existing discovery surfaces rather than creating a separate recommendation-only destination for the MVP.

Authenticated users may see personalized modules; unauthenticated users should continue to receive normal discovery content.

The product mechanic is defined in `docs/product/taste-profile-mechanic-v1.md`.

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

Discover should provide clear access to both general coffee browsing and geographical exploration.

Coffee records may expose useful attributes such as:

* country
* region
* recipe type
* brewing method

where those attributes are available.

These attributes do not automatically require separate dedicated browsing hierarchies.

---

## 7.3 Discover as a Primary Destination

Discover should function as a stable primary destination regardless of whether users enter through Home, persistent navigation, or another discovery path.

Geographical Exploration remains a child discovery experience rather than a separate top-level product area.

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

The IA defines the coffee entity being represented.

Whether that entity appears as a Coffee Card, Coffee Row, or another reusable presentation belongs to the design system and wireframes.

---

## 8.3 Navigation

```text
Coffee Library
        ↓
Coffee
        ↓
Recipe Detail
```

Selecting a coffee should lead to its canonical structured recipe-detail experience.

---

# 9. Geographical Exploration

## 9.1 Purpose

Allow users to discover coffee through geographical relationships.

Geographical Exploration belongs within Discover.

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

The exact presentation may use:

* hierarchical lists
* visual geographic groups
* map-supported exploration
* another suitable navigation pattern

The IA defines the relationships, not the visualization technique.

A future map-supported experience should complement rather than replace an understandable accessible hierarchy.

---

## 9.4 Geographic Context

Where useful, Brewcipe should preserve the user's understanding of their position within the geographical hierarchy.

For example:

```text
Discover
    ↓
Asia
    ↓
Southeast Asia
    ↓
Vietnam
```

The exact breadcrumb, back-navigation, or contextual-navigation treatment belongs to interaction design.

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

## 10.3 Navigation

```text
Geographical Exploration
        ↓
Continent
        ↓
Region
```

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

## 12.3 Geographic Context

Country should remain connected to its parent geography where available.

Conceptually:

```text
Asia
→ Southeast Asia
→ Vietnam
```

The exact interaction treatment belongs to the wireframes.

---

# 13. Coffee / Recipe Detail

## 13.1 Purpose

Provide the complete available structured information needed to understand and prepare a Brewcipe coffee.

This is one of Brewcipe's primary content destinations.

All major coffee-discovery paths should resolve here when a user selects a canonical Brewcipe coffee.

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

The IA should preserve a place for provenance without prescribing its exact visual treatment.

Source attribution remains secondary to the recipe itself but should remain structurally available where required.

---

## 13.5 Related Actions

Depending on implemented scope, recipe detail may provide access to:

```text
Favorite
Geographical Context
AI Recommendation Context
```

These are supporting relationships rather than separate recipe destinations.

Related-coffee recommendations are not required for the current MVP.

---

## 13.6 Canonical Coffee Destination

Brewcipe should maintain one canonical recipe-detail destination for each coffee.

The following paths should not create duplicate recipe content:

```text
Discover
Search
Geography
Favorites
AI Coffee Sommelier
```

Instead:

```text
Any Coffee Discovery Path
        ↓
Canonical Coffee / Recipe Detail
```

---

# 14. Search

## 14.1 Purpose

Allow users who know what they are looking for to find relevant coffee without browsing the full library.

Search is a primary Brewcipe discovery path.

---

## 14.2 Core Search

MVP search must support coffee-name discovery.

Users should be able to submit a query such as:

```text
Café de olla
```

or another coffee name.

---

## 14.3 Search Destination

Search may be presented through:

* a dedicated Search destination
* a globally available search control
* search entry points within discovery experiences

These should lead into the same underlying search system.

The IA does not require each search entry point to become a separate route.

---

## 14.4 Additional Search Attributes

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

The IA does not require results to use cards.

The design system and wireframes may choose compact Coffee Rows, Coffee Cards, or another reusable coffee presentation according to context.

Selecting a result opens the corresponding canonical Recipe Detail.

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

Provide conversational coffee discovery for users who do not know exactly what they want to search for, while using the user's available personalization context when authenticated.

The Sommelier is a discovery tool rather than a separate coffee-content system.

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
├── Suggested Coffee
├── Explanation
└── Route to Brewcipe Recipe
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

## 16.5 Navigation Label

The product area remains:

```text
AI Coffee Sommelier
```

A shorter navigation label such as:

```text
Ask
```

may be used where navigation space is constrained if it remains understandable and consistent.

The shortened label should not redefine the underlying product concept.

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

The exact authentication-provider interaction and interface flow belong to implementation and interaction design.

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

---

## 17.4 Context Preservation

Authentication should preserve the user's originating context where practical.

For example:

```text
Recipe Detail
    ↓
Favorite
    ↓
Authentication
    ↓
Recipe Detail
    ↓
Favorite Completed
```

The exact post-authentication interaction remains subject to implementation validation.

---

# 18. Favorites

## 18.1 Access

Authenticated users only.

---

## 18.2 Purpose

Provide access to coffees intentionally saved by the current user.

Favorites is a return path into Brewcipe's existing coffee library rather than a separate content system.

---

## 18.3 Structure

```text
Favorites
    ↓
Saved Coffee
    ↓
Recipe Detail
```

Favorites should reuse Brewcipe's standard coffee entities rather than creating an unrelated dashboard-style information structure.

---

## 18.4 Navigation Role

When Favorites is included in the release, users should have persistent and predictable access to it.

On mobile, Favorites may occupy a primary bottom-navigation destination.

On larger screens, it should remain available through the equivalent desktop navigation hierarchy.

Exact placement belongs to the wireframes and design system.

---

## 18.5 Empty State

When a user has not saved any coffees, the page should:

* communicate that no favorites are currently saved
* provide a clear route back to coffee discovery

---

# 19. Account Access

## 19.1 Purpose

Provide lightweight access to user-specific account actions.

Brewcipe requires a way for users to:

* authenticate
* understand whether they are authenticated
* access relevant user-specific functionality
* log out

---

## 19.2 Unauthenticated State

Conceptually:

```text
Account Access
      ↓
Sign In / Register
```

---

## 19.3 Authenticated State

Conceptually:

```text
Account Access
│
├── Authenticated Identity
├── Favorites where appropriate
└── Logout
```

Favorites may also remain independently accessible through primary navigation.

---

## 19.4 MVP Boundary

A dedicated profile-management system is **not currently required** by the MVP requirements.

The Account destination should therefore remain lightweight.

If later product requirements introduce:

* profile information
* account settings
* preferences
* user history

the IA can be expanded accordingly.

---

# 20. Page and View Inventory

The following represents the current Brewcipe MVP information architecture.

| ID    | Page / View               | Access                 | Priority    | Primary Purpose                                 |
| ----- | ------------------------- | ---------------------- | ----------- | ----------------------------------------------- |
| IA-01 | Home                      | Public                 | Core        | Entry into Brewcipe discovery                   |
| IA-02 | Discover / Coffee Library | Public                 | Must Have   | Browse available coffees                        |
| IA-03 | Geographic Explore        | Public                 | Must Have   | Enter geographical discovery                    |
| IA-04 | Continent                 | Public                 | Must Have   | Browse relevant regions                         |
| IA-05 | Region                    | Public                 | Must Have   | Browse relevant countries                       |
| IA-06 | Country                   | Public                 | Must Have   | Browse coffees associated with a country        |
| IA-07 | Coffee / Recipe Detail    | Public                 | Must Have   | Understand and prepare a coffee                 |
| IA-08 | Search                    | Public                 | Must Have   | Submit a coffee search                          |
| IA-09 | Search Results            | Public                 | Must Have   | View matching coffees                           |
| IA-10 | AI Coffee Sommelier       | Public                 | Should Have | Conversational coffee discovery                 |
| IA-11 | Favorites                 | Authenticated          | Should Have | View saved coffees                              |
| IA-12 | Authentication            | Public / Contextual    | Should Have | Register or authenticate                        |
| IA-13 | Account Access            | Public / Authenticated | Should Have | Access authentication state and account actions |

A single application route may support more than one IA state.

For example:

* Search and Search Results may use one route or interface.
* Authentication may appear contextually rather than requiring a dedicated full page.
* Account Access may use a page, menu, sheet, or another interface pattern.

The IA inventory describes conceptual user-facing states rather than requiring a one-to-one relationship with frontend files.

---

# 21. Dynamic Content Templates

Geographical entities and coffee records should use reusable templates rather than requiring separately designed pages for every database record.

Conceptually:

```text
Continent Template
        ↓
Selected Continent Data

Region Template
        ↓
Selected Region Data

Country Template
        ↓
Selected Country Data

Recipe Template
        ↓
Selected Coffee Data
```

This allows Brewcipe's content library to grow without creating new page designs for every coffee or location.

The same content entity may use different visual representations in different discovery contexts without becoming a different IA entity.

For example:

```text
Coffee Card
Coffee Row
AI Recommendation
Favorite Item
        ↓
Same Coffee Entity
        ↓
Canonical Recipe Detail
```

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
├── AI Coffee Sommelier
│   └── Recommendation
│       └── Coffee
│           └── Recipe Detail
│
└── Favorites
    └── Saved Coffee
        └── Recipe Detail
```

Favorites provide a user-specific return path to existing coffee records rather than creating duplicate recipe content.

---

# 23. Core User Journeys

## 23.1 Browse Coffee

```text
Home / Primary Navigation
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
Home / Discover
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
Home / Primary Navigation / Search Entry
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
Home / Primary Navigation
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
Coffee / Recipe Detail
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
Primary Navigation / Account Access
        ↓
Favorites
        ↓
Saved Coffee
        ↓
Recipe Detail
```

---

## 23.7 Authenticate From Account Access

```text
Account Access
        ↓
Sign In / Register
        ↓
Authentication
        ↓
Authenticated Account State
```

---

# 24. Navigation Rules

## NAV-001 — Core Navigation

Users should have a clear and persistent route to Brewcipe's primary discovery experiences.

---

## NAV-002 — Coffee Destination

Coffee discovery, search results, geographical results, favorites, and relevant AI recommendations should resolve to the canonical Coffee / Recipe Detail experience.

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

## NAV-008 — Responsive Navigation Equivalence

Primary destinations should remain accessible across mobile, tablet, desktop, and wide-desktop layouts.

The navigation component may change, but the information hierarchy should remain coherent.

Conceptually:

```text
Mobile Bottom Navigation
        ↓
Tablet Adaptive Navigation
        ↓
Desktop Navigation

Same Destination Hierarchy
```

---

## NAV-009 — Primary vs Contextual Actions

Primary navigation should contain product destinations.

Contextual actions such as:

```text
Back
Favorite
Close
Filter
Clear
```

should not become primary navigation destinations merely because they use icons.

---

## NAV-010 — Account Separation

Account / Authentication may remain visually separated from Brewcipe's primary coffee-discovery destinations.

Its placement should remain predictable and accessible.

---

## NAV-011 — Search Accessibility

Search should remain directly accessible from Brewcipe's primary application structure.

If multiple search entry points exist, they should resolve to the same underlying search experience.

---

## NAV-012 — Release-Aware Navigation

Navigation should reflect functionality actually included in the current release.

If a Should Have capability such as Favorites or the AI Coffee Sommelier is deferred, its primary navigation destination should not appear as an inactive placeholder.

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

account

authentication
```

Exact URL patterns, slugs, route parameters, and routing implementation belong to frontend and technical architecture decisions.

The IA should not prescribe implementation-specific paths unless those routes later become part of a deliberate product decision.

Multiple interface presentations should not create unnecessary duplicate URLs for the same canonical coffee content.

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

Visual inspiration from other coffee applications should not be interpreted as permission to add their product functionality to Brewcipe's IA.

---

# 27. Resolved and Open IA Decisions

## 27.1 Resolved Direction

The following decisions now have sufficient direction to guide wireframing:

| Decision                     | Current Direction                                                  |
| ---------------------------- | ------------------------------------------------------------------ |
| Mobile navigation pattern    | Persistent bottom navigation for primary destinations              |
| Tablet navigation pattern    | Mobile pattern or adaptive transition according to available space |
| Desktop navigation pattern   | Persistent larger-screen navigation                                |
| Account placement            | Accessible but may remain separate from primary coffee navigation  |
| Favorites navigation         | Persistent destination when feature is included                    |
| Sommelier navigation         | Primary discovery destination when feature is included             |
| Geographic Explore hierarchy | Discover → Continent → Region → Country → Coffee                   |
| Canonical coffee destination | One Coffee / Recipe Detail experience                              |
| Responsive navigation        | Presentation changes; destination hierarchy remains consistent     |

---

## 27.2 Decisions Still Open

| Decision                                                                      | Current Status                           |
| ----------------------------------------------------------------------------- | ---------------------------------------- |
| Final primary navigation labels                                               | Needs terminology validation             |
| Whether `AI Coffee Sommelier` uses `Sommelier` or `Ask` in compact navigation | Needs terminology / usability validation |
| Exact number of mobile bottom-navigation destinations                         | Depends on included release capabilities |
| Dedicated Search page versus combined global + destination search             | Interaction validation                   |
| Exact tablet navigation transition point                                      | Responsive implementation validation     |
| Desktop header versus another validated larger-screen presentation            | Wireframe / high-fidelity validation     |
| Geographic list versus richer visual/map-supported exploration                | Future design decision                   |
| Which search attributes beyond coffee name belong in MVP                      | Product decision                         |
| How much cultural context appears in discovery versus recipe detail           | Content-design decision                  |
| Exact visible treatment of source attribution                                 | Content / visual-design decision         |
| Exact post-authentication favorite completion behavior                        | Interaction validation                   |
| Final account/authentication presentation                                     | Interaction validation                   |

Open decisions should remain visible until intentionally resolved.

They should not prevent implementation of the established hierarchy.

---

# 28. Relationship to Wireframes

This document defines:

* what information exists
* what destinations exist
* how destinations relate
* which destinations are primary
* which relationships are contextual
* which experiences resolve to canonical coffee content

The wireframes should determine:

* exact navigation-control placement
* exact bottom-navigation composition
* icon treatment
* application-header structure
* how Home is composed
* Coffee Card versus Coffee Row usage
* how geographic hierarchy is visually presented
* whether Search occupies a page, field, overlay, or combination
* how recipe information is visually ordered
* how Favorites and Sommelier interactions work
* how navigation transforms across mobile, tablet, desktop, and wide desktop

The wireframes should preserve the IA hierarchy.

They should not introduce new product capabilities without corresponding product requirements.

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

Regardless of entry point:

```text
Discover ────────────┐
Search ──────────────┤
Geography ───────────┤
Sommelier ───────────┼──→ Coffee ──→ Canonical Recipe Detail
Favorites ───────────┘
```

The architecture should remain understandable without requiring users to understand Brewcipe's database model, internal taxonomy, responsive implementation, or AI architecture.

Navigation presentation may change across devices, but users should continue to recognize the same Brewcipe structure and destinations.

The intended result is an information architecture that supports both:

```text
Exploration
+
Efficient Application Navigation
```

without allowing navigation mechanics to overshadow the coffee itself.
