---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Terraform Module

> [!summary] In one sentence
> A module is a self-contained, reusable collection of resources, data sources,
> and supporting assets that Terraform manages together as one unit.

## What it is
At its core a module is a collection of data sources, resources, and any assets
(configuration files, templates) bundled together into a reusable component.
Think of modules as reusable libraries that can be packaged up and distributed
for reuse. HashiCorp's own definition is deliberately narrow: "A module is a
collection of resources that Terraform manages together."

Concretely, a module is just a directory containing one or more `.tf` files.
There is nothing special about the files themselves - grouping `.tf` files in a
directory *is* what makes a module. A module typically consists of several
Terraform files, all in the same directory.

## How it works
You do not "run" most modules directly. Instead one module **calls** another
using a `module` block, passing values in and reading values out:

```hcl
module "web_server" {
  source        = "./modules/web-server"   # where to get the module
  instance_type = "t3.micro"               # an input variable
  subnet_id     = var.subnet_id
}
```

The relationship is a hierarchy:
- The configuration in a workspace's root directory is the [[Root Module]].
- Any module a `module` block pulls in is a **child module**.
- When you apply, the root module calls the child, and Terraform adds the
  child's resources to your workspace and manages them as part of the
  configuration. A child module can itself call further nested child modules.

Communication across that boundary uses three constructs:
- [[Terraform Input Variables]] are the parameters the caller passes *in*.
- [[Terraform Output Values]] are the results the module exposes back *out*
  (readable as `module.<label>.<output>`).
- [[Terraform Local Values]] are private intermediate values used *inside* the
  module only.

## Why it matters / tradeoffs
Modularizing and sharing configurations lets you standardize how you provision
infrastructure and provision resources quickly and predictably. When you
repeatedly provision collections of resources with similar configuration (for
example the networking for every new dev environment), you should codify them
in a reusable module instead of copy-pasting resource blocks.

A module can play one of three roles depending on where it comes from:
- [[Root Module]] - the entry point Terraform starts from.
- [[Shared Module]] - pulled from a registry or Git repository for reuse.
- [[Submodule]] - distributed as part of a larger parent module.

## Connections
- Plays the role of [[Root Module]], [[Shared Module]], or [[Submodule]]
- Called using [[Terraform Module Meta-Arguments]] (`source`, `version`, `providers`)
- Parameterized by [[Terraform Input Variables]] and returns [[Terraform Output Values]]
- Uses [[Terraform Local Values]] for internal, module-scoped expressions
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "Modules overview" (Introduction, Hierarchy). https://developer.hashicorp.com/terraform/language/modules (accessed 2026-09-15)
- HashiCorp. "module block reference" (Introduction). https://developer.hashicorp.com/terraform/language/modules/syntax (accessed 2026-09-15)
