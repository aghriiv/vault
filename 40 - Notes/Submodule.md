---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Submodule

> [!summary] In one sentence
> A submodule is a module distributed *inside* another module - tightly coupled
> to its parent, which is why it is not published on its own.

## What it is
Submodules are modules that are distributed as part of another module. They
might live inside a [[Root Module]] or inside a [[Shared Module]]. In general
they tend to be coupled to their parent module, which is exactly why they are
not distributed separately - they only make sense in the context of the parent.

## How it works
A package (a module stored in a version-control repository or archive) can
contain nested modules in subdirectories. When you call a module whose source is
a package, Terraform extracts the *entire* package to local disk but reads only
the requested module directory. Because the whole package is present locally, a
module in a subdirectory can reference a sibling submodule in the same package
using an ordinary local path (`./` or `../`).

To point a `source` at a subdirectory within a package, add `//` to mark where
the sub-path begins:

```hcl
module "consul_cluster" {
  # everything after // is a submodule path inside the package
  source = "git::https://example.com/network.git//modules/consul-cluster"
}
```

By convention, reusable submodules that ship with a parent module are placed in a
`modules/` directory, while any example usage lives under `examples/`.

## Why it matters / tradeoffs
Submodules let a large module be factored into smaller internal pieces without
polluting a registry with fragments that have no standalone meaning. The
tradeoff is coupling: because a submodule assumes its parent's context, you
should not treat it as an independently versioned, reusable unit the way you
would a [[Shared Module]]. If a piece is genuinely reusable on its own, promote
it to a standalone shared module instead of leaving it as a submodule.

## Connections
- A role played by a [[Terraform Module]]
- Distributed inside a [[Root Module]] or [[Shared Module]] (its parent)
- Contrast with [[Shared Module]], which *is* distributed separately
- Addressed via the `source` subdirectory (`//`) syntax in [[Terraform Module Meta-Arguments]]
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "module block reference" (source, sub-directories within a package, `//` syntax). https://developer.hashicorp.com/terraform/language/modules/syntax (accessed 2026-09-15)
