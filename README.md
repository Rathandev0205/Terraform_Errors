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

2. While trying to launch an EKS Node Group with instance type of t2.medium that is not eligible for AWS Free Tier.

`Error: creating EC2 Instance: operation error EC2: RunInstances, https response error StatusCode: 400, RequestID: 6219fff2-d5c8-4695-9f93-8352ef9104db, api error InvalidParameterCombination: The specified instance type is not eligible for Free Tier. For a list of Free Tier instance types, run 'describe-instance-types' with the filter 'free-tier-eligible=true'.`

**Fix:**

- Modified the Node group instance type from t2.medium to c7i-flex.large **(which is most similar to t2.medium).** AWS’s recent Free Tier changes that took effect around **July 15, 2025**, the **c7i‑flex.large** instance type included under AWS Free Tier, which is not the case earlier.
