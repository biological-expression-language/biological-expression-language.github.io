# Genomic Relationships

These relationship types link related terms, like orthologous terms from two
different species or the `geneAbundance()` and `rnaAbundance()` terms for the
same namespace value.

In most cases, these relationships will be introduced by the BEL Namespace
resources, and are not needed for creation of BEL Statements and BEL Documents.

## Orthology

For terms A and B, `A orthologous B` indicates that A and B represent entities
in different species which are sequence similar and which are therefore
presumed to share a common ancestor. For example,

```bel
g(hgnc:391 ! AKT1) orthologous g(mgi:87986 ! Akt1)
```

indicates that the mouse and human AKT1 genes are orthologs.

## Transcription

For RNA abundance term R and gene abundance term G, `G transcribedTo R` or
`G :> R` indicates that members of R are produced by the transcription of
members of G. For example:

```bel
g(hgnc:391 ! AKT1) :> r(hgnc:391 ! AKT1)
```

indicates that the human AKT1 RNA is transcribed from the human AKT1 gene.

## Translation

For RNA abundance term R and protein abundance term P, `R translatedTo P` or
`R  P` indicates that members of P are produced by the translation of members
of R. For example:

```bel
# long form
r(HGNC:AKT1) translatedTo p(HGNC:AKT1)

# short form
r(HGNC:AKT1) >> p(HGNC:AKT1)
```
