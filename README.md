# Ansible Pull Ubuntu Desktop

Ansible playbook for setting up the local Ubuntu desktop: system packages,
applications, and per-user configuration.

## Run

From this directory, run:

```sh
ansible-playbook --ask-become-pass local.yml
```

The playbook uses `USER` and `HOME` from the environment in which it is run to
choose the desktop account for user-level configuration. Run it as that user;
Ansible prompts for sudo access.

## Layout

```text
local.yml                         # Entry playbook
roles/
  system_packages/tasks/main.yml  # Base packages and Ubuntu components
  terraform/tasks/main.yml       # HashiCorp APT source and Terraform
  snap_packages/                  # Configured Snap packages (defaults + tasks)
  ghostwriter/tasks/main.yml      # Ghostwriter package from Ubuntu Universe
  yazi/tasks/main.yml             # Yazi repository, package, and previews
  ulauncher/tasks/main.yml        # Ulauncher PPA and package
  applications/tasks/main.yml     # Other applications and app-specific setup
  os_configuration/tasks/main.yml # Per-user shell and command configuration
```

Add related tasks to the existing role. Create another role when a group of
tasks has its own clear responsibility or needs to be enabled independently.

Applications configured here include Keeper Security (Snap), Ghostwriter (from
Ubuntu Universe), Yazi, Ulauncher, Ghostty, FSearch, auto-cpufreq, Atuin, and
JetBrains Mono Nerd Font. Terraform is installed from HashiCorp's architecture-
scoped APT repository.
