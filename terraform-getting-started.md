# Getting Started with Terraform

Terraform is a tool for defining and provisioning infrastructure as code (IaC). In this guide, you'll learn how to install Terraform and use it to define, provision, and destroy resources.

## Prerequisites

- Experience using a CLI

## Download and Install Terraform
Before getting started, visit [Terraform.io](https://www.terraform.io/downloads.html) to download the latest appropriate version of Terraform for your system. After the file downloads, unzip it to install.

## Terraform Configuration
Now that Terraform is installed, you can start creating infrastructure. The first step is to create a Terraform configuration. Terraform configurations are where you describe your infrastructure resources. For more information on how to write a Terraform configuration, see the [configuration documentation](https://www.terraform.io/docs/configuration/index.html).

We recommend that you create your configuration inside a new directory:

#### CLI commands

Create a new directory called `terraform-demo` and change into it:

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Create a configuration file called `main.tf` inside your new directory:

```shell
$ touch main.tf
```

Open `main.tf` in a text editor and paste in the following block of sample code:

```hcl
provider "docker" {
    host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

This codes defines the infrastructure used for this demo. After pasting, you can save and exit the file.

## Initialize Terraform
Next, from the same directory as your configuration, you can initialize Terraform using the `init` command. This command downloads and installs the providers described in your Terraform configuration. 

#### CLI commands

```shell
$ terraform init
Initializing the backend...

Initializing provider plugins...
- Checking for available provider plugins...
- Downloading plugin for provider "docker" (terraform-providers/docker) 2.7.0...

The following providers do not have any version constraints in configuration, so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking changes, it is recommended to add version = "..." constraints to the corresponding provider blocks in configuration, with the constraint strings suggested below.

* provider.docker: version = "~> 2.7"

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see any changes that are required for your infrastructure. All Terraform commands should now work.
```


## Provision Your Resources
If the `init` command ran without error, you can now provision the resource(s) by running the `apply` command.

#### CLI commands

```shell
$ terraform apply

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # docker_container.nginx will be created
  + resource "docker_container" "nginx" {
      + attach           = false
      + bridge           = (known after apply)
      + command          = (known after apply)
      + container_logs   = (known after apply)
      + entrypoint       = (known after apply)
      + env              = (known after apply)
      + exit_code        = (known after apply)
      + gateway          = (known after apply)
      + hostname         = (known after apply)
      + id               = (known after apply)
      + image            = (known after apply)
      + ip_address       = (known after apply)
      + ip_prefix_length = (known after apply)
      + ipc_mode         = (known after apply)
      + log_driver       = "json-file"
      + logs             = false
      + must_run         = true
      + name             = "training"
      + network_data     = (known after apply)
      + read_only        = false
      + restart          = "no"
      + rm               = false
      + shm_size         = (known after apply)
      + start            = true

      + labels {
          + label = (known after apply)
          + value = (known after apply)
        }

      + ports {
          + external = 80
          + internal = 80
          + ip       = "0.0.0.0"
          + protocol = "tcp"
        }
    }

  # docker_image.nginx will be created
  + resource "docker_image" "nginx" {
      + id     = (known after apply)
      + latest = (known after apply)
      + name   = "nginx:latest"
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: 
```

After entering this command, you'll see output in your CLI similar to the output above. Terraform will prompt you for confirmation. Type `yes` into your CLI and hit the ENTER key to confirm.

After confirmation, this command _may_ take a few minutes to run. Terraform will display a message once the resource is created.

## Destroy the Infrastructure
To stop the resources in your Terraform configuration, run the `destroy` command.

#### CLI commands

```shell
$ terraform destroy
docker_image.nginx: Refreshing state... [id=sha256:e791337790a6181d5ce870b3bb16de1a4d5aa3a916e8fba6907f57eb409934cfnginx:latest]
docker_container.nginx: Refreshing state... [id=9407d83e13e7a5b3ff494c0de8c9e51fce9ad82449f63b27b335b26f1544ecb0]

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # docker_container.nginx will be destroyed
  - resource "docker_container" "nginx" {
      - attach            = false -> null
      - command           = [
          - "nginx",
          - "-g",
          - "daemon off;",
        ] -> null
      - cpu_shares        = 0 -> null
      - dns               = [] -> null
      - dns_opts          = [] -> null
      - dns_search        = [] -> null
      - entrypoint        = [] -> null
      - env               = [
          - "NGINX_VERSION=1.17.10",
          - "NJS_VERSION=0.3.9",
          - "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
          - "PKG_RELEASE=1~buster",
        ] -> null
      - gateway           = "172.17.0.1" -> null
      - group_add         = [] -> null
      - hostname          = "9407d83e13e7" -> null
      - id                = "9407d83e13e7a5b3ff494c0de8c9e51fce9ad82449f63b27b335b26f1544ecb0" -> null
      - image             = "sha256:e791337790a6181d5ce870b3bb16de1a4d5aa3a916e8fba6907f57eb409934cf" -> null
      - ip_address        = "172.17.0.2" -> null
      - ip_prefix_length  = 16 -> null
      - ipc_mode          = "private" -> null
      - links             = [] -> null
      - log_driver        = "json-file" -> null
      - log_opts          = {} -> null
      - logs              = false -> null
      - max_retry_count   = 0 -> null
      - memory            = 0 -> null
      - memory_swap       = 0 -> null
      - must_run          = true -> null
      - name              = "training" -> null
      - network_data      = [
          - {
              - gateway          = "172.17.0.1"
              - ip_address       = "172.17.0.2"
              - ip_prefix_length = 16
              - network_name     = "bridge"
            },
        ] -> null
      - network_mode      = "default" -> null
      - privileged        = false -> null
      - publish_all_ports = false -> null
      - read_only         = false -> null
      - restart           = "no" -> null
      - rm                = false -> null
      - shm_size          = 64 -> null
      - start             = true -> null
      - sysctls           = {} -> null
      - tmpfs             = {} -> null

      - labels {
          - label = "maintainer" -> null
          - value = "NGINX Docker Maintainers <docker-maint@nginx.com>" -> null
        }

      - ports {
          - external = 80 -> null
          - internal = 80 -> null
          - ip       = "0.0.0.0" -> null
          - protocol = "tcp" -> null
        }
    }

  # docker_image.nginx will be destroyed
  - resource "docker_image" "nginx" {
      - id     = "sha256:e791337790a6181d5ce870b3bb16de1a4d5aa3a916e8fba6907f57eb409934cfnginx:latest" -> null
      - latest = "sha256:e791337790a6181d5ce870b3bb16de1a4d5aa3a916e8fba6907f57eb409934cf" -> null
      - name   = "nginx:latest" -> null
    }

Plan: 0 to add, 0 to change, 2 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: 
```

After running this command, Terraform will prompt you for confirmation. To confirm, type `yes` and hit ENTER. Terraform will then destroy any resources in your Terraform configuration file.

## Next Steps

Terraform's IaC offering lets you manage your infrastructure resources through code instead of navigating and configuring resources through different user interfaces. This guide taught you the basics of getting started with Terraform. Now, see a more [in-depth example workflow](https://learn.hashicorp.com/terraform/getting-started/build) to dive deeper.
