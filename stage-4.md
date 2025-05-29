# ☸️ DevOps Roadmap – Stage 4: Infrastructure as Code with Terraform

> Terraform lets you define cloud infrastructure (VMs, storage, networks, databases, etc.) using code, so it can be versioned, reviewed, and deployed repeatably and safely.

## 🧠 1. What is Terraform?

Terraform is a tool from HashiCorp that uses a declarative language (HCL) to manage infrastructure on:

- AWS
- Google Cloud (GCP)
- Azure
- Kubernetes
- and many more...

It enables Idempotent deployments: You can apply the same configuration many times and get the same result.

## 🔍 2. Key Terraform Concepts

| Concept | Description |
| ------- | ----------- |
| Provider | Plugin to connect Terraform with a cloud (e.g., AWS, GCP) |
| Resource | A piece of infrastructure (e.g., VM, database, bucket) |
| Variable | Inputs that make your configs flexible |
| Output | Return values after deployment |
| State File | Tracks real-world infrastructure state |
| Module | Reusable group of Terraform files |

## ⚙️ 3. Installing Terraform

[🧭 Terraform Installation Guide](https://developer.hashicorp.com/terraform/downloads)

```bash
# On Ubuntu
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt install terraform
```

## 📁 4. Your First Terraform Project (GCP Example)

You’ll need a GCP service account with a JSON key and the project ID.

**📄 main.tf:**

```tf
provider "google" {
  project = var.project_id
  region  = var.region
  credentials = file(var.credentials_file)
}

resource "google_compute_instance" "default" {
  name         = "demo-vm"
  machine_type = "e2-micro"
  zone         = var.zone

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  network_interface {
    network = "default"
    access_config {}
  }
}
```

**📄 variables.tf:**

```txt
variable "project_id" {}
variable "region" { default = "us-central1" }
variable "zone" { default = "us-central1-a" }
variable "credentials_file" {}
```

**📄 terraform.tfvars:**

```hcl
project_id       = "your-gcp-project-id"
zone             = "us-central1-a"
credentials_file = "account-key.json"
```

## 🚀 5. Running Terraform

```bash
terraform init      # Download providers
terraform plan      # Show what will be created
terraform apply     # Apply the configuration
terraform destroy   # Delete the infrastructure
```

## 💡 6. Using Variables & Outputs

```txt
variable "instance_name" {
  default = "my-instance"
}

output "external_ip" {
  value = google_compute_instance.default.network_interface[0].access_config[0].nat_ip
}
```

After applying, run:

```bash
terraform output
```

## 🔐 7. Backend & State Management

Terraform saves your state in `terraform.tfstate`.

You can store it:

- Locally (default)
- In remote backends like:
  - S3 (AWS)
  - GCS (Google)
  - Terraform Cloud

[📘 Terraform State Backends](https://developer.hashicorp.com/terraform/language/settings/backends/configuration)

## 🧰 8. Modules (Reusable Config)

```txt
module "network" {
  source = "./modules/vpc"
  cidr_block = "10.0.0.0/16"
}
```

Organize large projects into:

```css
main.tf
variables.tf
outputs.tf
modules/
  vpc/
    main.tf
    variables.tf
    outputs.tf
```

[📘 Terraform Modules](https://developer.hashicorp.com/terraform/language/modules)

## ✅ 9. Practice Tasks

- [ ] Provision a VM in GCP or AWS using Terraform
- [ ] Create a VPC, subnet, and firewall
- [ ] Output public IP of VM after deployment
- [ ] Destroy everything cleanly
- [ ] Store secrets using environment variables or .tfvars

## 📚 Learning Resources

| Topic | Link |
| ----- | ---- |
| Official Docs | https://developer.hashicorp.com/terraform |
| Terraform GCP Guide | https://registry.terraform.io/providers/hashicorp/google/latest/docs |
| FreeCodeCamp YouTube Guide | [Terraform Full Course – FreeCodeCamp](https://www.youtube.com/watch?v=V4waklkBC38) |
| Terraform Up & Running (Book) | https://www.terraformupandrunning.com/ |
| Hands-on Labs | https://www.kodekloud.com/courses/terraform-for-beginners/ |

## 🧪 Self-Check Questions

- What does terraform plan do?
- How does Terraform handle "drift" (when real infrastructure changes)?
- What happens if your .tfstate file is lost?
- Why is it better to store state remotely?
