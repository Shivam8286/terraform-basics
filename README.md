# Terraform Basics: Getting Started Guide

Welcome to the Terraform Basics repository! This guide will walk you through the essential steps to verify your Terraform installation and deploy your first resource—a Google Cloud VM instance—using Terraform.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Task 1: Verify Terraform Installation](#task-1-verify-terraform-installation)
3. [Task 2: Build and Deploy Infrastructure](#task-2-build-and-deploy-infrastructure)
    - [a. Create a Terraform Configuration](#a-create-a-terraform-configuration)
    - [b. Initialize Terraform](#b-initialize-terraform)
    - [c. Plan Infrastructure Changes](#c-plan-infrastructure-changes)
    - [d. Apply Infrastructure Changes](#d-apply-infrastructure-changes)
    - [e. Inspect Terraform State](#e-inspect-terraform-state)
4. [Cleanup](#cleanup)
5. [References](#references)

---

## Prerequisites

- Access to [Google Cloud Shell](https://shell.cloud.google.com/) (Terraform comes pre-installed).
- Sufficient permissions to create resources in Google Cloud Platform (GCP).

---

## Task 1: Verify Terraform Installation

Open a new Cloud Shell tab and verify that Terraform is available by running:

```sh
terraform
```

You should see the Terraform help output, including available commands such as `apply`, `plan`, `destroy`, and more.

---

## Task 2: Build and Deploy Infrastructure

### a. Create a Terraform Configuration

In Cloud Shell, create a new configuration file:

```sh
touch instance.tf
```

Open the file in the Cloud Shell Editor and add the following configuration. Replace the `project` and `zone` values with your actual GCP project ID and desired zone.

```hcl
resource "google_compute_instance" "terraform" {
  project      = "<YOUR_PROJECT_ID>"
  name         = "terraform"
  machine_type = "e2-medium"
  zone         = "<YOUR_ZONE>"

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
<img width="1877" height="774" alt="Image" src="https://github.com/user-attachments/assets/3445e28c-3f6e-4478-85f7-85aff7993a3d" />

**Note:**  
- The `resource` block defines the GCP VM instance to be created.
- Ensure there are no other `.tf` files in your directory, as Terraform loads all configuration files.

List directory contents to verify:

```sh
ls
```

---

### b. Initialize Terraform

Run the following command to initialize Terraform and download the necessary provider plugins:

```sh
terraform init
```
<img width="924" height="443" alt="Image" src="https://github.com/user-attachments/assets/b77332ac-cba4-4b36-be24-66a79e08f052" />
You should see output indicating that the Google provider has been installed.

---

### c. Plan Infrastructure Changes

Generate an execution plan to see what Terraform will do:

```sh
terraform plan
```


<img width="1414" height="596" alt="Image" src="https://github.com/user-attachments/assets/6f72ce0b-0868-45ac-aaf4-b6bbb787373c" />
<img width="1868" height="794" alt="Image" src="https://github.com/user-attachments/assets/844c0516-3c70-4190-a962-d501e7fccca4" />
This command will show the actions Terraform will take based on your configuration.

*Tip: Use the optional `-out` flag to save the plan for later use with `terraform apply`.*

---

### d. Apply Infrastructure Changes

Apply your configuration to create the VM instance:

```sh
terraform apply
```
<img width="1459" height="310" alt="Image" src="https://github.com/user-attachments/assets/cce448e3-9be1-41ac-b91b-41ef3929676b" />
Terraform will show the execution plan and prompt you for approval. Type `yes` to proceed.

Terraform will now provision your VM instance. This may take a few minutes.

---

### e. Inspect Terraform State

Terraform maintains a `terraform.tfstate` file that tracks resources it manages. To view the current state:

```sh
terraform show
```

You’ll see detailed information about the created VM instance, including IDs, resource attributes, and links.

---

<img width="1470" height="624" alt="Image" src="https://github.com/user-attachments/assets/73ba4146-0271-462a-ae5c-b99538344239" />

## Cleanup

To delete the resources you created, use:

```sh
terraform destroy
```

Confirm when prompted to clean up all managed resources.

---

## References

- [Terraform Documentation](https://www.terraform.io/docs/index.html)
- [Google Cloud Terraform Provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
- [Google Cloud Shell](https://cloud.google.com/shell/docs/)

---
Congratulations! You’ve deployed your first VM instance using Terraform. Continue exploring to manage more complex infrastructure with code.
