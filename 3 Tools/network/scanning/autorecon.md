---
tags:
  - "#type/tool"
Link: https://github.com/AutoRecon/AutoRecon/wiki/Usage
Purpose: '"meta-automation" of active recon'
---
# Info

Automation tool for active recon. It triggers other automated tools such as nmap, nikto, directory fuzzing, etc. and stores the results in a structured way.

# Usage

**Example:** `autorecon --exclude-tags="long" --only-scans-dir <ip/cidr_range> [ip2] [ip3]`

While running, adjust verbosity with `up/down keys` - use high verbosity to print plugin output. Press `s` for status.

| Option                                | Purpose                                                                                              |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `-l`                                  | list available plugins                                                                               |
| `--tags="<tags/plugin-slug>"`         | only run plugins with tags                                                                           |
| `--exclude-tags="<tags/plugin-slug>"` | exclude plugin with tags<br>exclude single plugin by specifying its "slug", e.g. `default-port-scan` |
| `--only-scans-dir`                    | only create "scans" directory for each host, but no "exploit", "notes" and "loot" directories        |

Typically, long scan durations are caused by the `portscan-all-tcp-ports` and the `dirbuster` plugins. Consider disabling those specifically, or all plugins tagged `long`.

To understand what a plugin is doing and which tags it has, best check in the plugins directory at `~/.config/AutoRecon/plugins` or `~/.local/share/AutoRecon/plugins`.

# Snippets
