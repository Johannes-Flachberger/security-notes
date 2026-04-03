---
tags:
  - "#type/tool"
Link: https://github.com/AutoRecon/AutoRecon/wiki/Usage
Purpose: '"meta-automation" of active recon'
---
# Info

Automation tool for active recon. It triggers other automated tools such as nmap, nikto, directory fuzzing, etc. and stores the results in directory structure.

# Usage

**Recommended Workflow:**

1. If scanning a whole ip range, run a portscan using [[3 Tools/network/scanning/nmap|nmap]] and create a list of active hosts.
2. Run autorecon on the list of active hosts without the `dirbuster` plugin (this one takes forever).

**Example:** `autorecon --only-scans-dir --exclude-tags="dirbuster" <ip1> [ip2] [ip3]`

While running, adjust verbosity with `up/down keys` - use high verbosity to print plugin output. Press `s` for status.

> [!NOTE]
> Apart from the options below, autorecon lets you configure many aspects of the tools used, such as number of threads, wordlists, etc.

| Option                                | Purpose                                                                                              |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `-l`                                  | list available plugins                                                                               |
| `--tags="<tags/plugin-slug>"`         | only run plugins with tags                                                                           |
| `--exclude-tags="<tags/plugin-slug>"` | exclude plugin with tags<br>exclude single plugin by specifying its "slug", e.g. `default-port-scan` |
| `--only-scans-dir`                    | only create "scans" directory for each host, but no "exploit", "notes" and "loot" directories        |
| `-o <path>`                           | output directory - useful if you want to give some context, e.g. "DMZ"                               |
| `--dirbuster.wordlist <path>`         | wordlist to use for directory busting                                                                |
| `--dirbuster.threads <num>`           | number of threads for directory busting                                                              |

Typically, long scan durations are caused by the `portscan-all-tcp-ports` and the `dirbuster` plugins. Consider disabling those specifically, or all plugins tagged `long`.

To understand what a plugin is doing and which tags it has, best check in the plugins directory at `~/.config/AutoRecon/plugins` or `~/.local/share/AutoRecon/plugins`.

> [!Hint] Personal preferences
> - The markdown report and additional directories dont provide much value for me --> run with `--only-scans-dir`.
> - If the network & targets can handle parallel scans, it does not hurt to run with plugins tagged `long` and to start manual work in the meantime. Otherwise, run with `--exclude-tags="long"`.

# Snippets
