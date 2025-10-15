**Type:** #type/theory
**Tags:** #tactic/reconnaissance/passive 

---

- Usually outperforms traditional recon tools - still it is best to use traditional tools for fact-checking
- Always consider that your prompts & the LLMs response may be analysed by the LLM provider.
- A lot of LLMs provide dedicated research modes.
# Tools:
- ChatGPT
- Perplexity - much faster than ChatGPT deep research
# Use Cases & Prompts

> [!TIP] Hint: Use the [[1_Theory/Security-Testing/1_In/1 Reconnaissance/Overview - Reconnaissance#Big Checklist|Big Reconnaissance Checklist]] in Prompts
 

**Get employee info**
```
Can you print out all the public information about company structure and employees of <company>?
```
**Retrieve technology stack about the website**
```
Retrieve the technology stack of the example.com website
```
**Generate wordlists**
```
Using only publicly available information from <company>’s official web presence and other open sources, and based on reasonable inferences about its organizational structure, services, and product names, produce a categorized set of candidate subdomain naming **patterns** and conventions.
- Include common naming patterns used for infrastructure and environments (for example: api, dev, test, staging).

- Include service- and protocol-related patterns (for example: mail, auth, cdn, status).

- Include departmental and functional patterns (for example: hr, sales, support).

- Include geographic and regional patterns where relevant (for example: us, eu, apac).

- Consider industry-specific terminology and frequently used abbreviations relevant to <company>’s sector.

Present the output as a clean, de-duplicated, lowercase list of naming patterns.
```
