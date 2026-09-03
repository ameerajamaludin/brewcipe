# Brewcipe — Design Direction

## 1. Purpose

This document defines the overall experience and visual direction for Brewcipe.

It translates Brewcipe's product goals into design principles that guide the application's interface, content presentation, visual character, and interaction approach.

This document defines **direction rather than detailed implementation specifications**.

Detailed decisions such as exact colors, typography scales, spacing tokens, component variants, and interaction states are maintained in `docs/design/design-system.md`.

Page structure and navigation are maintained in:

* `docs/design/information-architecture-v3.md`
* `docs/design/wireframes-v3.md`

Product scope and system behavior are defined separately in:

* `docs/product/prd.md-v3`
* `docs/product/requirements.md-v3`

---

# 2. Design Vision

Brewcipe should feel like a **modern digital coffee companion**: warm, knowledgeable, culturally curious, and rooted in coffee.

The experience should combine the clarity of a modern web application with inspiration from:

* specialty coffee culture
* brewing guides
* recipe cards
* coffee publications
* café menus
* coffee packaging
* editorial food and drink design

The interface should have a recognizable identity that makes sense specifically for a product about coffee.

Brewcipe should not feel like a generic technology product with coffee content placed on top of it.

The coffee, its preparation, and its cultural context should remain the focus of the experience.

---

# 3. Experience Principles

## 3.1 Coffee First

Coffee should shape Brewcipe's visual and content experience.

Design decisions may draw inspiration from coffee environments and materials, but references to coffee should remain intentional rather than decorative.

The product should communicate its coffee identity through elements such as:

* typography
* photography
* color
* content hierarchy
* recipe presentation
* geographical context
* subtle material or editorial references

Coffee-inspired design should never reduce usability or readability.

---

## 3.2 Content First

Coffee discovery and recipe information are Brewcipe's primary content.

The interface should help users quickly understand:

* what the coffee is
* where it is associated with
* what type of coffee or preparation it is
* what ingredients are required
* what brewing method or equipment is relevant, where available
* how the coffee is prepared
* what cultural context is available
* where the information came from, where source attribution is presented

Visual decoration should support this information rather than compete with it.

---

## 3.3 Accessible Exploration

Brewcipe is intended for both experienced coffee enthusiasts and users with limited knowledge of coffee terminology.

The interface should therefore make exploration approachable without oversimplifying the underlying coffee information.

Users should be able to browse, search, and understand recipes without needing specialist knowledge before using the product.

---

## 3.4 Culture With Context

Brewcipe presents coffee traditions from different countries, regions, languages, and cultural contexts.

The design should treat this information respectfully.

Native coffee names, transliterations, geographical information, and cultural context should be presented as meaningful product content rather than decorative markers of difference.

The interface should avoid visual or written treatment that exoticizes unfamiliar coffee traditions.

---

## 3.5 AI as a Supporting Experience

The AI Coffee Sommelier is a feature within Brewcipe, not Brewcipe's visual identity.

AI functionality should inherit the same visual language as the rest of the product.

The interface should emphasize:

* the user's coffee question
* relevant recommendations
* Brewcipe coffee information
* pathways back into structured recipe content

AI-specific decoration should not dominate the experience.

---

## 3.6 Mobile First

Brewcipe should be designed from smaller viewports outward.

Mobile layouts should prioritize:

* readable recipe content
* comfortable touch interaction
* concise navigation
* accessible search
* clear content hierarchy
* scannable preparation instructions
* prominent primary actions

Larger layouts should progressively use available space without changing the fundamental experience.

Mobile should not be treated as a compressed desktop layout.

---

# 4. Visual Personality

Brewcipe should feel:

**Warm, but not rustic.**

**Modern, but not generic.**

**Editorial, but practical.**

**Considered, but approachable.**

**Coffee-inspired, but not clichéd.**

**Culturally curious, without exoticizing coffee traditions.**

The overall experience should feel closer to a thoughtfully designed coffee guide, brewing journal, café publication, or recipe collection than a generic SaaS application.

---

# 5. Visual Language

## 5.1 Color Direction

Brewcipe's color direction may draw inspiration from coffee and café environments, including references such as:

* espresso
* roasted coffee
* crema
* milk
* oat
* parchment
* ceramic
* wood
* warm interior lighting

This inspiration should not result in an interface composed entirely of brown and beige.

The primary interface should use a restrained palette with clear hierarchy and sufficient contrast.

Accent colors should be intentional and consistent.

Exact color values and semantic color tokens are defined in the design system.

### Avoid

The visual direction should avoid:

* excessive brown-on-brown treatment
* low-contrast neutral palettes
* unnecessary gradients
* neon or stereotypically futuristic AI colors
* unrelated bright accent colors
* excessive competing colors
* page-specific colors without a shared system

Coffee inspiration should never compromise readability or accessibility.

---

## 5.2 Typography Direction

Typography should contribute strongly to Brewcipe's identity while keeping recipe and interface content highly readable.

A suitable direction may combine:

* a characterful editorial or display typeface for selected headings
* a highly readable typeface for body and interface content

The final typography system should support the characters and scripts required by Brewcipe's content.

Because Brewcipe may present native coffee names and transliterations, multilingual and Unicode support must be considered when selecting fonts.

Exact font families, sizes, weights, line heights, and typography tokens belong to the design system.

---

## 5.3 Native Names and Multilingual Content

Native coffee names should be treated as meaningful content.

Where available, the interface may present combinations such as:

**Cà phê vợt**
Vietnam

or:

**Türk kahvesi**
Turkey

The exact hierarchy between native name, transliteration, English name, and geographical information depends on the available data and final component design.

The interface should preserve Unicode characters correctly and avoid treating native names as technical metadata.

---

## 5.4 Shape and Surface Direction

Cards and containers should be used when they improve:

* grouping
* hierarchy
* interaction
* separation
* scannability

Not every section needs to exist inside a card.

Brewcipe should avoid creating visual complexity by placing every piece of information inside separate floating containers.

Surface treatments should remain restrained and support content hierarchy.

Exact border radius, border, elevation, and shadow treatments belong to the design system.

---

## 5.5 Spacing and Layout Direction

Layouts should feel calm and readable while making efficient use of available space.

Spacing should support:

* clear visual hierarchy
* readable recipe content
* comfortable interaction
* predictable grouping
* separation between related and unrelated content
* efficient mobile layouts

Desktop layouts may use additional horizontal space while preserving the hierarchy established on mobile.

Exact spacing values belong to the design system.

---

# 6. Photography and Imagery

Photography may contribute strongly to Brewcipe's identity and discovery experience.

Where imagery is used, it should help users understand or experience the coffee rather than merely decorate the interface.

Relevant imagery may include:

* finished coffee drinks
* brewing equipment
* preparation processes
* ingredients
* traditional serving vessels
* regional preparation methods
* coffee environments where contextually useful

Photography should feel relevant to the represented coffee and avoid generic corporate stock imagery.

Images should not imply cultural or geographical authenticity when that relationship cannot be supported.

Meaningful imagery should include appropriate alternative text.

---

# 7. Iconography

Icons should be used when they improve recognition, navigation, or interface efficiency.

Potential applications include:

* favorites
* search
* navigation
* servings
* temperature
* brewing information where applicable

Icons should not be added solely as decoration.

The interface should use a consistent icon family and visual treatment.

Text should be preferred when an icon alone would make an action ambiguous.

---

# 8. Coffee Discovery Experience

Coffee discovery should encourage exploration without overwhelming users.

The core discovery experience should support the product requirements for:

* browsing available coffees
* coffee-name search
* geographical exploration
* navigation into individual recipes

Discovery interfaces should make individual coffees easy to distinguish and should provide clear pathways into recipe details.

Future filtering, richer geographical visualization, or recommendation features should extend this experience without requiring the core discovery interface to be redesigned fundamentally.

---

# 9. Geographical Exploration Experience

Geography is part of Brewcipe's core discovery model rather than decorative metadata.

Geographical interfaces should help users understand relationships between coffee and place.

The MVP should support the geographical hierarchy established by the product and data model while keeping navigation understandable to users unfamiliar with regional classifications.

Geographical presentation should:

* provide clear location labels
* preserve the relationship between relevant geographical levels
* provide pathways from location to coffee
* avoid implying unsupported cultural or geographical claims
* handle locations with no available recipes gracefully

Richer geographical visualization may be considered beyond the core MVP.

---

# 10. Coffee Recipe Experience

Recipe pages are one of Brewcipe's primary experiences.

The content hierarchy should help users answer:

1. What coffee is this?
2. Where is it associated with?
3. What kind of preparation is it?
4. What ingredients do I need?
5. What brewing method or equipment is relevant, where available?
6. How do I prepare it?
7. What cultural context is available?
8. What source information is available?

Recipe information should be easy to scan while preparing coffee.

Important quantities, ingredients, and preparation steps should not be buried inside unnecessarily long blocks of text.

Optional information should disappear gracefully when unavailable rather than leaving confusing gaps in the layout.

Native names, transliterations, geographical information, and cultural context should form part of the recipe's information hierarchy where available.

---

# 11. Search Experience

Search should provide a straightforward path for users who already have a coffee in mind.

For the core MVP:

* search should be easy to locate and understand
* users should be able to search by coffee name
* search results should be easy to distinguish
* results should provide a clear route to recipe details
* zero-result states should explain that no matching coffee was found
* failures should provide understandable feedback

Additional filtering and searchable attributes may be introduced as the product evolves.

---

# 12. Authentication and Favorites Experience

Authentication should support user-specific functionality without becoming the focus of Brewcipe.

Registration and login interfaces should remain consistent with the wider Brewcipe visual language.

Saving a favorite should feel lightweight and immediately understandable.

Favorite state should remain visually consistent wherever the action appears.

The saved-coffee experience should reuse Brewcipe's established coffee presentation patterns rather than introducing an unrelated dashboard-style interface.

---

# 13. AI Coffee Sommelier Experience

The AI Coffee Sommelier should feel like part of Brewcipe's coffee discovery experience.

The interaction should feel closer to asking a knowledgeable coffee specialist for a recommendation than interacting with a generic chatbot.

The interface should emphasize:

* the user's question
* understandable recommendations
* relevant Brewcipe coffees
* links or pathways to structured recipe information
* clear loading and failure states

Avoid:

* glowing AI orbs
* futuristic gradients
* robot imagery
* generic AI assistant avatars
* excessive sparkle effects
* turning the entire Brewcipe interface into a chat application

The AI interface should remain visually subordinate to Brewcipe's overall coffee identity.

---

# 14. Interaction and Motion Direction

Interactions should feel responsive and restrained.

Motion may be used when it helps:

* communicate state changes
* provide interaction feedback
* reveal information
* reinforce navigation
* preserve perceived continuity

Animation should not exist simply to make Brewcipe appear more technologically advanced.

Motion should not interfere with reading recipes or following preparation instructions.

Reduced-motion preferences should be respected where applicable.

---

# 15. Accessibility Direction

Accessibility should be considered throughout the design process rather than added after interface implementation.

The design should account for:

* sufficient text and interface contrast
* visible keyboard focus
* readable typography
* clear content hierarchy
* appropriately sized interactive targets
* accessible form controls
* meaningful alternative text for relevant imagery
* keyboard-operable core interactions
* communication that does not rely solely on color

Detailed accessibility implementation and component behavior should be defined through the design system and validated during testing.

---

# 16. Responsive Direction

## Mobile

Mobile is the primary design starting point.

Prioritize:

* single-column reading where appropriate
* comfortable touch interaction
* concise navigation
* easy recipe scanning
* accessible search
* clear primary actions

## Tablet

Tablet layouts may progressively introduce additional columns or supporting information where space permits.

## Desktop

Desktop layouts may make greater use of:

* content grids
* wider recipe layouts
* additional supporting content
* expanded navigation where useful

Desktop should remain an extension of the mobile experience rather than become a separate visual system.

---

# 17. Reusable Design Direction

Brewcipe should favor reusable interface patterns over page-specific solutions.

Common patterns may eventually include:

* coffee cards
* recipe information groups
* ingredient lists
* preparation steps
* geographical navigation
* search inputs
* favorite controls
* loading states
* error states
* empty states
* AI recommendation presentation

These represent design roles rather than finalized component specifications.

Exact components, variants, states, tokens, and implementation rules belong to `design-system-v3.md`.

---

# 18. Design Anti-Patterns

Brewcipe should avoid:

* generic AI-generated website aesthetics
* generic SaaS dashboard aesthetics
* excessive gradients
* excessive glassmorphism
* excessive floating cards
* excessive pill-shaped controls
* decorative AI imagery
* inconsistent typography
* arbitrary colors
* arbitrary spacing
* inconsistent interaction patterns
* unnecessary animation
* desktop-first layouts compressed into mobile screens
* excessive coffee clichés
* visual decoration that competes with recipe information
* cultural imagery used without meaningful relevance
* interfaces that make AI appear more important than coffee

---

# 19. Relationship to the Design System

This document defines Brewcipe's **design direction**.

`design-system-v3.md` should translate this direction into reusable implementation rules, including:

* color tokens
* typography
* spacing
* layout foundations
* border and radius treatments
* elevation
* icons
* buttons
* inputs
* cards
* navigation patterns
* feedback states
* accessibility states
* responsive component behavior

When a detailed visual or component decision changes, the design system should normally be updated rather than expanding this document with implementation-level specifications.

If the broader visual or experience philosophy changes, this document should be reviewed.

---

# 20. Desired Overall Impression

When someone opens Brewcipe, the experience should communicate:

> **This is a product made for people who enjoy exploring coffee.**

It should feel closer to a thoughtfully designed coffee guide, brewing journal, café publication, or recipe collection than a generic technology dashboard.

Technology, including AI, should support that experience quietly.

**Coffee remains the main character.**
