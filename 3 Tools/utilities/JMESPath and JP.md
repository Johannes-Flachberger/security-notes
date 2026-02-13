---
tags:
  - "#type/tool"
Link: https://jmespath.org/
Purpose: query language and tool for large json files
---
# Info

JMESPath is a query language for json. It helps with extracting information from large json files.

**Example:** see [official usage examples](https://jmespath.org/examples.html)

# Usage

JMESPath is supprted by various tools and frameworks. To query local json files use [JP](https://github.com/jmespath/jp)

**Simple Example:** `jp -f auth-details.json 'UserDetailList[].UserName'`

**Complex Example:** `jp -f auth-details.json "UserDetailList[?contains(UserName,'admin') && contains(Path,'admin')].UserName"`

For data exploration, function are useful:

| Expression        | Purpose                                                                    |
| ----------------- | -------------------------------------------------------------------------- |
| `@`               | the current element                                                        |
| `keys(<element>)` | show keys of an object<br>e.g. `keys(@)` shows the keys in the root object |
| `type(<element>)` | get json type of an element                                                |
| `length(<array>)` | get length of an array                                                     |

# Snippets
