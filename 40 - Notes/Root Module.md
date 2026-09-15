---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Root Module

> [!summary] In one sentence
> The root module is the module Terraform starts from - the configuration in a
> workspace's root directory - and it is the only place you can configure
> providers.

## What it is
Every Terraform project starts with a root module. It is the configuration in
the root directory that Terraform begins executing from. Importantly, "root"
does not refer to *where* the module sits in your repository's folder structure;
it is simply the module Terraform starts from for a given run. The same
directory of `.tf` files can be a root module in one context and a called child
module in another.

Root modules do two jobs:
1. They configure providers (see below).
2. They call any other modules that are needed.

## How it works
When you run `terraform init` inside a root module, Terraform creates a
**workspace** for it. From that point the root module is the entry point: when
you `apply`, the root module calls its child modules, and Terraform pulls all
their resources into the workspace and manages them together.

The root module is special in one crucial way: it is the *only* place where you
can configure providers using the `provider` block.

```hcl
# Only valid in a root module
provider "aws" {
  region = "eu-central-1"
}

module "network" {
  source = "./modules/network"   # a child module call
}
```

Child modules do not configure their own providers; they inherit provider
configurations, or receive specific aliases explicitly via the `providers`
meta-argument (see [[Terraform Module Meta-Arguments]]).

## Why it matters / tradeoffs
Because provider configuration is root-only, shared and reusable modules should
*not* declare provider blocks - doing so makes them hard to reuse and can cause
problems when the module is called multiple times. Keep provider setup in the
root module and pass what child modules need down to them.

## Connections
- A role played by a [[Terraform Module]]
- Contrast with [[Shared Module]] and [[Submodule]]
- Turned into a workspace by `terraform init` (see [[Terraform Workspace]])
- Only place you can use the `provider` block (see [[Terraform Provider]])
- Calls child modules using [[Terraform Module Meta-Arguments]]
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "Modules overview" (Hierarchy: "Terraform refers to this configuration as the root module"). https://developer.hashicorp.com/terraform/language/modules (accessed 2026-09-15)
