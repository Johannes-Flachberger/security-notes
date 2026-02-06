---
tags:
  - "#type/tool"
Link: https://www.kali.org/tools/cloud-enum/
Purpose: Public Cloud Enum based on keywords
---
# Info

Enumerates public cloud services based on keywords

# Usage

**Example:** `cloud_enum -k <keyword> --quickscan`

Per default, multiple cloud providers are enumerated.

| Option                | Purpose                                                                                                                          |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `--disable-azure`     | dont search in azure                                                                                                             |
| `--disable-gcp`       | dont search in google cloud                                                                                                      |
| `--keyword <keyword>` | keyword to search for                                                                                                            |
| `-kf <path>`          | file to get keywords from                                                                                                        |
| `-m <path>`           | file from which to add extra words to the keywords<br>if no argument is given, `/usr/lib/cloud-enum/enum_tools/fuzz.txt` is used |

# Snippets
