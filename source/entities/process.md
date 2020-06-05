## Process Functions

The following BEL Functions represent classes of events or phenomena taking place at the level of the cell or the organism which do not correspond to molecular abundances, but instead to a biological process like angiogenesis or a pathology like cancer.

### Biological Processes and Pathways

Pathways, biological processes, and high-order molecular-level phenomena can be represented with the `biologicalProcess()` / `bp()` function.

For example, the process of angiogenesis can be represented with:

```text
# long form
biologicalProcess(go:0001525 ! angiogenesis)

# short form
bp(go:0001525 ! angiogenesis)
```

Likewise, the Signaling by Hippo pathway from Reactome can be represented with:

```text
bp(reactome:R-HSA-2028269 ! "Signaling by Hippo")
```

There are no modifiers to the `bp()` function.

#### Recommended Nomenclatures

| prefix | name |
| :--- | :--- |
| [go](https://registry.identifiers.org/registry/go) | Gene Ontology |
| [wikipathways](https://registry.identifiers.org/registry/wikipathways) | WikiPathways |
| [reactome](https://registry.identifiers.org/registry/reactome) | Reactome |

#### Not Recommended Nomenclature

| prefix | name | reason |
| :--- | :--- | :--- |
| [mesh](https://registry.identifiers.org/registry/mesh) | Medical Subject Headings | no cross-references to other nomenclatures |
| [ncit](https://registry.identifiers.org/registry/ncit) | National Cancer Institute Thesaurus | few cross-references maintained |
| [kegg.pathway](https://registry.identifiers.org/registry/kegg.pathway) | Kyoto Encyclopedia of Genes and Genomes | data not easily accessible |
| [pid.pathway](https://registry.identifiers.org/registry/pid.pathway) | NCI Pathway Interaction Database | not maintained |

If you need help mapping between pathway databases, see [ComPath](https://www.nature.com/articles/s41540-018-0078-8).

### Phenotypes and Pathologies

Diseases, pathologies, phenotypes, psychiatric conditions, side effects, and organism-level phenomena can be represented with the `pathology()` / `path()` function. We're aware that "pathology" is not only inappropriate, but also indelicate in some situations, so an update to the more general term "phenotype" will come with the next backwards-incompatible language update.

For now, disease pathologies like muscle hypotonia can be represented by:

```text
# long form
pathology(mesh:D009123 ! "Muscle Hypotonia")

# short form
path(mesh:D009123 ! "Muscle Hypotonia")
```

In general, a pathology can be encoded like an abundance, population, or biological process like:

```text
path(prefix:identifier [! name])
```

#### Recommended Nomenclatures

| prefix | name |
| :--- | :--- |
| [doid](https://registry.identifiers.org/registry/doid) | Disease Ontology |
| [efo](https://registry.identifiers.org/registry/efo) | Experimental Factor Ontology |
| [hpo](https://registry.identifiers.org/registry/hpo) | Human Phenotype Ontology |
| [mondo](https://registry.identifiers.org/registry/mondo) | Monarch Disease Ontology |
| [mesh](https://registry.identifiers.org/registry/mesh) | Medical Subject Headings |

#### Not Recommended Nomenclatures

| prefix | name | reason |
| :--- | :--- | :--- |
| icd9 | ICD 9 | Not maintained |
| [icd](https://registry.identifiers.org/registry/icd) | ICD 10 | Almost impossible to get data |
| icd11 | ICD 11 | You didn't even know there was a version 11, did you? |
| sdis | Selventa Diseases | Not maintained |

