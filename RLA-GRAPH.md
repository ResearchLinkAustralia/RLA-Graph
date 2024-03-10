**Last update: 17 Jan 2024**

Research Link Australia (RLA) Graph is [heterogeneous graph](https://arxiv.org/pdf/1903.07293) derived from [Research Graph Schema](https://researchgraph.org/schema). This meta model consists of five main node types including [[Researcher]], [[Organisation]], [[Publication]], [[Grant]], [[ResearchData]]. These node types are designed to be inclusive of a diverse research objects enabling grouping of similar nodes in a single type. 

These node types are mainly formed by connecting three main persistent identifiers([[PIDs]]) including [[ORCID]], [[DOI]], [[PubMed ID]], and [[ROR]], and linking to Australian national level identifiers including Australian Business Number ([[ABN]]) and grant id from Australian Research Council ([[ARC]]), and National Medical Health Research Institute ([[NHMRC]]).

RLA Graph is captured in a [[Neo4j Graph database]], and in the context of this repository, we use [[Cypher]] language to describe the queries and present the provenance behind the content of the graph.

The following list provides the summary of information accessible via the RLA Graph at the time of the **Last Update** for this repository.

## Nodes by Source and Type

The following nodes and relationships are extracted from graph version 1.1.6 (2024-01-17).

```
match (n) return n.source as Source, n.type as Type, count(n) order by Source, Type
```

| Source         | Type           | Node Count |
| :------------- | :------------- | ---------: |
| "abr.gov.au"   | "organisation" |      5,464 |
| "arc.gov.au"   | "grant"        |     32,238 |
| "arc.gov.au"   | "organisation" |     14,736 |
| "crossref.org" | "dataset"      |      2,219 |
| "crossref.org" | "organisation" |      6,586 |
| "crossref.org" | "publication"  |  1,764,309 |
| "datacite.org" | "dataset"      |      8,495 |
| "datacite.org" | "publication"  |     13,546 |
| "grid.ac"      | "organisation" |     14,282 |
| "nhmrc.org"    | "grant"        |     28,547 |
| "orcid.org"    | "dataset"      |     16,852 |
| "orcid.org"    | "grant"        |     27,416 |
| "orcid.org"    | "organisation" |    221,450 |
| "orcid.org"    | "publication"  |  6,508,316 |
| "orcid.org"    | "researcher"   |    815,442 |
| "pubmed.gov"   | "publication"  |    468,975 |
| "ror.org"      | "organisation" |    107,096 |
| "scopus.com"   | "publication"  |  1,020,052 |
| "twitter.com"  | "tweet"        |    347,962 |
| "wikidata.org" | "organisation" |      1,444 |

>[!Note]
>RLA Graph is an undirected connected graph, that means all nodes in this graph have at least one link to other nodes. Any grant, publication, research data, or organisation with no links to other PIDs is excluded form this graph.


## Relationships
```
match (n)-[r]-(m) where (n.source)<>(m.source) return n.source as Source1, m.source as Source2, n.type as Type1, m.type as Type2, count(r) as Relations
```

| Source1        | Source2        | Type1          | Type2          | Relations   |
|:---------------|:---------------|:---------------|:---------------|------------:|
| "abr.gov.au"   | "arc.gov.au"   | "organisation" | "organisation" | 6,388       |
| "arc.gov.au"   | "abr.gov.au"   | "organisation" | "organisation" | 6,388       |
| "arc.gov.au"   | "orcid.org"    | "grant"        | "researcher"   | 46,502      |
| "arc.gov.au"   | "ror.org"      | "organisation" | "organisation" | 2,951       |
| "arc.gov.au"   | "wikidata.org" | "grant"        | "organisation" | 31,800      |
| "crossref.org" | "orcid.org"    | "dataset"      | "dataset"      | 1,425       |
| "crossref.org" | "orcid.org"    | "dataset"      | "researcher"   | 3,438       |
| "crossref.org" | "orcid.org"    | "organisation" | "grant"        | 26,515      |
| "crossref.org" | "orcid.org"    | "organisation" | "researcher"   | 76,975      |
| "crossref.org" | "orcid.org"    | "publication"  | "dataset"      | 2,513       |
| "crossref.org" | "orcid.org"    | "publication"  | "publication"  | 6,637,015   |
| "crossref.org" | "orcid.org"    | "publication"  | "researcher"   | 5,624,695   |
| "crossref.org" | "pubmed.gov"   | "publication"  | "publication"  | 443,666     |
| "crossref.org" | "scopus.com"   | "publication"  | "publication"  | 1,034,621   |
| "crossref.org" | "twitter.com"  | "publication"  | "tweet"        | 353,141     |
| "datacite.org" | "orcid.org"    | "dataset"      | "dataset"      | 14,244      |
| "datacite.org" | "orcid.org"    | "dataset"      | "researcher"   | 16,302      |
| "datacite.org" | "orcid.org"    | "publication"  | "publication"  | 23,776      |
| "datacite.org" | "orcid.org"    | "publication"  | "researcher"   | 21,614      |
| "datacite.org" | "twitter.com"  | "publication"  | "tweet"        | 1,932       |
| "grid.ac"      | "orcid.org"    | "organisation" | "organisation" | 1,803       |
| "grid.ac"      | "orcid.org"    | "organisation" | "researcher"   | 146,623     |
| "grid.ac"      | "ror.org"      | "organisation" | "organisation" | 14,282      |
| "nhmrc.org"    | "orcid.org"    | "grant"        | "researcher"   | 2,611       |
| "orcid.org"    | "arc.gov.au"   | "researcher"   | "grant"        | 46,502      |
| "orcid.org"    | "crossref.org" | "dataset"      | "dataset"      | 1,425       |
| "orcid.org"    | "crossref.org" | "dataset"      | "publication"  | 2,513       |
| "orcid.org"    | "crossref.org" | "grant"        | "organisation" | 26,515      |
| "orcid.org"    | "crossref.org" | "publication"  | "publication"  | 6,637,015   |
| "orcid.org"    | "crossref.org" | "researcher"   | "dataset"      | 3,438       |
| "orcid.org"    | "crossref.org" | "researcher"   | "organisation" | 76,975      |
| "orcid.org"    | "crossref.org" | "researcher"   | "publication"  | 5,624,695   |
| "orcid.org"    | "datacite.org" | "dataset"      | "dataset"      | 14,244      |
| "orcid.org"    | "datacite.org" | "publication"  | "publication"  | 23,776      |
| "orcid.org"    | "datacite.org" | "researcher"   | "dataset"      | 16,302      |
| "orcid.org"    | "datacite.org" | "researcher"   | "publication"  | 21,614      |
| "orcid.org"    | "grid.ac"      | "organisation" | "organisation" | 1,803       |
| "orcid.org"    | "grid.ac"      | "researcher"   | "organisation" | 146,623     |
| "orcid.org"    | "nhmrc.org"    | "researcher"   | "grant"        | 2,611       |
| "orcid.org"    | "pubmed.gov"   | "researcher"   | "publication"  | 289,218     |
| "orcid.org"    | "wikidata.org" | "organisation" | "organisation" | 2,280       |
| "pubmed.gov"   | "crossref.org" | "publication"  | "publication"  | 443,666     |
| "pubmed.gov"   | "orcid.org"    | "publication"  | "researcher"   | 289,218     |
| "ror.org"      | "arc.gov.au"   | "organisation" | "organisation" | 2,951       |
| "ror.org"      | "grid.ac"      | "organisation" | "organisation" | 14,282      |
| "scopus.com"   | "crossref.org" | "publication"  | "publication"  | 1,034,621   |
| "twitter.com"  | "crossref.org" | "tweet"        | "publication"  | 353,141     |
| "twitter.com"  | "datacite.org" | "tweet"        | "publication"  | 1,932       |
| "wikidata.org" | "arc.gov.au"   | "organisation" | "grant"        | 31,800      |
| "wikidata.org" | "orcid.org"    | "organisation" | "organisation" | 2,280       |


