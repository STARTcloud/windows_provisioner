# Hosts Configuration Templates

This repository (`windows_provisioner`) is the Windows provisioner — it provisions a Windows Server guest from a STARTcloud Windows box using the Windows roles of the `startcloud.startcloud_roles` collection. Adjust the enabled roles under `roles:` in your `Hosts.yml`.

## Hosts.template.yml

- **Purpose**: A true Jinja2 template rendered by the hyperweaver-agent generator (gonja; nunjucks on zoneweaver when its render step lands) to produce the final `Hosts.yml`. Context comes from the machine spec: structured `settings`/`networks`/`roles` plus manifest field answers by exact field name; every settings key echoes the create context with the package value as fallback (`| default(...)`), and enabled picker roles are appended after the base foundation roles.
- **Usage**: Rendered by the agent at machine create. Dialect: standard Jinja2 — parenthesized filter args (`|default("x")`), `loop.*` metadata, `is defined` works; undefined variables render empty.

## Hand-writing a Hosts.yml (plain vagrant use)

Create `Hosts.yml` at the repository root (it is gitignored). The driver ships reference documents under `driver/examples/` — the driver directory is fetched automatically on first `vagrant up` from the core_provisioner release pinned in `driver.version`.

## Add your own

If you add your own template, update this README.md with a brief description of what it does, and in your pull request mention why it differs from the existing ones.
