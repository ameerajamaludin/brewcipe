# Brewcipe — Design System

## 1. Overview

### 1.1 Purpose

This document defines the reusable visual, interaction, and component system for Brewcipe.

It translates the experience principles established in `design-direction-v3.md` into concrete foundations and reusable patterns for the Brewcipe web application.

The design system exists to support:

* visual consistency
* reusable design patterns
* predictable interaction behavior
* maintainable frontend implementation
* mobile-first responsive design
* accessible interfaces
* multilingual coffee content
* flexible theming
* a distinctive Brewcipe brand identity

The design system should be consulted before introducing page-specific visual patterns or new reusable components.

---

### 1.2 Scope

This document defines:

* design tokens
* color
* typography
* spacing
* layout
* responsive behavior
* shape
* borders and elevation
* iconography
* imagery
* motion
* shared UI components
* Brewcipe-specific components
* interaction states
* accessibility
* theme architecture
* multilingual content behavior
* component architecture and governance

This document does not define:

* product scope
* feature priorities
* user stories
* detailed page information architecture
* complete page layouts
* backend behavior
* database structure

Those responsibilities belong to the relevant Brewcipe product, architecture, information architecture, and wireframe documentation.

---

### 1.3 Relationship to Other Documentation

```text
Product requirements
        ↓
Design Direction
        ↓
Design System
        ↓
Information Architecture / Wireframes
        ↓
Frontend Implementation
```

`design-direction-v3.md` defines how Brewcipe should feel.

`design-system-v3.md` defines the reusable visual and interaction rules used to achieve that direction.

`information-architecture-v3.md` and `wireframes-v3.md` define how content and functionality are organized into actual user experiences.

---

# 2. Design Principles

## 2.1 Coffee First

Coffee remains the primary subject of the interface.

The design system should support coffee content rather than competing with it.

Coffee influence should come through typography, color, photography, content, and atmosphere rather than excessive decorative coffee motifs.

---

## 2.2 Content First

Structured coffee information should remain easy to discover, read, and use.

Visual treatments should strengthen content hierarchy rather than obscure it.

---

## 2.3 Reuse Before Creating

Before introducing a new UI pattern:

1. check whether an existing Brewcipe component supports the requirement
2. check whether existing primitives can be composed to support it
3. create a new reusable component only when existing patterns cannot reasonably satisfy the requirement

Individual pages should not independently recreate shared patterns.

---

## 2.4 Tokens Before Arbitrary Values

Recurring visual properties should use design tokens.

This includes:

* colors
* typography
* spacing
* radius
* borders
* elevation
* motion where applicable

Avoid scattering arbitrary values throughout individual components or pages.

---

## 2.5 Mobile First, Responsive Throughout

Mobile is the baseline Brewcipe experience.

Layouts and component behavior should support smaller screens first, then adapt deliberately across tablet, desktop, and wide desktop viewports.

Responsive adaptation may change:

* navigation presentation
* column count
* content width
* spacing
* component arrangement
* control placement
* information density

The same core content hierarchy and interaction model should remain recognizable across screen sizes.

Mobile patterns do not need to be reproduced literally on larger screens. For example, persistent mobile bottom navigation may transform into desktop header navigation while preserving access to the same primary destinations.

Larger-screen behavior should progressively enhance the experience rather than create an unrelated desktop design system.

---

## 2.6 Accessible by Default

Accessibility should be incorporated into shared foundations and components rather than treated as a page-level correction.

Brewcipe targets WCAG 2.2 Level AA for the web interface.

---

# Foundations

# 3. Design Tokens

## 3.1 Token Architecture

Brewcipe uses three conceptual token layers:

```text
Primitive Tokens
        ↓
Semantic Tokens
        ↓
Component Tokens
```

This architecture separates raw visual values from their purpose within the interface.

It allows Brewcipe to:

* change the visual palette without redesigning individual components
* support additional themes
* maintain consistent UI behavior
* reduce arbitrary implementation values

---

## 3.2 Primitive Tokens

Primitive tokens represent raw design values.

Examples:

```text
color.charcoal.*
color.wine.*
color.taupe.*
color.espresso.*
color.gold.*
color.grey.*

space.*
radius.*
font.*
```

Primitive tokens should generally not determine component meaning by themselves.

For example:

```text
color.wine.600
```

describes a color.

It does not mean:

```text
primary button
```

---

## 3.3 Semantic Tokens

Semantic tokens describe the purpose of a value.

Examples:

```text
color.background.primary
color.background.secondary

color.surface.primary
color.surface.secondary
color.surface.elevated

color.text.primary
color.text.secondary
color.text.muted
color.text.inverse

color.border.default
color.border.strong

color.action.primary
color.action.primary.hover
color.action.primary.active

color.focus

color.status.success
color.status.warning
color.status.error
color.status.information
```

Components should prefer semantic tokens over direct primitive colors.

---

## 3.4 Component Tokens

Component tokens may be introduced where a reusable component requires more specific control.

Examples:

```text
button.primary.background
button.primary.text
button.primary.border

input.background
input.border
input.border.focus

card.background
card.border
```

Component tokens should reference semantic or primitive foundations rather than introducing unrelated values.

Not every component requires its own token layer.

---

## 3.5 Naming Convention

Token names should describe purpose clearly and remain independent from individual pages.

Prefer:

```text
color.text.secondary
```

over:

```text
recipeGrey
```

Prefer:

```text
color.surface.elevated
```

over:

```text
modalDark
```

Names should remain meaningful if Brewcipe's palette changes in the future.

---

# 4. Color

## 4.1 Color Philosophy

Brewcipe uses a dark-first color system inspired by:

* roasted coffee
* espresso
* warm café interiors
* ceramics
* printed coffee publications
* natural materials

The interface should feel:

* dark
* warm
* editorial
* tactile
* quiet
* coffee-focused

It should not feel:

* cyberpunk
* gaming-oriented
* neon
* generic SaaS
* generically AI-themed
* black-and-gold luxury themed

Dark mode should use warm dark tones rather than relying exclusively on pure black.

---

## 4.2 Brand Palette

The initial Brewcipe brand palette is:

```text
Charcoal Black     #2C2C2C
Deep Wine          #702632
Muted Taupe        #A4978E
Espresso Brown     #594A42
Warm Gold          #C2A878
Ash Grey           #D6D6D6
```

These values establish Brewcipe's initial brand direction.

They are brand primitives rather than fixed component assignments.

---

## 4.3 Primitive Palette

The final implementation palette should derive usable tonal ranges from the Brewcipe brand colors.

Conceptually:

```text
charcoal.*
wine.*
taupe.*
espresso.*
gold.*
grey.*
```

Additional tones may be introduced where required for:

* surface hierarchy
* hover states
* active states
* disabled states
* borders
* text hierarchy
* accessibility

Exact tonal scales remain to be finalized through visual and contrast testing.

---

## 4.4 Semantic Color Roles

The UI should use semantic color roles such as:

```text
Background Primary
Background Secondary

Surface Primary
Surface Secondary
Surface Elevated

Text Primary
Text Secondary
Text Muted
Text Inverse

Border Default
Border Strong

Action Primary
Action Primary Hover
Action Primary Active

Focus

Success
Warning
Error
Information
```

Exact mappings will be established when the expanded dark palette is finalized.

---

## 4.5 Brand Colors

### Deep Wine

`#702632`

Deep Wine provides a distinctive Brewcipe brand accent.

It may support:

* selected brand moments
* emphasis
* interactive treatments where sufficient contrast is maintained
* selected states

It should not automatically become the background of every primary button.

---

### Espresso Brown

`#594A42`

Espresso Brown introduces coffee warmth into the system.

It should be used selectively rather than making every interface element brown.

---

### Warm Gold

`#C2A878`

Warm Gold may provide selective warmth, emphasis, or highlighting.

It should not be used excessively or in ways that make Brewcipe resemble a black-and-gold luxury brand.

---

## 4.6 Surface Colors

Dark-mode surfaces should establish clear but restrained hierarchy.

Conceptually:

```text
Page Background
        ↓
Primary Surface
        ↓
Secondary Surface
        ↓
Elevated Surface
```

Surface separation may use:

* subtle luminance differences
* borders
* spacing
* elevation where necessary

Not every content group requires a card.

---

## 4.7 Text Colors

The system should provide at minimum:

```text
Primary text
Secondary text
Muted text
Inverse text
```

Dark-mode text should use warm or neutral light tones where appropriate rather than defaulting automatically to pure white.

Muted text must remain sufficiently readable.

---

## 4.8 Border Colors

Borders should remain subtle while maintaining sufficient visibility against dark surfaces.

At minimum:

```text
Border Default
Border Strong
```

Borders should often be preferred over heavy shadows for defining interface structure.

---

## 4.9 Interactive Colors

Interactive colors should account for:

```text
Default
Hover
Active / Pressed
Selected
Disabled
Focus
```

State differences should remain understandable without relying exclusively on color.

---

## 4.10 Status Colors

Semantic status colors should be separate from the Brewcipe coffee palette.

The system should provide:

```text
Success
Warning
Error
Information
```

Exact values remain TBD and should be selected according to accessibility and recognizability rather than forcing all statuses into Brewcipe's brand colors.

---

## 4.11 Focus Color

Interactive controls must provide a visible focus treatment.

The final focus token should:

* remain visible against all supported surfaces
* meet accessibility needs
* remain consistent across components

Exact value: **TBD**

---

## 4.12 Contrast Requirements

Color combinations should be tested against Brewcipe's WCAG 2.2 AA accessibility target.

Special attention should be given to:

* muted text
* disabled controls
* text over imagery
* borders
* Deep Wine on dark surfaces
* Warm Gold combinations
* interactive states

A visually attractive color combination should not be accepted if it makes important content difficult to perceive.

---

## 4.13 Color Usage Rules

Do not:

* introduce arbitrary page-specific colors
* hard-code brand primitives throughout components
* use pure black automatically for all dark surfaces
* use brown for every coffee-related element
* use gradients as default surfaces
* introduce neon AI accents
* use Deep Wine everywhere simply because it is the brand accent
* use Warm Gold excessively
* communicate states through color alone

---

# 5. Typography

## 5.1 Typography Strategy

Brewcipe should use a restrained typography system combining three clearly defined roles:

```text
Brand Typography
        +
Editorial / Coffee Typography
        +
Interface / Content Typography
```

Each typeface should have a specific responsibility within the product.

```text
Piscolabis
Brand identity and rare expressive moments

Fraunces
Coffee identity, recipe titles, and editorial moments

Plus Jakarta Sans
Interface, content, controls, and structured data
```

Typography should contribute substantially to Brewcipe's warm, editorial, and coffee-focused character.

Decorative coffee graphics should not be required to make the product feel coffee-oriented.

The typography system should remain restrained. The three typefaces should not compete for attention or be used together without a clear semantic reason.

---

## 5.2 Brand Typeface

**Typeface: Piscolabis**

Piscolabis is Brewcipe's dedicated brand typeface.

Its role is narrower than the product's editorial and interface typography. It should provide distinctive brand character without affecting the readability of everyday product experiences.

Potential uses include:

* Brewcipe wordmark exploration
* brand treatments
* selected campaign or promotional moments
* rare expressive brand applications

Piscolabis should not be used for:

* coffee names
* recipe titles
* section headings
* body copy
* recipe instructions
* form controls
* navigation
* metadata
* AI responses
* long passages
* general application UI

Piscolabis should rarely appear alongside both Fraunces and Plus Jakarta Sans within the same interface composition.

Its use remains subject to visual and multilingual validation where applicable.

---

## 5.3 Editorial / Coffee Typeface

**Typeface: Fraunces**

Fraunces is Brewcipe's secondary typeface and provides the product's editorial character.

It should primarily be used where typography represents coffee identity, discovery, storytelling, or editorial emphasis rather than interface functionality.

Appropriate uses include:

* coffee names
* recipe titles
* selected discovery titles
* editorial features
* selected hero typography
* prominent coffee-focused content moments

Fraunces should not automatically be applied to every heading.

Functional section headings such as:

* Ingredients
* Instructions
* Cultural Context
* Geography
* Brewing Details

should generally use the interface typeface unless a specific editorial treatment is justified.

Fraunces should not be used for:

* body copy
* long-form cultural context
* recipe instructions
* navigation
* buttons
* form controls
* filters
* metadata
* structured recipe data
* AI responses
* dense application UI

This distinction allows Fraunces to retain its visual impact without making Brewcipe excessively serif-heavy.

---

## 5.4 Interface / Content Typeface

**Typeface: Plus Jakarta Sans**

Plus Jakarta Sans is Brewcipe's primary interface and content typeface.

It should be used for the majority of product interactions and reading experiences, including:

* navigation
* interface headings
* section headings
* body copy
* ingredients
* preparation instructions
* buttons
* forms
* filters
* search
* metadata
* geography labels
* recipe measurements
* brew ratios
* temperatures
* brew times
* AI Sommelier responses

Plus Jakarta Sans should provide a clear, contemporary, and highly readable foundation while allowing Fraunces and Piscolabis to provide character in more selective roles.

Numerical information should remain particularly clear because structured brewing data is an important part of Brewcipe's content.

Tabular numerals may be used where numerical alignment provides a functional benefit, such as:

* timers
* comparison views
* tables
* aligned recipe measurements
* structured numerical displays

Tabular numerals should not be enabled globally where proportional numerals provide more natural reading within prose.

---

## 5.5 Font Fallbacks

Brewcipe contains multilingual coffee names and content.

Font stacks should therefore provide appropriate fallbacks when the primary typeface does not contain the required glyph.

Conceptually, interface typography should follow:

```css
font-family:
  "Plus Jakarta Sans",
  "Noto Sans",
  system-ui,
  sans-serif;
```

Editorial typography should follow:

```css
font-family:
  "Fraunces",
  "Noto Serif",
  serif;
```

Script-specific Noto fonts or equivalent fallbacks may be introduced where required by Brewcipe's production data.

Fallback behavior should be determined by the scripts represented in the actual coffee dataset rather than English content alone.

A missing glyph must never be treated as an acceptable degradation.

---

## 5.6 Type Scale

The type scale should remain limited, semantic, and mobile-first.

Recommended starting scale:

```text
Display
48–56px / 1.05–1.10
Fraunces

Coffee Title
36–40px / 1.10
Fraunces

Heading 1
32px / 40px
Plus Jakarta Sans / Semibold

Heading 2
24px / 32px
Plus Jakarta Sans / Semibold

Heading 3
20px / 28px
Plus Jakarta Sans / Semibold

Body Large
18px / 28px
Plus Jakarta Sans / Regular

Body
16px / 26px
Plus Jakarta Sans / Regular

Body Small
14px / 20px
Plus Jakarta Sans / Regular or Medium

Label
14px / 20px
Plus Jakarta Sans / Medium or Semibold

Caption
12px / 16px
Plus Jakarta Sans / Medium
```

Display and coffee-title sizes may scale responsively where justified.

Large typography should not be increased solely for visual impact. It should reflect the hierarchy and importance of the content.

The scale should be validated across actual Brewcipe interfaces, particularly:

* Home
* Discover
* Search
* Geography
* Recipe Detail
* AI Sommelier

---

## 5.7 Font Weights

The primary Plus Jakarta Sans weight set should remain restrained.

Recommended interface weights:

```text
Regular       400
Medium        500
Semibold      600
```

Bold `700` should not be loaded or used by default unless a recurring product need is identified during implementation.

Avoid relying on excessive font weight to establish hierarchy.

Hierarchy should primarily come from:

* typeface role
* font size
* spacing
* placement
* surface hierarchy
* content importance

Fraunces weights should also be limited to those required by actual editorial treatments.

---

## 5.8 Line Height

Line height should prioritize readability and comfortable reading.

Reading-heavy content such as:

* cultural context
* ingredients
* preparation instructions
* coffee descriptions
* AI responses

should use generous line spacing.

The default body style should use approximately:

```text
16px / 26px
```

Display and coffee-title typography may use tighter line heights where readability remains strong.

Line height should be evaluated using real Brewcipe content, including long coffee names and multilingual text.

---

## 5.9 Letter Spacing

Letter spacing should generally follow each typeface's natural metrics.

Custom tracking may be introduced for specific display, label, or metadata styles when visually justified.

Avoid:

* arbitrary tracking values
* excessive uppercase letter spacing
* applying the same tracking treatment across different typefaces
* compensating for poor hierarchy through letter spacing

Letter spacing should be defined through reusable typography tokens rather than individual components.

---

## 5.10 Text Styles

Reusable semantic text styles should reflect content roles rather than arbitrary visual sizes.

Core styles may include:

```text
text.display
text.coffeeTitle

text.heading1
text.heading2
text.heading3

text.bodyLarge
text.body
text.bodySmall

text.label
text.caption
text.button
```

Typeface mapping should conceptually follow:

```text
text.display        → Fraunces
text.coffeeTitle    → Fraunces

text.heading1       → Plus Jakarta Sans
text.heading2       → Plus Jakarta Sans
text.heading3       → Plus Jakarta Sans

text.bodyLarge      → Plus Jakarta Sans
text.body           → Plus Jakarta Sans
text.bodySmall      → Plus Jakarta Sans

text.label          → Plus Jakarta Sans
text.caption        → Plus Jakarta Sans
text.button         → Plus Jakarta Sans
```

Editorial exceptions may use Fraunces where the content represents coffee identity, discovery, or storytelling.

Components should consume semantic typography styles rather than independently defining font family, font size, weight, line height, and letter spacing.

Additional styles should only be introduced where recurring product needs justify them.

---

## 5.11 Numerical Typography

Brewing data is an important part of Brewcipe's information hierarchy.

Numerical content may include:

* coffee-to-water ratios
* ingredient quantities
* temperatures
* brew times
* serving quantities
* measurements

Plus Jakarta Sans should be used for structured numerical information.

Examples include:

```text
1:15
18 g
250 ml
93°C
2:30
```

Tabular numerals should be enabled where values need to align consistently or remain visually stable as they change.

Examples include:

* active timers
* structured data columns
* comparison interfaces
* aligned measurement groups

Proportional numerals should remain the default for numbers embedded naturally within body copy.

---

## 5.12 Multilingual Typography

Typography must be tested using representative Brewcipe content rather than English placeholder text alone.

Testing should include:

* native coffee names
* accented Latin characters
* long coffee names
* transliterated names
* non-Latin scripts represented in Brewcipe's production data
* mixed-script content
* numerical recipe information

Representative examples should include actual coffee names from Brewcipe's dataset.

Fraunces should only be used for a native coffee name when the required characters and script are rendered correctly.

When Fraunces does not support the required script, the interface should fall back gracefully to an appropriate script-compatible typeface.

Native coffee names are meaningful product content and should not be visually reduced to insignificant metadata solely because a fallback font is required.

Fallback typography should preserve the intended hierarchy as closely as possible.

No coffee name should display:

* missing glyphs
* tofu characters
* broken Unicode
* unreadable substitutions
* inappropriate script rendering

---

## 5.13 Typography Usage Rules

Do:

* use Plus Jakarta Sans as the default product typeface
* use Fraunces selectively for coffee identity and editorial emphasis
* reserve Piscolabis for brand-specific applications
* use semantic typography tokens
* prioritize readability for recipe and cultural content
* test typography with real multilingual Brewcipe data
* use tabular numerals only where alignment provides functional value
* preserve hierarchy when fallback fonts are required

Do not:

* use Fraunces for every heading
* use Piscolabis as a general display or interface font
* use display or editorial typography for long-form content
* introduce arbitrary font sizes
* introduce arbitrary font weights
* introduce arbitrary line heights or tracking
* use multiple decorative typefaces without clearly defined roles
* place all three Brewcipe typefaces together without a clear reason
* sacrifice readability for brand character
* assume all coffee names use Latin characters
* allow missing glyphs or broken Unicode to reach the interface
* create typography styling independently inside individual components when an existing semantic style can be reused

---

## 5.14 Typography Principle

Brewcipe's typography should communicate three layers of the product:

```text
Piscolabis
Brand

Fraunces
Coffee + Editorial Character

Plus Jakarta Sans
Product + Reading + Interaction
```

The interface should feel expressive because the typography roles are deliberate, not because decorative typography is used everywhere.

When in doubt, default to Plus Jakarta Sans and introduce Fraunces or Piscolabis only when the content's role clearly justifies it.


---

# 6. Spacing

## 6.1 Base Unit

Brewcipe uses a **4px base spacing unit**.

---

## 6.2 Spacing Scale

```text
0       0
1       4px
2       8px
3       12px
4       16px
5       20px
6       24px
8       32px
10      40px
12      48px
16      64px
20      80px
24      96px
```

---

## 6.3 Usage Guidance

Typical relationships:

```text
4–8px       closely related content
8–12px      compact component spacing
16px        standard component spacing
24px        content grouping
32px        section separation
48–64px     major content separation
```

Use the established scale before introducing custom spacing values.

---

# 7. Layout & Grid

## 7.1 Layout Philosophy

Brewcipe should use responsive containers and content-aware layouts rather than stretching interfaces indefinitely across available screen width.

Layout should support both:

* compact, application-oriented interfaces
* comfortable, reading-oriented coffee and recipe content

Different content types may use different maximum widths while remaining aligned to the same responsive system.

---

## 7.2 Responsive Layout Classes

Brewcipe should design for four general viewport classes:

```text
Mobile              320–767px
Tablet              768–1023px
Desktop             1024–1439px
Wide Desktop        1440px+
```

These ranges are design guidance rather than requirements to trigger every responsive change at an exact pixel value.

Components should respond when their content or interaction requires adaptation rather than relying exclusively on device categories.

---

## 7.3 Page Gutters

Initial horizontal page gutters:

```text
Mobile              16px
Tablet              24px
Desktop             32px
Wide Desktop        40–48px
```

These values should use Brewcipe's established spacing tokens.

Individual components should not introduce unrelated page gutters.

---

## 7.4 Content Containers

Brewcipe may use multiple content-container types according to content purpose.

### App Container

Supports general application screens and structured interface content.

### Discovery Container

Supports search results, coffee discovery, geography exploration, and layouts that benefit from additional horizontal space.

### Reading Container

Supports recipe instructions, cultural context, descriptive content, and other reading-heavy material.

### Narrow Container

Supports focused forms, authentication, and similarly constrained tasks.

### Full-Bleed Media

May be used selectively for imagery where edge-to-edge presentation strengthens the experience.

Container selection should follow content needs rather than page-specific arbitrary widths.

---

## 7.5 Columns

Column count should respond to content and available space.

Mobile interfaces should generally use a single primary content column.

Tablet layouts may introduce two-column structures where content benefits from additional horizontal space.

Desktop and wide-desktop discovery interfaces may use multi-column grids.

Reading-heavy recipe content should remain constrained even when surrounding layouts become wider.

---

## 7.6 Content Width

Wide displays should increase useful whitespace and layout capacity before excessively increasing individual component width.

Discovery grids may use more horizontal space than reading-heavy recipe sections.

Content should remain visually connected and should not become excessively dispersed on large displays.

---

## 7.7 Reading Width

Recipe instructions, preparation steps, cultural context, descriptions, and other reading-heavy content should maintain comfortable line lengths.

Reading containers should remain constrained on desktop and wide-desktop screens rather than expanding to the full application width.

---

## 7.8 Alignment

Major page elements should align to shared container boundaries wherever practical.

Headers, search controls, section headings, lists, grids, and reading content should establish intentional alignment relationships.

Avoid arbitrary horizontal offsets that weaken visual rhythm.

---

# 8. Responsive Design

## 8.1 Mobile-First Approach

Mobile is the baseline Brewcipe experience.

Responsive design should preserve the same product hierarchy while adapting navigation, layout, density, and component arrangement to available space.

Desktop should progressively enhance the mobile experience rather than behave as an unrelated product.

---

## 8.2 Responsive Layout Modes

Brewcipe should account for four general responsive modes.

### Mobile

Typical behavior:

* single-column primary content
* persistent bottom navigation for primary destinations
* compact app or page headers
* full-width or near-full-width search controls
* vertically stacked cards and lists
* touch-first interactions
* 16px page gutters

### Tablet

Typical behavior:

* one- or two-column layouts depending on content
* increased page gutters
* larger content regions
* selective split layouts
* adaptive navigation based on available width
* increased information density where useful

Bottom navigation may remain appropriate on smaller tablet layouts and may transition to a larger-screen navigation pattern when sufficient horizontal space is available.

### Desktop

Typical behavior:

* desktop navigation replacing mobile bottom navigation
* multi-column discovery layouts where useful
* wider search and results interfaces
* selective split-detail layouts
* constrained reading widths
* increased whitespace
* pointer and keyboard interaction alongside touch support

### Wide Desktop

Typical behavior:

* maximum-width content containers
* additional discovery columns where appropriate
* increased surrounding whitespace
* stable reading widths
* restrained component scaling

Wide screens should not cause content, controls, or reading lines to expand indefinitely.

---

## 8.3 Responsive Transformation

Responsive behavior may change:

* width
* spacing
* layout direction
* column count
* positioning
* navigation presentation
* control placement
* content density
* visibility of secondary information where appropriate

Responsive changes should preserve the user's understanding of the interface.

Primary actions and destinations should not disappear without an equivalent accessible presentation.

---

## 8.4 Responsive Typography

Display and heading sizes may increase on larger viewports where appropriate.

Body text should remain readable and relatively stable across viewport sizes.

Typography should respond to available space without creating excessively large text merely because a screen is wide.

---

## 8.5 Responsive Components

Reusable components should define responsive behavior whenever their structure changes meaningfully across viewport sizes.

A responsive component may:

* change orientation
* change width
* change internal spacing
* expose additional information
* rearrange actions
* transform between compact and expanded variants

The underlying content and interaction purpose should remain consistent.

---

## 8.6 Responsive Navigation

Primary navigation should adapt to the available viewport rather than using one presentation at every screen size.

Conceptually:

```text
Mobile
Bottom Navigation
        ↓
Tablet
Bottom or Adaptive Navigation
        ↓
Desktop / Wide Desktop
Desktop Navigation
```

Navigation destinations should remain consistent with Brewcipe's information architecture even when their presentation changes.
---

# 9. Shape

## 9.1 Shape Philosophy

Brewcipe should use restrained rounding.

The interface should avoid the excessively soft, pill-heavy appearance common in generic SaaS interfaces.

---

## 9.2 Radius Scale

Proposed starting scale:

```text
Small       4px
Medium      8px
Large       12px
Full        9999px
```

The scale should be validated visually before implementation.

---

## 9.3 Circular and Pill Treatments

Full rounding should be reserved for legitimate cases such as:

* circular icon controls
* avatars where applicable
* metadata treatments where a pill genuinely improves recognition

Not every label or control should become a pill.

---

## 9.4 Usage Rules

Prefer consistent, restrained shapes.

Do not introduce page-specific radius values without a reusable reason.

---

# 10. Borders & Elevation

## 10.1 Border Tokens

The system should provide:

```text
border.default
border.strong
```

Exact dark-theme values remain dependent on the expanded color palette.

---

## 10.2 Dividers

Dividers may be used to separate content where spacing alone does not provide sufficient hierarchy.

They should remain visually subtle.

---

## 10.3 Elevation Levels

Conceptual levels:

```text
None
Subtle
Elevated
```

---

## 10.4 Shadows

Shadows should be used sparingly.

Dark-mode hierarchy should rely primarily on:

* surface contrast
* borders
* spacing
* typography

rather than large blurred shadows.

---

## 10.5 Surface Hierarchy

Surface hierarchy should remain shallow and structured.

Conceptually:

```text
Page Background
        ↓
Base Surface
        ↓
Interactive Surface
        ↓
Selected / Active Surface
        ↓
Overlay / Elevated Surface
```

Content-heavy recipe pages should frequently use spacing, typography, and dividers instead of card containers.

---

# 11. Iconography

# 11. Iconography

## 11.1 Icon Direction

Brewcipe should use one consistent icon family across navigation, actions, controls, and informational UI.

The preferred direction is a restrained, simple icon family with consistent geometry and visual weight.

Icons should support Brewcipe's modern application structure without making the interface feel generic, overly technical, playful, or decorative.

The final icon library should be selected during implementation based on visual compatibility, coverage, accessibility, and frontend maintainability.

---

## 11.2 Icon Size Scale

Use a restrained icon size scale:

```text
16px        Inline and metadata
20px        Standard controls
24px        Primary navigation and prominent controls
28–32px     Rare prominent use
```

The visible icon size is independent from the interactive touch target.

Avoid introducing arbitrary icon sizes where an established size is suitable.

---

## 11.3 Stroke and Weight

Icons should maintain consistent visual weight throughout the interface.

Icons from different sources should not be mixed when their stroke, geometry, or visual proportions are noticeably inconsistent.

---

## 11.4 Navigation Icons

Primary mobile navigation should pair recognizable icons with concise text labels.

Navigation icons should define:

* default state
* selected state
* focus state
* active / pressed state
* disabled state where applicable

Selected navigation may use a stronger or filled icon treatment where supported by the chosen icon family.

Selection should not rely solely on color.

---

## 11.5 Interactive Icons

Interactive icons may support recognizable actions such as:

* search
* favorite
* back
* close
* filter
* menu
* clear
* account
* navigation

Icon-only controls should be reserved for actions whose meaning remains sufficiently recognizable.

Less familiar actions should include visible text where practical.

---

## 11.6 Decorative and Coffee-Specific Icons

Decorative icons should remain limited.

Coffee-specific icons may be used when they communicate meaningful information, such as a brewing method or recurring coffee attribute.

They should not be introduced merely to make the interface appear more coffee-themed.

---

## 11.7 Accessibility

Icon-only controls must provide accessible names.

Decorative icons should be hidden from assistive technologies where appropriate.

Interactive icons must provide sufficiently large interaction targets even when the visible icon itself is smaller.

---

# 12. Imagery

## 12.1 Photography Direction

Photography is an important part of Brewcipe's visual identity.

The direction should feel:

* natural
* editorial
* warm
* tactile
* coffee-focused
* culturally respectful

---

## 12.2 Coffee Imagery

Coffee photography may provide much of the interface's natural warmth and visual richness.

Images do not need to be artificially darkened simply because Brewcipe uses a dark theme.

Natural contrast from:

* crema
* ceramic
* metal brewing equipment
* glass
* wood
* milk
* coffee

can provide visual interest against dark surfaces.

---

## 12.3 Cultural Imagery

Cultural imagery should only be used when it meaningfully relates to the coffee, preparation method, location, or context being presented.

Avoid generic or stereotypical representations of cultures and regions.

---

## 12.4 Image Ratios

Potential reusable ratios include:

```text
4:3
3:2
1:1
```

The appropriate ratio should depend on the component.

---

## 12.5 Cropping

Cropping should preserve the important subject of an image.

Avoid aggressive cropping that removes meaningful brewing or cultural context.

---

## 12.6 Responsive Images

Images should:

* use appropriate responsive sizing
* avoid unnecessary full-resolution loading
* minimize layout shifts
* maintain predictable layout behavior

---

## 12.7 Alternative Text

Meaningful images should provide useful alternative text.

Decorative imagery should use appropriate accessibility treatment.

---

# 13. Motion

## 13.1 Motion Principles

Motion should support comprehension rather than spectacle.

It should feel:

```text
Subtle
Quick
Purposeful
```

---

## 13.2 Duration

Exact motion durations remain:

**TBD**

A small shared duration scale should be established when interaction design begins.

---

## 13.3 Easing

Use a limited shared easing system.

Exact values:

**TBD**

---

## 13.4 Transitions

Appropriate uses may include:

* navigation opening and closing
* state changes
* favorite feedback
* contextual content reveal
* overlays

---

## 13.5 Loading Motion

Loading animation should communicate progress without unnecessary visual spectacle.

---

## 13.6 Reduced Motion

Brewcipe should respect reduced-motion preferences where applicable.

---

# Components

# 14. Component Principles

## 14.1 Reuse Before Creating

Existing components should be reused before new ones are introduced.

---

## 14.2 Composition

Complex components should be composed from smaller reusable primitives where practical.

---

## 14.3 Anatomy

Reusable components should document their meaningful structural parts where needed.

---

## 14.4 Variants

Variants should represent genuine recurring use cases.

Avoid creating variants merely to solve one page-specific styling exception.

---

## 14.5 States

Components should define the states applicable to their behavior.

---

## 14.6 Responsive Behavior

Components should document responsive changes where their layout, density, navigation role, or interaction changes meaningfully.

Responsive variants should preserve the same underlying purpose and content hierarchy rather than becoming unrelated components for different devices.

Where appropriate, components may transition between compact, standard, and expanded presentations.

---

## 14.7 Accessibility

Accessibility requirements should be part of component specifications.

---

# 15. Actions

## 15.1 Button

Core button variants:

```text
Primary
Secondary
Ghost
```

Buttons may support the following sizes where required:

```text
Small
Medium
Large
```

Applicable states may include:

```text
Default
Hover
Focus
Active
Disabled
Loading
```

Buttons may contain:

```text
Label
Icon + Label
Label + Icon
```

Primary buttons should communicate the strongest action within the current context rather than being used for every available action.

Exact visual specifications should use the finalized dark semantic color system.

---

## 15.2 Icon Button

Icon buttons support recognizable compact actions.

Common uses may include:

* favorite
* back
* close
* clear
* filter
* menu

The visible icon should use the established icon scale while the surrounding interactive area provides a comfortable touch target.

Icon buttons must provide accessible names.

Unfamiliar or ambiguous actions should not rely on icon-only presentation.
---

## 15.3 Link

Links should remain visually identifiable as interactive elements.

Text links should not depend solely on subtle color differences that become difficult to perceive in dark mode.

---

# 16. Forms & Inputs

## 16.1 Text Input

Text inputs should share consistent:

* typography
* height
* spacing
* border
* radius
* focus treatment
* validation behavior

---

## 16.2 Search Input

Search is a core Brewcipe discovery interaction.

The reusable search pattern may include:

* search icon
* text input
* clear action when content is present
* optional contextual filter or action where required

Search may support:

```text
Standard
Prominent / Discovery
Compact

---

## 16.3 Form Labels

Labels should remain available where required.

Placeholders should not be the sole method of identifying a field.

---

## 16.4 Validation

Validation should:

* clearly identify the affected field
* explain the issue
* provide recovery guidance where useful
* avoid relying on color alone

---

# 17. Navigation

## 17.1 Navigation Principles

Navigation should reflect Brewcipe's information architecture.

The design system defines how navigation destinations are presented and behave across viewport sizes. The information architecture remains responsible for defining the final destination hierarchy.

Navigation should be:

* immediately recognizable
* consistent across screens
* responsive to available space
* accessible by keyboard and touch
* clear in its selected state
* restrained in visual complexity

---

## 17.2 Primary Navigation

Primary navigation provides persistent access to Brewcipe's core destinations.

The exact destinations and labels should follow `information-architecture-v3.md`.

Primary destinations should remain conceptually consistent across responsive layouts even when navigation presentation changes.

---

## 17.3 Mobile Bottom Navigation

Mobile should use persistent bottom navigation for Brewcipe's primary destinations unless usability testing demonstrates a stronger alternative.

The pattern should:

* remain fixed to the bottom of the viewport
* contain a restrained number of primary destinations
* use an icon and concise text label for each destination
* provide a clear selected state
* provide comfortable touch targets
* account for device safe areas
* avoid obscuring page content
* remain visually distinct from scrollable content without excessive elevation

Content containers should include sufficient bottom spacing so that content and actions are not hidden behind persistent navigation.

---

## 17.4 Tablet Navigation

Tablet navigation should adapt according to available width and content needs.

Smaller tablet layouts may retain bottom navigation.

Larger tablet layouts may transition toward the desktop navigation pattern when this improves space efficiency and clarity.

The navigation hierarchy should not change merely because its presentation changes.

---

## 17.5 Desktop Navigation

Desktop and wide-desktop layouts should replace mobile bottom navigation with an appropriate larger-screen navigation pattern.

The default direction is a persistent application header containing:

* Brewcipe brand identity
* primary navigation destinations
* account or authentication access
* contextual actions where appropriate

A navigation rail may be considered through wireframing if it provides a stronger layout for Brewcipe's actual content.

Desktop navigation should not simply stretch the mobile bottom-navigation component across the top of the screen.

---

## 17.6 App and Page Headers

Brewcipe should use consistent header patterns to establish:

* page identity
* navigation context
* back navigation where required
* relevant contextual actions

Mobile headers should remain compact.

Desktop headers may integrate with the primary application navigation where appropriate.

---

## 17.7 Back Navigation

Back navigation should be provided where users enter a deeper content hierarchy or focused task.

Back controls should use a consistent icon and interaction pattern.

Browser navigation behavior should remain functional and predictable.

---

## 17.8 Contextual Navigation

Contextual navigation may support relationships within Brewcipe content without competing with primary navigation.

Examples may include:

* tabs
* segmented controls
* section navigation
* geography hierarchy
* related-content navigation

Contextual navigation should not duplicate primary navigation unnecessarily.

---

## 17.9 Navigation States

Navigation items should support relevant states including:

```text
Default
Hover
Focus
Active / Pressed
Selected
Disabled where applicable
```

Selected navigation should remain understandable without relying solely on color.

---

## 17.10 Responsive Navigation Transformation

Navigation presentation should adapt without changing the user's underlying mental model.

Conceptually:

```text
Mobile
Persistent Bottom Navigation
        ↓
Tablet
Bottom or Adaptive Navigation
        ↓
Desktop / Wide Desktop
Application Header or validated larger-screen equivalent
```

A destination available through primary navigation on one viewport should not disappear on another viewport without an equivalent accessible route.
---

# 18. Content & Surfaces

# 18. Content & Surfaces

## 18.1 Surface

Surfaces should use semantic background tokens and maintain a restrained hierarchy.

Surface changes should communicate meaningful grouping, interaction, selection, or elevation rather than decorating every content block.

---

## 18.2 Divider

Dividers should support content organization without becoming visually dominant.

Spacing should be preferred where it already provides sufficient separation.

---

## 18.3 Card

Cards should represent meaningful grouped or interactive content.

Content should not automatically be placed inside a card merely because it exists.

Cards should remain relatively flat and should avoid excessive shadow, rounding, or nested containers.

---

## 18.4 List Row

List rows provide a compact alternative to cards for structured or repeated content.

A list row may contain:

* optional thumbnail or icon
* primary label
* secondary information
* metadata
* trailing action or disclosure indicator

List rows should support efficient scanning and should be considered for search results, favorites, geography, and other information-dense contexts where a full card is unnecessary.

---

## 18.5 Image

Reusable image treatments should define:

* ratio
* radius where applicable
* loading behavior
* fallback behavior
* accessibility treatment

Image presentation may adapt between card, list, detail, and editorial contexts.

---

## 18.6 Metadata

Metadata should remain easy to scan without visually overpowering primary coffee information.

Related metadata may be grouped through spacing, alignment, or typography rather than automatically using badges or pills.

---

## 18.7 Tag / Badge

Tags and badges should represent meaningful categorical or status information.

Avoid turning all metadata into pills.

---

## 18.8 Section Header

Section headers should establish clear hierarchy between major content groups.

A section header may contain:

* title
* optional supporting text
* optional contextual action

Repeated section-header patterns should maintain consistent alignment and spacing.

---

## 18.9 Tabs

Tabs may be used when multiple peer views occupy the same content context.

Tabs should provide:

* clear labels
* visible selected state
* keyboard accessibility
* sufficient touch targets

Tabs should not be used merely as decorative category labels.

---

## 18.10 Segmented Control

Segmented controls may support switching between a small number of closely related views or modes.

They should remain compact, clearly selected, and understandable without relying solely on color.

Segmented controls should not become the default treatment for ordinary navigation.

---

## 18.11 Information Row

Information rows may present structured label-value relationships compactly.

They are appropriate for recurring recipe or coffee metadata where scanning is more useful than card presentation.

---

## 18.12 Action Row

Action rows may group a small set of contextually related actions.

Action hierarchy should remain clear and should avoid presenting every action with equal visual weight.

---

# 19. Feedback

## 19.1 Loading

Loading may use:

* progress indicators
* skeletons
* button loading states

according to context.

---

## 19.2 Empty State

Empty states should explain the situation and provide an appropriate next action when one exists.

---

## 19.3 Error State

Errors should:

* explain the issue clearly
* avoid unnecessary technical language
* provide recovery actions where possible

---

## 19.4 Success Feedback

Success feedback should confirm meaningful completed actions without interrupting the user unnecessarily.

---

## 19.5 Inline Validation

Inline validation should appear close to the relevant control and remain accessible.

---

# 20. Brewcipe Product Components

Brewcipe-specific components should be introduced as actual product needs are established through information architecture and wireframing.

The initial component set may include the following.

---

## 20.1 Coffee Card

The Coffee Card represents a coffee in visually led discovery contexts.

Potential content includes:

* coffee imagery where available
* coffee name
* native name where appropriate
* geographical information
* relevant secondary information
* favorite action where applicable

Coffee Cards may support recurring responsive variants.

### Standard Coffee Card

The standard variant is image-led and is appropriate for:

* discovery
* geographical exploration
* recommendations
* larger search presentations

### Compact Coffee Card

The compact variant reduces image and internal spacing while preserving the same primary information.

It may be appropriate for:

* smaller viewports
* denser discovery layouts
* recommendations
* contexts where vertical space is limited

Coffee Card variants should preserve consistent information hierarchy and interaction behavior.

Exact anatomy should be validated through wireframing.

---

## 20.2 Coffee Row

The Coffee Row provides a denser alternative to the Coffee Card.

It may be used for:

* search results
* favorites
* compact recommendation lists
* geography-based coffee lists
* other information-dense contexts

Potential anatomy includes:

* optional thumbnail
* coffee name
* native name where appropriate
* geographical or secondary information
* favorite action where applicable
* disclosure indicator where the entire row opens the coffee detail

Coffee Rows should prioritize fast scanning and should not reproduce the full visual weight of a Coffee Card.

Coffee Card and Coffee Row should represent the same coffee entity using context-appropriate density rather than competing information hierarchies.

---

## 20.3 Recipe Metadata

Recipe metadata should present available structured information clearly and compactly.

Potential fields depend on Brewcipe's canonical data model.

---

## 20.4 Ingredient List

Ingredient presentation should prioritize:

* readability
* quantities
* ingredient names
* scanning during preparation

Exact layout should follow actual recipe data.

---

## 20.5 Preparation Step

Ordered preparation instructions should clearly preserve sequence.

Conceptually:

```text
01
Rinse the filter.

02
Add the ground coffee.

03
Pour the initial water.
```

---

## 20.6 Favorite Control

Favorite behavior should use one consistent pattern.

The state must remain understandable without relying solely on color.

Accessible labels should describe the available action.

---

# System Behavior

# 21. Interaction States

The design system should support relevant states consistently.

## 21.1 Default

Normal interactive state.

## 21.2 Hover

Pointer-hover feedback where supported.

## 21.3 Focus

Visible keyboard focus.

## 21.4 Active / Pressed

Feedback while an action is being activated.

## 21.5 Selected

Communicates persistent selection or state.

Selected states may use a combination of:

* foreground treatment
* background treatment
* icon treatment
* typographic emphasis
* border or indicator
* surface treatment

Selection should remain recognizable without relying solely on color.

Navigation, tabs, segmented controls, favorite controls, and other persistent selections should use consistent selected-state logic.

## 21.6 Disabled

Communicates that an interaction is unavailable.

## 21.7 Loading

Communicates that an operation is processing.

## 21.8 Error

Communicates a problem requiring attention or recovery.

Not every component requires every state.

---

# 22. Accessibility

## 22.1 Accessibility Target

Brewcipe targets:

**WCAG 2.2 Level AA**

for the web interface.

Accessibility should be validated during implementation and testing rather than assumed from visual specifications.

---

## 22.2 Color and Contrast

Text, controls, focus indicators, and meaningful visual states should provide sufficient contrast.

Dark-mode muted text requires particular attention.

---

## 22.3 Keyboard Interaction

Core interactive functionality should remain keyboard operable where applicable.

---

## 22.4 Focus

Keyboard focus should always remain visible.

Focus treatments should remain consistent across shared components.

---

## 22.5 Touch Targets

Interactive controls should provide comfortable touch targets across touch-capable devices.

Visible icons may remain visually compact while their surrounding interactive area provides a larger touch target.

Navigation items, icon buttons, tabs, segmented controls, and other frequently used touch interactions require particular attention.

Adjacent touch targets should provide sufficient separation to reduce accidental activation.

Touch-target requirements should be validated against Brewcipe's WCAG 2.2 Level AA accessibility target during implementation.

---

## 22.6 Forms

Forms should provide:

* visible or accessible labels
* understandable validation
* programmatic relationships where appropriate
* keyboard support

---

## 22.7 Images

Meaningful imagery should provide appropriate alternative text.

---

## 22.8 Motion

Reduced-motion preferences should be respected where applicable.

---

## 22.9 Semantic Structure

Implementation should use semantic HTML and appropriate accessible relationships rather than reproducing semantic behavior visually alone.

---

# 23. Themes

## 23.1 Theme Architecture

Themes should map semantic tokens to theme-specific primitive values.

Components should consume semantic tokens.

Conceptually:

```text
Primitive Palette
        ↓
Semantic Roles
        ↓
Dark Theme Mapping
        ↓
Components
```

Future:

```text
                    Semantic Roles
                    /            \
                   /              \
             Dark Theme       Light Theme
                   \              /
                    \            /
                     Components
```

Components should not require separate dark-mode and light-mode styling logic for every color.

---

## 23.2 Dark Theme — MVP

Brewcipe launches with a **dark theme**.

The dark theme is the primary visual expression of the initial Brewcipe product.

It should use:

* warm near-black or charcoal backgrounds
* restrained surface hierarchy
* warm neutral text
* selective brand color
* strong photography
* accessible contrast

It should avoid generic pure-black SaaS styling.

---

## 23.3 Light Theme — Future

Light mode is not required for the initial MVP.

The token architecture should allow a future light theme to map the same semantic roles onto a different primitive palette without redesigning individual components.

---

## 23.4 Theme Token Mapping

Example:

```text
Semantic Token
color.background.primary

Dark
→ dark charcoal primitive

Future Light
→ light warm-neutral primitive
```

Components continue referencing:

```text
color.background.primary
```

regardless of active theme.

---

## 23.5 Implementation Rules

Do not:

* hard-code dark-theme colors directly throughout components
* create duplicated light and dark component implementations
* name semantic tokens after their current visual appearance
* assume a semantic token will always map to the same primitive color

---

# 24. Content & Localization

## 24.1 Native Coffee Names

Native coffee names should be preserved as meaningful content.

They should not be treated as technical metadata.

---

## 24.2 Transliteration

Where Brewcipe data provides transliteration, its presentation should follow the hierarchy established through wireframing.

---

## 24.3 Unicode

All Brewcipe interfaces should preserve Unicode correctly.

Broken character encoding is unacceptable.

---

## 24.4 Font Fallback

Font fallbacks should provide appropriate glyph coverage for the scripts represented in Brewcipe.

---

## 24.5 Text Expansion

Components should tolerate longer names and translated content without breaking their layout.

---

## 24.6 Truncation

Truncation should only be used where space genuinely requires it.

Important coffee names and instructions should not be unnecessarily hidden.

---

## 24.7 Directionality

Interfaces displaying right-to-left scripts should preserve correct text direction where applicable.

The overall application layout does not automatically need to change direction merely because an individual native coffee name uses a right-to-left script.

---

# Governance

# 25. Component Architecture

## 25.1 UI Primitives

Foundational UI elements provide basic visual and interactive behavior.

Examples may include:

```text
Button
IconButton
Input
Link
Surface
Divider
Icon
Image
```

---

## 25.2 Shared Components

Shared components combine primitives into reusable application patterns.

---

## 25.3 Product Components

Product components represent recurring Brewcipe concepts.

Examples may include:

```text
CoffeeCard
RecipeMetadata
IngredientList
PreparationStep
FavoriteControl
```

---

## 25.4 Feature Components

Feature components combine shared and product components to support a particular Brewcipe feature.

---

## 25.5 Pages

Pages compose feature and reusable components into complete experiences.

Conceptually:

```text
Design Tokens
      ↓
UI Primitives
      ↓
Shared Components
      ↓
Brewcipe Product Components
      ↓
Feature Components
      ↓
Pages
```

---

# 26. Usage & Contribution Rules

## 26.1 Reuse Existing Patterns

Before introducing a new pattern, check whether the existing system already provides an appropriate solution.

---

## 26.2 Introducing New Tokens

A new token should represent a recurring system need rather than a one-off page value.

---

## 26.3 Introducing New Components

Create a new reusable component when:

* the pattern recurs
* existing components cannot reasonably support it
* its behavior can be clearly defined
* it belongs in the shared system

---

## 26.4 Modifying Existing Components

Changes to shared components should consider all existing usages rather than solving only the current screen.

---

## 26.5 Deprecating Patterns

Patterns that are replaced should be removed or clearly deprecated to prevent competing implementations.

---

# 27. Design Review Checklist

Before considering a Brewcipe interface ready for implementation or release, review the following.

## 27.1 Product Alignment

* Does the interface support a current product requirement?
* Does it accidentally introduce functionality outside current scope?
* Are optional data fields handled appropriately?

---

## 27.2 Brand and Visual Identity

* Does the interface feel like Brewcipe?
* Does it feel dark, warm, editorial, and coffee-focused?
* Does coffee remain the primary subject?
* Does it avoid generic SaaS and AI aesthetics?
* Are brand colors used intentionally rather than excessively?

---

## 27.3 System Consistency

* Are semantic tokens being used?
* Are established typography styles being used?
* Is spacing drawn from the shared scale?
* Are shape and border treatments consistent?
* Are icons drawn from the established icon system?
* Are icon sizes and visual weights consistent?
* Are cards being used only where meaningful grouping or interaction requires them?
* Could a compact list row communicate the content more efficiently?
* Are navigation and selected states consistent?
* Are existing components reused where possible?

---

## 27.4 Responsive Behavior

* Was the experience designed mobile first?
* Does it adapt deliberately across mobile, tablet, desktop, and wide desktop?
* Does navigation transform appropriately for the available viewport?
* Are primary destinations preserved across responsive navigation patterns?
* Do discovery layouts use available horizontal space effectively?
* Does reading-heavy content remain appropriately constrained?
* Do components change density or arrangement where useful without changing their underlying purpose?
* Are touch interactions comfortable?
* Does content remain readable?
* Does wide-screen content remain intentionally bounded rather than stretching indefinitely?

---

## 27.5 Content

* Are coffee names clear?
* Are native names preserved correctly?
* Are recipe instructions easy to follow?
* Is geographical and cultural information treated respectfully?
* Does multilingual content remain usable?

---

## 27.6 Accessibility

* Is contrast sufficient?
* Are focus states visible?
* Are core interactions keyboard operable where applicable?
* Are interactive states understandable without relying solely on color?
* Are meaningful images appropriately described?
* Is reduced motion respected where applicable?

---

## 27.7 Reuse

* Could an existing component be reused?
* Could existing primitives be composed?
* Is a new component genuinely necessary?
* If a new pattern is reusable, has it been incorporated into the shared system?

---

# 28. Design System Goal

The Brewcipe design system should allow different pages and features to be designed and implemented while still feeling like parts of one coherent product.

The system should be:

* flexible enough to support future visual evolution
* structured enough to prevent arbitrary implementation
* small enough to remain maintainable
* accessible by default
* appropriate for multilingual coffee content
* capable of supporting future themes without redesigning components

The desired result is an interface that combines:

* Brewcipe's dark, warm, editorial coffee identity
* the clarity and efficiency of a modern application
* compact, structured information where appropriate
* comfortable reading experiences for recipes and cultural content
* consistent icon-led interaction
* responsive behavior across mobile, tablet, desktop, and wide desktop

The interface should feel:

> **crafted around coffee rather than assembled from generic UI patterns.**

Application-oriented structure should strengthen Brewcipe's usability without replacing its distinctive visual identity with generic SaaS conventions.

The design system should make good design decisions easier to repeat without adding complexity for its own sake.

# 29. Product References

## Visual Product References

Brewcipe's interface direction is informed in part by selected patterns observed in the following coffee-focused digital products:

* AeroPress Recipe  
  https://aeroprecipe.com/images/weMakeCoffee_preview_01.webp

* iBrew — app interface reference  
  https://ibrew.coffee/assets/images/screenshots/app_01.png

* iBrew — app interface reference  
  https://ibrew.coffee/assets/images/screenshots/app_05.png

These references are used as directional inspiration rather than templates to reproduce.

Relevant qualities include:

* compact, application-oriented interface structure
* clear mobile navigation
* icon-led primary actions and navigation
* persistent bottom navigation where appropriate
* strong page and application headers
* efficient use of cards, rows, and structured information
* clear grouping of metadata
* restrained, utility-oriented controls
* mobile-native interaction patterns
* layouts that prioritize fast scanning and task completion

Brewcipe should interpret these qualities through its own visual identity.

Brewcipe should retain:

* its dark-first visual system
* warm coffee-oriented color palette
* editorial typography
* restrained use of surfaces and elevation
* cultural and geographical emphasis
* recipe-first information hierarchy
* distinctive Brewcipe brand character

Brewcipe should not reproduce the reference products literally.

In particular, it should not adopt their light visual themes, exact navigation structure, exact component styling, typography, branding, or proprietary visual assets.

The intended direction is:

> Brewcipe's warm, dark, editorial identity combined with the clarity and efficiency of a modern coffee application.
