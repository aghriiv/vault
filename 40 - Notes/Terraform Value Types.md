---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Terraform Value Types

> [!summary] In one sentence
> Every Terraform value has a type - primitives (string, number, bool), the
> special null, collections (list, map, set), or structural types (object,
> tuple) - and type constraints on variables enforce which shapes are allowed.

## What it is
A type constraint describes what kind of value is acceptable. The set of types
is: **String, Number, Boolean, List, Object, Map, Set, Tuple, or the special
Null type.** They fall into three families:

- **Primitive types** - simple types not built from others:
  - `string`: a sequence of Unicode characters, e.g. `"hello"`.
  - `number`: whole numbers like `15` and fractions like `6.283185`.
  - `bool`: `true` or `false`, usable in conditional logic.
  Terraform auto-converts between primitives when needed (e.g. `15` <-> `"15"`,
  `true` <-> `"true"`).
- **`null`** - a special value representing "absent / unset".
- **Collection types** - many values of *one* element type:
  - `list(...)`: ordered sequence indexed from 0.
  - `map(...)`: values keyed by string labels.
  - `set(...)`: unique, unordered values with no index.
- **Structural types** - group values of *potentially different* types via a schema:
  - `object({...})`: named attributes, each with its own type.
  - `tuple([...])`: a fixed-length ordered sequence where each position has its
    own type.

## How it works

Primitives and simple collections:

```hcl
variable "booleans_only" {
  type    = bool
  default = true
}

variable "list_of_strings" {
  type    = list(string)
  default = ["list", "of", "strings"]
}
```

Structural types carry a schema. A tuple fixes the type at each position:

```hcl
variable "example_tuple" {
  type    = tuple([string, string, number])
  default = ["alpha", "bravo", 42]
}
```

An object names each attribute; keys may have different types, and a value must
contain all specified keys:

```hcl
variable "my_object" {
  type = object({
    name    = string,
    enabled = bool
  })
  default = {
    name    = "default"
    enabled = false
  }
}
```

Object attributes can be marked `optional`, optionally with a default:

```hcl
variable "optional_keys" {
  type = object({
    alpha   = string,
    bravo   = optional(string)
    charlie = optional(string, "default_string")
  })
}
```

Because structural types nest, you can build arbitrarily complex data
structures - an object whose key is another object whose key is another object,
mixing in tuples and other complex types along the way:

```hcl
variable "nested_object" {
  type = object({
    key = object({
      subkey = object({
        nested_string = string
        nested_tuple  = tuple([string, string, string])
      })
    })
  })
  default = {
    key = {
      subkey = {
        nested_string = "hello world",
        nested_tuple  = ["one", "two", "three"]
      }
    }
  }
}
```

## Why it matters / tradeoffs
Type constraints are documentation *and* validation: they reject bad inputs
before a plan runs and make a module's contract explicit. Note the key
distinction between families: a **collection** (list/map/set) holds many values
of the *same* type, while a **structural** type (object/tuple) holds a fixed
schema of *possibly different* types. During type conversion, an object value
with extra keys beyond the schema keeps matching, but the extra attributes are
discarded.

## Connections
- Declared as the `type` of a [[Terraform Input Variables|Terraform input variable]]
- Enforced further by [[Terraform Variable Validation]]
- Also the types carried by [[Terraform Output Values]] and [[Terraform Local Values]]
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "Type Constraints" (Primitive Types, Complex Types, Collection Types, Structural Types). https://developer.hashicorp.com/terraform/language/expressions/type-constraints (accessed 2026-09-15)
