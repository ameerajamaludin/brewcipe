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

## 2.5 Mobile First

Base layouts and component behavior should support smaller screens first.

Larger-screen behavior should progressively enhance the experience rather than create a separate desktop design system.

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

Brewcipe should use a restrained typography system combining:

```text
Display / Brand Typography
        +
Interface / Content Typography
```

Typography should contribute substantially to Brewcipe's editorial character.

Decorative coffee graphics should not be required to make the product feel coffee-oriented.

---

## 5.2 Display Typeface

**Current candidate: Piscolabis**

Piscolabis is being considered for Brewcipe's display and brand typography.

Potential uses include:

* selected hero headings
* prominent editorial moments
* brand treatments
* wordmark exploration

It should be used selectively.

Piscolabis should not be used for:

* body copy
* recipe instructions
* form controls
* navigation
* metadata
* long passages
* general application UI

Final approval remains subject to visual and multilingual testing.

---

## 5.3 Interface Typeface

**Status: TBD**

Brewcipe requires a highly readable interface typeface for:

* coffee names
* headings
* body copy
* ingredients
* instructions
* navigation
* buttons
* forms
* metadata
* AI responses

The selected typeface should feel:

* human
* warm
* contemporary
* highly readable
* restrained

It should avoid feeling excessively corporate, geometric, or generic.

---

## 5.4 Font Fallbacks

Brewcipe contains multilingual coffee names.

Font stacks should therefore provide appropriate fallbacks when the primary typeface does not contain the required glyph.

Conceptually:

```css
font-family:
  "Brewcipe Interface",
  "Noto Sans",
  system-ui,
  sans-serif;
```

Actual fallback configuration should be based on the scripts represented in Brewcipe's production data.

---

## 5.5 Type Scale

The final type scale should remain limited and mobile-first.

Proposed starting scale:

```text
Display
40px / 48px

Heading 1
32px / 40px

Heading 2
24px / 32px

Heading 3
20px / 28px

Body Large
18px / 28px

Body
16px / 24px

Body Small
14px / 20px

Caption
12px / 16px
```

Larger display sizes may be introduced responsively where justified.

The scale should be validated through actual Brewcipe wireframes before being considered final.

---

## 5.6 Font Weights

Proposed interface weights:

```text
Regular       400
Medium        500
Semibold      600
Bold          700
```

Only weights supported and required by the final typefaces should be included.

---

## 5.7 Line Height

Line height should prioritize readability.

Reading-heavy content such as:

* cultural context
* ingredients
* preparation instructions
* AI responses

should use comfortable line spacing.

Display typography may use tighter line heights where readability remains strong.

---

## 5.8 Letter Spacing

Letter spacing should generally follow the selected typeface's natural metrics.

Custom tracking may be introduced for specific display or metadata styles when visually justified.

Avoid arbitrary letter-spacing values throughout individual components.

---

## 5.9 Text Styles

Reusable semantic text styles may include:

```text
text.display
text.heading1
text.heading2
text.heading3

text.bodyLarge
text.body
text.bodySmall
text.caption

text.label
text.button
```

Additional styles should only be introduced where recurring product needs justify them.

---

## 5.10 Multilingual Typography

Typography should be tested using representative Brewcipe content rather than English placeholder text alone.

Testing should include:

* native coffee names
* accented Latin characters
* longer coffee names
* non-Latin scripts represented in Brewcipe's data

Native names must remain readable when the display typeface does not support the required script.

---

## 5.11 Typography Usage Rules

Do not:

* use display typography for long-form content
* introduce arbitrary font sizes
* use multiple decorative typefaces without defined roles
* sacrifice readability for brand character
* assume all coffee names use Latin characters
* allow missing glyphs or broken Unicode to reach the interface

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

## 7.1 Page Container

Content should use responsive page containers rather than stretching indefinitely across large screens.

---

## 7.2 Grid

The final grid configuration should be established through wireframing and responsive testing.

Status: **TBD**

---

## 7.3 Columns

Column behavior should respond to content needs rather than forcing every page into the same grid.

Discovery views may use multi-column layouts on larger screens while reading-heavy recipe content may remain narrower.

---

## 7.4 Gutters

Initial horizontal spacing direction:

```text
Mobile             16px
Larger mobile      24px
Desktop            32px or appropriate responsive value
```

Final gutter behavior should be validated during wireframing.

---

## 7.5 Content Width

Wide displays should use maximum content widths appropriate to the content.

Discovery grids may use more horizontal space than reading-heavy recipe sections.

---

## 7.6 Reading Width

Recipe instructions, cultural context, and other reading-heavy content should maintain comfortable line lengths.

---

# 8. Responsive Design

## 8.1 Mobile-First Approach

Mobile is the baseline Brewcipe experience.

Desktop layouts should progressively enhance the mobile structure.

---

## 8.2 Breakpoints

Brewcipe may initially align with the breakpoint system provided by the selected frontend styling framework.

Final breakpoint decisions should respond to actual layout needs.

---

## 8.3 Responsive Layout Behavior

Components should adapt through:

* width
* spacing
* layout
* visibility where appropriate
* positioning
* content density

Avoid maintaining unrelated mobile and desktop component systems.

---

## 8.4 Responsive Typography

Display and heading sizes may increase on larger viewports where appropriate.

Body text should remain readable and stable.

---

## 8.5 Responsive Components

Reusable components should define responsive behavior when their structure changes meaningfully across viewport sizes.

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

Surface hierarchy should remain shallow.

Avoid:

```text
card
inside card
inside another card
inside floating container
```

Content-heavy recipe pages should frequently use spacing, typography, and dividers instead of card containers.

---

# 11. Iconography

## 11.1 Icon Family

Brewcipe should use one consistent icon family.

Exact family: **TBD**

A restrained outline family is preferred as the initial direction.

---

## 11.2 Sizes

A limited icon size scale should be established alongside component implementation.

Status: **TBD**

---

## 11.3 Stroke and Weight

Icons should maintain consistent visual weight throughout the interface.

---

## 11.4 Interactive Icons

Interactive icons should be used when their purpose is sufficiently recognizable.

Examples may include:

* search
* favorite
* menu
* close

---

## 11.5 Decorative Icons

Decorative icons should remain limited.

Coffee-specific icons should only be introduced where they communicate useful information.

---

## 11.6 Accessibility

Icon-only controls must provide accessible names.

Decorative icons should be hidden from assistive technologies where appropriate.

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

Components should document responsive changes where their layout or interaction changes meaningfully.

---

## 14.7 Accessibility

Accessibility requirements should be part of component specifications.

---

# 15. Actions

## 15.1 Button

Initial button variants:

```text
Primary
Secondary
Ghost
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

Exact visual specifications should be established after the dark semantic color system is finalized.

---

## 15.2 Icon Button

Icon buttons may support recognizable compact actions.

They must provide accessible names.

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

The search input should be:

* visually identifiable
* comfortable on mobile
* keyboard accessible
* consistent wherever coffee search is available

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

The design system defines navigation presentation and behavior, not the final destination hierarchy.

---

## 17.2 Global Navigation

Exact structure:

**To be determined through information architecture and wireframing.**

---

## 17.3 Mobile Navigation

Mobile navigation should prioritize core user activities while remaining space-efficient and accessible.

Exact pattern:

**TBD**

---

## 17.4 Contextual Navigation

Contextual navigation may be introduced where Brewcipe's content hierarchy requires it.

---

# 18. Content & Surfaces

## 18.1 Surface

Surfaces should use semantic background tokens and maintain a restrained hierarchy.

---

## 18.2 Divider

Dividers should support content organization without becoming visually dominant.

---

## 18.3 Card

Cards should represent meaningful grouped or interactive content.

Content should not automatically be placed inside a card merely because it exists.

---

## 18.4 Image

Reusable image treatments should define:

* ratio
* radius where applicable
* loading behavior
* fallback behavior
* accessibility treatment

---

## 18.5 Metadata

Metadata should remain easy to scan without visually overpowering primary coffee information.

---

## 18.6 Tag / Badge

Tags and badges should represent meaningful categorical or status information.

Avoid turning all metadata into pills.

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

A reusable Coffee Card may represent a coffee within:

* discovery
* search
* favorites
* geographical exploration
* AI recommendations

Potential content includes:

* coffee imagery where available
* coffee name
* native name where appropriate
* geographical information
* relevant secondary information
* favorite action where applicable

Exact anatomy should be finalized through wireframing.

---

## 20.2 Recipe Metadata

Recipe metadata should present available structured information clearly and compactly.

Potential fields depend on Brewcipe's canonical data model.

---

## 20.3 Ingredient List

Ingredient presentation should prioritize:

* readability
* quantities
* ingredient names
* scanning during preparation

Exact layout should follow actual recipe data.

---

## 20.4 Preparation Step

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

## 20.5 Favorite Control

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

Interactive controls should provide comfortable touch targets on mobile.

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
Input
Link
Surface
Divider
Icon
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
* Are existing components reused where possible?

---

## 27.4 Responsive Behavior

* Was the experience designed mobile first?
* Does it adapt appropriately to larger screens?
* Are touch interactions comfortable?
* Does content remain readable?

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

The desired result is an interface that feels:

> **crafted around coffee rather than assembled from generic UI patterns.**

The design system should make good design decisions easier to repeat without adding complexity for its own sake.
