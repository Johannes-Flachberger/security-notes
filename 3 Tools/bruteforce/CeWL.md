---
tags:
  - type/tool 
  - tactic/ressource-development 
Link: 
Purpose: wordlist generator based on websites
---
# Info
can crawl websites etc. and create wordlists from it
# Usage
e.g. ```cewl http://10.10.17.32 -w output.txt``` 

#### How To Customise the Output for Specific Tasks
CeWL provides a lot of options that allow you to tailor the wordlist to your needs:

1. **Specify spidering depth:** The `-d` option allows you to set how deep CeWL should spider. For example, to spider two links deep: `cewl http://10.10.17.32 -d 2 -w output1.txt`
2. **Set minimum and maximum word length:** Use the `-m` and `-x` options respectively. For instance, to get words between 5 and 10 characters: `cewl http://10.10.17.32 -m 5 -x 10 -w output2.txt`
3. **Handle authentication:** If the target site is behind a login, you can use the `-a` flag for form-based authentication.
4. **Custom extensions:** The `--with-numbers` option will append numbers to words, and using `--extension` allows you to append custom extensions to each word, making it useful for directory or file brute-forcing.
5. **Follow external links:** By default, CeWL doesn't spider external sites, but using the `--offsite` option allows you to do so.