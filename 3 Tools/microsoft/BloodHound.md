---
tags:
  - "#type/tool"
Link: https://bloodhound.specterops.io/collect-data/ce-collection/overview
Purpose: collection of tools for active directory enumeration
---
# Info

A collection of tools tools for active directory enumeration. Commercial and Community Editions are available.

**Workflow:** Use [[#Data Collectors]] to gather data, transfer it to your workstation and analyze the data with [[#BloodHound]]

# Data Collectors

> [!NOTE] There are also lots of third-party data collectors:
> - [RustHound](https://github.com/g0h4n/RustHound-CE): cross platform, uses provided credentials to gather data
> - [bloodhound-python](https://www.kali.org/tools/bloodhound.py/), uses provided credentials to gather data

> [!Hint] With the opengraph API,ingestors for other platforms can be developed.
> List of ingestors: [Opengraph Library](https://bloodhound.specterops.io/opengraph/library)

## SharpHound

Should be run from a compromised host within an AD environment.

Automatically enumerates Active Directory and stores the data in a file. It also supports being run periodically & caching to analyse how the directory changes.

Available in different formats:

- source
- executable
- [[3 Tools/shells/PowerShell|PowerShell]] script

### Usage

When using PowerShell:

1. `Import-Module .\Sharphound.ps1`
2. E.g.: `Invoke-BloodHound -CollectionMethod All -OutputDirectory <directory> -OutputPrefix "<filename_prefix>" -ZipPassword <password>`

|     |     |
| --- | --- |
|     |     |

## AzureHound

Data Collector for Azure Environments.

# BloodHound

BloodHound uses Neo4j as an engine / underlying graph database.

## Installation

The easiest way to install is a docker-based install using the `bloodhound-cli` - see [Bloodhound CE Quickstart](https://bloodhound.specterops.io/get-started/quickstart/community-edition-quickstart)

**Hint:** bloodhound-cli also supports starting / stopping the containers, & managing the admin password.

After starting the containers, Bloodhound should be available at `http://localhost:8080/ui/login`

## Usage

**Setup:** See [[#Installation]]

**Workflow:**

1. Import the data collected by a data collector.
2. Mark objects you own as "owned principals".
3. Use queries to analyse data.

**Hints:**

In menu at top left:

- "Cypher" provides access to queries. Especially useful is the "shortest path" category of the saved queries:

### Cypher Queries

See: [Quick Start Guide](https://bloodhound.specterops.io/analyze-data/explore/cypher-search)

Most relevant queries are already available as saved queries.

List objects within the domain - e.g. `Computer`, `User`, `Group`:

```cypher
 MATCH (m:<object_type>) RETURN m
```

List active sessions:

```cypher
MATCH p = (c:Computer)-[:HasSession]->(m:User) RETURN p
```
