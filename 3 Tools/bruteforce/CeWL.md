**Tags:** #type/tool #tactic/ressource-development 
**Link:** 
**Purpose:** wordlist generator for customized wordlists

---
# Info
can crawl websites etc. and create wordlists from it
## why use ceWL?
1. **Target-specific wordlists:** CeWL crafts wordlists specifically from the content of a targeted website. This means that the generated list is inherently tailored to the vocabulary and terminology used on that site. Such custom lists can increase the efficiency of brute-forcing tasks.
2. **Depth of search:** CeWL can spider a website to a specified depth, thereby extracting words from not just one page but also from linked pages up to the set depth.
3. **Customisable outputs:** CeWL provides various options to fine-tune the wordlist, such as setting a minimum word length, removing numbers, and including meta tags. This level of customisation can be advantageous for targeting specific types of credentials or vulnerabilities.
4. **Built-in features:** While its primary purpose is wordlist generation, CeWL includes functionalities such as username enumeration from author meta tags and email extraction.
5. **Efficiency:** Given its customisability, CeWL can often generate shorter but more relevant word lists than generic ones, making password attacks quicker and more precise.
6. **Integration with other tools:** Being command-line based, CeWL can be integrated seamlessly into automated workflows, and its outputs can be directly fed into other cyber security tools.
7. **Actively maintained:** CeWL is actively maintained and updated. This means it stays relevant and compatible with contemporary security needs and challenges.
# Usage
e.g. ```cewl http://10.10.17.32 -w output.txt``` 

#### How To Customise the Output for Specific Tasks
CeWL provides a lot of options that allow you to tailor the wordlist to your needs:

1. **Specify spidering depth:** The `-d` option allows you to set how deep CeWL should spider. For example, to spider two links deep: `cewl http://10.10.17.32 -d 2 -w output1.txt`
2. **Set minimum and maximum word length:** Use the `-m` and `-x` options respectively. For instance, to get words between 5 and 10 characters: `cewl http://10.10.17.32 -m 5 -x 10 -w output2.txt`
3. **Handle authentication:** If the target site is behind a login, you can use the `-a` flag for form-based authentication.
4. **Custom extensions:** The `--with-numbers` option will append numbers to words, and using `--extension` allows you to append custom extensions to each word, making it useful for directory or file brute-forcing.
5. **Follow external links:** By default, CeWL doesn't spider external sites, but using the `--offsite` option allows you to do so.