# Brewcipe — Database Schema v3

## 1. Purpose

This document defines the relational database design for the Brewcipe v3 MVP.

Brewcipe uses:

```text
Supabase PostgreSQL
```

as its canonical production application data store.

This document translates the logical coffee model defined in:

```text
docs/architecture/coffee-data-schema-v3.md
```

into PostgreSQL entities, relationships, constraints, indexes, and access-control boundaries.

It defines:

* database tables
* primary keys
* foreign keys
* one-to-many relationships
* many-to-many relationships
* nullability
* uniqueness rules
* ordering rules
* lookup/reference data
* favorite ownership
* Row Level Security boundaries
* indexing requirements
* migration expectations
* mapping from the private curated dataset

This document does not contain the production coffee dataset.

Production records are imported separately from privately maintained data-preparation artifacts.

---

# 2. Relationship to the Coffee Data Schema

The documentation relationship is:

```text
coffee-data-schema-v3.md
"What does Brewcipe coffee data mean?"

            ↓

database-schema-v3.md
"How is that data stored relationally?"

            ↓

supabase/migrations/
"How is the schema created reproducibly?"
```

The current curated dataset contains concepts such as:

```text
coffee recipe
geography
recipe type
brewer
serving temperature
ingredients
instructions
cultural context
source
verification
```

The relational database should preserve those concepts without reproducing unnecessary inconsistencies from the JSON representation.

---

# 3. Database Design Principles

## 3.1 Relational Integrity

Relationships that have meaningful reusable identity should use foreign keys rather than repeated free-text values where practical.

For example:

```text
coffee recipe
    ↓
country
    ↓
region
    ↓
continent
```

should be represented relationally rather than storing all geographical names independently on every recipe row.

---

## 3.2 Normalize Reusable Concepts

Reusable controlled concepts should be normalized where doing so improves:

* consistency
* validation
* search
* geographical exploration
* future maintainability

Examples include:

```text
continents
regions
countries
recipe types
brewers
serving temperatures
```

---

## 3.3 Do Not Over-Normalize Editorial Content

Not every string needs its own lookup table.

For example:

```text
native_name
transliteration
meal_description
instruction text
ingredient notes
```

are recipe-specific content.

Creating separate reference tables for every textual concept would add complexity without meaningful MVP benefit.

---

## 3.4 Preserve Ordered Data

Ingredients and instructions have meaningful ordering.

The relational model must therefore explicitly preserve:

```text
ingredient position
instruction position
```

rather than relying on unspecified database row order.

---

## 3.5 Support Optional Data

Optional canonical attributes should support:

```text
NULL
```

where appropriate.

Empty strings such as:

```text
''
```

should generally not represent missing production data.

---

## 3.6 Support Multi-Valued Concepts Relationally

The curated JSON currently contains some values as either:

```text
string
```

or:

```text
array
```

depending on the recipe.

Examples include:

```text
brewer
temperature
```

PostgreSQL should not reproduce this mixed representation.

Instead, multi-valued relationships should use junction tables.

---

## 3.7 Separate Public Content From Internal Metadata

Ordinary recipe data and internal curation metadata serve different purposes.

Public application content should remain separate from internal verification or import information where practical.

---

## 3.8 Supabase Auth Owns Authentication Identity

Brewcipe should not create a separate password or authentication system.

Authentication identity is managed by:

```text
auth.users
```

in Supabase Auth.

Application tables may reference authenticated users through their Supabase user UUID.

---

# 4. High-Level Entity Model

The proposed MVP relational model is:

```text
continents
    ↓
regions
    ↓
countries
    ↓
recipe_countries
    ↓
coffee_recipes
       │
       ├── recipe_types
       │
       ├── recipe_brewers ──→ brewers
       │
       ├── recipe_temperatures ──→ serving_temperatures
       │
       ├── recipe_ingredients
       │
       ├── recipe_instructions
       │
       ├── recipe_sources ──→ sources
       │
       └── recipe_verification

auth.users
    ↓
favorites
    ↓
coffee_recipes
```

---

# 5. Proposed Tables

The MVP database contains the following application tables:

```text
continents
regions
countries

recipe_types
brewers
serving_temperatures

coffee_recipes

recipe_brewers
recipe_temperatures

recipe_ingredients
recipe_instructions

recipe_countries

sources
recipe_sources

recipe_verification

favorites
```

Supabase additionally provides:

```text
auth.users
```

which is managed by Supabase Auth rather than Brewcipe migrations.

---

# 6. Geography Tables

Geographical discovery follows:

```text
Continent
    ↓
Region
    ↓
Country
    ↓
Recipe Country
    ↓
Coffee Recipe
```

The corresponding tables are:

```text
continents
regions
countries
```

---

# 7. `continents`

## Purpose

Stores canonical continent-level geography.

## Proposed Columns

| Column       | Type          | Null | Rule                            |
| ------------ | ------------- | ---: | ------------------------------- |
| `id`         | `uuid`        |   No | Primary key                     |
| `name`       | `text`        |   No | Canonical continent name        |
| `slug`       | `text`        |   No | URL/application-safe identifier |
| `created_at` | `timestamptz` |   No | Default current timestamp       |

## Constraints

```text
PRIMARY KEY (id)

UNIQUE (name)

UNIQUE (slug)

CHECK name is not blank

CHECK slug is not blank
```

## Example Data

```text
Asia
Africa
Europe
Oceania
North America
South America
```

The exact canonical continent vocabulary must be finalized before production import.

---

# 8. `regions`

## Purpose

Stores Brewcipe's geographical grouping between continent and country.

Examples:

```text
Southeast Asia
East Asia
North Africa
Southern Europe
```

## Proposed Columns

| Column         | Type          | Null | Rule                        |
| -------------- | ------------- | ---: | --------------------------- |
| `id`           | `uuid`        |   No | Primary key                 |
| `continent_id` | `uuid`        |   No | FK → `continents.id`        |
| `name`         | `text`        |   No | Canonical region name       |
| `slug`         | `text`        |   No | Application-safe identifier |
| `created_at`   | `timestamptz` |   No | Default current timestamp   |

## Constraints

```text
PRIMARY KEY (id)

FOREIGN KEY (continent_id)
REFERENCES continents(id)

UNIQUE (continent_id, name)

UNIQUE (continent_id, slug)

CHECK name is not blank

CHECK slug is not blank
```

---

# 9. `countries`

## Purpose

Stores canonical countries used by Brewcipe recipes.

## Proposed Columns

| Column       | Type          | Null | Rule                        |
| ------------ | ------------- | ---: | --------------------------- |
| `id`         | `uuid`        |   No | Primary key                 |
| `region_id`  | `uuid`        |   No | FK → `regions.id`           |
| `name`       | `text`        |   No | Canonical country name      |
| `slug`       | `text`        |   No | Application-safe identifier |
| `created_at` | `timestamptz` |   No | Default current timestamp   |

## Constraints

```text
PRIMARY KEY (id)

FOREIGN KEY (region_id)
REFERENCES regions(id)

UNIQUE (name)

UNIQUE (slug)

CHECK name is not blank

CHECK slug is not blank
```

---

# 10. Geography Relationship

# 10. Geography Relationship

The geographical model becomes:

```text
continents.id
      ↑
regions.continent_id

regions.id
      ↑
countries.region_id

countries.id
      ↑
recipe_countries.country_id

coffee_recipes.id
      ↑
recipe_countries.recipe_id
```

A recipe therefore does not need separate:

```text
continent_id
region_id
country_id
```

columns.

Its country determines the complete hierarchy:

```text
Recipe
  ↓
Country
  ↓
Region
  ↓
Continent
```

This prevents impossible combinations such as:

```text
country = Vietnam
region = Western Europe
continent = Africa
```
```md

# 10.1 `recipe_countries`

## Purpose

Associates coffee recipes with one or more canonical countries.

## Proposed Columns

| Column       | Type   | Null | Rule                     |
| ------------ | ------ | ---: | ------------------------ |
| `recipe_id`  | `uuid` |   No | FK → `coffee_recipes.id` |
| `country_id` | `uuid` |   No | FK → `countries.id`      |

## Primary Key

```text
PRIMARY KEY (recipe_id, country_id)

---

# 11. `recipe_types`

## Purpose

Stores the controlled recipe classification vocabulary.

The current v3 curated dataset uses:

```text
Cultural
Brewing
Traditional
```

## Proposed Columns

| Column        | Type       | Null | Rule                |
| ------------- | ---------- | ---: | ------------------- |
| `id`          | `smallint` |   No | Primary key         |
| `name`        | `text`     |   No | Recipe type         |
| `description` | `text`     |  Yes | Internal definition |

## Constraints

```text
PRIMARY KEY (id)

UNIQUE (name)

CHECK name is not blank
```

## Initial Reference Data

```text
Cultural
Brewing
Traditional
```

A lookup table is preferred over a PostgreSQL enum because the taxonomy is still subject to refinement.

---

# 12. `coffee_recipes`

## Purpose

Stores the central canonical Brewcipe recipe record.

## Proposed Columns

| Column             | Type          | Null | Rule                              |
| ------------------ | ------------- | ---: | --------------------------------- |
| `id`               | `uuid`        |   No | Internal primary key              |
| `coffee_recipe_id` | `text`        |   No | Stable Brewcipe domain identifier |
| `english_name`     | `text`        |   No | Primary display name              |
| `native_name`      | `text`        |  Yes | Native/local name                 |
| `transliteration`  | `text`        |  Yes | Latin-script rendering            |
| `recipe_type_id`   | `smallint`    |  Yes | FK → `recipe_types.id`            |
| `servings`         | `integer`     |  Yes | Intended servings                 |
| `associated_meal`  | `text`        |  Yes | Short cultural-context label      |
| `meal_description` | `text`        |  Yes | Cultural/contextual description   |
| `created_at`       | `timestamptz` |   No | Default current timestamp         |
| `updated_at`       | `timestamptz` |   No | Default current timestamp         |

---

# 13. Coffee Recipe Keys

Two identifiers serve different purposes.

## Internal Primary Key

```text
id UUID
```

Used for:

* foreign keys
* internal database relationships
* Supabase/PostgreSQL operations

## Stable Domain Identifier

```text
coffee_recipe_id
```

Example:

```text
coffee_recipe_053
```

Used as Brewcipe's stable recipe identifier derived from the curated data model.

## Constraints

```text
PRIMARY KEY (id)

UNIQUE (coffee_recipe_id)
```

The database must not rely on:

```text
english_name
```

as the unique recipe identifier.

Different recipes may legitimately have similar or identical names.

---

# 14. Coffee Recipe Constraints

Recommended constraints include:

```text
CHECK coffee_recipe_id is not blank

CHECK english_name is not blank

CHECK servings IS NULL OR servings > 0
```

Foreign keys:

```text

recipe_type_id
→ recipe_types.id
```

---

# 15. Optional Coffee Identity

The canonical model permits future records where:

```text
native_name = NULL
```

or:

```text
transliteration = NULL
```

even though the current curated dataset is more consistently populated.

The database should support the canonical model rather than forcing placeholder text.

---

# 16. Cultural Context Storage

The current curated JSON represents:

```text
cultural_context.associated_meal
cultural_context.meal_description
```

These fields are stored directly on:

```text
coffee_recipes
```

because they are one-to-one, recipe-specific editorial attributes.

A separate `cultural_context` table would add little value for the current MVP.

Therefore:

```text
coffee_recipes.associated_meal
coffee_recipes.meal_description
```

are nullable text fields.

---

# 17. `brewers`

## Purpose

Stores normalized brewer, equipment, or brewing-method vocabulary used by recipes.

Examples may include:

```text
Phin
AeroPress
French Press
Coffee Sock
Dallah
Espresso Machine
Hario V60
Stovetop Pot
```

## Proposed Columns

| Column       | Type          | Null | Rule                          |
| ------------ | ------------- | ---: | ----------------------------- |
| `id`         | `uuid`        |   No | Primary key                   |
| `name`       | `text`        |   No | Canonical brewer name         |
| `slug`       | `text`        |   No | Stable machine-friendly value |
| `created_at` | `timestamptz` |   No | Default current timestamp     |

## Constraints

```text
PRIMARY KEY (id)

UNIQUE (name)

UNIQUE (slug)

CHECK name is not blank
```

---

# 18. Why Brewer Is Not Stored Directly on `coffee_recipes`

Most current records contain:

```text
brewer: string
```

but some contain:

```text
brewer: string[]
```

Therefore:

```text
coffee_recipes.brewer TEXT
```

would incorrectly assume one brewer.

And:

```text
coffee_recipes.brewer TEXT[]
```

would reduce relational integrity.

Instead:

```text
coffee_recipes
      ↓
recipe_brewers
      ↓
brewers
```

supports one or multiple brewers consistently.

---

# 19. `recipe_brewers`

## Purpose

Junction table between recipes and brewers.

## Proposed Columns

| Column      | Type   | Null | Rule                     |
| ----------- | ------ | ---: | ------------------------ |
| `recipe_id` | `uuid` |   No | FK → `coffee_recipes.id` |
| `brewer_id` | `uuid` |   No | FK → `brewers.id`        |

## Primary Key

```text
PRIMARY KEY (recipe_id, brewer_id)
```

This prevents duplicate brewer assignments.

## Foreign Keys

```text
recipe_id
→ coffee_recipes.id

brewer_id
→ brewers.id
```

## Delete Behaviour

```text
recipe_id ON DELETE CASCADE
```

so deleting a recipe removes its associations.

Deleting a brewer that is still referenced should normally be restricted.

---

# 20. `serving_temperatures`

## Purpose

Stores the supported finished-drink serving temperature vocabulary.

The current canonical vocabulary is:

```text
Hot
Iced
```

## Proposed Columns

| Column | Type       | Null | Rule                       |
| ------ | ---------- | ---: | -------------------------- |
| `id`   | `smallint` |   No | Primary key                |
| `name` | `text`     |   No | Temperature classification |

## Constraints

```text
PRIMARY KEY (id)

UNIQUE (name)
```

## Initial Reference Data

```text
Hot
Iced
```

---

# 21. `recipe_temperatures`

## Purpose

Associates one recipe with one or more serving-temperature values.

## Proposed Columns

| Column           | Type       | Null | Rule                           |
| ---------------- | ---------- | ---: | ------------------------------ |
| `recipe_id`      | `uuid`     |   No | FK → `coffee_recipes.id`       |
| `temperature_id` | `smallint` |   No | FK → `serving_temperatures.id` |

## Primary Key

```text
PRIMARY KEY (recipe_id, temperature_id)
```

Examples:

```text
Recipe A → Hot

Recipe B → Iced

Recipe C → Hot
Recipe C → Iced
```

This replaces the current mixed JSON representation of:

```text
"Hot"
```

and:

```text
["Hot", "Iced"]
```

with one consistent relational model.

---

# 22. Brewing Temperature

The top-level v3 coffee field:

```text
temperature
```

means serving temperature.

It does not mean exact brewing-water temperature.

Therefore this schema does not currently contain:

```text
brew_temperature_celsius
```

or equivalent.

Exact values such as:

```text
93°C
90–95°C
```

remain inside recipe instructions unless a future product requirement introduces structured brew-temperature data.

---

# 23. Ingredient Modelling

The current curated model contains ordered ingredient objects:

```text
ingredient
amount
unit
alternate_measure
```

There are two possible relational approaches:

```text
Shared ingredient vocabulary
```

or:

```text
Recipe-specific ingredient rows
```

For the current MVP, Brewcipe should prefer **recipe-specific ingredient rows**.

---

# 24. Why There Is No Separate `ingredients` Vocabulary Table Yet

A normalized shared ingredient table might look like:

```text
ingredients
recipe_ingredients
```

However, the current dataset contains recipe-specific descriptions such as:

```text
light-roasted washed Pu'er Catimor coffee beans

Thai coffee mixture

sweetened Vietnamese coffee concentrate

coffee, medium-fine

fresh milk or condensed milk
```

A shared ingredient vocabulary would require additional decisions about:

* aliases
* ingredient variants
* preparation states
* qualifiers
* canonical ingredient naming
* ingredient search

Those capabilities are not required by the MVP.

Therefore Brewcipe should initially store ingredient descriptions directly on:

```text
recipe_ingredients
```

This avoids premature normalization.

---

# 25. `recipe_ingredients`

## Purpose

Stores the ordered ingredients belonging to a recipe.

## Proposed Columns

| Column             | Type          | Null | Rule                      |
| ------------------ | ------------- | ---: | ------------------------- |
| `id`               | `uuid`        |   No | Primary key               |
| `recipe_id`        | `uuid`        |   No | FK → `coffee_recipes.id`  |
| `position`         | `integer`     |   No | Ingredient order          |
| `ingredient_name`  | `text`        |   No | Ingredient description    |
| `amount`           | `numeric`     |  Yes | Primary amount            |
| `unit`             | `text`        |  Yes | Primary unit/qualifier    |
| `alternate_amount` | `numeric`     |  Yes | Alternate quantity        |
| `alternate_unit`   | `text`        |  Yes | Alternate unit            |
| `created_at`       | `timestamptz` |   No | Default current timestamp |

---

# 26. Ingredient Constraints

Recommended constraints:

```text
PRIMARY KEY (id)

FOREIGN KEY (recipe_id)
REFERENCES coffee_recipes(id)
ON DELETE CASCADE

UNIQUE (recipe_id, position)

CHECK position > 0

CHECK ingredient_name is not blank
```

Amounts may be:

```text
NULL
```

because ingredients such as:

```text
ice — as needed
sugar — to taste
milk — optional
```

do not necessarily have numeric quantities.

---

# 27. Ingredient Numeric Type

Ingredient amounts should use:

```text
numeric
```

rather than:

```text
integer
```

because the dataset includes values such as:

```text
0.125
0.25
1.5
2.5
```

The exact precision and scale may be selected during migration implementation.

A reasonable starting point is:

```text
numeric(10,4)
```

provided validation confirms it can represent all required production quantities.

---

# 28. Unit Storage

For the MVP:

```text
unit
alternate_unit
```

remain text values.

This is intentional.

The current dataset mixes formal measurement units:

```text
g
ml
L
tbsp
tsp
cups
```

with quantity or usage qualifiers:

```text
to taste
as needed
optional
for garnish
```

A dedicated unit taxonomy would require additional normalization decisions that are not currently required for core application functionality.

Unit normalization should still occur during private data preparation.

---

# 29. Missing Alternate Measurements

The curated JSON sometimes contains:

```json
{
  "alternate_measure": {
    "amount": null,
    "unit": ""
  }
}
```

The relational database should normalize this to:

```text
alternate_amount = NULL
alternate_unit = NULL
```

rather than storing empty strings.

---

# 30. Ingredient Ordering

The private import transformation converts JSON array order into:

```text
position
```

Example:

```text
1 → ground coffee
2 → condensed milk
3 → water
4 → ice
```

Queries retrieving ingredients should order by:

```text
position ASC
```

---

# 31. `recipe_instructions`

## Purpose

Stores ordered preparation instructions.

## Proposed Columns

| Column             | Type          | Null | Rule                      |
| ------------------ | ------------- | ---: | ------------------------- |
| `id`               | `uuid`        |   No | Primary key               |
| `recipe_id`        | `uuid`        |   No | FK → `coffee_recipes.id`  |
| `position`         | `integer`     |   No | Preparation order         |
| `instruction_text` | `text`        |   No | Step content              |
| `created_at`       | `timestamptz` |   No | Default current timestamp |

---

# 32. Instruction Constraints

```text
PRIMARY KEY (id)

FOREIGN KEY (recipe_id)
REFERENCES coffee_recipes(id)
ON DELETE CASCADE

UNIQUE (recipe_id, position)

CHECK position > 0

CHECK instruction_text is not blank
```

Instruction array order from the private curated dataset is transformed into:

```text
position
```

during import.

---

# 33. Sources and Provenance

The current curated JSON contains one:

```text
source
```

object per recipe.

However, source identity is meaningfully reusable.

For example, one publisher may support several recipes.

The database should therefore separate:

```text
sources
```

from:

```text
recipe_sources
```

This also permits future recipes to use more than one source without changing the recipe table.

---

# 34. `sources`

## Purpose

Stores identifiable external recipe/source publications.

## Proposed Columns

| Column                 | Type          | Null | Rule                         |
| ---------------------- | ------------- | ---: | ---------------------------- |
| `id`                   | `uuid`        |   No | Primary key                  |
| `recipe_author`        | `text`        |  Yes | Author/publisher attribution |
| `original_publication` | `text`        |   No | Source URL                   |
| `created_at`           | `timestamptz` |   No | Default current timestamp    |

## Constraints

```text
PRIMARY KEY (id)

UNIQUE (original_publication)

CHECK original_publication is not blank
```

A missing author does not invalidate a source when the publication URL is known.

---

# 35. Source URL Validation

PostgreSQL does not need to implement sophisticated URL validation through an overly complex database constraint.

The backend/private import process should perform stronger URL validation.

The database should at minimum prevent:

```text
NULL
blank string
```

for `original_publication`.

---

# 36. `recipe_sources`

## Purpose

Associates recipes with supporting sources.

## Proposed Columns

| Column       | Type      | Null | Rule                     |
| ------------ | --------- | ---: | ------------------------ |
| `recipe_id`  | `uuid`    |   No | FK → `coffee_recipes.id` |
| `source_id`  | `uuid`    |   No | FK → `sources.id`        |
| `is_primary` | `boolean` |   No | Default `false`          |

## Primary Key

```text
PRIMARY KEY (recipe_id, source_id)
```

## Foreign Keys

```text
recipe_id
→ coffee_recipes.id

source_id
→ sources.id
```

---

# 37. Why Support Multiple Sources in PostgreSQL

The current curated JSON contains only:

```text
source
```

rather than:

```text
sources[]
```

The database nevertheless benefits from a many-to-many source relationship because:

* the same source page can support multiple recipes
* a future recipe may need separate recipe and cultural-context sources
* provenance requirements benefit from avoiding a hard one-source database limitation

For the current import:

```text
one JSON source
→ one recipe_sources relationship
```

Future data can add more without a schema redesign.

---

# 38. Internal Verification Metadata

The curated dataset contains:

```text
verification.confidence
verification.notes[]
```

This information is useful during:

* curation
* review
* production import
* provenance inspection

It is not ordinary public recipe content.

---

# 39. `recipe_verification`

## Purpose

Stores internal verification information for canonical recipe records when retained in the production database.

## Proposed Columns

| Column              | Type          | Null | Rule                                    |
| ------------------- | ------------- | ---: | --------------------------------------- |
| `recipe_id`         | `uuid`        |   No | PK/FK → `coffee_recipes.id`             |
| `confidence_level`  | `text`        |  Yes | Normalized level where available        |
| `confidence_reason` | `text`        |  Yes | Explanation of source support/inference |
| `notes`             | `text[]`      |  Yes | Internal review/history notes           |
| `updated_at`        | `timestamptz` |   No | Default current timestamp               |

## Relationship

```text
coffee_recipes
      1
      │
      │
      0..1
recipe_verification
```

---

# 40. Verification Transformation

The current JSON combines confidence level and explanation:

```text
"medium-high — coffee dose source-stated; water volume inferred"
```

Private transformation may separate this into:

```text
confidence_level:
medium-high

confidence_reason:
coffee dose source-stated; water volume inferred
```

The original meaning must be preserved.

---

# 41. Verification Access Boundary

`recipe_verification` is internal metadata.

Ordinary public users should not require direct access to:

```text
needs rechecking

identifier changed after duplicate removal

quantity inferred during curation
```

The table should therefore not be exposed through public application responses.

Backend/admin access may use privileged database credentials where necessary.

---

# 42. Authentication

Authentication is provided through:

```text
Supabase Auth
```

Supabase maintains user identities in:

```text
auth.users
```

Brewcipe should not duplicate authentication credentials into an application table.

---

# 43. User Profile Table

A dedicated:

```text
profiles
```

table is **not currently required** by the Brewcipe MVP.

The product does not currently require:

* public profiles
* display-name customization
* avatars
* biographies
* social relationships
* extensive account preferences

If future requirements introduce application-specific user metadata, a `profiles` table may then reference:

```text
auth.users.id
```

For the current MVP, favorites can directly reference the Supabase user UUID.

---

# 44. `favorites`

## Purpose

Stores coffee recipes saved by authenticated users.

## Proposed Columns

| Column       | Type          | Null | Rule                      |
| ------------ | ------------- | ---: | ------------------------- |
| `user_id`    | `uuid`        |   No | FK → `auth.users.id`      |
| `recipe_id`  | `uuid`        |   No | FK → `coffee_recipes.id`  |
| `created_at` | `timestamptz` |   No | Default current timestamp |

## Primary Key

```text
PRIMARY KEY (user_id, recipe_id)
```

This prevents duplicate favorites automatically.

---

# 45. Favorite Relationships

```text
auth.users
     │
     │ 1
     ↓
favorites
     ↑
     │ *
     │
coffee_recipes
```

A user may favorite many recipes.

A recipe may be favorited by many users.

---

# 46. Favorite Delete Behaviour

Recommended relationships:

```text
user_id
REFERENCES auth.users(id)
ON DELETE CASCADE
```

and:

```text
recipe_id
REFERENCES coffee_recipes(id)
ON DELETE CASCADE
```

Therefore:

* deleting a user removes their favorites
* deleting a recipe removes corresponding favorite references

---

# 47. Row Level Security

RLS is primarily required for user-specific data.

For the MVP:

```text
favorites
```

must use Row Level Security.

Public canonical recipe tables are primarily read-only application data.

---

# 48. Favorites RLS Policies

Conceptually, authenticated users should be able to:

```text
SELECT their own favorites

INSERT a favorite where user_id = auth.uid()

DELETE a favorite where user_id = auth.uid()
```

Users must not be able to:

```text
read another user's private favorite records
create a favorite on behalf of another user
delete another user's favorite
```

Conceptual policy condition:

```text
user_id = auth.uid()
```

Exact SQL policy syntax belongs in the migration implementation.

---

# 49A. Taste Profile & Recipe Interaction Data

Brewcipe's personalization mechanic introduces user-specific application data in addition to the existing `favorites` relationship.

These tables are not part of the canonical coffee recipe dataset.

## `user_taste_profiles`

### Purpose

Stores the authenticated user's current explicit taste profile used by the recommendation engine and Sommelier context builder.

### Current Logical Fields

```text
user_id
preferences
brewers
discovery_style
```

`user_id` references `auth.users.id` and identifies the owner of the profile.

The current supported preference signals are:

```text
sweet
milky
strong
spiced
simple
```

Supported brewer and discovery-style values are defined by the application taste-profile schema.

## `recipe_interactions`

### Purpose

Stores meaningful user interactions with Brewcipe recipes that can be used as personalization evidence.

### Current Logical Fields

```text
user_id
recipe_id
interaction
created_at
```

`recipe_id` references the internal UUID of `coffee_recipes.id`.

The stable public recipe identifier `coffee_recipe_id` remains the application-facing domain identifier. Application services translate between the database UUID and stable recipe identifier where required.

### Current Interaction Types

```text
tried
skipped
```

The current primary key is:

```text
(user_id, recipe_id, interaction)
```

This allows a user to retain one row per interaction type for a recipe while preventing duplicate identical interaction rows.

## Personalization Relationship

```text
auth.users
   │
   ├──────────────→ user_taste_profiles
   │
   ├──────────────→ favorites ─────────→ coffee_recipes
   │
   └──────────────→ recipe_interactions ─→ coffee_recipes
```

The recommendation engine consumes this user-specific information but does not write canonical recipe facts.

## Saved vs Tried vs Skipped

```text
Favorite / Saved
    = explicit interest

Tried
    = stronger evidence from actual experience

Skipped
    = avoidance / negative discovery evidence
```

Favorite weighting is not yet equivalent to tried-history learning in the current recommendation implementation.

---

# 49. Recipe Data Access

Core coffee content is publicly discoverable.

Therefore the application requires read access to approved canonical recipe data for:

```text
coffee_recipes
continents
regions
countries
recipe_types
brewers
recipe_brewers
serving_temperatures
recipe_temperatures
recipe_ingredients
recipe_instructions
sources
recipe_sources
```

Write access to canonical production coffee data should **not** be available to ordinary public users.

Production recipe creation and modification occur through controlled private/admin processes rather than unrestricted client writes.

---

# 50. Verification Access

`recipe_verification` should not receive the same public-read treatment as ordinary recipe data.

Access should remain restricted to trusted backend or administrative workflows.

---

# 51. Search Support

The MVP requires coffee-name search.

The database should therefore support efficient lookup against:

```text
coffee_recipes.english_name
coffee_recipes.native_name
coffee_recipes.transliteration
```

The exact search implementation remains an application decision.

The initial direction should remain PostgreSQL-native.

---

# 52. Search Indexes

At minimum, normal indexes should support relevant lookup and join operations.

Potential name-search optimization may later use PostgreSQL capabilities such as:

```text
lower(...)
```

or:

```text
pg_trgm
```

if partial/fuzzy name search is implemented.

A dedicated external search platform is not required by the MVP.

---

# 53. Required Indexes

Primary keys and unique constraints automatically create relevant indexes.

Additional recommended indexes include:

```text
regions(continent_id)

countries(region_id)

recipe_countries(country_id)

coffee_recipes(recipe_type_id)

recipe_brewers(brewer_id)

recipe_temperatures(temperature_id)

recipe_ingredients(recipe_id, position)

recipe_instructions(recipe_id, position)

recipe_sources(source_id)

favorites(recipe_id)

favorites(user_id, created_at)
```

Some composite indexes overlap with primary/unique indexes and should not be duplicated unnecessarily.

Final index creation should be verified against actual query patterns.

---

# 54. Geographic Query Paths

The schema supports:

```text
all continents

continent → regions

region → countries

country → recipes
```

For example:

```text
Asia
  ↓
Southeast Asia
  ↓
Vietnam
  ↓
Vietnamese Egg Coffee
```

The backend can query the hierarchy through foreign-key joins.

---

# 55. Recipe Detail Query

A complete recipe detail requires data from:

```text
coffee_recipes
countries
regions
continents
recipe_countries

recipe_types

recipe_brewers
brewers

recipe_temperatures
serving_temperatures

recipe_ingredients

recipe_instructions

recipe_sources
sources
```

The backend is responsible for shaping these relational rows into an application-friendly response.

---

# 56. Example Logical-to-Relational Mapping

Curated JSON:

```json
{
  "coffee_recipe_id": "coffee_recipe_050",
  "english_name": "Vietnamese Iced Milk Coffee",
  "geography": {
    "country": "Vietnam",
    "region": "Southeast Asia",
    "continent": "Asia"
  },
  "recipe_type": "Cultural",
  "brewer": "Phin",
  "temperature": "Iced",
  "servings": 1
}
```

becomes conceptually:

```text
continents
Asia

regions
Southeast Asia → Asia

countries
Vietnam → Southeast Asia

recipe_types
Cultural

brewers
Phin

serving_temperatures
Iced

coffee_recipes
coffee_recipe_050
Vietnamese Iced Milk Coffee
recipe_type_id → Cultural
servings → 1

recipe_countries
coffee_recipe_050 → Vietnam

recipe_brewers
coffee_recipe_050 → Phin

recipe_temperatures
coffee_recipe_050 → Iced
```

---

# 57. Ingredient Mapping Example

Curated JSON:

```json
{
  "ingredient": "ground coffee",
  "amount": 25,
  "unit": "g",
  "alternate_measure": {
    "amount": 4,
    "unit": "tbsp"
  }
}
```

becomes:

```text
recipe_ingredients

recipe_id:
<recipe UUID>

position:
1

ingredient_name:
ground coffee

amount:
25

unit:
g

alternate_amount:
4

alternate_unit:
tbsp
```

---

# 58. Instruction Mapping Example

Curated JSON:

```json
[
  "Add coffee to a phin.",
  "Bloom with part of the hot water.",
  "Pour over ice."
]
```

becomes:

```text
recipe_instructions

recipe_id | position | instruction_text
----------|----------|------------------------------
...       | 1        | Add coffee to a phin.
...       | 2        | Bloom with part...
...       | 3        | Pour over ice.
```

---

# 59. Null and Empty-Value Mapping

During private transformation:

```text
""
```

used to represent unavailable optional data should generally become:

```text
NULL
```

Examples:

```text
associated_meal: ""
→ NULL

meal_description: ""
→ NULL

alternate_measure.unit: ""
→ NULL
```

This prevents empty-string placeholders from becoming canonical missing values.

---

# 60. Data Import Order

Foreign-key dependencies require a controlled import sequence.

Recommended order:

```text
1. continents

2. regions

3. countries

4. recipe_types

5. brewers

6. serving_temperatures

7. coffee_recipes

8. recipe_countries

9. recipe_brewers

10. recipe_temperatures

11. recipe_ingredients

12. recipe_instructions

13. sources

14. recipe_sources

15. recipe_verification
```

`favorites` are created through normal application use and are not part of initial coffee-data import.

---

# 61. Canonical Import Boundary

The private JSON dataset should not be loaded blindly into PostgreSQL.

The transformation pipeline should conceptually perform:

```text
coffee-recipes-v3.json
        ↓
validate identifiers
        ↓
normalize geography
        ↓
normalize brewer vocabulary
        ↓
normalize temperature values
        ↓
normalize missing values
        ↓
validate ingredients
        ↓
preserve ordering
        ↓
validate sources
        ↓
review verification status
        ↓
transform relational entities
        ↓
import approved data
```

---

# 62. Production Readiness

A recipe should be imported as approved canonical application data only after it satisfies:

```text
valid stable identifier

valid geographical mapping

recognized recipe type where applicable

valid brewer mapping

valid serving temperature mapping

positive servings where present

at least one valid ingredient

at least one valid instruction

required source attribution

acceptable verification/review status
```

The exact editorial threshold for:

```text
acceptable verification/review status
```

must be determined by the data-preparation workflow.

---

# 63. Timestamps

Application-managed tables should generally include:

```text
created_at
```

where creation history is useful.

Mutable canonical entities such as:

```text
coffee_recipes
recipe_verification
```

may also contain:

```text
updated_at
```

An update mechanism should ensure `updated_at` changes when the corresponding row is modified.

The exact trigger implementation belongs in migrations.

---

# 64. UUID Generation

Application tables using UUID primary keys should use PostgreSQL/Supabase-supported UUID generation.

Conceptually:

```text
id UUID PRIMARY KEY DEFAULT gen_random_uuid()
```

Exact SQL should be verified against the configured Supabase PostgreSQL environment during migration implementation.

---

# 65. Cascading Deletes

Recommended cascade behavior:

```text
coffee_recipes
    ↓ CASCADE
recipe_ingredients

coffee_recipes
    ↓ CASCADE
recipe_countries

coffee_recipes
    ↓ CASCADE
recipe_instructions

coffee_recipes
    ↓ CASCADE
recipe_brewers

coffee_recipes
    ↓ CASCADE
recipe_temperatures

coffee_recipes
    ↓ CASCADE
recipe_sources

coffee_recipes
    ↓ CASCADE
recipe_verification

coffee_recipes
    ↓ CASCADE
favorites
```

Reference vocabulary should generally not be cascade-deleted through recipe relationships.

For example, deleting:

```text
Vietnam
```

should not automatically delete every Vietnamese recipe.

Reference-data deletion should normally be restricted while referenced.

---

# 66. Entity Relationship Diagram

Conceptual ERD:

```text
┌──────────────┐
│  continents  │
└──────┬───────┘
       │ 1
       │
       │ *
┌──────▼───────┐
│   regions    │
└──────┬───────┘
       │ 1
       │
       │ *
┌──────▼───────┐
│  countries   │
└──────┬───────┘
       │ 1
       │
       │ *
┌──────▼─────────────┐
│   coffee_recipes   │
└─┬─────┬─────┬────┬─┘
  │     │     │    │
  │     │     │    └──────────────┐
  │     │     │                   │
  │     │     │                   │
  │     │     │             ┌─────▼────────────┐
  │     │     │             │ recipe_sources   │
  │     │     │             └─────┬────────────┘
  │     │     │                   │
  │     │     │             ┌─────▼────┐
  │     │     │             │ sources  │
  │     │     │             └──────────┘
  │     │     │
  │     │     ├──────────────→ recipe_ingredients
  │     │     │
  │     │     └──────────────→ recipe_instructions
  │     │
  │     ├────→ recipe_brewers ─────→ brewers
  │     │
  │     └────→ recipe_temperatures ─→ serving_temperatures
  │
  └──────────→ recipe_verification


recipe_types
     │
     └────────→ coffee_recipes


auth.users
     │
     │
     ▼
 favorites
     │
     ▼
coffee_recipes
```

---

# 67. Relationship Cardinality Summary

| Relationship                     | Cardinality        |
| -------------------------------- | ------------------ |
| Continent → Regions              | One-to-many        |
| Region → Countries               | One-to-many        |
| Country → Recipes                | One-to-many        |
| Recipe Type → Recipes            | One-to-many        |
| Recipe ↔ Brewers                 | Many-to-many       |
| Recipe ↔ Serving Temperatures    | Many-to-many       |
| Recipe → Ingredients             | One-to-many        |
| Recipe → Instructions            | One-to-many        |
| Recipe ↔ Sources                 | Many-to-many       |
| Recipe → Verification            | One-to-zero-or-one |
| User ↔ Recipes through Favorites | Many-to-many       |

---

# 68. Tables Intentionally Not Included

The MVP schema does not currently require:

```text
profiles
reviews
ratings
comments
social_followers
coffee_journals
brew_history
equipment_catalog
shopping_products
nutrition
recipe_scaling
images
AI_conversations
AI_generated_recipes
notifications
moderation
community_submissions
```

These should not be added merely because they are common application patterns.

Future product requirements may introduce them later.

---

# 69. No Generic `coffees` + `recipes` Split Yet

The current Brewcipe dataset fundamentally represents:

```text
coffee recipe records
```

rather than a clearly separated catalogue of:

```text
Coffee Identity
        ↓
Multiple Independent Recipes
```

For example, the dataset already contains method-specific records such as different Kenyan brewing preparations and publisher-specific espresso recipes.

Creating both:

```text
coffees
recipes
```

would require a new business rule defining what constitutes the shared parent coffee identity.

That rule is not currently established.

Therefore the MVP should use:

```text
coffee_recipes
```

as the central entity.

A separate parent `coffees` entity may be introduced in a future schema if product requirements require grouping multiple recipes under one canonical coffee identity.

---

# 70. No Generic Ingredient Catalogue Yet

The MVP does not create:

```text
ingredients
```

as a reusable ingredient master table.

Recipe ingredient descriptions remain directly associated with their recipes.

This can be reconsidered if future features require:

```text
ingredient search
ingredient filtering
dietary analysis
shopping lists
inventory
recipe comparison
```

---

# 71. No Dedicated Cultural Context Table

Current cultural context is a one-to-one attribute of a recipe.

Therefore:

```text
associated_meal
meal_description
```

remain on:

```text
coffee_recipes
```

rather than being moved into an unnecessary separate table.

---

# 72. No Dedicated Search Infrastructure

Search remains PostgreSQL-based for the MVP.

The database schema should support name-based querying without introducing:

```text
Elasticsearch
OpenSearch
Algolia
vector database
dedicated search cluster
```

unless future requirements justify additional infrastructure.

---

# 73. Migration Strategy

Schema changes must be represented through version-controlled migrations under:

```text
supabase/migrations/
```

Conceptually:

```text
database-schema-v3.md
        ↓
SQL migration
        ↓
Supabase PostgreSQL
```

Migration files should contain:

```text
schema creation
constraints
indexes
reference-data definitions where appropriate
RLS policies
database functions/triggers where required
```

They should not contain the complete production coffee dataset.

---

# 74. Initial Reference Data in Migrations

Small controlled lookup values may reasonably be included in migrations where they form part of the schema.

Examples:

```text
recipe types:

Cultural
Brewing
Traditional
```

and:

```text
serving temperatures:

Hot
Iced
```

Geographical and recipe production records should be handled according to the private import boundary rather than embedding the full coffee library into public migrations.

---

# 75. Public Repository Boundary

The public repository may contain:

```text
database migrations
schema documentation
constraints
RLS definitions
validation scripts
synthetic examples
small controlled reference values
```

It should not contain:

```text
complete production coffee records
private import files
private research notes
private transformation artifacts
credentials
```

---

# 76. Database Validation

After migrations are applied, verification should confirm:

```text
all expected tables exist

primary keys exist

foreign keys exist

uniqueness constraints work

nullable fields match the canonical model

ingredient ordering is enforceable

instruction ordering is enforceable

duplicate favorites are prevented

multi-brewer recipes are supported

Hot + Iced recipes are supported

geographical relationships are valid

RLS protects favorites

internal verification data is not publicly exposed

production data is absent from public migrations
```

---

# 77. Representative Database Tests

Database testing should include representative scenarios.

## Recipe

```text
Insert valid recipe
→ succeeds
```

```text
Insert duplicate coffee_recipe_id
→ fails
```

```text
Insert servings = 0
→ fails
```

---

## Geography

```text
Insert country referencing missing region
→ fails
```

---

## Ingredients

```text
Insert two ingredients with same recipe + position
→ fails
```

---

## Instructions

```text
Insert instruction with position <= 0
→ fails
```

---

## Favorites

```text
Same user favorites same recipe twice
→ fails
```

```text
User attempts to modify another user's favorite
→ blocked
```

---

## Multi-Value Relationships

```text
One recipe → AeroPress
One recipe → French Press
```

should both be valid simultaneously.

Likewise:

```text
One recipe → Hot
One recipe → Iced
```

should both be valid simultaneously.

---

# 78. Proposed Database Decisions

## DB-DECISION-001

Use Supabase PostgreSQL as the canonical Brewcipe production application database.

---

## DB-DECISION-002

Use `coffee_recipes` as the central MVP coffee entity.

---

## DB-DECISION-003

Use UUID primary keys for core application entities while retaining `coffee_recipe_id` as a unique stable Brewcipe domain identifier.

---

## DB-DECISION-004

Normalize geographical hierarchy into:

```text
continents
regions
countries
```

---

## DB-DECISION-005

A recipe references its country only; region and continent are derived relationally.

---

## DB-DECISION-006

Store recipe classifications through a `recipe_types` lookup table.

---

## DB-DECISION-007

Model brewers through:

```text
brewers
recipe_brewers
```

so recipes may support one or more brewers.

---

## DB-DECISION-008

Model service temperature through:

```text
serving_temperatures
recipe_temperatures
```

so recipes may support Hot, Iced, or both.

---

## DB-DECISION-009

Do not use the top-level temperature concept for structured brew-water temperature.

---

## DB-DECISION-010

Store recipe ingredients as ordered recipe-specific rows rather than introducing a shared ingredient master table for the MVP.

---

## DB-DECISION-011

Use numeric nullable ingredient amounts.

---

## DB-DECISION-012

Store ingredient units as normalized text for the MVP rather than introducing a unit-reference subsystem.

---

## DB-DECISION-013

Represent missing alternate measurements using SQL `NULL`.

---

## DB-DECISION-014

Store preparation instructions as ordered rows.

---

## DB-DECISION-015

Normalize sources into:

```text
sources
recipe_sources
```

even though the current curated JSON contains one source object per recipe.

---

## DB-DECISION-016

Treat verification information as internal metadata rather than ordinary public recipe data.

---

## DB-DECISION-017

Use Supabase `auth.users` as the authoritative user identity store.

---

## DB-DECISION-018

Do not create a separate application `profiles` table until product requirements require user-specific profile metadata.

---

## DB-DECISION-019

Use a composite primary key on:

```text
favorites(user_id, recipe_id)
```

to prevent duplicate favorites.

---

## DB-DECISION-020

Apply RLS to favorites so authenticated users can access only their own favorite relationships.

---

## DB-DECISION-021

Keep canonical coffee data publicly readable through controlled application architecture while preventing unrestricted public writes.

---

## DB-DECISION-022

Do not introduce a separate `coffees` parent entity until Brewcipe defines a business rule for grouping multiple recipes under one canonical coffee identity.

---

## DB-DECISION-023

Do not introduce dedicated external search infrastructure for the MVP.

---

## DB-DECISION-024

Represent database changes through version-controlled migrations under:

```text
supabase/migrations/
```

---

# 79. Open Database Decisions

## DB-TBD-001 — Geography Vocabulary

Finalize canonical values before reference data is imported.

Known issues include:

```text
West Asia vs Western Asia

North America vs Northern America

America vs North America / South America
```

---

## DB-TBD-002 — Brewer Vocabulary

Finalize normalized brewer names and determine whether some current values represent:

```text
brewer equipment
brewing method
preparation technique
```

---

## DB-TBD-003 — Recipe Type Definitions

Clarify the business distinction between:

```text
Cultural
Traditional
Brewing
```

before new production records are classified programmatically.

---

## DB-TBD-004 — Verification Retention

Determine whether production Supabase should retain all:

```text
recipe_verification.notes
```

or whether detailed curation history should remain exclusively in private preparation artifacts.

---

## DB-TBD-005 — Name Search Index

Determine whether standard PostgreSQL text matching is sufficient or whether MVP search should enable:

```text
pg_trgm
```

for partial/fuzzy coffee-name search.

---

## DB-TBD-006 — Source Provenance Granularity

Determine whether future source relationships need information such as:

```text
source role
recipe source
cultural-context source
field-level provenance
```

Current MVP schema supports recipe-to-source relationships without field-level provenance.

---

## DB-TBD-007 — Updated Timestamp Implementation

Determine whether `updated_at` is maintained through:

```text
application code
```

or:

```text
database trigger
```

A database trigger may provide more consistent enforcement.

---

# 80. Final Relational Model

The proposed Brewcipe v3 MVP database can be summarized as:

```text
GEOGRAPHY
─────────

continents
    ↓
regions
    ↓
countries
    ↓
coffee_recipes


RECIPE CLASSIFICATION
─────────────────────

recipe_types
    ↓
coffee_recipes


BREWERS
───────

coffee_recipes
    ↓
recipe_brewers
    ↓
brewers


SERVING TEMPERATURE
───────────────────

coffee_recipes
    ↓
recipe_temperatures
    ↓
serving_temperatures


RECIPE CONTENT
──────────────

coffee_recipes
    ↓
recipe_ingredients

coffee_recipes
    ↓
recipe_instructions


PROVENANCE
──────────

coffee_recipes
    ↓
recipe_sources
    ↓
sources


INTERNAL DATA QUALITY
─────────────────────

coffee_recipes
    ↓
recipe_verification


AUTHENTICATION & PERSONALIZATION
────────────────────────────────

Supabase auth.users
    ├── user_taste_profiles
    ├── favorites ─────────────→ coffee_recipes
    └── recipe_interactions ───→ coffee_recipes
```

---

# 81. Schema Summary

The database is intentionally relational where relationships matter and intentionally simple where further normalization would not currently improve the product.

It normalizes:

```text
geography
recipe type
brewers
serving temperatures
sources
user favorites
```

It keeps recipe-specific content simple:

```text
names
cultural context
ingredients
instructions
```

It solves known JSON inconsistencies such as:

```text
string vs array brewer values

string vs array temperature values

repeated geographical text

empty strings representing missing values

nested alternate measurements

ordered arrays without explicit database position
```

without changing the supported meaning of the curated dataset.

The resulting database provides the relational foundation for:

```text
coffee discovery
recipe detail
coffee-name search
geographical exploration
favorites
AI grounding
```

while remaining appropriately scoped for the Brewcipe MVP.
