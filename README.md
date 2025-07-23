## Terraform Errors that I've faced and how I resolved

Terraform is a powerful tool for infrastructure as code, but like any tool, it comes with its own set of challenges. Below is a list of common errors DevOps engineers encounter while using Terraform, along with potential causes and solutions.

---

1. When executing Terraform plan for Easyshop project I got this error
    
    **Error: Unsupported argument**
    
    `│ Error: Unsupported argument
    │
    │   on .terraform/modules/eks/main.tf line 420, in resource "aws_eks_addon" "before_compute":
    │  420:   resolve_conflicts        = try(each.value.resolve_conflicts, "OVERWRITE")
    │
    │ An argument named "resolve_conflicts" is not expected here.`
    
    **Fix:**
    
    - modify the terraform eks module version to 20.37.2 / latest as below
    `module "eks" {
    source  = "terraform-aws-modules/eks/aws"
    version = "20.37.2"
    }`
    - Save and execute "terraform init -upgrade"
