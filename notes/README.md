To split your `main.tf` into a more modular and maintainable Terraform project, you can organize it into multiple files:

---

### ✅ Folder Structure

```
.
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars (optional)
```

---

### ✅ `main.tf` – Main Configuration

```hcl
provider "aws" {
  region = var.aws_region
}

resource "aws_instance" "example" {
  ami           = var.ami_id
  instance_type = var.instance_type
  subnet_id     = var.subnet_id
  key_name      = var.key_name
}
```

---

### ✅ `variables.tf` – Input Variables

```hcl
variable "aws_region" {
  description = "AWS region to deploy resources in"
  type        = string
  default     = "us-east-1"
}

variable "ami_id" {
  description = "AMI ID for the instance"
  type        = string
}

variable "instance_type" {
  description = "Instance type"
  type        = string
  default     = "t2.micro"
}

variable "subnet_id" {
  description = "Subnet ID"
  type        = string
}

variable "key_name" {
  description = "SSH key name"
  type        = string
}
```

---

### ✅ `terraform.tfvars` – Variable Values

```hcl
ami_id        = "ami-020cba7c55df1f615"
subnet_id     = "subnet-0ffa1a1f762804b4d"
key_name      = "nodes"
```

> This file is optional. You can also provide variables via `-var` in CLI or environment variables.

---

### ✅ `outputs.tf` – Outputs

```hcl
output "instance_id" {
  value = aws_instance.example.id
}

output "instance_public_ip" {
  value = aws_instance.example.public_ip
}
```

---

### ✅ How to Initialize & Apply

```bash
terraform init
terraform plan
terraform apply
```

---

Example: Module Structure
css
Copy
Edit
project/
├── main.tf
├── variables.tf
├── outputs.tf
└── modules/
    └── ec2/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
