# Brewcipe — Product Idea

## Overview

Brewcipe is a personalized coffee discovery web app that recommends what to brew based on the user's preferences, equipment, saved recipes and brewing history.

This web app combines structured coffee recipe data, geographical discovery, cultural context, and personalized recommendations to make coffee exploration more accessible and engaging.

Brewcipe is designed both as a consumer-facing coffee discovery product and as a portfolio project demonstrating product thinking, UX design, data modelling, system design, and full-stack application development.

---

## Problem

Coffee recipes and brewing traditions are widely distributed across different websites, regions, languages, and formats.

Users interested in exploring coffee beyond familiar drinks often encounter several challenges:

* Recipe information is fragmented across many sources.
* Naming conventions differ between countries and cultures.
* Brewing instructions and ingredient measurements are presented inconsistently.
* Cultural and geographical context is often separated from the recipe itself.
* Discovering similar coffees from other regions requires significant manual research.

There is no single structured experience for discovering coffee recipes while also understanding where they come from, how they are prepared, and how they relate to other coffee traditions.

---

## Product Vision

Brewcipe aims to become a structured discovery layer for global coffee culture.

Instead of presenting coffee recipes as isolated instructions, Brewcipe connects recipes with:

* countries and regions
* local and translated names
* brewing methods
* ingredients
* preparation instructions
* cultural context
* source attribution
* related coffee traditions

The goal is to allow users to move naturally between recipes, brewing methods, and geographical discovery.

---

## Target Users

Brewcipe is designed for:

### Coffee Enthusiasts

Users who enjoy discovering new coffee drinks, recipes, and brewing techniques.

### Home Brewers

Users looking for structured preparation instructions that can be followed at home.

### Coffee Explorers

Users interested in discovering how coffee is prepared across different countries and cultures.

### Casual Coffee Drinkers

Users who may not know brewing terminology but want an approachable way to explore coffee.

---

## Core Product Experience

### Global Coffee Discovery

Users can browse coffee recipes from different countries and regions.

Geographical information helps users understand where a coffee preparation originates or is commonly associated with.

### Structured Recipe Pages

Each coffee recipe is represented using a consistent data model that can include:

* English name
* native name
* transliteration
* country and region
* recipe type
* brewing method or brewer
* serving information
* temperature
* ingredients
* preparation instructions
* cultural context
* source attribution

This allows recipes from very different sources and traditions to be presented through a consistent interface.

### Search

Users can discover recipes based on attributes such as:

* coffee name
* country
* region
* brewing method
* recipe type

### User Accounts

Users can create and access Brewcipe accounts using supported authentication methods.

For the MVP, authentication may include:

* email and password
* Google Sign-In

Authentication is provided through Supabase Auth and enables user-specific features such as saved favorites.

### Personal Coffee Discovery

Brewcipe 2.0 extends saved coffees and coffee history into a personal discovery loop.

The product uses a Taste Profile Mechanic rather than treating personalization as a static settings form:

```text
Taste Model
     ↓
Saved Coffees + Coffee History + User Signals
     ↓
Recommendation Engine
     ↓
Personalized Home + Sommelier
     ↓
User interaction
     ↓
Taste model evolves
```

The taste model begins with explicit user preferences and discovery constraints. As users save, try, or skip coffees, Brewcipe can derive additional signals from those interactions and improve future recommendations.

The recommendation engine remains deterministic and grounded in Brewcipe's structured recipe data. The AI Coffee Sommelier sits above that system as a conversational interface that can use the user's current personalization context.

The detailed mechanic is defined in `taste-profile-mechanic-v1.md`.



### Favorites

Authenticated users can save coffee recipes to their personal collection for future reference.

### AI Coffee Sommelier

The AI Coffee Sommelier provides conversational coffee discovery.

Users can describe their preferences or ask questions such as:

* “I want something sweet and iced.”
* “What coffee should I try from Vietnam?”
* “I like strong coffee but don't own an espresso machine.”

The assistant uses Brewcipe's structured coffee data as context when generating recommendations.

---

## Coffee Data

Brewcipe uses a privately maintained, structured coffee recipe dataset stored in the application's Supabase database.

The initial dataset was manually researched and curated from publicly available coffee recipe sources.

Because recipe information varies significantly between sources, records were normalized into Brewcipe's canonical data model before being prepared for application use.

The data model supports source attribution and verification metadata so that Brewcipe can distinguish between source-provided information and values that required normalization or interpretation during curation.

The complete production dataset and private data-preparation artifacts are not included in the public Brewcipe repository.

The public repository instead documents the application's data model, database structure, architecture, and implementation.

---

## Product Principles

### Structured, Not Fragmented

Coffee information should follow a consistent model even when the original sources use different formats.

### Culture With Context

Coffee should not be reduced to ingredients and instructions.

Where relevant, Brewcipe should preserve geographical, linguistic, and cultural information associated with a recipe.

### Traceable Information

Coffee records should maintain source attribution so that information can be traced back to its reference material.

### Accessible Exploration

Users should not need specialist coffee knowledge to explore Brewcipe.

The interface should make coffee terminology and brewing information understandable to casual users while remaining useful to enthusiasts.

### AI as an Interface, Not the Database

The AI Coffee Sommelier should use Brewcipe's structured data as grounding context rather than act as the authoritative source of coffee information.

---

## Portfolio Purpose

Brewcipe is also designed as a portfolio project demonstrating the end-to-end development of a digital product.

The project demonstrates:

* product discovery and requirements definition
* information architecture
* UX and interface design
* structured data modelling
* relational database design
* API design
* frontend and backend development
* authentication and user-specific features
* AI-assisted product functionality
* technical documentation
* architectural decision-making

The public repository focuses on the product and its technical implementation while keeping the production coffee dataset and private data-preparation materials outside the repository.

---

## Long-Term Direction

Future versions of Brewcipe may expand into:

* more advanced coffee discovery and filtering
* personalized recommendation signals
* richer geographical exploration
* community contributions
* recipe comparison
* brewing equipment recommendations
* multilingual content
* improved AI-assisted discovery
* administrative data-management tools
* assisted data enrichment and validation workflows

Automation may support future data-management workflows where it improves efficiency without compromising data quality, provenance, or reviewability.
