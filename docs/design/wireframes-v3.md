# Brewcipe — Low-Fidelity Wireframes

## 1. Overview

### 1.1 Purpose

This document defines low-fidelity wireframes for the Brewcipe MVP.

The wireframes translate Brewcipe's information architecture into preliminary screen structures that establish:

* content hierarchy
* navigation relationships
* primary actions
* mobile-first layout
* reusable interface patterns
* major interaction flows
* loading, empty, and error states
* responsive adaptation

These wireframes intentionally avoid final visual styling.

Final visual implementation should follow:

* `design-direction.md`
* `design-system.md`
* `information-architecture.md`

Product scope remains governed by:

* `prd.md`
* `requirements.md`

---

### 1.2 Wireframe Scope

The current wireframes cover:

#### Must Have

* Home
* Discover / Coffee Library
* Geographic Explore
* Continent
* Region
* Country
* Coffee / Recipe Detail
* Search
* Search Results
* core loading, empty, and error states

#### Should Have

* AI Coffee Sommelier
* AI recommendation result
* Favorites
* Authentication

Should Have wireframes are included so the experience can be designed coherently even if those capabilities are delivered after the initial Must Have experience.

---

### 1.3 Fidelity

These wireframes define:

```text
Structure
Hierarchy
Placement
Relationships
Actions
States
Responsive intent
```

They do not define:

```text
Final colors
Final typography
Exact spacing
Exact radius
Final imagery
Animation
Production copy
Final iconography
```

Those decisions belong to later design stages or the design system.

---

# 2. Wireframing Principles

## 2.1 Mobile First

All core experiences should be designed for narrow mobile viewports first.

Desktop layouts should progressively enhance the same content hierarchy.

---

## 2.2 Coffee First

Coffee content should receive visual and structural priority.

Navigation, authentication, AI, and supporting controls should help users reach coffee rather than dominate the interface.

---

## 2.3 Content First

Users should encounter useful information early.

Avoid unnecessary introductory sections before core coffee content.

---

## 2.4 Reusable Patterns

Recurring interface structures should reuse common patterns where appropriate.

Examples include:

```text
Coffee Card
Search Input
Page Header
Section Heading
Favorite Control
Geographic Item
Loading State
Empty State
Error State
```

---

## 2.5 Progressive Disclosure

Discovery screens should show enough information to support selection.

Detailed recipe, cultural, geographical, and provenance information belongs primarily in deeper content views.

---

## 2.6 Optional Data

Wireframes must tolerate incomplete optional recipe information.

Missing data should not produce:

```text
N/A
Unknown
—
Empty section
```

unless there is a genuine product reason to communicate that absence.

---

## 2.7 Native Content

Native coffee names and Unicode content should be represented correctly throughout the interface.

For example:

```text
Cà phê vợt
Café de olla
Türk kahvesi
```

---

# 3. Application Shell

The final navigation pattern remains subject to wireframe validation.

The application requires access to:

```text
Home
Discover
Search
Sommelier
Favorites
Authentication / Account Access
```

but these destinations do not necessarily require equal placement or permanent navigation items.

---

## 3.1 Mobile Shell — Working Hypothesis

A mobile screen may use:

```text
┌───────────────────────────────┐
│ Brewcipe              [Menu]  │
├───────────────────────────────┤
│                               │
│                               │
│         Page Content          │
│                               │
│                               │
│                               │
└───────────────────────────────┘
```

or a persistent navigation pattern if later usability testing demonstrates that it better supports core journeys.

The IA does not require a fixed bottom navigation.

---

## 3.2 Desktop Shell — Working Hypothesis

Desktop may expose major destinations through a persistent header.

```text
┌──────────────────────────────────────────────────────────────┐
│ BREWCIPE        Discover   Search   Sommelier    [Account]   │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│                         Page Content                         │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

If Favorites is implemented, it should remain readily accessible to authenticated users.

Exact navigation labels and placement remain subject to validation.

---

# 4. Home

## 4.1 Goal

Help users immediately begin exploring Brewcipe.

---

## 4.2 Primary Actions

Home should provide clear entry into:

* coffee discovery
* search
* geographical exploration
* AI Coffee Sommelier, if implemented

---

## 4.3 Mobile Wireframe

```text
┌───────────────────────────────┐
│ Brewcipe              [Menu]  │
│                               │
│ Discover coffee               │
│ from around the world.        │
│                               │
│ [ Search coffee...          ] │
│                               │
│ ───────────────────────────── │
│                               │
│ Explore coffee                │
│                               │
│ Discover recipes, brewing     │
│ traditions and coffee from    │
│ around the world.             │
│                               │
│ [ Browse coffees →          ] │
│                               │
│ ───────────────────────────── │
│                               │
│ Explore by place              │
│                               │
│ [ Geographic preview        ] │
│                               │
│ [ Explore the world →       ] │
│                               │
│ ───────────────────────────── │
│                               │
│ Not sure what to try?         │
│                               │
│ Ask the Coffee Sommelier for  │
│ a recommendation.             │
│                               │
│ [ Ask the Sommelier →       ] │
│                               │
└───────────────────────────────┘
```

The Sommelier section should only appear when the feature is included in the release.

---

## 4.4 Notes

Home should not become a long marketing landing page.

The primary discovery actions should appear early.

The exact amount of featured coffee content remains a wireframe/high-fidelity design decision.

---

# 5. Discover / Coffee Library

## 5.1 Goal

Allow users to browse available Brewcipe coffees without needing a specific query.

---

## 5.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Discover                   │
│                               │
│ Explore coffee                │
│                               │
│ [ Search coffee...          ] │
│                               │
│ [ Explore by geography →    ] │
│                               │
│ ───────────────────────────── │
│                               │
│ Coffee Library                │
│                               │
│ ┌───────────────────────────┐ │
│ │       Coffee Image        │ │
│ │                           │ │
│ │ Vietnam                   │ │
│ │ Cà phê vợt             ♡  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
│ ┌───────────────────────────┐ │
│ │       Coffee Image        │ │
│ │                           │ │
│ │ Mexico                    │ │
│ │ Café de olla           ♡  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
│ ...                           │
│                               │
└───────────────────────────────┘
```

The Favorite control only appears if Favorites is implemented.

---

## 5.3 Notes

Advanced filtering is not assumed.

Coffee cards may expose useful available attributes, but those attributes do not automatically require filter controls.

---

# 6. Geographic Explore

## 6.1 Goal

Provide entry into Brewcipe's geographical coffee hierarchy.

---

## 6.2 Hierarchy

```text
Continent
    ↓
Region
    ↓
Country
    ↓
Coffee
```

---

## 6.3 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Explore by Place           │
│                               │
│ Coffee around the world       │
│                               │
│ Explore coffee through the    │
│ places and traditions         │
│ associated with it.           │
│                               │
│ ┌───────────────────────────┐ │
│ │ Asia                    → │ │
│ │ [Available coffee count]  │ │
│ └───────────────────────────┘ │
│                               │
│ ┌───────────────────────────┐ │
│ │ Europe                  → │ │
│ │ [Available coffee count]  │ │
│ └───────────────────────────┘ │
│                               │
│ ┌───────────────────────────┐ │
│ │ Africa                  → │ │
│ │ [Available coffee count]  │ │
│ └───────────────────────────┘ │
│                               │
│ ...                           │
│                               │
└───────────────────────────────┘
```

Coffee counts should only appear if reliable and useful.

---

## 6.4 Visualization

This wireframe uses a hierarchical list as the simplest structural representation.

It does **not** establish that lists must be the final geographical visualization.

A richer visual or map-supported experience may be explored separately.

---

# 7. Continent

## 7.1 Example

Asia

---

## 7.2 Goal

Allow users to move from a continent into represented regions.

---

## 7.3 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Asia                       │
│                               │
│ Explore Asia                  │
│                               │
│ Regions                       │
│                               │
│ ┌───────────────────────────┐ │
│ │ Southeast Asia          → │ │
│ │ [Supporting information]  │ │
│ └───────────────────────────┘ │
│                               │
│ ┌───────────────────────────┐ │
│ │ East Asia               → │ │
│ │ [Supporting information]  │ │
│ └───────────────────────────┘ │
│                               │
│ ...                           │
│                               │
└───────────────────────────────┘
```

Only regions represented by Brewcipe data should appear.

---

# 8. Region

## 8.1 Example

Southeast Asia

---

## 8.2 Goal

Allow users to move from a region into represented countries.

---

## 8.3 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Southeast Asia             │
│                               │
│ Explore Southeast Asia        │
│                               │
│ Countries                     │
│                               │
│ [ Vietnam                  → ]│
│                               │
│ [ Thailand                 → ]│
│                               │
│ [ Malaysia                 → ]│
│                               │
│ [ Indonesia                → ]│
│                               │
│ [ Singapore                → ]│
│                               │
└───────────────────────────────┘
```

---

# 9. Country

## 9.1 Example

Vietnam

---

## 9.2 Goal

Allow users to discover coffees associated with a selected country.

---

## 9.3 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Vietnam                    │
│                               │
│ Vietnam                       │
│ Southeast Asia · Asia         │
│                               │
│ [Optional country context]    │
│                               │
│ ───────────────────────────── │
│                               │
│ Coffees                       │
│                               │
│ ┌───────────────────────────┐ │
│ │       Coffee Image        │ │
│ │                           │ │
│ │ Cà phê vợt             ♡  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
│ ┌───────────────────────────┐ │
│ │       Coffee Image        │ │
│ │                           │ │
│ │ Cà phê kho             ♡  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
│ ...                           │
│                               │
└───────────────────────────────┘
```

The Favorite action only appears if the feature is implemented.

---

## 9.4 Notes

The country page should not invent country-level editorial content unless supported by Brewcipe content.

Country context is optional.

---

# 10. Coffee / Recipe Detail

## 10.1 Goal

Present the available structured recipe information clearly while preserving geographical, cultural, and source context.

This is Brewcipe's primary content-detail experience.

---

## 10.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←                         ♡   │
│                               │
│ [        Coffee Image       ] │
│                               │
│ Vietnam                       │
│                               │
│ Cà phê vợt                    │
│ [Transliteration if relevant] │
│ [English name if different]   │
│                               │
│ [Recipe type / brewer]        │
│                               │
│ ───────────────────────────── │
│                               │
│ Recipe                        │
│                               │
│ Servings        Temperature   │
│ [value]         [value]       │
│                               │
│ Brewer / Method               │
│ [value]                       │
│                               │
│ ───────────────────────────── │
│                               │
│ Ingredients                   │
│                               │
│ • [quantity] [ingredient]     │
│ • [quantity] [ingredient]     │
│ • [quantity] [ingredient]     │
│                               │
│ ───────────────────────────── │
│                               │
│ How to make it                │
│                               │
│ 01                            │
│ [Preparation instruction]     │
│                               │
│ 02                            │
│ [Preparation instruction]     │
│                               │
│ 03                            │
│ [Preparation instruction]     │
│                               │
│ ───────────────────────────── │
│                               │
│ About this coffee             │
│                               │
│ [Cultural context]            │
│                               │
│ ───────────────────────────── │
│                               │
│ From                          │
│                               │
│ Asia                          │
│ → Southeast Asia              │
│ → Vietnam                     │
│                               │
│ ───────────────────────────── │
│                               │
│ Source                        │
│                               │
│ [Source attribution]          │
│                               │
└───────────────────────────────┘
```

Favorite appears only when implemented.

---

## 10.3 Data Rules

The wireframe should render only available data.

For example:

```text
servings available
→ show Servings

temperature available
→ show Temperature

brewer available
→ show Brewer / Method

transliteration available
→ show Transliteration

cultural context available
→ show About this coffee
```

Do not create placeholders such as:

```text
Temperature: N/A
Brewer: Unknown
```

Missing optional information should collapse naturally.

---

## 10.4 Recipe Identity

Coffee naming may require multiple layers:

```text
Native name
Transliteration
English name
```

The exact visual priority between them should depend on the data and be validated during high-fidelity design.

Native names should remain meaningful content rather than appearing like technical metadata.

---

## 10.5 Geographic Context

Where useful, users should be able to understand the coffee's geographical relationship.

Conceptually:

```text
Asia
→ Southeast Asia
→ Vietnam
```

The final implementation may use:

* breadcrumbs
* links
* a dedicated context section
* another accessible pattern

---

## 10.6 Source

The structure should preserve space for source attribution.

The exact visible treatment remains subject to product and visual-design decisions.

---

# 11. Recipe Detail — Minimal Data Variant

A coffee with fewer optional fields should still produce a coherent page.

```text
┌───────────────────────────────┐
│ ←                             │
│                               │
│ [        Coffee Image       ] │
│                               │
│ Country                       │
│ Coffee Name                   │
│                               │
│ ───────────────────────────── │
│                               │
│ Ingredients                   │
│                               │
│ • Ingredient                  │
│ • Ingredient                  │
│                               │
│ ───────────────────────────── │
│                               │
│ How to make it                │
│                               │
│ 01                            │
│ Instruction                   │
│                               │
│ 02                            │
│ Instruction                   │
│                               │
│ ───────────────────────────── │
│                               │
│ Source                        │
│ [Source attribution]          │
│                               │
└───────────────────────────────┘
```

The page should not look broken simply because optional metadata is absent.

---

# 12. Search — Initial State

## 12.1 Goal

Allow users to find coffee directly by name.

---

## 12.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Search                     │
│                               │
│ Search coffee                 │
│                               │
│ [ Search coffee...          ] │
│                               │
│ [Optional discovery prompt]   │
│                               │
└───────────────────────────────┘
```

Advanced filtering is not assumed.

---

# 13. Search Results

## 13.1 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Search                     │
│                               │
│ [ café de olla              ×]│
│                               │
│ Results                       │
│                               │
│ ┌───────────────────────────┐ │
│ │       Coffee Image        │ │
│ │                           │ │
│ │ Mexico                    │ │
│ │ Café de olla           ♡  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
│ ...                           │
│                               │
└───────────────────────────────┘
```

Selecting a result opens the canonical recipe-detail page.

---

# 14. Search Empty State

```text
┌───────────────────────────────┐
│ ←  Search                     │
│                               │
│ [ xyzcoffee                 ×]│
│                               │
│ No coffees found              │
│                               │
│ Try another coffee name or    │
│ explore the coffee library.   │
│                               │
│ [ Explore coffee ]            │
│                               │
└───────────────────────────────┘
```

---

# 15. Search Error State

```text
┌───────────────────────────────┐
│ ←  Search                     │
│                               │
│ [ café de olla              ×]│
│                               │
│ We couldn't search the coffee │
│ library right now.            │
│                               │
│ [ Try again ]                 │
│                               │
└───────────────────────────────┘
```

---

# 16. AI Coffee Sommelier

**Priority: Should Have**

## 16.1 Goal

Allow users to describe what they want and receive contextual coffee recommendations.

The experience should feel integrated with Brewcipe rather than like a separate generic chatbot.

---

## 16.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Coffee Sommelier           │
│                               │
│ What are you in the mood for? │
│                               │
│ Tell me what you're looking   │
│ for and I'll suggest coffee   │
│ from Brewcipe.                │
│                               │
│ ┌───────────────────────────┐ │
│ │ I want something sweet    │ │
│ │ and iced.                 │ │
│ │                           │ │
│ └───────────────────────────┘ │
│                               │
│ [ Ask the Sommelier ]         │
│                               │
│ ───────────────────────────── │
│                               │
│ Try asking                     │
│                               │
│ "What coffee should I try     │
│ from Malaysia?"               │
│                               │
│ "I like strong coffee but     │
│ don't have an espresso        │
│ machine."                     │
│                               │
└───────────────────────────────┘
```

Suggested prompts are optional supporting content.

---

# 17. AI Sommelier — Recommendation

## 17.1 Goal

Provide understandable recommendations that lead users back into Brewcipe's canonical coffee library.

---

## 17.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Coffee Sommelier           │
│                               │
│ You asked                     │
│                               │
│ "I want something sweet       │
│ and iced."                    │
│                               │
│ ───────────────────────────── │
│                               │
│ You might like                │
│                               │
│ ┌───────────────────────────┐ │
│ │       Coffee Image        │ │
│ │                           │ │
│ │ Coffee Name               │ │
│ │ Country                   │ │
│ │                           │ │
│ │ [ View Recipe ]           │ │
│ └───────────────────────────┘ │
│                               │
│ Why it fits                   │
│                               │
│ [Recommendation explanation]  │
│                               │
│ [ Ask another question ]      │
│                               │
└───────────────────────────────┘
```

---

## 17.3 Recommendation Rule

When the Sommelier recommends an existing Brewcipe coffee:

```text
AI recommendation
        ↓
View Recipe
        ↓
Canonical Brewcipe Recipe Detail
```

The AI experience should not duplicate or replace canonical recipe information.

---

# 18. AI Sommelier — Loading

```text
┌───────────────────────────────┐
│ ←  Coffee Sommelier           │
│                               │
│ Finding a coffee for you...   │
│                               │
│ [ Loading indicator ]         │
│                               │
└───────────────────────────────┘
```

---

# 19. AI Sommelier — Error

```text
┌───────────────────────────────┐
│ ←  Coffee Sommelier           │
│                               │
│ We couldn't generate a        │
│ recommendation right now.     │
│                               │
│ [ Try again ]                 │
│                               │
│ [ Explore coffee instead ]    │
│                               │
└───────────────────────────────┘
```

AI failure should not block access to Brewcipe's normal coffee discovery.

---

# 20. Favorite Action

**Priority: Should Have**

The Favorite control should be reusable across relevant coffee contexts.

Possible locations include:

```text
Coffee Card
Recipe Detail
Favorites
```

---

## 20.1 Authenticated Flow

```text
User taps Favorite
        ↓
Saved
        ↓
Favorite state updates
```

---

## 20.2 Unauthenticated Flow

```text
User taps Favorite
        ↓
Authentication required
        ↓
Authentication
        ↓
Return to coffee context
        ↓
Continue intended action
```

Exact post-authentication behavior remains to be validated.

---

# 21. Favorites

**Priority: Should Have**

## 21.1 Goal

Allow authenticated users to return to coffees they intentionally saved.

---

## 21.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ ←  Favorites                  │
│                               │
│ Your favorite coffees         │
│                               │
│ ┌───────────────────────────┐ │
│ │       Coffee Image        │ │
│ │                           │ │
│ │ Vietnam                   │ │
│ │ Cà phê vợt             ♥  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
│ ┌───────────────────────────┐ │
│ │       Coffee Image        │ │
│ │                           │ │
│ │ Mexico                    │ │
│ │ Café de olla           ♥  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
└───────────────────────────────┘
```

Favorites should reuse the standard Coffee Card.

---

# 22. Favorites Empty State

```text
┌───────────────────────────────┐
│ ←  Favorites                  │
│                               │
│ No favorites yet              │
│                               │
│ Save coffees you want to brew │
│ or return to later.           │
│                               │
│ [ Discover coffee ]           │
│                               │
└───────────────────────────────┘
```

---

# 23. Authentication

**Priority: Should Have**

## 23.1 Goal

Authenticate users when functionality requires persistent user-specific information.

Authentication should remain lightweight and should not block normal public discovery.

---

## 23.2 Authentication Entry

```text
┌───────────────────────────────┐
│ ×                             │
│                               │
│ Brewcipe                      │
│                               │
│ Sign in to save your favorite │
│ coffees and return to them    │
│ later.                        │
│                               │
│ [ Authentication options ]    │
│                               │
│ [ Continue without signing in │
│   where applicable ]          │
│                               │
└───────────────────────────────┘
```

The exact authentication options depend on the implemented authentication strategy.

---

## 23.3 Contextual Authentication

When authentication is triggered by a protected action, the interface should explain why sign-in is being requested.

For example:

```text
Save this coffee to Favorites

Sign in to save coffees and
return to them later.

[ Authentication options ]
```

---

# 24. Authenticated Account Access

Brewcipe requires a way for authenticated users to:

* understand that they are signed in
* access Favorites
* log out

A dedicated full Profile or Account page is not currently required.

A lightweight account menu or similar interaction may be sufficient.

Conceptually:

```text
┌───────────────────────────────┐
│ Account                       │
│                               │
│ [Authenticated identity]      │
│                               │
│ Favorites                  →  │
│                               │
│ Log out                       │
│                               │
└───────────────────────────────┘
```

Exact presentation remains a wireframe/interaction decision.

---

# 25. Shared Coffee Card

## 25.1 Purpose

Represent a Brewcipe coffee consistently across discovery contexts.

---

## 25.2 Base Structure

```text
┌───────────────────────────────┐
│                               │
│         Coffee Image          │
│                               │
├───────────────────────────────┤
│ Country                       │
│                               │
│ Coffee Name                ♡  │
│ Native Name / metadata        │
│                               │
└───────────────────────────────┘
```

---

## 25.3 Potential Contexts

The same base pattern may appear within:

* Discover
* Country
* Search Results
* Favorites
* AI recommendations
* Home discovery modules

---

## 25.4 Content Rules

The card should prioritize identification over detailed recipe information.

Potential content includes:

```text
Coffee image
Coffee name
Native name where useful
Country
Relevant secondary metadata
Favorite action where applicable
```

Avoid placing complete recipe information inside discovery cards.

---

# 26. Shared Geographic Item

Geographical navigation should reuse a simple base pattern.

```text
┌───────────────────────────────┐
│ Southeast Asia             →  │
│ [Optional supporting info]    │
└───────────────────────────────┘
```

Potential contexts:

```text
Continent → Region
Region → Country
Geographic Explore → Continent
```

The final high-fidelity treatment may use imagery or other visual representation.

---

# 27. Shared Page States

## 27.1 Loading

Content-loading pages should communicate that data is being retrieved.

Possible low-fidelity representation:

```text
[ Page heading ]

[ Loading content ]

[ Loading content ]

[ Loading content ]
```

The final design may use skeletons, progress indicators, or another design-system pattern.

---

## 27.2 Empty

Collections should:

* explain why no content is shown
* avoid looking broken
* provide a useful next action where one exists

---

## 27.3 Error

Errors should:

* explain the problem in understandable language
* provide recovery where possible
* preserve access to other Brewcipe discovery paths

---

# 28. Desktop Adaptation

Desktop should expand the mobile information hierarchy rather than create unrelated page structures.

---

## 28.1 Coffee Collection

### Mobile

```text
Coffee Card

Coffee Card

Coffee Card
```

### Desktop

```text
Coffee Card     Coffee Card     Coffee Card

Coffee Card     Coffee Card     Coffee Card
```

The final column count should respond to available width and card requirements rather than being hard-coded at the wireframe stage.

---

# 29. Recipe Detail — Desktop

A potential larger-screen structure:

```text
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  ┌──────────────────────┐   Country                      │
│  │                      │                                │
│  │                      │   Coffee Name              ♡   │
│  │     Coffee Image     │   Native / transliteration    │
│  │                      │                                │
│  │                      │   Recipe type / brewer         │
│  └──────────────────────┘                                │
│                                                          │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Recipe Information                                     │
│                                                          │
│  Servings          Temperature          Brewer / Method  │
│                                                          │
├───────────────────────────┬──────────────────────────────┤
│                           │                              │
│  Ingredients              │  How to make it              │
│                           │                              │
│  • Ingredient             │  01  Instruction             │
│  • Ingredient             │                              │
│  • Ingredient             │  02  Instruction             │
│                           │                              │
│                           │  03  Instruction             │
│                           │                              │
├───────────────────────────┴──────────────────────────────┤
│                                                          │
│  About this coffee                                      │
│                                                          │
│  [Cultural context]                                     │
│                                                          │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  From                                                    │
│  Asia → Southeast Asia → Vietnam                        │
│                                                          │
│  Source                                                  │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

This is a **working layout hypothesis**, not a final desktop specification.

Actual recipe length may make a different arrangement more appropriate.

---

# 30. Geographic Exploration — Desktop

A larger viewport may allow geographical items to be presented in a multi-column structure.

Conceptually:

```text
Explore by Place

Asia                  Europe                Africa
[Supporting info]     [Supporting info]     [Supporting info]

North America         South America         Oceania
[Supporting info]     [Supporting info]     [Supporting info]
```

A future map-supported experience should not remove accessible hierarchical navigation.

---

# 31. Search — Desktop

Search may use a wider content container while maintaining the same conceptual flow:

```text
Search coffee

[ Search field                                  ]

Results

Coffee Card       Coffee Card       Coffee Card

Coffee Card       Coffee Card       Coffee Card
```

Advanced filtering should not be added unless the product scope is updated.

---

# 32. Responsive Principles

Across responsive layouts:

### Preserve

* content hierarchy
* terminology
* primary actions
* canonical coffee destinations

### Adapt

* column count
* content width
* spacing
* navigation presentation
* image sizing
* selected component arrangement

### Avoid

* hiding essential content on mobile
* creating unrelated mobile and desktop experiences
* introducing desktop-only functionality without product justification

---

# 33. Wireframe Validation Checklist

Before moving a wireframe into high-fidelity design, validate the following.

## 33.1 Product Alignment

* Does the screen support a current PRD requirement?
* Has unsupported functionality been introduced?
* Is the feature correctly treated as Must Have or Should Have?

---

## 33.2 Purpose

* Is the purpose of the screen clear?
* Is the primary user action understandable?
* Does the screen help the user progress toward coffee content?

---

## 33.3 Information Hierarchy

* Is the most important information appropriately prioritized?
* Is unnecessary information removed?
* Is detailed information progressively disclosed?

---

## 33.4 Navigation

* Can users understand where they are?
* Is there a clear next destination?
* Can they return to major Brewcipe areas?
* Does geographical navigation preserve the correct hierarchy?

---

## 33.5 Mobile

* Does the experience work in a narrow viewport?
* Are controls usable by touch?
* Does content remain readable?
* Is essential content preserved?

---

## 33.6 Reuse

* Is the shared Coffee Card reused where appropriate?
* Are common navigation patterns reused?
* Are common states reused?
* Is a new component genuinely required?

---

## 33.7 Data

* Does the screen use fields supported by Brewcipe's data model?
* Does it tolerate missing optional data?
* Are native coffee names preserved correctly?
* Does the interface avoid inventing unavailable metadata?

---

## 33.8 Accessibility

* Is the content order logical?
* Can important actions receive visible focus?
* Are controls understandable without color alone?
* Can icon-only actions receive accessible labels?
* Is important content represented as text rather than imagery alone?

---

## 33.9 States

Where relevant, have the following been considered?

```text
Loading
Empty
Error
Unauthenticated
Authenticated
Saved / Unsaved
AI Processing
AI Failure
```

---

# 34. Wireframe Status

| Experience                  | Priority    | Status             |
| --------------------------- | ----------- | ------------------ |
| Application Shell           | Foundation  | Working hypothesis |
| Home                        | Core        | Drafted            |
| Discover / Coffee Library   | Must Have   | Drafted            |
| Geographic Explore          | Must Have   | Drafted            |
| Continent                   | Must Have   | Drafted            |
| Region                      | Must Have   | Drafted            |
| Country                     | Must Have   | Drafted            |
| Coffee / Recipe Detail      | Must Have   | Drafted            |
| Recipe Minimal-Data Variant | Must Have   | Drafted            |
| Search Initial State        | Must Have   | Drafted            |
| Search Results              | Must Have   | Drafted            |
| Search Empty State          | Must Have   | Drafted            |
| Search Error State          | Must Have   | Drafted            |
| AI Coffee Sommelier         | Should Have | Drafted            |
| AI Recommendation           | Should Have | Drafted            |
| AI Loading / Error          | Should Have | Drafted            |
| Favorite Action             | Should Have | Drafted            |
| Favorites                   | Should Have | Drafted            |
| Favorites Empty State       | Should Have | Drafted            |
| Authentication              | Should Have | Drafted            |
| Account Access              | Should Have | Working hypothesis |

---

# 35. Open Wireframe Decisions

The following decisions should be explored rather than prematurely fixed.

| Decision                                                    | Status |
| ----------------------------------------------------------- | ------ |
| Mobile primary navigation pattern                           | TBD    |
| Desktop navigation composition                              | TBD    |
| Home content density                                        | TBD    |
| Home featured-coffee treatment                              | TBD    |
| Search as dedicated page vs globally integrated interaction | TBD    |
| Geographic list vs visual/map-supported exploration         | TBD    |
| Geographic supporting information                           | TBD    |
| Coffee Card final anatomy                                   | TBD    |
| Coffee naming hierarchy                                     | TBD    |
| Recipe hero composition                                     | TBD    |
| Recipe metadata presentation                                | TBD    |
| Cultural-context placement                                  | TBD    |
| Source-attribution treatment                                | TBD    |
| Authentication presentation                                 | TBD    |
| Post-authentication favorite behavior                       | TBD    |
| Sommelier response composition                              | TBD    |

These should be resolved through iterative wireframing, content testing, and high-fidelity exploration.

---

# 36. MVP Wireframe Boundaries

Current wireframes should not introduce:

* dedicated brewing-method directory pages
* dedicated brewing-method detail pages
* equipment directories
* advanced filter panels
* related-coffee recommendation sections
* recipe comparison
* community submissions
* ratings
* reviews
* comments
* social feeds
* brewing journals
* brewing history
* interactive brewing timers
* recipe scaling
* shopping
* extensive profile management
* administrative interfaces

If one of these becomes a product requirement later, its wireframe can be added after the corresponding PRD and requirements update.

---

# 37. Next Design Step

The low-fidelity wireframes establish the initial screen hierarchy but do not represent final interface designs.

The next design stage should validate the wireframes against:

1. the canonical Brewcipe coffee data
2. real coffee names and multilingual content
3. realistic recipe lengths
4. missing optional data
5. mobile viewport constraints
6. the Brewcipe design system
7. accessibility requirements

After validation, selected core screens can progress into high-fidelity design.

Priority should begin with the **Must Have journey**:

```text
Home
   ↓
Discover
   ↓
Coffee / Recipe Detail

Home
   ↓
Search
   ↓
Search Results
   ↓
Coffee / Recipe Detail

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
Coffee / Recipe Detail
```

Once these core experiences are coherent, Should Have flows such as Favorites and the AI Coffee Sommelier can be refined against the same system.
