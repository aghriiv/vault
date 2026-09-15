---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Terraform Input Variables

> [!summary] In one sentence
> Input variables are the parameters a module accepts - declared with a
> `variable` block, referenced as `var.<name>`, and (unusually) constant for the
> whole run once set.

## What it is
An input variable is a named parameter you declare with a `variable` block so a
module's behavior can change without editing its code. Defining variables gives
the module consumer the flexibility to change values at run time instead of
hardcoding them.

```hcl
variable "ami" {
  type        = string
  description = "The Amazon Machine Image to use when launching the EC2 Instance."
}

variable "subnet_id" {
  type        = string
  description = "The ID of the Subnet to launch the instance into."
}

variable "instance_type" {
  type        = string
  description = "The type of instance to launch."
  default     = "t3.micro"
}
```

A `variable` block commonly carries:
- `type` - the [[Terraform Value Types|value type]] the variable must match.
- `description` - human-readable documentation.
- `default` - a fallback value; if omitted the variable is required.
- `validation` - custom rules on the value (see [[Terraform Variable Validation]]).
- `sensitive` / `ephemeral` - handling for secret values.

## How it works
You reference a variable elsewhere in the configuration with `var.<NAME>`:

```hcl
resource "aws_instance" "web" {
  ami           = var.ami
  instance_type = var.instance_type
  subnet_id     = var.subnet_id
}
```

If a variable has no `default`, Terraform prompts the user (or requires a value
from somewhere) before it will generate a plan. In the root module you can
supply values through several methods with a defined order of precedence:
`-var` / `-var-file` on the CLI and HCP Terraform variables (highest), then
`*.auto.tfvars` files in lexical order, then `terraform.tfvars.json`, then
`terraform.tfvars`, then `TF_VAR_*` environment variables, then the block's
`default` (lowest). Child modules, by contrast, receive their inputs as
arguments from the parent `module` block.

> [!note] Variables are constants
> Terraform variables have a feature that makes them very different from most
> languages: **all Terraform variables are constants**. Their value can only be
> set once during a program, and then it cannot be changed or altered during
> that run. Once you assign a value to a variable, you cannot reassign it within
> the same file.

## Why it matters / tradeoffs
Variables are what make a module reusable rather than a one-off. Hardcoded values
make a module inflexible and hard to reuse; replacing anything that changes
between runs with a variable lets one module serve many environments. Because
variables are constant per run, you cannot use them as mutable accumulators -
for computed intermediate values use [[Terraform Local Values]] instead, and to
return data to the caller use [[Terraform Output Values]].

## Connections
- Declared with `type` from [[Terraform Value Types]]
- Constrained by [[Terraform Variable Validation]]
- The input side of a [[Terraform Module]]; distinct from [[Terraform Module Meta-Arguments]]
- Contrast with [[Terraform Local Values]] (internal) and [[Terraform Output Values]] (outputs)
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "Use variables to customize configurations." https://developer.hashicorp.com/terraform/language/values/variables (accessed 2026-09-15)
