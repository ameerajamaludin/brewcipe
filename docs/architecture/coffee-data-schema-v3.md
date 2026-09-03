# Brewcipe — Coffee Data Schema v3

## 1. Purpose

This document defines the canonical logical data model for coffee recipes in Brewcipe.

It describes:

* what information a Brewcipe coffee recipe contains
* what each field means
* the expected structure and data type of each field
* which values are required or optional
* how source-derived, normalized, and inferred information is represented
* known inconsistencies in the current dataset that must be resolved before production import
* the boundary between canonical coffee data and internal verification metadata

This document is based on the current Brewcipe v3 curated dataset:

```text
coffee-recipes-v3.json
```

The current dataset contains:

```text
198 coffee recipe records
```

This document does **not** define PostgreSQL tables, foreign keys, indexes, Row Level Security policies, or other physical database implementation details.

Those decisions belong in:

```text
docs/architecture/database-schema-v3.md
```

The relationship is:

```text
Private Curated Dataset
        ↓
Coffee Data Schema
        ↓
Canonical Validation / Normalization
        ↓
Database Schema
        ↓
Supabase PostgreSQL
```

---

# 2. Current Dataset Structure

Every current recipe record contains the following top-level fields:

```text
coffee_recipe_id
native_name
transliteration
english_name
geography
recipe_type
brewer
temperature
servings
ingredients
instructions
cultural_context
source
verification
```

Conceptually:

```text
CoffeeRecipe
│
├── coffee_recipe_id
├── native_name
├── transliteration
├── english_name
│
├── geography
│   ├── country
│   ├── region
│   └── continent
│
├── recipe_type
├── brewer
├── temperature
├── servings
│
├── ingredients[]
│   ├── ingredient
│   ├── amount
│   ├── unit
│   └── alternate_measure
│       ├── amount
│       └── unit
│
├── instructions[]
│
├── cultural_context
│   ├── associated_meal
│   └── meal_description
│
├── source
│   ├── recipe_author
│   └── original_publication
│
└── verification
    ├── confidence
    └── notes[]
```

This is the logical representation of the current curated dataset.

It does not require the production database to store every object exactly in this nested form.

---

# 3. Canonical Data Principles

## 3.1 Preserve Existing Meaning

Normalization should improve structural consistency without changing the supported meaning of the source information.

For example:

```text
"millilitres"
"milliliters"
"ml"
```

may be normalized to:

```text
ml
```

However:

```text
"serve in several cups"
```

should not automatically become:

```text
servings = 4
```

unless such an interpretation is intentionally supported and recorded.

---

## 3.2 Source-Stated and Inferred Data Are Different

The current dataset contains both:

```text
source-stated values
```

and:

```text
normalized or inferred values
```

For example, current verification notes include explanations such as:

```text
coffee dose source-stated
water volume inferred
```

or:

```text
range normalized to midpoint
```

Brewcipe must not represent an inferred value as though the source directly stated it.

---

## 3.3 Missing Data Should Not Be Fabricated

Where reliable information is unavailable, Brewcipe should preserve the absence rather than inventing a value.

Depending on the field, this may currently appear as:

```text
null
```

or:

```text
""
```

The production canonical representation should standardize missing-value handling before database import.

---

## 3.4 Structure Before Storage

This document defines what Brewcipe's information means.

It does not determine whether PostgreSQL eventually represents a concept using:

```text
a column
a related table
a join table
an enum
a lookup table
a JSON value
```

Those are physical database decisions.

---

## 3.5 Provenance Matters

Brewcipe recipes are derived from external public recipe and cultural sources.

Source information and verification history therefore form part of Brewcipe's data-management process.

However, internal verification metadata does not necessarily belong in the public user-facing recipe response.

---

# 4. `coffee_recipe_id`

## Purpose

Uniquely identifies a curated Brewcipe coffee recipe.

Current format:

```text
coffee_recipe_001
coffee_recipe_002
...
coffee_recipe_198
```

## Current Type

```text
string
```

## Current Requirement

```text
Required
Unique
Non-empty
```

All 198 current records have unique identifiers.

## Rule

The identifier should remain stable once a record is considered production-ready.

The display name should not be used as the sole identifier because names may:

* change during editorial review
* contain Unicode
* share similar wording
* represent different preparations of the same coffee tradition

The production database may eventually use a different internal primary-key implementation while retaining `coffee_recipe_id` as a stable domain identifier.

---

# 5. `english_name`

## Purpose

Primary English-language display name for the recipe.

Examples:

```text
Traditional Saudi Coffee
Vietnamese Egg Coffee
Singapore Kopi
Kenyan French Press Coffee
```

## Current Type

```text
string
```

## Current Requirement

```text
Required
Non-empty
```

## Rule

The field represents Brewcipe's primary English recipe name.

It should identify the recipe rather than reproduce an article headline or promotional page title.

---

# 6. `native_name`

## Purpose

Stores a locally used or native-script name associated with the coffee recipe where represented in the dataset.

Examples include:

```text
القهوة السعودية التقليدية
กาแฟเย็น
Cà phê trứng
ウィンナーコーヒー
```

## Current Type

```text
string
```

## Current Dataset

All current records contain a non-empty string.

## Canonical Rule

```text
string | null
```

is preferable for the production model because future records may not have a sufficiently supported native name.

The application should not invent one merely to satisfy the field.

---

# 7. `transliteration`

## Purpose

Provides a Latin-script rendering of the native or locally used name.

Examples:

```text
Al-Qahwa Al-Saudiyya Al-Taqlidiyya
Gafae Yen
Ca Phe Trung
Winnā Kōhī
```

## Current Type

```text
string
```

## Current Dataset

All current records contain a value.

Some records already use Latin-script native names, so the transliteration may be identical to the native name.

Example:

```text
native_name: Kopi Tubruk
transliteration: Kopi Tubruk
```

## Canonical Rule

Transliteration should remain separate from translation.

Conceptually:

```text
native_name       = original/local form
transliteration   = Latin-script rendering
english_name      = English display name
```

Future records may allow:

```text
transliteration = null
```

where transliteration is unnecessary or unsupported.

---

# 8. `geography`

## Purpose

Supports Brewcipe's geographical discovery hierarchy.

Current structure:

```json
{
  "country": "Vietnam",
  "region": "Southeast Asia",
  "continent": "Asia"
}
```

## Current Type

```text
object
```

All 198 current records contain:

```text
country
region
continent
```

---

# 9. `geography.country`

## Purpose

Represents the country associated with the coffee recipe or coffee tradition.

Examples:

```text
Vietnam
Japan
Saudi Arabia
Morocco
Indonesia
```

## Current Type

```text
string
```

## Current Requirement

```text
Required
Non-empty
```

## Rule

Country represents the geographical association of the recipe itself.

It should not merely reflect where the source website or recipe author is located.

---

# 10. `geography.region`

## Purpose

Represents Brewcipe's geographical grouping between continent and country.

Examples currently present include:

```text
Southeast Asia
East Asia
South Asia
Western Asia
West Asia
East Africa
West Africa
North Africa
Southern Africa
Eastern Europe
Western Europe
Southern Europe
Northern Europe
Central Europe
Central America
South America
North America
Northern America
Australia and New Zealand
```

## Current Type

```text
string
```

## Current Requirement

```text
Required
Non-empty
```

## Known Normalization Issue

The current dataset contains overlapping terminology such as:

```text
Western Asia
West Asia
```

and:

```text
North America
Northern America
```

These should not be silently changed in the source dataset.

A canonical controlled geographical vocabulary must be established before production import.

---

# 11. `geography.continent`

## Purpose

Represents the highest geographical level used by Brewcipe.

Current values include:

```text
Asia
Europe
Africa
Oceania
North America
South America
America
```

## Current Type

```text
string
```

## Known Normalization Issue

The dataset currently mixes:

```text
America
```

with:

```text
North America
South America
```

as continent values.

The production geographical hierarchy should choose one consistent model.

This remains a canonical normalization decision rather than something to silently correct in the curated source file.

---

# 12. Geographical Hierarchy

Brewcipe's intended discovery structure is:

```text
Continent
    ↓
Region
    ↓
Country
    ↓
Coffee Recipe
```

The current dataset contains sufficient fields to support this hierarchy once vocabulary inconsistencies are normalized.

The physical database may represent geography through separate relational entities.

---

# 13. `recipe_type`

## Purpose

Classifies the overall nature of the coffee recipe.

## Current Type

```text
string
```

## Current Values

The current dataset uses exactly three values:

```text
Cultural
Brewing
Traditional
```

Current distribution:

```text
Cultural       136
Brewing         50
Traditional     12
```

## Current Canonical Vocabulary

For v3, these three values represent the current dataset vocabulary:

```text
Cultural
Brewing
Traditional
```

## Interpretation

### `Cultural`

Primarily identifies a coffee drink or preparation associated with a place, culinary practice, local adaptation, or cultural context.

### `Brewing`

Primarily represents a brewing preparation or method-oriented coffee recipe.

### `Traditional`

Represents recipes explicitly classified in the curated dataset as traditional coffee preparations.

## Open Issue

The semantic boundary between:

```text
Cultural
Traditional
```

is not completely defined by the dataset itself.

Before production use, Brewcipe should document clearer classification rules so new records can be categorized consistently.

---

# 14. `brewer`

## Purpose

Identifies the brewer, equipment, or preparation method associated with the recipe.

Examples include:

```text
Dallah
Phin
Coffee Sock
French Press
AeroPress
Hario V60
Espresso Machine
Stovetop Pot
Cold Brew
Instant Coffee
Pour Over
Jabana
```

## Current Type

The current dataset contains two shapes:

```text
string
```

for 195 records, and:

```text
array<string>
```

for 3 records.

Examples of multiple brewers include:

```json
["AeroPress", "French Press"]
```

## Canonical Direction

The logical model should support:

```text
one or more brewers / methods
```

rather than assuming every recipe has exactly one.

Conceptually:

```text
brewer: string | string[]
```

describes the current curated format.

The production database should likely normalize this into relational associations rather than preserving mixed scalar/list storage.

That decision belongs in `database-schema-v3.md`.

---

# 15. Brewer Vocabulary

Current brewer values should be treated as candidate controlled vocabulary.

Normalization is required because naming conventions may vary.

For example, current data includes differences such as:

```text
Coffee Sock
coffee sock
```

Case variation should not create separate canonical brewer concepts.

Other semantic questions may also require review, such as whether:

```text
Pour Over
Hario V60
Dripper
```

represent:

* separate brewer types
* parent/child classifications
* brewer versus method

The dataset itself does not fully resolve this distinction.

---

# 16. `temperature`

## Purpose

Represents how the finished coffee recipe is served.

It does **not** represent exact brewing-water temperature.

## Current Type

The current dataset contains:

```text
string
```

for 189 records, and:

```text
array<string>
```

for 9 records.

## Current Values

Single-value records use:

```text
Hot
Iced
```

Some recipes support both:

```json
["Hot", "Iced"]
```

Current distribution by record:

```text
Hot             128
Iced             61
Hot + Iced        9
```

## Canonical Meaning

This field should therefore be understood as:

```text
service_temperature
```

conceptually, even if the current dataset field name remains:

```text
temperature
```

## Important Distinction

Exact brewing temperatures such as:

```text
93°C
195°F
90–95°C
```

currently appear inside source-derived recipe instructions where relevant.

They are not represented by the top-level `temperature` field.

A separate structured brewing-temperature field should only be introduced if future product requirements justify it.

---

# 17. `servings`

## Purpose

Represents the intended number of servings or portions.

## Current Type

```text
integer
```

All 198 current records contain an integer value.

## Current Requirement

```text
Required in the current curated dataset
Positive integer
```

## Data-Quality Note

Not all serving values are equally source-supported.

Some are explicitly provided by the source.

Others are inferred from:

* recipe yield
* container size
* normalized cup size
* practical serving assumptions

This distinction is currently documented inside:

```text
verification.confidence
```

and:

```text
verification.notes
```

---

# 18. `ingredients`

## Purpose

Stores the ordered ingredient list for a recipe.

## Current Type

```text
array<object>
```

The current dataset contains 817 ingredient entries.

Every current ingredient object uses:

```text
ingredient
amount
unit
alternate_measure
```

Structure:

```json
{
  "ingredient": "water",
  "amount": 1,
  "unit": "L",
  "alternate_measure": {
    "amount": 4.23,
    "unit": "cups"
  }
}
```

---

# 19. `ingredients[].ingredient`

## Purpose

Human-readable ingredient description.

Examples:

```text
ground coffee
sweetened condensed milk
cardamom pods
hot water
ice
```

## Current Type

```text
string
```

## Requirement

```text
Required
Non-empty
```

Ingredient descriptions may include meaningful qualifiers such as:

```text
medium-fine
light-roasted
freshly ground
cold
sweetened
```

The dataset currently retains these qualifiers in the ingredient text.

---

# 20. `ingredients[].amount`

## Purpose

Primary quantity for the ingredient.

## Current Type

Current values may be:

```text
integer
float
null
```

Examples:

```text
20
1.5
0.25
null
```

## Meaning of `null`

`null` is used where no meaningful numeric amount is supplied.

For example:

```text
ice — as needed
sugar — to taste
milk — optional
```

This is valid and should not automatically be replaced with a guessed numeric amount.

---

# 21. `ingredients[].unit`

## Purpose

Describes the measurement or usage unit associated with the primary amount.

Examples include:

```text
g
ml
L
cup
cups
tbsp
tsp
whole
pieces
pods
shots
pinch
to taste
as needed
optional
```

## Current Type

```text
string
```

## Current Data Characteristic

`unit` currently represents more than strict physical measurement units.

It may also carry semantic quantity information such as:

```text
to taste
as needed
optional
for garnish
```

This is an important modelling issue.

A future canonical relational model may benefit from separating:

```text
measurement unit
```

from:

```text
quantity / usage qualifier
```

but the current curated dataset does not make that distinction consistently.

---

# 22. `alternate_measure`

## Purpose

Provides an alternative representation of an ingredient quantity.

Example:

```json
{
  "amount": 40,
  "unit": "g",
  "alternate_measure": {
    "amount": 6,
    "unit": "tbsp"
  }
}
```

This allows Brewcipe to preserve both:

```text
40 g
```

and:

```text
6 tbsp
```

where the curated recipe contains or normalizes both representations.

## Current Type

```text
object
```

All current ingredient records contain:

```text
alternate_measure.amount
alternate_measure.unit
```

---

# 23. `alternate_measure.amount`

## Current Type

```text
integer | float | null
```

A null value is valid when no numeric alternate quantity exists.

Example:

```json
{
  "amount": null,
  "unit": ""
}
```

---

# 24. `alternate_measure.unit`

## Current Type

```text
string
```

The current dataset sometimes uses:

```text
""
```

when no alternate measurement is available.

## Canonical Normalization Direction

For production data:

```text
alternate_measure = null
```

or equivalent relational absence would be cleaner than:

```json
{
  "amount": null,
  "unit": ""
}
```

However, this should occur during canonical transformation rather than silently altering the curated source dataset.

---

# 25. Ingredient Ordering

Ingredient order should be preserved.

The current array order provides the sequence in which ingredients are presented by the curated recipe.

The relational implementation should therefore include an explicit ordering mechanism if ingredient records are normalized into related tables.

---

# 26. `instructions`

## Purpose

Contains the ordered recipe preparation steps.

## Current Type

```text
array<string>
```

Example:

```json
[
  "Add coffee to a phin.",
  "Bloom with part of the hot water.",
  "Stir the brewed coffee with condensed milk.",
  "Pour over ice."
]
```

## Requirement

```text
One or more usable instructions
Ordered
```

## Canonical Interpretation

Array position currently defines instruction order.

For relational storage, the equivalent structure will require something such as:

```text
position
instruction_text
```

The database representation will be defined later.

---

# 27. `cultural_context`

## Purpose

Stores contextual information related to how, when, where, or socially why the coffee is consumed or understood.

Current structure:

```json
{
  "associated_meal": "hospitality / gatherings",
  "meal_description": "..."
}
```

## Current Type

```text
object
```

All 198 records contain both nested fields.

However, empty strings currently exist.

---

# 28. `cultural_context.associated_meal`

## Purpose

Provides a concise contextual label describing a consumption setting, occasion, meal, or social context.

Examples:

```text
hospitality / gatherings
breakfast / morning coffee
coffee ceremony
street drink / hospitality
café / dessert drink
kopitiam
refreshment
```

## Current Type

```text
string
```

## Current Dataset

Some records use:

```text
""
```

when no associated meal or context was established.

## Canonical Direction

Missing contextual information should preferably become:

```text
null
```

rather than an empty string during canonical transformation.

---

# 29. `cultural_context.meal_description`

## Purpose

Provides a concise cultural or contextual description.

Examples may explain:

* hospitality use
* café traditions
* traditional serving practices
* meal associations
* origins stated by the source
* modern café context
* regional consumption context

## Current Type

```text
string
```

Some records currently contain an empty string.

## Rule

Cultural context should remain supported by research or source material.

Brewcipe should avoid:

* unsupported historical claims
* stereotypes
* generic country descriptions
* presenting a modern adaptation as universally traditional
* exoticizing language

Where no supported context exists, absence is preferable.

---

# 30. `source`

## Purpose

Identifies the public source used for the current recipe record.

Current structure:

```json
{
  "recipe_author": "Example Author",
  "original_publication": "https://example.com/recipe"
}
```

## Current Type

```text
object
```

All current records contain the `source` object.

---

# 31. `source.recipe_author`

## Purpose

Identifies the author, publisher, organization, or source attribution available for the recipe.

Examples include:

```text
UCC Ueshima Coffee
Pailin Chongchitnant
Counter Culture Coffee
Kopi House
```

## Current Type

Mostly:

```text
string
```

Some current records contain:

```text
null
```

## Canonical Rule

```text
string | null
```

A missing author should not invalidate a recipe when a valid original publication URL is available.

---

# 32. `source.original_publication`

## Purpose

Stores the original publication URL used during recipe research and curation.

## Current Type

```text
string
```

## Current Requirement

All current records contain a value.

## Rule

The URL should point to the relevant source material where possible rather than merely the publisher's homepage.

The production import process should validate URL structure.

---

# 33. Single-Source Model

The current v3 curated dataset uses:

```text
source
```

rather than:

```text
sources[]
```

Therefore, the current canonical mapping should not assume that every record already supports multiple source objects.

If future requirements need multiple sources per recipe, the database schema may support that relationship without requiring the curated JSON structure to change immediately.

This remains a future architecture/data-model decision.

---

# 34. `verification`

## Purpose

Stores internal curation and data-quality information about the recipe record.

Current structure:

```json
{
  "confidence": "high — quantities and method are source-stated",
  "notes": [
    "needs rechecking"
  ]
}
```

## Current Type

```text
object
```

All current records contain:

```text
confidence
notes
```

---

# 35. `verification.confidence`

## Purpose

Describes how strongly the curated recipe values are supported by the source and identifies where normalization or inference has occurred.

Examples include statements such as:

```text
high — quantities and method explicitly stated
```

```text
medium — method source-stated; quantities inferred
```

```text
medium-high — coffee dose source-stated; water volume inferred
```

## Current Type

```text
string
```

## Important Observation

`confidence` is currently descriptive text, not a pure enumerated value.

For example, it combines:

```text
confidence level
+
reasoning / provenance note
```

Conceptually:

```text
"medium-high — coffee dose source-stated; water volume inferred"
```

contains two separate ideas.

A future canonical internal model may normalize this into:

```text
confidence_level
confidence_reason
```

but the current dataset does not yet make that separation.

---

# 36. `verification.notes`

## Purpose

Stores internal curation history and review notes.

## Current Type

```text
array<string>
```

Examples include:

```text
needs rechecking
```

and change-history notes such as:

```text
coffee_recipe_id updated after duplicate removal
```

or:

```text
temperature updated from 'Hot or Iced' to ['Hot', 'Iced']
```

## Important Boundary

These notes are **internal data-preparation metadata**.

They are not intended to be shown as recipe content to ordinary Brewcipe users.

---

# 37. Application Data vs Internal Curation Metadata

The current JSON combines two categories of information.

## Application-facing canonical recipe data

```text
coffee_recipe_id
native_name
transliteration
english_name
geography
recipe_type
brewer
temperature
servings
ingredients
instructions
cultural_context
source
```

## Internal curation metadata

```text
verification
```

This distinction should be preserved in the production architecture.

Conceptually:

```text
Curated Dataset Record
│
├── Canonical Recipe Data
│
└── Internal Verification Metadata
```

The backend does not need to return internal verification notes in ordinary public recipe responses.

---

# 38. Current Logical Schema

A current dataset record can be represented as:

```text
CoffeeRecipeRecord
│
├── coffee_recipe_id: string
├── native_name: string
├── transliteration: string
├── english_name: string
│
├── geography
│   ├── country: string
│   ├── region: string
│   └── continent: string
│
├── recipe_type:
│   └── Cultural | Brewing | Traditional
│
├── brewer:
│   └── string | string[]
│
├── temperature:
│   └── Hot | Iced | [Hot, Iced]
│
├── servings: integer
│
├── ingredients[]
│   ├── ingredient: string
│   ├── amount: number | null
│   ├── unit: string
│   └── alternate_measure
│       ├── amount: number | null
│       └── unit: string
│
├── instructions[]
│   └── string
│
├── cultural_context
│   ├── associated_meal: string
│   └── meal_description: string
│
├── source
│   ├── recipe_author: string | null
│   └── original_publication: string
│
└── verification
    ├── confidence: string
    └── notes[]
        └── string
```

---

# 39. Current Example

The following structure illustrates the actual v3 model:

```json
{
  "coffee_recipe_id": "coffee_recipe_050",
  "native_name": "Cà phê sữa đá",
  "transliteration": "Ca Phe Sua Da",
  "english_name": "Vietnamese Iced Milk Coffee",

  "geography": {
    "country": "Vietnam",
    "region": "Southeast Asia",
    "continent": "Asia"
  },

  "recipe_type": "Cultural",

  "brewer": "Phin",

  "temperature": "Iced",

  "servings": 1,

  "ingredients": [
    {
      "ingredient": "ground coffee",
      "amount": 25,
      "unit": "g",
      "alternate_measure": {
        "amount": 4,
        "unit": "tbsp"
      }
    }
  ],

  "instructions": [
    "Add coffee to a phin.",
    "Bloom with part of the hot water, then add the rest and let the coffee drip.",
    "Stir the brewed coffee with condensed milk.",
    "Pour over ice."
  ],

  "cultural_context": {
    "associated_meal": "breakfast / morning coffee",
    "meal_description": "A familiar Vietnamese morning coffee."
  },

  "source": {
    "recipe_author": "Tuyết Phương / Hướng Nghiệp Á Âu",
    "original_publication": "https://www.huongnghiepaau.com/ca-phe-sua-da"
  },

  "verification": {
    "confidence": "medium-high — 25 g coffee and 2 tbsp condensed milk are source-stated; 120 ml water is inferred for a small phin",
    "notes": [
      "needs rechecking"
    ]
  }
}
```

This demonstrates the current structure rather than defining the eventual API response or PostgreSQL representation.

---

# 40. Normalization Requirements

The current curated dataset is structurally consistent overall but still requires canonical normalization before production import.

Normalization should address at least:

```text
geographical vocabulary
brewer naming
scalar-versus-array representation
missing-value representation
unit vocabulary
alternate-measure absence
verification metadata
```

Normalization should not silently rewrite source meaning.

---

# 41. Geography Normalization

Known inconsistencies include terminology such as:

```text
West Asia
Western Asia
```

and:

```text
North America
Northern America
```

as well as mixed continent modelling:

```text
America
North America
South America
```

A controlled geographical vocabulary must be established before relational import.

---

# 42. Brewer Normalization

The current dataset uses both:

```text
single brewer
```

and:

```text
multiple brewers
```

It also contains naming and capitalization variations.

Canonical transformation should:

1. normalize equivalent brewer names
2. preserve legitimate multiple-brewer relationships
3. avoid forcing multiple brewers into one delimited text string

---

# 43. Temperature Normalization

The logical concept supports one or more serving temperatures.

Canonical representation should therefore accommodate:

```text
Hot
Iced
```

and recipes supporting both.

The database should not require mixed:

```text
string
```

and:

```text
array
```

storage.

The relational database design should provide one consistent representation.

---

# 44. Ingredient Unit Normalization

Current ingredient units include both measurement units and descriptive qualifiers.

Examples of physical or count units:

```text
g
ml
L
cup
tbsp
tsp
whole
pieces
pods
shots
```

Examples of semantic qualifiers currently stored in `unit`:

```text
to taste
as needed
optional
for garnish
```

This should be reviewed before database design.

The schema should not assume every `unit` is mathematically convertible.

---

# 45. Alternate Measurement Normalization

The current dataset represents missing alternate measurements as:

```json
{
  "amount": null,
  "unit": ""
}
```

For production data, canonical transformation should preferably represent the absence of an alternate measurement as an actual absence rather than an object containing empty values.

The source dataset may remain unchanged.

---

# 46. Missing-Value Normalization

The current dataset contains several patterns:

```text
null
""
[]
```

These have different meanings depending on context.

For production canonical data:

```text
null
```

should normally represent an optional scalar value that is not available.

Empty strings should generally not be used as missing-data placeholders.

Empty arrays should represent an intentionally empty collection only where valid.

---

# 47. Verification Normalization

The current verification field mixes confidence classification and explanatory provenance.

Potential future internal structure:

```text
verification
├── confidence_level
├── confidence_reason
└── notes[]
```

However, this is **not yet the current dataset format**.

Any transformation should preserve the original verification meaning.

---

# 48. Structural Validation

Before a curated recipe is considered ready for production import, validation should confirm:

```text
coffee_recipe_id exists
coffee_recipe_id is unique

english_name exists

geography exists
country exists
region exists
continent exists

recipe_type belongs to the accepted vocabulary

brewer structure is valid

temperature uses accepted values

servings is a positive integer

ingredients is non-empty
each ingredient has an ingredient name
amount is numeric or null
alternate measurement is structurally valid

instructions is non-empty
instruction values are strings

cultural context has expected fields

source has original publication URL

verification has confidence and notes
```

---

# 49. Structural Validation vs Editorial Verification

These are separate concerns.

## Structural validation

asks:

> Does the record follow Brewcipe's expected schema?

Example:

```text
servings is a valid positive integer
```

## Editorial verification

asks:

> Is the recipe information sufficiently supported by its source?

Example:

```text
Was the water quantity explicitly stated, normalized, or inferred?
```

A record can be structurally valid while still requiring editorial rechecking.

---

# 50. Production Readiness

A record should not automatically become production-ready merely because it exists in `coffee-recipes-v3.json`.

Conceptual workflow:

```text
Curated Dataset
        ↓
Structural Validation
        ↓
Editorial Review
        ↓
Canonical Normalization
        ↓
Approved Production Record
        ↓
Relational Transformation
        ↓
Supabase PostgreSQL
```

Records marked with verification notes such as:

```text
needs rechecking
```

should remain identifiable during this process.

---

# 51. Data Lineage

The current workflow should preserve the distinction between:

```text
external source
```

```text
curated Brewcipe dataset
```

```text
normalized production record
```

Conceptually:

```text
Public Recipe Source
        ↓
Research / Curation
        ↓
coffee-recipes-v3.json
        ↓
Canonical Transformation
        ↓
Production Database
```

The curated JSON therefore acts as an input dataset.

It should not be assumed to already match the final physical production database structure.

---

# 52. Private Dataset Boundary

`coffee-recipes-v3.json` represents Brewcipe's curated production-oriented dataset and should remain outside the public GitHub repository if it contains the complete production coffee library.

The public repository may contain:

```text
schema documentation
database migrations
validation code
transformation logic
synthetic records
small illustrative examples
API models
```

The public repository should not contain:

```text
the complete production dataset
private research notes
private intermediate curation artifacts
private import files
credentials
```

---

# 53. API Boundary

The canonical logical schema does not require the API to expose every field.

For example, a discovery response may return:

```text
coffee_recipe_id
english_name
native_name
geography
recipe_type
brewer
temperature
```

while a recipe-detail response may additionally include:

```text
servings
ingredients
instructions
cultural_context
source
```

Internal fields such as:

```text
verification
```

should normally remain server-side or administrative.

---

# 54. AI Boundary

The AI Coffee Sommelier may use approved canonical Brewcipe records as grounding context.

Conceptually:

```text
Approved Coffee Records
        ↓
Backend Retrieval
        ↓
AI Grounding Context
        ↓
LLM
        ↓
Generated Recommendation
```

The LLM is not the canonical source of coffee data.

AI-generated information must not automatically modify:

```text
coffee-recipes-v3.json
```

or canonical production records.

---

# 55. Logical vs Relational Model

The current JSON structure is designed for curation and readability.

The production relational database may represent the same information differently.

For example:

```text
JSON:

geography:
  country: Vietnam
```

may become:

```text
recipes.country_id
        ↓
countries.id
```

Likewise:

```text
ingredients[]
```

may become:

```text
recipes
   ↓
recipe_ingredients
   ↓
ingredients
```

and:

```text
brewer: ["AeroPress", "French Press"]
```

may become:

```text
recipes
   ↓
recipe_brewers
   ↓
brewers
```

These relational decisions belong in `database-schema-v3.md`.

---

# 56. Fields Not Present in the Current Dataset

The current v3 dataset does not contain dedicated top-level fields for:

```text
preparation_time
brew_time
difficulty
ratings
reviews
nutrition
calories
cost
equipment shopping links
user tags
likes
comments
brew_water_temperature
grind_size
coffee_origin_farm
roaster
image
```

Some of these concepts may occasionally appear inside ingredient or instruction text.

They should **not** be promoted into canonical required fields unless future product requirements justify them.

---

# 57. Current Canonical Decisions

## CD-DECISION-001

The v3 canonical model is derived from the current `coffee-recipes-v3.json` structure rather than a hypothetical generic recipe schema.

---

## CD-DECISION-002

Each current coffee recipe has a stable `coffee_recipe_id`.

---

## CD-DECISION-003

Coffee identity uses three separate fields:

```text
native_name
transliteration
english_name
```

---

## CD-DECISION-004

Geographical discovery uses:

```text
continent
region
country
```

---

## CD-DECISION-005

The current `recipe_type` vocabulary is:

```text
Cultural
Brewing
Traditional
```

---

## CD-DECISION-006

`brewer` logically supports one or more brewer/method values.

---

## CD-DECISION-007

Top-level `temperature` means serving temperature rather than precise brew-water temperature.

---

## CD-DECISION-008

Supported serving-temperature values are currently:

```text
Hot
Iced
```

with some recipes supporting both.

---

## CD-DECISION-009

Ingredients contain:

```text
ingredient
amount
unit
alternate_measure
```

---

## CD-DECISION-010

Ingredient amount values may be numeric or null.

---

## CD-DECISION-011

Alternate measurements are part of the current Brewcipe curated data model.

---

## CD-DECISION-012

Instructions are ordered strings.

---

## CD-DECISION-013

Cultural context currently contains:

```text
associated_meal
meal_description
```

---

## CD-DECISION-014

The current curated record contains one `source` object.

---

## CD-DECISION-015

`verification` is internal curation metadata rather than ordinary user-facing recipe content.

---

## CD-DECISION-016

Normalized or inferred values must remain distinguishable from directly source-stated information.

---

## CD-DECISION-017

The complete production-oriented dataset and private preparation artifacts remain outside the public repository.

---

## CD-DECISION-018

The logical data model is independent of its eventual PostgreSQL representation.

---

# 58. Open Data Decisions

## CD-TBD-001 — Geography Vocabulary

Resolve canonical terminology for:

```text
West Asia vs Western Asia
North America vs Northern America
America vs North America / South America
```

---

## CD-TBD-002 — Brewer Taxonomy

Define which brewer values represent:

```text
equipment
brewing method
preparation technique
```

and whether these need separate concepts.

---

## CD-TBD-003 — Brewer Cardinality

Determine the final canonical representation for recipes supporting multiple brewers.

The current JSON uses arrays for a small number of records.

---

## CD-TBD-004 — Temperature Cardinality

Determine the final database representation for recipes that support both:

```text
Hot
Iced
```

---

## CD-TBD-005 — Unit Vocabulary

Define the controlled unit vocabulary and determine how to separate measurement units from qualifiers such as:

```text
to taste
optional
as needed
for garnish
```

---

## CD-TBD-006 — Missing Alternate Measurements

Determine whether canonical transformation should represent missing alternate measurements using:

```text
null
```

rather than an empty nested object.

---

## CD-TBD-007 — Verification Structure

Determine whether:

```text
verification.confidence
```

should remain descriptive text or be split into:

```text
confidence_level
confidence_reason
```

for internal use.

---

## CD-TBD-008 — Source Cardinality

Determine whether the production relational model should support multiple sources per recipe even though the current curated JSON contains one source object.

---

## CD-TBD-009 — Cultural Context Nullability

Standardize empty cultural-context strings into canonical null values where information is genuinely unavailable.

---

## CD-TBD-010 — Brewing Temperature

Determine whether Brewcipe needs a dedicated structured brew-water-temperature field in a future version.

The current top-level `temperature` field does not serve that purpose.

---

# 59. Relationship to Database Schema

This document answers:

> What does Brewcipe's coffee data mean?

`database-schema-v3.md` will answer:

> How should that information be stored relationally in Supabase PostgreSQL?

The next design step should therefore translate:

```text
Coffee Recipe
Geography
Brewers
Ingredients
Instructions
Cultural Context
Sources
Verification / Internal Metadata
```

into relational entities and relationships.

The database design should solve current structural inconsistencies rather than reproducing them blindly.

---

# 60. Relationship to Development Roadmap

The development roadmap requires:

```text
canonical mapping
geographical mapping
recipe mapping
ingredient mapping
instruction mapping
source/provenance mapping
optional / missing-value handling
schema validation
identifier validation
unit validation
duplicate detection
dataset statistics
```

This data schema defines the logical foundation for those activities.

---

# 61. Canonical Transformation Summary

The current workflow should be:

```text
coffee-recipes-v3.json
        ↓
Preserve Original Curated Meaning
        ↓
Normalize Controlled Vocabulary
        ↓
Normalize Missing Values
        ↓
Resolve Scalar / Multi-value Fields
        ↓
Validate Structure
        ↓
Review Verification Metadata
        ↓
Transform to Relational Model
        ↓
Import Approved Records
        ↓
Supabase PostgreSQL
```

---

# 62. Final Schema Summary

The current Brewcipe v3 coffee recipe model is:

```text
Coffee Recipe
│
├── Identity
│   ├── coffee_recipe_id
│   ├── native_name
│   ├── transliteration
│   └── english_name
│
├── Geography
│   ├── country
│   ├── region
│   └── continent
│
├── Classification
│   ├── recipe_type
│   ├── brewer(s)
│   └── serving temperature(s)
│
├── Recipe
│   ├── servings
│   ├── ingredients
│   │   ├── ingredient
│   │   ├── amount
│   │   ├── unit
│   │   └── alternate_measure
│   └── ordered instructions
│
├── Cultural Context
│   ├── associated_meal
│   └── meal_description
│
├── Source Attribution
│   ├── recipe_author
│   └── original_publication
│
└── Internal Verification
    ├── confidence
    └── notes
```

The current dataset provides a strong and mostly consistent logical foundation.

The remaining work is not to redesign the coffee data from scratch.

It is to:

```text
formalize it
normalize known inconsistencies
separate application data from internal metadata
define canonical null / multi-value rules
translate the logical model into a relational database
```

That relational translation is the responsibility of `database-schema-v3.md`.
