# Terra

**Self-hosted Ansible controller in a container — automated, on-demand, and isolated.**

## 🔧 What It Is

Terra is a lightweight Docker Compose–driven Ansible server. Rather than installing Ansible directly on your system, Terra runs as a containerized controller that:

- Executes modular playbooks against your network via SSH  
- Runs on a fixed interval or by manual trigger (via HTTP webhook)  
- Mounts host-side secrets, vault data, and inventory as read-only  
- Stays self-contained, restartable, and decoupled from your OS

Ideal for home labs and self-hosted environments where you want automation without clutter.

## 🧩 Key Features

- **Containerized Ansible**  
  Based on `alpine/ansible:latest`, running isolated from your host

- **Interval-Based Execution**  
  Default 30-minute interval, configurable at runtime

- **Webhook Triggers**  
  Lightweight HTTP interface for manual control and config updates

- **External Secrets & Inventory**  
  All credentials and vault files mount externally from host

- **Scoped System Access**  
  Uses a dedicated `ansible` user across systems, managed via SSH keys

## 📁 Repo Layout

```
terra/
├── docker-compose.yml       # Defines the Ansible container and mounts
├── entrypoint.sh            # Starts Flask webhook + interval runner
├── webhook.py               # Flask app handling control endpoints
└── playbooks/
    ├── 00-master.yml        # Top-level playbook (includes others)
    ├── 01-host_edits.yml    # User/group/hosts file configuration
    ├── 02-user.yml          # Shell aliases and bashrc updates
    └── 03-software.yml      # Installs essential packages
```

Secrets and inventory live on the host at:
```
/opt/ansible_secrets  
```

## 🧠 Philosophy

Terra isn't a full-blown control plane. It's a clean, repeatable Ansible execution environment — small enough to fit in a single container, strong enough to manage your entire home lab or server fleet.

## 📬 Contact

Have questions or ideas?  
📧 **chris@bosman.solutions**

_Built with care by Bosman Solutions in Los Angeles._

