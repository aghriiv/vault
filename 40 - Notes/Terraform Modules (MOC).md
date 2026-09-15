---
tags: [moc, topic/terraform, topic/iac]
created: 2026-09-15
---

# Terraform Modules - Map of Content

> [!abstract] Read this like a chapter
> A Terraform *module* is a reusable bundle of resources, data sources, and
> supporting files. Everything below builds from that one idea: what a module
> is, the three roles a module can play (root, shared, submodule), how you wire
> one module to another with meta-arguments, and the four building blocks you
> use *inside* a module to make it flexible - input variables, value types,
> outputs, and locals. Start at [[Terraform Module]] and walk outward.

## Foundations
- [[Terraform Module]] - what a module actually is: a packaged, reusable collection of resources
- [[Root Module]] - the entry point Terraform starts from; becomes the workspace
- [[Shared Module]] - a module pulled from a registry or Git for reuse
- [[Submodule]] - a module distributed *inside* another module

## Calling and wiring modules
- [[Terraform Module Meta-Arguments]] - `source`, `version`, `providers` - the arguments unique to `module` blocks

## Building blocks inside a module
- [[Terraform Input Variables]] - the parameters a module accepts (`var.<name>`)
- [[Terraform Value Types]] - string, number, bool, list, map, set, object, tuple, null
- [[Terraform Variable Validation]] - enforcing rules on input values
- [[Terraform Output Values]] - the return values a module exposes
- [[Terraform Local Values]] - named intermediate expressions, module-scoped

## Open threads / to expand
- [[Terraform Provider]] - the `provider` block (only configurable in the root module)
- [[Terraform Workspace]] - what `terraform init` creates from a root module
- [[Terraform Registry]] - public and private module distribution
- [[Terraform State]]

## Sources
- HashiCorp. "Modules overview." https://developer.hashicorp.com/terraform/language/modules (accessed 2026-09-15)
- HashiCorp. "module block reference." https://developer.hashicorp.com/terraform/language/modules/syntax (accessed 2026-09-15)
