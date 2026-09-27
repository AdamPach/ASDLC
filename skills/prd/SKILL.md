---
name: prd
description: "Test"
---

# Goal

Your goal is to create or update a structured document called **PRD - Product Reqirement Documentation**, based on the provided input.

# Process

This section describes exactly how you work and how you must process the user input. You can work in two modes. First is create a new PRD document from description. Second is to update existing PRD based on new information. In each step you must differentiate between them and do only what is required for current mode.

## Input

### New (creating) PRD

User must provide you a detiled description of the product. It can be long unstructered text which descibes the product or transription of the meeting where the product was desctibed. Any other types of input you must not accept.

Input must cover this information, or at least you must be able to understand them.
- Basic description and purpose of the product
- Required functionalities what product must me able to do
- Description of the Interface, how should be used and how it should look like
- Scope of this version and what is not covered by this version or unresolved questions 

When user does not provide this description you must ask him to provide it. When he cannot provide a description which fits all your needs **you must end here**.

### Existing (updating) PRD

User must provide new details about the product. The input must be talking about the exiting PRD document otherwise you should not accept it and stop. For example when PRD is about cinema reservation system and user is talking about pizza order system stop there and tell to the user that this is wrong project.

Possible input can be for example this
- New requirements, new features which were not discussed yet
- Clarification or specification for unclear parts
- Providing more context or more info about the product.

## PRD Structure and Creation Guiderails

This subsection describes how the output PRD document must look like and how you must work and process the given input. Below you can find detailed description for every section of the PRD.

### Short Product Description

**Purpose:** Provide a context what product do, what problem solves, why exists and who will use it.

**What should be covered**
- What is the product about
- Who will use it and which main roles works with him
- What problem solves and how this help
- Potentional conditions which infulence whole product.

**Output format:** It should to 1-3 short paragraphs about the product. It must be a general description not a description of a specific feature. 

## Output

`docs/product/...`

## Language in the PRD document