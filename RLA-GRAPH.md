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
```
match (n)-[r]-(m) where (n.source)<>(m.source) return n.source as Source1, m.source as Source2, n.type as Type1, m.type as Type2, count(r) as Relations
```

| Source1        | Source2             | Type1       | Type2       | Relations   |
|:--------------|:-------------------|:-----------|:-----------|-----------:|
| orcid.org      | crossref.org        | organisation| organisation|     592     |
| orcid.org      | grid.ac             | organisation| organisation|   1,423     |
| orcid.org      | wikidata.org        | organisation| organisation|   2,278     |
| wikidata.org   | ror.org             | organisation| organisation|     938     |
| wikidata.org   | orcid.org           | organisation| organisation|   2,278     |
| wikidata.org   | crossref.org        | organisation| organisation|     211     |
| wikidata.org   | isni.ringgold.com   | organisation| organisation|     499     |
| wikidata.org   | arc.gov.au          | organisation| grant       |  20,266     |
| wikidata.org   | wikipedia.org       | organisation| wikipedia   |     797     |
| wikidata.org   | grid.ac             | organisation| organisation|     613     |
| orcid.org      | crossref.org        | researcher  | publication | 5,635,618   |
| orcid.org      | grid.ac             | researcher  | organisation| 123,753     |
| orcid.org      | pubmed.gov          | researcher  | publication | 263,578     |
| orcid.org      | arc.gov.au          | researcher  | grant       |  41,401     |
| orcid.org      | nhmrc.org           | researcher  | grant       |  87,467     |
| orcid.org      | crossref.org        | researcher  | organisation|  53,769     |
| orcid.org      | datacite.org        | researcher  | publication |  17,714     |
| orcid.org      | datacite.org        | researcher  | dataset     |  14,426     |
| grid.ac        | ror.org             | organisation| organisation|  26,700     |
| grid.ac        | orcid.org           | organisation| organisation|   1,423     |
| grid.ac        | orcid.org           | organisation| researcher  | 123,753     |
| grid.ac        | wikidata.org        | organisation| organisation|     613     |
| grid.ac        | isni.ringgold.com   | organisation| organisation|     534     |
| grid.ac        | wikipedia.org       | organisation| wikipedia   |     790     |
| grid.ac        | crossref.org        | organisation| organisation|     298     |
| crossref.org   | orcid.org           | dataset     | publication |     557     |
| crossref.org   | orcid.org           | dataset     | researcher  |   2,837     |
| orcid.org      | crossref.org        | researcher  | dataset     |   2,837     |
| orcid.org      | crossref.org        | grant       | organisation|  24,833     |
| crossref.org   | orcid.org           | publication | researcher  | 5,635,618   |
| crossref.org   | orcid.org           | publication | publication | 6,446,806   |
| crossref.org   | pubmed.gov          | publication | publication | 412,355     |
| crossref.org   | scopus.com          | publication | publication | 932,530     |
| crossref.org   | twitter.com         | publication | tweet       | 293,522     |
| arc.gov.au     | wikidata.org        | grant       | organisation|  20,266     |
| arc.gov.au     | orcid.org           | grant       | researcher  |  41,401     |
| pubmed.gov     | crossref.org        | publication | publication | 412,355     |
| pubmed.gov     | orcid.org           | publication | researcher  | 263,578     |
| isni.ringgold.com | ror.org          | organisation| organisation|     535     |
| isni.ringgold.com | grid.ac          | organisation| organisation|     534     |
| isni.ringgold.com | wikidata.org     | organisation| organisation|     499     |
| orcid.org      | crossref.org        | dataset     | publication |     252     |
| scopus.com     | crossref.org        | publication | publication | 932,530     |
| orcid.org      | crossref.org        | publication | publication | 6,446,806   |
| nhmrc.org      | orcid.org           | grant       | researcher  |  87,467     |
| crossref.org   | orcid.org           | organisation| researcher  |  53,769     |
| wikipedia.org  | wikidata.org        | wikipedia   | organisation|     797     |
| wikipedia.org  | grid.ac             | wikipedia   | organisation|     790     |
| grid.ac        | isni.org            | organisation| organisation|      35     |
| crossref.org   | wikidata.org        | organisation| organisation|     211     |
| crossref.org   | orcid.org           | organisation| organisation|     592     |
| crossref.org   | orcid.org           | organisation| grant       |  24,833     |
| crossref.org   | grid.ac             | organisation| organisation|     298     |
| twitter.com    | crossref.org        | tweet       | publication | 293,522     |
| orcid.org      | crossref.org        | dataset     | dataset     |   1,314     |
| orcid.org      | datacite.org        | dataset     | dataset     |  14,097     |
| scopus.com     | datacite.org        | publication | publication |     284     |
| datacite.org   | orcid.org           | publication | researcher  |  17,714     |
| datacite.org   | orcid.org           | publication | publication |  19,157     |
| datacite.org   | orcid.org           | dataset     | researcher  |  14,426     |
| datacite.org   | orcid.org           | dataset     | dataset     |  14,097     |
| orcid.org      | datacite.org        | publication | publication |  19,157     |
| orcid.org      | crossref.org        | grant       | grant       |      17     |
| crossref.org   | orcid.org           | publication | dataset     |     252     |
| orcid.org      | datacite.org        | dataset     | publication |     397     |
| datacite.org   | orcid.org           | dataset     | publication |     741     |
| datacite.org   | scopus.com          | dataset     | publication |      26     |
| crossref.org   | orcid.org           | dataset     | dataset     |   1,314     |
| datacite.org   | orcid.org           | publication | dataset     |     397     |
| orcid.org      | crossref.org        | publication | dataset     |     557     |
| twitter.com    | datacite.org        | tweet       | publication |   1,725     |
| wikidata.org   | isni.org            | organisation| organisation|      30     |
| isni.org       | ror.org             | organisation| organisation|      35     |
| isni.org       | grid.ac             | organisation| organisation|      35     |
| isni.org       | wikidata.org        | organisation| organisation|      30     |
| orcid.org      | datacite.org        | publication | dataset     |     741     |
| datacite.org   | twitter.com         | dataset     | tweet       |     424     |
| orcid.org      | crossref.org        | publication | null        |      18     |
| datacite.org   | twitter.com         | publication | tweet       |   1,725     |
| scopus.com     | datacite.org        | publication | dataset     |      26     |
| twitter.com    | datacite.org        | tweet       | dataset     |     424     |
| datacite.org   | scopus.com          | publication | publication |     284     |
| crossref.org   | twitter.com         | dataset     | tweet       |      11     |
| crossref.org   | orcid.org           | null        | publication |      18     |
| datacite.org   | pubmed.gov          | publication | publication |      10     |
| crossref.org   | orcid.org           | grant       | grant       |      17     |
| pubmed.gov     | datacite.org        | publication | publication |      10     |
| crossref.org   | orcid.org           | null        | dataset     |       1     |
| twitter.com    | crossref.org        | tweet       | dataset     |      11     |
| orcid.org      | crossref.org        | dataset     | null        |       1     |
| ror.org        | grid.ac             | organisation | organisation | 26,700   |
| ror.org        | isni.ringgold.com   | organisation | organisation |    535   |
| ror.org        | arc.gov.au          | organisation | organisation |  1,967   |
| ror.org        | wikidata.org        | organisation | organisation |    938   |
| ror.org        | isni.org            | organisation | organisation |     35   |
| arc.gov.au     | abr.gov.au          | organisation | organisation |  3,855   |
| arc.gov.au     | ror.org             | organisation | organisation |  1,967   |
| abr.gov.au     | arc.gov.au          | organisation | organisation |  3,855   |


