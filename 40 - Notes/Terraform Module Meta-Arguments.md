---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Terraform Module Meta-Arguments

> [!summary] In one sentence
> `module` blocks accept a few special meta-arguments that other block types do
> not - most importantly `source` (where to get the module), `version` (which
> release to allow), and `providers` (which provider aliases to pass down).

## What it is
When you call a module you write a `module` block. Beyond the module's own input
variables, that block understands meta-arguments that Terraform interprets
itself rather than passing to the module. The three that are unique to modules
and central to reuse are `source`, `version`, and `providers`. (Modules also
accept the general meta-arguments `count`, `for_each`, and `depends_on`.)

## How it works

### `source` (required)
`source` tells Terraform where to get the module from and is the one required
argument. It can be a URL pointing to a module in a hosted registry, or a path
pointing to a module on the local filesystem.

```hcl
module "web" {
  source = "./modules/web-server"   # local path
}
```

Rules worth remembering:
- The value must be a literal string - `source` does not accept arbitrary
  expressions or template sequences.
- You must run `terraform init` after changing `source` so Terraform fetches the
  updated code.
- The same `source` can appear in multiple `module` blocks as long as each block
  has a unique label, letting you stamp out the same module with different
  inputs.

### `version`
`version` tells Terraform what the allowed version range is. It is used when the
`source` is a registry and lets the developer lock into a specific version range
for a module. This way developers control when their modules get updated, so new
changes do not silently break their expectations.

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "~> 5.0"   # allow 5.x, but not 6.0
}
```

`version` is only available for modules sourced from a registry - it is
meaningless (and unavailable) for local-path or direct-Git sources, where you
pin versions with a `ref` in the source URL instead.

### `providers`
`providers` lets the developer specify which provider aliases from the outer
(calling) module get passed to the called module. It maps a provider name as the
child module expects it to a provider configuration from the parent:

```hcl
module "replica" {
  source = "./modules/db"
  providers = {
    aws = aws.us_east_1   # pass the parent's aliased provider to the child
  }
}
```

This matters because only a [[Root Module]] can configure providers with a
`provider` block; `providers` is how the root hands specific configurations down
to child modules.

## Why it matters / tradeoffs
These three arguments are what turn a directory of `.tf` files into a
distributable, versioned, reusable unit. `source` makes a module locatable,
`version` makes upgrades intentional instead of accidental, and `providers`
keeps provider configuration in the root while still letting children use the
right accounts/regions.

## Connections
- Used to call a [[Terraform Module]]
- `version` is what makes a [[Shared Module]] safe to consume over time
- `source` `//` subdirectory syntax is how you reach a [[Submodule]]
- `providers` bridges provider config from the [[Root Module]] to children (see [[Terraform Provider]])
- Distinct from [[Terraform Input Variables]], which are the module's own parameters
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "module block reference" (source, version, providers). https://developer.hashicorp.com/terraform/language/modules/syntax (accessed 2026-09-15)
