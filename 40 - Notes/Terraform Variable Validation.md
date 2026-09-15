---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Terraform Variable Validation

> [!summary] In one sentence
> A `validation` block inside a `variable` lets you enforce custom rules on the
> value a consumer supplies, failing early with a clear error message if the
> rule is not met.

## What it is
Type constraints (see [[Terraform Value Types]]) guarantee the *shape* of an
input, but often you need stricter rules - a maximum length, a value from an
allowed set, a matching pattern. A `validation` block, nested inside a
[[Terraform Input Variables|variable]] block, expresses exactly those rules.

## How it works
A `validation` block has two required arguments:
- `condition` - a boolean expression that must be `true` for the value to be
  accepted. It can reference the variable being validated with `var.<name>`.
- `error_message` - the message Terraform shows the user when the condition is
  `false`.

```hcl
variable "description" {
  description = "An optional description to apply to resources."
  type        = string
  default     = ""                     # by default, an empty string
  validation {
    condition     = length(var.description) <= 125
    error_message = "The name can not be longer than 125 characters."
  }
}
```

A common pattern is restricting a value to an allowed set with `contains`:

```hcl
variable "environment" {
  type        = string
  default     = "dev"
  validation {
    condition     = contains(["dev", "staging", "prod"], var.environment)
    error_message = "Environment must be dev, staging, or prod."
  }
}
```

If the `condition` evaluates to `false`, Terraform rejects the value and prints
`error_message` instead of generating a plan. You can attach more than one
`validation` block to a single variable to check independent rules.

## Why it matters / tradeoffs
Validation moves failures to the earliest, cheapest point: the plan is refused
before any resource is touched, and the consumer gets a human-readable reason
rather than a confusing downstream provider error. It also documents a module's
expectations right next to the variable. Keep conditions self-contained (they
should generally reference only the variable under validation) and write
`error_message` from the consumer's point of view, telling them how to fix it.

## Connections
- Lives inside a [[Terraform Input Variables|Terraform input variable]] block
- Complements the `type` constraint from [[Terraform Value Types]]
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "Use variables to customize configurations" (validation block example). https://developer.hashicorp.com/terraform/language/values/variables (accessed 2026-09-15)
