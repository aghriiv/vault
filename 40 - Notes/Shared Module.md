---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Shared Module

> [!summary] In one sentence
> A shared module is one you pull down from a Git repository or a Terraform
> registry rather than writing inline - either a public third-party module or
> part of your team's private registry.

## What it is
Shared modules are modules that are pulled down from a Git repository or a
Terraform Module Registry. They come in two flavours:
- **Public modules** made by third parties (HashiCorp, partners, the community),
  hosted on the public Terraform Registry and free to use.
- **Private modules** that are part of a private registry of modules developed
  and maintained by your own team. HCP Terraform and Terraform Enterprise
  include a private module registry for sharing modules internally.

## How it works
You consume a shared module the same way you call any child module - with a
`module` block - but the `source` points at a remote location and, for registry
modules, you also pin a `version`:

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"   # registry address
  version = "~> 5.0"                            # only valid for registry sources

  name = "my-vpc"
  cidr = "10.0.0.0/16"
}
```

Terraform can load shared modules from several source types, including the local
file system, a Terraform registry, and VCS repositories such as GitHub. When the
source is a registry, Terraform can download the module automatically once you
specify the appropriate `source` and `version`. You must run `terraform init`
after adding or changing a module source so Terraform fetches the code.

The lifecycle behind shared modules has three phases: **develop** (collect
resources into a well-structured, documented module), **distribute** (publish to
a public or private registry, or make available via S3/GitHub), and **provision**
(consumers call it with a `module` block).

## Why it matters / tradeoffs
Sharing modules is how teams standardize infrastructure: instead of each project
reinventing a VPC or a database, everyone calls the same vetted module. Pinning
`version` is essential here - it lets you control exactly when a module updates
so a new release does not silently break your configuration (see
[[Terraform Module Meta-Arguments]]).

## Connections
- A role played by a [[Terraform Module]]
- Contrast with [[Root Module]] (local entry point) and [[Submodule]] (bundled inside a parent)
- Located and versioned via [[Terraform Module Meta-Arguments]] (`source`, `version`)
- Distributed through the [[Terraform Registry]]
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "Modules overview" (Sources, Workflows). https://developer.hashicorp.com/terraform/language/modules (accessed 2026-09-15)
- HashiCorp. "module block reference" (source, version). https://developer.hashicorp.com/terraform/language/modules/syntax (accessed 2026-09-15)
