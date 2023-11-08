**Last update: 8 Nov 2023**

Research Link Australia (RLA) Graph is [heterogeneous graph](https://arxiv.org/pdf/1903.07293) derived from [Research Graph Schema](https://researchgraph.org/schema). This meta model consists of five main node types including [[Researcher]], [[Organisation]], [[Publication]], [[Grant]], [[ResearchData]]. These node types are designed to be inclusive of a diverse research objects enabling grouping of similar nodes in a single type. 

These node types are mainly formed by connecting three main persistent identifiers([[PIDs]]) including [[ORCID]], [[DOI]], [[PubMed ID]], and [[ROR]], and linking to Australian national level identifiers including Australian Business Number ([[ABN]]) and grant id from Australian Research Council ([[ARC]]), and National Medical Health Research Institute ([[NHMRC]]).

RLA Graph is captured in a [[Neo4j Graph database]], and in the context of this repository, we use [[Cypher]] language to describe the queries and present the provenance behind the content of the graph.

The following list provides the summary of information accessible via the RLA Graph at the time of the **Last Update** for this repository.

## Nodes by Source and Type
```
match (n) return n.source as Source, n.type as Type, count(n) order by Source, Type
```

| Source          | Type         |  count(n) |
|-----------------|--------------|----------:|
| abr.gov.au      | organisation |     6,019 |
| arc.gov.au      | grant        |    20,352 |
| arc.gov.au      | organisation |    14,152 |
| crossref.org    | dataset      |     2,031 |
| crossref.org    | grant        |        86 |
| crossref.org    | organisation |     5,509 |
| crossref.org    | publication  | 1,523,389 |
| datacite.org    | dataset      |     8,392 |
| datacite.org    | publication  |    12,421 |
| grid.ac         | organisation |    13,350 |
| isni.org        | organisation |        35 |
| isni.ringgold.com | organisation |       538 |
| nhmrc.org       | grant        |    14,790 |
| orcid.org       | dataset      |    16,061 |
| orcid.org       | grant        |    25,700 |
| orcid.org       | organisation |   173,825 |
| orcid.org       | publication  | 6,467,279 |
| orcid.org       | researcher   |   668,895 |
| pubmed.gov      | publication  |   440,153 |
| ror.org         | organisation |   105,294 |
| scopus.com      | publication  |   932,840 |
| twitter.com     | tweet        |   293,433 |
| wikidata.org    | organisation |     1,888 |
| wikipedia.org   | wikipedia    |       474 |

>[!Note]
>RLA Graph is an undirected connected graph, that means all nodes in this graph have at least one link to other nodes. Any grant, publication, research data, or organisation with no links to other PIDs is excluded form this graph.


## Relationships
