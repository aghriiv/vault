---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Terraform Local Values

> [!summary] In one sentence
> Local values are named expressions scoped to a single module - handy for
> naming or reusing a computed value, but invisible outside the module that
> defines them.

## What it is
A local value assigns a name to an expression so you can use that name many
times within a module instead of repeating the expression. Local variables only
exist inside the module where they are defined - they are the module's private
scratch space, unlike [[Terraform Output Values]], which are deliberately
exposed to callers.

## How it works
You declare locals in a `locals` block. A module can have several `locals`
blocks; every value defined in any of them is available throughout the whole
module. Locals can also reference other locals.

```hcl
locals {
  alpha   = 1
  bravo   = "two"
  charlie = false
}

locals {
  delta = ["four", "five"]
  echo = {
    "foxtrot" = "six",
    "golf"    = "seven"
  }
}

locals {
  hotel = local.bravo   # a local can reference another local
}
```

You reference a local elsewhere with `local.<name>` (singular `local`, even
though the block is `locals`):

```hcl
resource "aws_s3_bucket" "example" {
  bucket = "${local.bravo}-bucket"
}
```

Notes on scope and evaluation:
- Every local is available through the whole module regardless of which
  `locals` block declared it.
- Locals can reference variables, resources, data sources, and other locals -
  Terraform figures out the dependency order.
- They are *not* visible to a parent module; to pass a computed value out, wire
  it into an `output`.

## Why it matters / tradeoffs
Locals keep configurations DRY: compute a name, tag map, or CIDR once and reuse
it, so a change happens in one place. They also make intent clearer than
inlining a complex expression repeatedly. The caution is overuse - a local that
is used only once can add indirection without benefit, and because locals are
hidden from callers they are for *internal* computation, not a module's public
interface. Use [[Terraform Input Variables]] for inputs, `local` values for
internal reuse, and [[Terraform Output Values]] for what you expose.

## Connections
- Internal to a single [[Terraform Module]]; contrast with [[Terraform Output Values]] (exposed) and [[Terraform Input Variables]] (inputs)
- Holds a value of some [[Terraform Value Types|value type]]
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "Use locals to reuse expressions." https://developer.hashicorp.com/terraform/language/values/locals (accessed 2026-09-15)
