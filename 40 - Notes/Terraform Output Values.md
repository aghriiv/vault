---
tags: [topic/terraform, topic/iac, concept]
created: 2026-09-15
---

# Terraform Output Values

> [!summary] In one sentence
> Output values are a module's return values - the data it exposes to its
> caller (or to the CLI), read from a parent as `module.<label>.<output>`.

## What it is
An `output` block declares a value a module makes available to whatever called
it. If [[Terraform Input Variables]] are a module's parameters, outputs are its
return values. They are how a child module hands results back up to its parent,
and how the root module surfaces useful data on the command line after an apply.

```hcl
output "load_balanced_aws_instance" {
  description = "The entire instance resource."
  value       = aws_instance.hello_world
  depends_on = [
    aws_lb_target_group_attachment.instance_attachement
  ]
}
```

An `output` block supports:
- `value` (required) - the expression to expose.
- `description` - documentation for the output.
- `sensitive` - suppress the value in CLI output.
- `depends_on` - explicit dependencies, as in the example above, for the rare
  case where Terraform cannot infer ordering automatically.

## How it works
When a child module exposes outputs, the calling module reads them with
`module.<label>.<output>` syntax, where `<label>` is the local name on the
`module` block:

```hcl
module "web" {
  source = "./modules/web-server"
}

resource "aws_route53_record" "app" {
  # read the child module's output
  records = [module.web.load_balanced_aws_instance.public_ip]
}
```

In the root module, output values are printed after `terraform apply` and can be
queried with `terraform output`. Outputs are also the only way values cross the
module boundary outward - internal [[Terraform Local Values]] are *not* visible
to a caller unless surfaced through an output.

## Why it matters / tradeoffs
Outputs define a module's public contract on the return side: they let you hide
internal resource wiring while still exposing exactly the handful of values
consumers need (an instance's IP, a bucket's ARN, a database endpoint). Mark
anything secret as `sensitive` so it does not leak into CLI logs. Keep outputs
minimal and well-described - each one is a promise other configurations may
depend on.

## Connections
- The output side of a [[Terraform Module]]; complements [[Terraform Input Variables]]
- Read across the boundary set up by [[Terraform Module Meta-Arguments]] (`module.<label>.<output>`)
- Surfaces values that may originate as [[Terraform Local Values]]
- Carries a value of some [[Terraform Value Types|value type]]
- Part of [[Terraform Modules (MOC)]]

## Sources
- HashiCorp. "Use outputs to expose module data." https://developer.hashicorp.com/terraform/language/values/outputs (accessed 2026-09-15)
- HashiCorp. "module block reference" (module.<label>.<output> syntax). https://developer.hashicorp.com/terraform/language/modules/syntax (accessed 2026-09-15)
