## Reified Entities

### Composites

The `compositeAbundance()` / `composite()` is the BEL version of an `AND` statement. Like `complex()`, you can put a list of physical entities \(or biological processes?\) inside it to denote that two things have to be present/active at the same time.

The `compositeAbundance(<abundance term list>)` function takes a list of abundance terms. The `compositeAbundance()` or `composite()` function is used to represent cases where multiple abundances synergize to produce an effect. The list is unordered, thus different orderings of the arguments should be interpreted as the same term. This function should not be used if any of the abundances alone are reported to cause the effect. `compositeAbundance()` terms should be used only as subjects of statements, not as objects.

For example, IL-6 and IL-23 synergistically induce Th17 differentiation as in:

```text
composite(p(HGNC:IL6), complex(GO:"interleukin-23 complex")) increases bp(GO:"T-helper 17 cell differentiation")
```

#### Example

```text
# long form
compositeAbundance(proteinAbundance(HGNC:TGFB1), proteinAbundance(HGNC:IL6))

# short form
 composite(p(HGNC:TGFB1), p(HGNC:IL6))
```

### Reactions

The `reaction()` / `rxn()` function denotes the transformations from a set of abundances to another set of abundances. It is written like:

```text
reaction(reactants(<abundance term list1>), products(<abundance term list2>))
```

where the frequency or abundance of events in which members of the abundances in `<abundance term list1>` \(the reactants\) are transformed into members of the abundances in `<abundance term list2>` \(the products\).

For example, the reaction in which superoxides are dismutated into oxygen and hydrogen peroxide can be represented as:

```text
rxn(reactants(a(CHEBI:superoxide)), products(a(CHEBI:"hydrogen peroxide"), a(CHEBI: "oxygen")))
```

#### Example

This BEL Term represents the reaction in which the reactants phosphoenolpyruvate and ADP are converted into pyruvate and ATP.

```text
# long form
reaction(reactants(abundance(CHEBI:phosphoenolpyruvate), abundance(CHEBI:ADP)), products(abundance(CHEBI:pyruvate), abundance(CHEBI:ATP)))

# short form
rxn(reactants(a(CHEBI:phophoenolpyruvate), a(CHEBI:ADP)), products(a(CHEBI:pyruvate), a(CHEBI:ATP)))
```

### Fusions

Fusions are when two gene, RNA, or proteins are combine. The `fusion()` / `fus()` functions can be used in place of an identifier within a gene, RNA, or protein abundance function to represent a hybrid gene, or gene product formed from two previously separate genes.

The `fusion()` expressions take the general form:

```text
fus(prefix:identifier [! name], "range5'", prefix:identifier [! name], "range3'")
```

where the first `prefix:identifier` is for the 5-prime fusion partner, `range5'` is the sequence coordinates of the 5-prime partner, the second `prefix:identifier` is for the 3-prime partner, and `range3'` is the sequence coordinates for the 3' partner. Ranges need to be in quotes.

For example, the fusion between the RNA of TMPRSS2 and ERG can be encoded as:

```text
r(fus(hgnc:11876 ! TMPRSS2, "r.1_79", hgnc:3446 ! ERG, "r.312_5034"))
```

The **r.** designation in the range fields indicates that the numbering uses the RNA sequence as the reference. RNA sequence numbering starts at the transcription initiation site. You use **c.\_** for `g()` fusions and **p.\_** for `p()` fusions. These **r.**, **c.**, and **p.** designations come from HGVS.

If the breakpoints are unspecified for the 5-prime range or the 3-prime range, the `"?"` can be used like in:

```text
r(fus(hgnc:11876 ! TMPRSS2, "?", hgnc:3446 ! ERG, "?"))
```

**Example - Fusion of Proteins**

The abundances of fusion proteins resulting from chromosomal translocation mutations can be specified by using the `fusion()` or `fus()` function within a protein abundance term.

```text
# long form
p(fusion(hgnc:1014 ! BCR, "p.1_426", hgnc:6192 ! JAK2, "p.812_1132"))

# short form
p(fus(hgnc:1014 ! BCR, "p.1_426", hgnc:6192 ! JAK2, "p.812_1132"))
```

This term represents the abundance of a fusion protein of the 5' partner BCR and 3' partner JAK2, with the breakpoint for BCR at amino acid 426 and JAK2 at 812. _p._ indicates that the protein sequence is used for the range coordinates provided. If the breakpoint is not specified, the fusion protein abundance can be represented as:

**Example - Unspecified Fusion of Proteins**

```text
p(fus(HGNC:1014 ! BCR, "?", HGNC:6192 ! JAK2, "?"))
```

