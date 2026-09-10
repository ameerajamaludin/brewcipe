# Brewcipe — Low-Fidelity Wireframes

## 1. Overview

### 1.1 Purpose

This document defines low-fidelity wireframes for the Brewcipe MVP.

The wireframes translate Brewcipe's information architecture and design system into preliminary screen structures that establish:

* content hierarchy
* navigation relationships
* primary actions
* mobile-first layout
* tablet and desktop adaptation
* reusable interface patterns
* major interaction flows
* loading, empty, and error states
* responsive behavior

These wireframes intentionally avoid final visual styling.

Final visual implementation should follow:

* `design-direction-v3.md`
* `design-system-v3.md`
* `information-architecture-v3.md`

Product scope remains governed by:

* `prd-v3.md`
* `requirements-v3.md`

The wireframes should reflect Brewcipe's updated interface direction: a dark, warm, editorial coffee identity combined with the clarity, compactness, and navigational efficiency of a modern coffee application.

External visual references documented in `design-direction-v3.md` should inform interaction structure and density rather than be reproduced literally.

---

### 1.2 Wireframe Scope

The current wireframes cover:

#### Must Have

* Application Shell
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
* Account access
* Taste profile and personalized discovery

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
Navigation behavior
Component relationships
Information density
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
Final icon library
```

Those decisions belong to the design system and high-fidelity implementation.

---

# 2. Wireframing Principles

## 2.1 Mobile First, Responsive Throughout

All core experiences should be designed for narrow mobile viewports first.

The same experience should then adapt deliberately across:

```text
Mobile
    ↓
Tablet
    ↓
Desktop
    ↓
Wide Desktop
```

Responsive adaptation may change:

* navigation presentation
* column count
* content width
* spacing
* component density
* image sizing
* component arrangement
* control placement

The underlying content hierarchy and product model should remain consistent.

---

## 2.2 Coffee First

Coffee content should receive visual and structural priority.

Navigation, authentication, AI, and supporting controls should help users reach and understand coffee rather than dominate the interface.

---

## 2.3 Content First

Users should encounter useful coffee content early.

Avoid unnecessary introductory or marketing content before primary discovery actions.

Brewcipe Home should behave primarily as a useful application entry point rather than a long promotional landing page.

---

## 2.4 Compact Where Useful

Application-oriented areas should support efficient scanning.

Compact patterns may be used for:

* navigation
* search results
* metadata
* geography
* favorites
* contextual actions
* repeated coffee results

Reading-heavy content should remain more spacious.

Compactness should improve usability without making Brewcipe feel crowded.

---

## 2.5 Reusable Patterns

Recurring interface structures should reuse common patterns where appropriate.

Examples include:

```text
App Header
Bottom Navigation
Desktop Navigation
Navigation Item
Search Input
Coffee Card
Coffee Row
Geographic Row
Section Header
Information Row
Favorite Control
Loading State
Empty State
Error State
```

---

## 2.6 Cards Are Not the Default

Not every repeated piece of content requires a large card.

Use:

```text
Coffee Card
```

when imagery and discovery benefit from stronger visual presentation.

Use:

```text
Coffee Row
```

when scanning efficiency and information density are more important.

Use spacing, typography, dividers, and information rows where containers are unnecessary.

---

## 2.7 Progressive Disclosure

Discovery screens should show enough information to support selection.

Detailed recipe, cultural, geographical, and provenance information belongs primarily in deeper content views.

---

## 2.8 Optional Data

Wireframes must tolerate incomplete optional recipe information.

Missing data should not produce:

```text
N/A
Unknown
—
Empty section
```

unless there is a genuine product reason to communicate that absence.

Sections without meaningful content should collapse naturally.

---

## 2.9 Native Content

Native coffee names and Unicode content should be represented correctly throughout the interface.

For example:

```text
Cà phê vợt
Café de olla
Türk kahvesi
```

Native names should be treated as meaningful coffee content rather than technical metadata.

---

# 3. Responsive Application Shell

Brewcipe should use a consistent application shell that adapts across screen sizes.

The final primary destinations and labels remain governed by `information-architecture-v3.md`.

The shell should preserve access to Brewcipe's major areas, including:

```text
Home
Discover
Search
Sommelier
Favorites
Authentication / Account Access
```

Not every destination necessarily requires equal prominence or permanent placement.

---

## 3.1 Mobile Shell

The default mobile direction is a compact app header combined with persistent bottom navigation.

```text
┌───────────────────────────────┐
│ Brewcipe                 [○]  │
├───────────────────────────────┤
│                               │
│                               │
│         Page Content          │
│                               │
│                               │
│                               │
│                               │
├───────────────────────────────┤
│  ◯      ◯      ◯      ◯      │
│ Label  Label  Label  Label    │
└───────────────────────────────┘
```

The exact destinations should follow the finalized information architecture.

The mobile bottom navigation should:

* remain persistently accessible on primary application screens
* use icon + concise text label
* communicate the selected destination clearly
* account for device safe areas
* provide comfortable touch targets
* avoid obscuring scrollable content

The top app header should remain compact and should not duplicate the bottom navigation.

It may provide:

* Brewcipe identity
* page title
* back navigation
* contextual action
* account access where appropriate

depending on the current screen.

---

## 3.2 Detail-Screen Mobile Header

Deeper content screens may replace the brand-oriented app header with contextual navigation.

Example:

```text
┌───────────────────────────────┐
│ ←  Coffee name            ♡   │
├───────────────────────────────┤
│                               │
│         Page Content          │
│                               │
```

Primary bottom navigation may remain available where it does not interfere with the focused experience.

The exact treatment should be validated during implementation.

---

## 3.3 Tablet Shell

Tablet should progressively expand the mobile structure.

Smaller tablet layouts may retain bottom navigation.

```text
┌─────────────────────────────────────┐
│ Brewcipe                        [○] │
├─────────────────────────────────────┤
│                                     │
│             Page Content            │
│                                     │
├─────────────────────────────────────┤
│    ◯        ◯        ◯        ◯     │
│  Label    Label    Label    Label   │
└─────────────────────────────────────┘
```

Larger tablet layouts may transition toward desktop navigation when horizontal space supports it.

Tablet should not be treated as merely an enlarged mobile layout.

It may introduce:

* two-column content
* wider cards
* compact grids
* split content where useful
* increased information density

---

## 3.4 Desktop Shell

Desktop should replace mobile bottom navigation with persistent larger-screen navigation.

Default direction:

```text
┌──────────────────────────────────────────────────────────────────┐
│ BREWCIPE    [Primary destinations]                  [Account]    │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│                         Page Content                             │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

The desktop shell should:

* preserve the same primary destination hierarchy as mobile
* provide clear selected navigation
* keep account access available
* support keyboard interaction
* avoid simply stretching the mobile bottom-navigation component horizontally

A navigation rail may be explored if later wireframing demonstrates a stronger fit, but the default direction is a persistent application header.

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

Home should expose useful coffee content early.

---

## 4.3 Mobile Wireframe

```text
┌───────────────────────────────┐
│ Brewcipe                 [○]  │
│                               │
│ Discover coffee               │
│ from around the world.        │
│                               │
│ [ 🔍 Search coffee...       ] │
│                               │
│ Explore                       │
│                               │
│ [ Coffee Library          → ] │
│ [ Explore by Place        → ] │
│                               │
│ ───────────────────────────── │
│                               │
│ Discover coffee               │
│                               │
│ ┌────────────┐ ┌────────────┐ │
│ │   IMAGE    │ │   IMAGE    │ │
│ │ Coffee     │ │ Coffee     │ │
│ │ Country  ♡ │ │ Country  ♡ │ │
│ └────────────┘ └────────────┘ │
│                               │
│ [ See all coffee → ]          │
│                               │
│ ───────────────────────────── │
│                               │
│ Not sure what to try?         │
│                               │
│ Ask the Coffee Sommelier for  │
│ a recommendation.             │
│                               │
│ [ Ask the Sommelier → ]       │
│                               │
├───────────────────────────────┤
│  ◯      ◯      ◯      ◯      │
│ Label  Label  Label  Label    │
└───────────────────────────────┘
```

The Sommelier section should only appear when included in the release.

---

## 4.4 Tablet / Desktop Adaptation

On larger screens, Home may place discovery entry points and featured coffee content into wider or multi-column layouts.

Example:

```text
Discover coffee from around the world.

[ Search coffee...                              ]

Explore

[ Coffee Library ]     [ Explore by Place ]     [ Ask Sommelier ]

Discover coffee

[ Coffee Card ]   [ Coffee Card ]   [ Coffee Card ]   [ Coffee Card ]
```

The page should remain content-led rather than becoming a marketing landing page.

---

# 4A. Taste Profile & Personalized Discovery

## 4A.1 Goal

Give users a simple way to establish their coffee preferences and make the recommendation loop understandable without turning Brewcipe into a settings-heavy profile application.

## 4A.2 Mechanic

```text
Taste Profile
      ↓
Personalized Recommendations
      ↓
Save / Try / Skip
      ↓
Updated Signals
      ↓
Better Recommendations
```

## 4A.3 Initial Taste Profile Wireframe

```text
┌───────────────────────────────┐
│ Tell Brewcipe what you like   │
│                               │
│ Flavor & style                │
│ [ Sweet ] [ Milky ]           │
│ [ Strong ] [ Spiced ]         │
│ [ Simple ]                    │
│                               │
│ Brewing                       │
│ [ Espresso ] [ French Press ] │
│ [ Pour Over ] [ Instant ]     │
│ [ No Equipment ] [ Any ]      │
│                               │
│ Discovery                     │
│ [ Familiar ] [ Global ]       │
│ [ Traditional ] [ Adventurous ]│
│                               │
│ [ Show My Coffees ]           │
└───────────────────────────────┘
```

The final control design belongs to the design system. The wireframe establishes the information and interaction structure only.

## 4A.4 Personalized Home Module

```text
┌───────────────────────────────┐
│ Good morning                  │
│ Coffees chosen for your taste │
│                               │
│ [ Coffee Card ]               │
│ Why this fits: Sweet + Iced  │
│ [ View Recipe ] [ Save ]      │
│                               │
│ [ Coffee Card ]               │
│ Why this fits: Strong + ...  │
│ [ View Recipe ] [ Save ]      │
│                               │
│ [ Ask the Sommelier ]         │
└───────────────────────────────┘
```

The recommendation explanation should be based on actual available signals. It must not invent unsupported taste attributes.

## 4A.5 Interaction Loop

The interface should make meaningful interactions available where recommendations are presented:

```text
Save → expresses interest
Try  → provides stronger preference evidence
Skip → provides avoidance evidence
```

After a supported interaction, the recommendation surface should eventually be able to refresh and reflect the updated signals.

# 5. Discover / Coffee Library

## 5.1 Goal

Allow users to browse Brewcipe coffees without requiring a specific query.

---

## 5.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ Discover                      │
│                               │
│ [ 🔍 Search coffee...       ] │
│                               │
│ [ Explore by Place        → ] │
│                               │
│ Coffee Library                │
│                               │
│ ┌───────────────────────────┐ │
│ │        Coffee Image       │ │
│ │                           │ │
│ │ Vietnam                   │ │
│ │ Cà phê vợt             ♡  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
│ ┌───────────────────────────┐ │
│ │        Coffee Image       │ │
│ │                           │ │
│ │ Mexico                    │ │
│ │ Café de olla           ♡  │ │
│ │ [Relevant metadata]       │ │
│ └───────────────────────────┘ │
│                               │
│ ...                           │
│                               │
├───────────────────────────────┤
│  ◯      ◯      ◯      ◯      │
│ Label  Label  Label  Label    │
└───────────────────────────────┘
```

The Favorite control appears only if Favorites is implemented.

---

## 5.3 Responsive Collection

Mobile should generally prioritize one strong content column.

Tablet may use:

```text
[ Coffee Card ]   [ Coffee Card ]

[ Coffee Card ]   [ Coffee Card ]
```

Desktop may use:

```text
[ Coffee Card ]   [ Coffee Card ]   [ Coffee Card ]

[ Coffee Card ]   [ Coffee Card ]   [ Coffee Card ]
```

Wide desktop may introduce additional columns where card readability remains strong.

Column count should respond to available width rather than being treated as a fixed requirement.

---

## 5.4 Notes

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
│ Continents                    │
│                               │
│ Asia                       →  │
│ [Optional supporting info]    │
│ ───────────────────────────── │
│ Europe                     →  │
│ [Optional supporting info]    │
│ ───────────────────────────── │
│ Africa                     →  │
│ [Optional supporting info]    │
│ ───────────────────────────── │
│ ...                           │
│                               │
├───────────────────────────────┤
│  ◯      ◯      ◯      ◯      │
│ Label  Label  Label  Label    │
└───────────────────────────────┘
```

This deliberately uses compact geographic rows instead of turning every continent into a large card.

Coffee counts should appear only if reliable and useful.

---

## 6.4 Tablet / Desktop

Larger screens may use a multi-column geographic layout:

```text
Explore by Place

Asia                  Europe                Africa
Supporting info       Supporting info       Supporting info
──────────────        ──────────────        ──────────────

North America         South America         Oceania
Supporting info       Supporting info       Supporting info
```

A future map-supported experience should not remove accessible hierarchical navigation.

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
│ Southeast Asia             →  │
│ [Supporting information]      │
│ ───────────────────────────── │
│ East Asia                  →  │
│ [Supporting information]      │
│ ───────────────────────────── │
│ ...                           │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
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
│ Vietnam                    →  │
│ ───────────────────────────── │
│ Thailand                   →  │
│ ───────────────────────────── │
│ Malaysia                   →  │
│ ───────────────────────────── │
│ Indonesia                  →  │
│ ───────────────────────────── │
│ Singapore                  →  │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
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
│ Coffees                       │
│                               │
│ [IMG] Cà phê vợt          ♡  │
│       [Relevant metadata]     │
│ ───────────────────────────── │
│ [IMG] Cà phê kho          ♡  │
│       [Relevant metadata]     │
│ ───────────────────────────── │
│ ...                           │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

A compact Coffee Row is appropriate here because the page already provides strong geographic context.

A Coffee Card variant may still be used if visual exploration proves more effective during high-fidelity design.

---

## 9.4 Notes

The country page should not invent country-level editorial content unless supported by Brewcipe content.

Country context is optional.

---

# 10. Coffee / Recipe Detail

## 10.1 Goal

Present available structured recipe information clearly while preserving geographical, cultural, and source context.

This is Brewcipe's primary content-detail experience.

Recipe readability takes priority over application density.

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
│ Servings       Temperature    │
│ [value]        [value]        │
│                               │
│ Brewer / Method               │
│ [value]                       │
│                               │
│ ───────────────────────────── │
│                               │
│ Ingredients                   │
│                               │
│ [qty]  [Ingredient]           │
│ [qty]  [Ingredient]           │
│ [qty]  [Ingredient]           │
│                               │
│ ───────────────────────────── │
│                               │
│ How to make it                │
│                               │
│ 01  [Preparation instruction] │
│                               │
│ 02  [Preparation instruction] │
│                               │
│ 03  [Preparation instruction] │
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
│ Asia → Southeast Asia         │
│      → Vietnam                │
│                               │
│ ───────────────────────────── │
│                               │
│ Source                        │
│ [Source attribution]          │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

Favorite appears only when implemented.

---

## 10.3 Tablet / Desktop

Recipe Detail should not simply become a wider version of the mobile page.

A larger-screen structure may use:

```text
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│ ┌────────────────────────┐   Vietnam                         │
│ │                        │                                   │
│ │      Coffee Image      │   Cà phê vợt                 ♡   │
│ │                        │   Native / transliteration        │
│ └────────────────────────┘   Recipe type / brewer            │
│                                                              │
├──────────────────────────────────────────────────────────────┤
│ Recipe Information                                           │
│                                                              │
│ Servings          Temperature          Brewer / Method       │
├────────────────────────────┬─────────────────────────────────┤
│                            │                                 │
│ Ingredients                │ How to make it                  │
│                            │                                 │
│ [Ingredient rows]          │ 01  Instruction                │
│                            │ 02  Instruction                │
│                            │ 03  Instruction                │
├────────────────────────────┴─────────────────────────────────┤
│                                                              │
│ About this coffee                                            │
│ [Constrained reading content]                                │
│                                                              │
│ From                                                         │
│ Asia → Southeast Asia → Vietnam                              │
│                                                              │
│ Source                                                       │
└──────────────────────────────────────────────────────────────┘
```

The exact ingredient/instruction split should respond to recipe length.

Long preparation instructions should not be forced into an excessively narrow column merely to preserve a two-column layout.

---

## 10.4 Data Rules

Render only available data.

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

Do not create:

```text
Temperature: N/A
Brewer: Unknown
```

Missing optional information should collapse naturally.

---

## 10.5 Recipe Identity

Coffee naming may require:

```text
Native name
Transliteration
English name
```

Exact visual priority should depend on available data.

Native names should remain meaningful content.

---

## 10.6 Geographic Context

Where useful:

```text
Asia
→ Southeast Asia
→ Vietnam
```

The final implementation may use breadcrumbs, links, a dedicated context section, or another accessible pattern.

---

## 10.7 Source

Preserve space for source attribution.

Source treatment should remain secondary to recipe content while remaining discoverable and legible.

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
│ Ingredients                   │
│                               │
│ [Ingredient]                  │
│ [Ingredient]                  │
│                               │
│ ───────────────────────────── │
│ How to make it                │
│                               │
│ 01  Instruction              │
│                               │
│ 02  Instruction              │
│                               │
│ ───────────────────────────── │
│ Source                        │
│ [Source attribution]          │
│                               │
└───────────────────────────────┘
```

Optional sections should disappear rather than leave empty visual structures.

---

# 12. Search — Initial State

## 12.1 Goal

Allow users to find coffee directly by name.

---

## 12.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ Search                        │
│                               │
│ [ 🔍 Search coffee...       ] │
│                               │
│ [Optional discovery prompt]   │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

Search is a primary destination and should not require unnecessary introductory content.

Advanced filtering is not assumed.

---

# 13. Search Results

Search results should prioritize scanning efficiency.

A Coffee Row is the default mobile hypothesis.

```text
┌───────────────────────────────┐
│ Search                        │
│                               │
│ [ 🔍 café de olla          ×] │
│                               │
│ Results                       │
│                               │
│ [IMG] Café de olla        ♡  │
│       Mexico                  │
│       [Relevant metadata]     │
│ ───────────────────────────── │
│ [IMG] Coffee name         ♡  │
│       Country                 │
│       [Relevant metadata]     │
│ ───────────────────────────── │
│ ...                           │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

Selecting a result opens the canonical Recipe Detail page.

Desktop may use a wider list or Coffee Card grid if testing demonstrates stronger scanability.

---

# 14. Search Empty State

```text
┌───────────────────────────────┐
│ Search                        │
│                               │
│ [ 🔍 xyzcoffee             ×] │
│                               │
│ No coffees found              │
│                               │
│ Try another coffee name or    │
│ explore the coffee library.   │
│                               │
│ [ Explore coffee ]            │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

---

# 15. Search Error State

```text
┌───────────────────────────────┐
│ Search                        │
│                               │
│ [ 🔍 café de olla          ×] │
│                               │
│ We couldn't search the coffee │
│ library right now.            │
│                               │
│ [ Try again ]                 │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

---

# 16. AI Coffee Sommelier

**Priority: Should Have**

## 16.1 Goal

Allow users to describe what they want and receive contextual coffee recommendations.

The experience should feel like a Brewcipe discovery tool rather than a generic chatbot.

---

## 16.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ Coffee Sommelier              │
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
│ Try asking                    │
│                               │
│ [ Coffee from Malaysia? ]     │
│                               │
│ [ Strong without espresso? ]  │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

Suggested prompts are optional supporting content.

They should not visually turn the Sommelier into a conventional messaging application.

---

# 17. AI Sommelier — Recommendation

## 17.1 Goal

Provide understandable recommendations that lead users into Brewcipe's canonical coffee library.

---

## 17.2 Mobile Wireframe

```text
┌───────────────────────────────┐
│ Coffee Sommelier              │
│                               │
│ You asked                     │
│ "I want something sweet       │
│ and iced."                    │
│                               │
│ You might like                │
│                               │
│ [IMG] Coffee Name             │
│       Country                 │
│       [Relevant metadata]     │
│                               │
│ Why it fits                   │
│ [Recommendation explanation]  │
│                               │
│ [ View Recipe ]               │
│                               │
│ ───────────────────────────── │
│                               │
│ [Additional recommendation]   │
│                               │
│ [ Suggest again ]             │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

Where the AI architecture returns multiple grounded recommendations, the same recommendation pattern should repeat consistently.

---

## 17.3 Recommendation Rule

```text
AI Recommendation
        ↓
Grounded Brewcipe Coffee
        ↓
View Recipe
        ↓
Canonical Recipe Detail
```

The Sommelier should not duplicate or replace canonical recipe information.

---

# 18. AI Sommelier — Loading and Error

## 18.1 Loading

```text
Coffee Sommelier

Finding coffee for you...

[ Loading indicator ]
```

## 18.2 Error

```text
Coffee Sommelier

We couldn't generate a
recommendation right now.

[ Try again ]

[ Explore coffee instead ]
```

AI failure should never block normal coffee discovery.

---

# 19. Favorite Action

**Priority: Should Have**

Favorite should be a reusable icon-led action.

Potential locations:

```text
Coffee Card
Coffee Row
Recipe Detail
Favorites
AI Recommendation
```

---

## 19.1 Authenticated Flow

```text
User taps Favorite
        ↓
Saved
        ↓
Favorite state updates
```

---

## 19.2 Unauthenticated Flow

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

Exact post-authentication behavior remains subject to validation.

---

# 20. Favorites

**Priority: Should Have**

## 20.1 Goal

Allow authenticated users to return efficiently to coffees they intentionally saved.

---

## 20.2 Mobile Wireframe

A compact list is the default hypothesis.

```text
┌───────────────────────────────┐
│ Favorites                     │
│                               │
│ Your saved coffees            │
│                               │
│ [IMG] Cà phê vợt          ♥  │
│       Vietnam                 │
│       [Relevant metadata]     │
│ ───────────────────────────── │
│ [IMG] Café de olla        ♥  │
│       Mexico                  │
│       [Relevant metadata]     │
│ ───────────────────────────── │
│ ...                           │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

Tablet and desktop may transition to Coffee Cards if the additional space meaningfully improves discovery.

---

# 21. Favorites Empty State

```text
┌───────────────────────────────┐
│ Favorites                     │
│                               │
│ No favorites yet              │
│                               │
│ Save coffees you want to brew │
│ or return to later.           │
│                               │
│ [ Discover coffee ]           │
│                               │
├───────────────────────────────┤
│      Persistent navigation    │
└───────────────────────────────┘
```

---

# 22. Authentication

**Priority: Should Have**

## 22.1 Goal

Authenticate users when functionality requires persistent user-specific information.

Authentication should remain lightweight and should not block public coffee discovery.

---

## 22.2 Authentication Entry

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

## 22.3 Contextual Authentication

When authentication is triggered by a protected action, explain why sign-in is required.

```text
Save this coffee

Sign in to save coffees and
return to them later.

[ Authentication options ]
```

---

# 23. Authenticated Account Access

Brewcipe requires a lightweight way for authenticated users to:

* understand that they are signed in
* access Favorites
* log out

A full profile-management experience is not required for the MVP.

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

Account presentation may use a page, menu, sheet, or another appropriate pattern depending on the final navigation architecture.

---

# 24. Shared Coffee Card

## 24.1 Purpose

Represent a Brewcipe coffee consistently in visually led discovery contexts.

---

## 24.2 Standard Structure

```text
┌───────────────────────────────┐
│                               │
│         Coffee Image          │
│                               │
├───────────────────────────────┤
│ Country                       │
│ Coffee Name                ♡  │
│ Native Name / metadata        │
└───────────────────────────────┘
```

---

## 24.3 Appropriate Contexts

Potential contexts include:

* Discover
* Home discovery modules
* wider Country layouts
* wider Favorites layouts
* selected recommendation layouts

---

## 24.4 Content Rules

Prioritize identification over detailed recipe information.

Potential content:

```text
Coffee image
Coffee name
Native name where useful
Country
Relevant secondary metadata
Favorite action where applicable
```

Do not place complete recipe information inside discovery cards.

---

# 25. Shared Coffee Row

## 25.1 Purpose

Provide a denser representation of a Brewcipe coffee for scanning-heavy contexts.

---

## 25.2 Structure

```text
┌───────────────────────────────┐
│ [IMG] Coffee Name          ♡  │
│       Country                 │
│       [Relevant metadata]     │
└───────────────────────────────┘
```

---

## 25.3 Appropriate Contexts

Potential contexts:

* Search Results
* Favorites
* Country
* compact recommendation lists
* information-dense discovery contexts

Coffee Card and Coffee Row should represent the same underlying coffee entity using different density.

---

# 26. Shared Geographic Row

Geographical navigation should reuse a compact row pattern.

```text
┌───────────────────────────────┐
│ Southeast Asia             →  │
│ [Optional supporting info]    │
└───────────────────────────────┘
```

Potential contexts:

```text
Explore → Continent
Continent → Region
Region → Country
```

Imagery may be introduced during high-fidelity design where it provides meaningful geographic or cultural context.

---

# 27. Shared App Header

The App Header should establish context without becoming visually dominant.

Possible mobile forms:

```text
Brewcipe                       ○
```

```text
←  Page Title                  ○
```

```text
←                          ♡
```

depending on context.

Avoid presenting every possible action in the header.

---

# 28. Shared Bottom Navigation

The mobile bottom-navigation wireframe should use:

```text
┌───────────────────────────────┐
│  ◯      ◯      ◯      ◯      │
│ Label  Label  Label  Label    │
└───────────────────────────────┘
```

The exact number, labels, and destinations should be resolved through `information-architecture-v3.md`.

Each item should contain:

```text
Icon
+
Short label
```

The current destination should have a persistent selected state.

Bottom navigation should not be used for contextual actions such as:

* back
* favorite
* close
* filter

Those belong to the relevant page or component.

---

# 29. Shared Page States

## 29.1 Loading

Loading pages should preserve enough surrounding structure that users understand where they are.

```text
[ Page Header ]

[ Loading content ]
[ Loading content ]
[ Loading content ]

[ Persistent Navigation ]
```

Skeletons, progress indicators, or another design-system pattern may be selected during high-fidelity implementation.

---

## 29.2 Empty

Empty collections should:

* explain why no content is shown
* avoid looking broken
* provide a useful next action where one exists

---

## 29.3 Error

Errors should:

* explain the problem clearly
* provide recovery where possible
* preserve access to other Brewcipe discovery paths

---

# 30. Responsive Collection Behavior

## 30.1 Mobile

Default:

```text
Coffee Card

Coffee Card

Coffee Card
```

or, in scanning-heavy contexts:

```text
Coffee Row
──────────
Coffee Row
──────────
Coffee Row
```

---

## 30.2 Tablet

Potential:

```text
Coffee Card       Coffee Card

Coffee Card       Coffee Card
```

Compact rows may remain full width where scanability is more important than visual discovery.

---

## 30.3 Desktop

Potential:

```text
Coffee Card       Coffee Card       Coffee Card

Coffee Card       Coffee Card       Coffee Card
```

---

## 30.4 Wide Desktop

Additional columns may be introduced where card width remains useful.

The interface should increase whitespace before excessively increasing component width.

---

# 31. Responsive Behavior by Viewport

## 31.1 Mobile

Typical behavior:

* single-column primary content
* persistent bottom navigation
* compact app headers
* full-width or near-full-width search
* touch-first controls
* vertical cards and rows
* reading content using available width within page gutters

---

## 31.2 Tablet

Typical behavior:

* one- or two-column content
* bottom or adaptive navigation
* increased gutters
* larger content areas
* selective split layouts
* increased information density where useful

---

## 31.3 Desktop

Typical behavior:

* persistent desktop navigation
* no mobile bottom navigation
* multi-column discovery layouts
* bounded search interfaces
* selective split-detail layouts
* constrained recipe reading widths
* pointer and keyboard interaction

---

## 31.4 Wide Desktop

Typical behavior:

* maximum-width application containers
* additional discovery columns where appropriate
* increased surrounding whitespace
* stable reading widths
* restrained component scaling

---

# 32. Responsive Principles

Across responsive layouts:

### Preserve

* content hierarchy
* terminology
* primary actions
* canonical coffee destinations
* navigation hierarchy
* component meaning
* accessible routes to functionality

### Adapt

* navigation presentation
* column count
* content width
* spacing
* component density
* image sizing
* control placement
* component arrangement

### Avoid

* hiding essential content on mobile
* treating tablet as an afterthought
* creating unrelated mobile and desktop experiences
* stretching content indefinitely on wide screens
* retaining mobile navigation literally when a better desktop presentation exists
* introducing desktop-only functionality without product justification

---

# 33. Core User Flows

## 33.1 Discovery

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

## 33.2 Search

```text
Search
   ↓
Search Results
   ↓
Recipe Detail
```

---

## 33.3 Geography

```text
Explore by Place
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

## 33.4 Sommelier

```text
Sommelier
   ↓
User Preference
   ↓
Grounded Recommendation
   ↓
Recipe Detail
```

---

## 33.5 Favorite

```text
Coffee
   ↓
Favorite
   ↓
Authentication if required
   ↓
Saved
   ↓
Favorites
   ↓
Recipe Detail
```

---

# 34. Wireframe Validation Checklist

Before moving a wireframe into high-fidelity design, validate the following.

## 34.1 Product Alignment

* Does the screen support a current PRD requirement?
* Has unsupported functionality been introduced?
* Is the feature correctly treated as Must Have or Should Have?

---

## 34.2 Purpose

* Is the screen purpose clear?
* Is the primary action understandable?
* Does the screen help users progress toward coffee content?

---

## 34.3 Information Hierarchy

* Is the most important information appropriately prioritized?
* Is unnecessary information removed?
* Is detailed information progressively disclosed?
* Is application UI compact where useful without compromising reading content?

---

## 34.4 Navigation

* Can users understand where they are?
* Is the selected primary destination clear?
* Can they return to major Brewcipe areas?
* Does mobile navigation remain reachable?
* Does desktop navigation provide equivalent access?
* Does geographical navigation preserve the correct hierarchy?
* Are back and contextual actions separated from primary navigation?

---

## 34.5 Responsive Behavior

* Does the experience work at narrow mobile widths?
* Does it adapt intentionally to tablet?
* Does it adapt intentionally to desktop?
* Does it remain controlled on wide desktop?
* Does navigation transform appropriately?
* Does reading content remain constrained?
* Do discovery layouts make useful use of additional horizontal space?

---

## 34.6 Touch and Interaction

* Are touch controls comfortable?
* Are frequently used controls easy to reach?
* Does persistent bottom navigation avoid obscuring content?
* Can desktop interactions also be operated by keyboard?

---

## 34.7 Reuse

* Is Coffee Card used where visual discovery matters?
* Would Coffee Row communicate the content more efficiently?
* Are common navigation patterns reused?
* Are common states reused?
* Is a new component genuinely required?

---

## 34.8 Data

* Does the screen use fields supported by Brewcipe's data model?
* Does it tolerate missing optional data?
* Are native coffee names preserved correctly?
* Does the interface avoid inventing unavailable metadata?

---

## 34.9 Accessibility

* Is content order logical?
* Can important actions receive visible focus?
* Are controls understandable without color alone?
* Do icon-only actions receive accessible labels?
* Do navigation icons also provide understandable labels where required?
* Is important content represented as text rather than imagery alone?

---

## 34.10 States

Where relevant, consider:

```text
Loading
Empty
Error
Unauthenticated
Authenticated
Saved / Unsaved
Selected Navigation
AI Processing
AI Failure
```

---

# 35. Wireframe Status

| Experience                   | Priority    | Status             |
| ---------------------------- | ----------- | ------------------ |
| Responsive Application Shell | Foundation  | Updated hypothesis |
| Mobile Bottom Navigation     | Foundation  | Updated hypothesis |
| Tablet Navigation            | Foundation  | Updated hypothesis |
| Desktop Navigation           | Foundation  | Updated hypothesis |
| Home                         | Core        | Updated            |
| Discover / Coffee Library    | Must Have   | Updated            |
| Geographic Explore           | Must Have   | Updated            |
| Continent                    | Must Have   | Updated            |
| Region                       | Must Have   | Updated            |
| Country                      | Must Have   | Updated            |
| Coffee / Recipe Detail       | Must Have   | Updated            |
| Recipe Minimal-Data Variant  | Must Have   | Updated            |
| Search Initial State         | Must Have   | Updated            |
| Search Results               | Must Have   | Updated            |
| Search Empty State           | Must Have   | Updated            |
| Search Error State           | Must Have   | Updated            |
| AI Coffee Sommelier          | Should Have | Updated            |
| AI Recommendation            | Should Have | Updated            |
| AI Loading / Error           | Should Have | Updated            |
| Favorite Action              | Should Have | Updated            |
| Favorites                    | Should Have | Updated            |
| Favorites Empty State        | Should Have | Updated            |
| Authentication               | Should Have | Updated            |
| Account Access               | Should Have | Working hypothesis |
| Coffee Card                  | Shared      | Updated            |
| Coffee Row                   | Shared      | Added              |
| Geographic Row               | Shared      | Updated            |
| App Header                   | Shared      | Added              |

---

# 36. Open Wireframe Decisions

The following decisions should remain open until the corresponding IA, data, usability, or high-fidelity work resolves them.

| Decision                                            | Status                    |
| --------------------------------------------------- | ------------------------- |
| Exact primary mobile navigation destinations        | IA decision               |
| Exact primary navigation labels                     | IA decision               |
| Number of persistent bottom-navigation items        | IA / usability decision   |
| Exact tablet navigation transition point            | Responsive validation     |
| Desktop header vs navigation rail                   | Wireframe validation      |
| Home content density                                | High-fidelity validation  |
| Home featured-coffee quantity                       | High-fidelity validation  |
| Search integration into desktop navigation          | Wireframe validation      |
| Geographic list vs future map-supported exploration | Future exploration        |
| Geographic supporting information                   | Data validation           |
| Coffee Card final anatomy                           | High-fidelity validation  |
| Coffee Row final anatomy                            | High-fidelity validation  |
| Coffee naming hierarchy                             | Content validation        |
| Recipe hero composition                             | High-fidelity validation  |
| Recipe metadata presentation                        | High-fidelity validation  |
| Recipe desktop column behavior                      | Content validation        |
| Cultural-context placement                          | Content validation        |
| Source-attribution treatment                        | High-fidelity validation  |
| Authentication presentation                         | Implementation validation |
| Post-authentication favorite behavior               | Interaction validation    |
| Sommelier recommendation composition                | AI / content validation   |

Navigation should not remain generically "TBD" where the design direction has already established a responsive navigation model.

The remaining navigation questions concern hierarchy, labels, exact destinations, and implementation details.

---

# 37. MVP Wireframe Boundaries

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

Visual inspiration from other coffee applications should not be interpreted as permission to introduce their product functionality into Brewcipe.

If one of these capabilities becomes a product requirement later, its wireframe can be added after the corresponding PRD and requirements update.

---

# 38. Relationship to Visual Direction

These wireframes establish Brewcipe's updated structural direction.

The intended relationship is:

```text
Brewcipe Identity
Dark + Warm + Editorial + Coffee-focused
                │
                ▼
Application Structure
Compact + Clear + Icon-led + Navigable
                │
                ▼
Responsive Experience
Mobile → Tablet → Desktop → Wide Desktop
```

The wireframes may take directional inspiration from modern coffee applications documented in `design-direction-v3.md`, particularly in:

* mobile navigation
* icon-led interaction
* compact information presentation
* app-header structure
* list and card density
* structured metadata
* responsive application organization

They should not reproduce another product's:

* branding
* visual theme
* exact navigation hierarchy
* proprietary icons
* exact layouts
* typography
* imagery
* feature set

Brewcipe should remain recognizably Brewcipe.

---

# 39. Next Design Step

These low-fidelity wireframes establish the updated responsive screen hierarchy but do not represent final interface designs.

The next design stage should validate them against:

1. the canonical Brewcipe coffee data
2. real coffee names and multilingual content
3. realistic recipe lengths
4. missing optional data
5. narrow mobile viewports
6. tablet viewports
7. desktop and wide-desktop viewports
8. the updated Brewcipe design system
9. finalized information architecture
10. accessibility requirements
11. persistent navigation behavior
12. realistic Coffee Card and Coffee Row content

Priority should begin with the Must Have journeys:

```text
Home
   ↓
Discover
   ↓
Coffee / Recipe Detail

Search
   ↓
Search Results
   ↓
Coffee / Recipe Detail

Explore by Place
   ↓
Continent
   ↓
Region
   ↓
Country
   ↓
Coffee / Recipe Detail
```

Before high-fidelity design is treated as stable, test these journeys at minimum in:

```text
Narrow Mobile
Standard Mobile
Tablet
Desktop
Wide Desktop
```

Once these core experiences are coherent, Should Have flows such as Favorites and the AI Coffee Sommelier should be refined against the same responsive system.
