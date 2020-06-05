# Entity Modifiers

While BEL terms and relations are the building bocks for BEL statements, there are a few things that can be added to make them much more rich.

## Edge Modifiers

### Molecular Activity

You might have noticed functions for representing chemicals, genes, RNAs, proteins, and all have the suffix `abundance`. Sometimes it makes more sense to talk about the activity of a physical entity being responsible \(as subject\) or modified \(as object\).

The `activity(<abundance>)` or `act(<abundance)` is used to specify events resulting from the molecular activity of an abundance. The `activity()` function provides distinct terms that enable differentiation of the increase or decrease of the molecular activity of a protein from changes in the abundance of the protein. `activity()` can be applied to a protein, complex, or RNA abundance term, and modified with a ```molecularActivity()`` argument to indicate a specific type of molecular activity.

```text
# long form
activity(p(hgnc:391 ! :AKT1))

# short form
act(p(hgnc:391 ! :AKT1))
```

To more specifically talk about what kind of activity a physical entity has, you can use the `molecularActivity()` or `ma()`. It comes after the BEL term inside the `act()` like below

```text
# long form
act(p(hgnc:391 ! AKT1), molecularActivity(kin))

# short form
act(p(hgnc:391 ! AKT1), ma(kin))

# using equivalent Gene Ontology
act(p(hgnc:391 ! AKT1), ma(go:0016301 ! "kinase activity"))
```

In general, the `ma()` function can be used like:

```text
ma(<default term>)

# OR

ma(prefix:identifier [! name])
```

The BEL default namespace has the following commonly used molecular activities, but it makes most sense to map these to entries in the Gene Ontology Molecular Function namespace.

| short | long | Gene Ontology | GO Label |
| :--- | :--- | :--- | :--- |
| cat | catalyticActivity | 0003824 | catalytic activity |
| chap | chaperoneActivity | 0044183 | protein binding involved in protein folding |
| gap | gapActivity | 0032794 | GTPase activating protein binding |
| gef | gefActivity | 0005085 | guanyl-nucleotide exchange factor activity |
| gtp | gtpBoundActivity | 0005525 | GTP binding |
| kin | kinaseActivity | 0016301 | kinase activity |
| pep | peptidaseActivity | 0008233 | peptidase activity |
| phos | phosphotaseActivity | 0016791 | phosphatase activity |
| ribo | ribosylationActivity | 0003956 | NAD\(P\)+-protein-arginine ADP-ribosyltransferase activity |
| tscript | transcriptionalActivity | 0001071 | nucleic acid binding transcription factor activity |
| tport | transportActivity | 0005215 | transporter activity |

#### Examples

**default BEL namespace, transcriptional activity \(DEFAULT namespace is optional\)**

```text
act(p(HGNC:FOXO1), ma(tscript))
```

**GO molecular function namespace, transcriptional activity**

```text
act(p(HGNC:FOXO1), ma(GO:"nucleic acid binding transcription factor activity"))
```

**default BEL namespace, kinase activity**

```text
act(p(HGNC:AKT1), ma(kin))
```

**GO molecular function namespace, kinase activity**

```text
act(p(HGNC:AKT1), ma(GO:"kinase activity"))
```

**Non-Specified Activities**

If the type of molecular activity is not reported, it does not need to be specified. The `activity()` function is sufficient for distinguishing the frequency of events mediated by an abundance from the amount of the abundance. This term represents the ligand-bound activity of the human non-catalytic receptor protein TLR7.

```text
# long form
activity(proteinAbundance(HGNC:TLR7))

# short form
act(p(HGNC:TLR7))
```

**Catalytic Activity**

A protein, complex, or ribozymes has catalytic activity when it acts as an enzymatic catalyst of biochemical reactions. Catalytic activity includes kinase, phosphatase, peptidase, and ADP-ribosylase activities, though these can be represented by more specific molecular activity terms.

This term represents the frequency of events in which the protein abundance of rat Sod1 acts as a catalyst.

```text
# Using BEL default namespace
act(p(RGD:Sod1), ma(cat))

# Using Gene Ontology
act(p(RGD:Sod1), ma(GO:"catalytic activity"))
```

**Peptidase Activity**

This term represents the frequency of events in which the protein abundance of mouse Casp3 acts as a peptidase.The more specific GO Molecular Function term "cysteine-type endopeptidase activity" is also applicable.

```text
# Using BEL default namespace
act(p(MGI:Casp3), ma(pep))

# Using Gene Ontology
act(p(MGI:Casp3), ma(GO:"peptidase activity"))
```

**G-proteins in the active \(GTP-bound\) state**

The activity of guanine nucleotide-binding proteins \(G-proteins\) like RAS in the active, GTP-bound state. This term represents the frequency of events caused by the active, GTP-bound form of the RAS protein family.

```text
# Using BEL default namespace
act(p(SFAM:"RAS Family"), ma(gtp))

# Using Gene Ontology
act(p(SFAM:"RAS Family"), ma(GO:"GTP binding"))
```

**Transporter Activity**

Molecular translocation events mediated by transporter proteins like ion channels or glucose transporters. This term represents the frequency of ion transport events mediated by the epithelial sodium channel \(ENaC\) complex.

```text
# Using BEL default namespace
act(complex(NCH:"ENaC Complex"), ma(tport))

# Using Gene Ontology
act(complex(NCH:"ENaC Complex"), ma(GO:"transporter activity"))
```

**Chaperone Activity**

This term represents the events in which the human Calnexin protein functions as a chaperone to aid the folding of other proteins.

```text
# Using BEL default namespace
act(p(HGNC:CANX), ma(chap))

# Using Gene Ontology
```

**Transcription Activity**

Events in which a protein or molecular complex acts to directly control transcription, including proteins acting directly as transcription factors, as well as transcriptional co-activators and co-repressors. This term represents the frequency of events in which the mouse p53 protein controls RNA expression.

```text
# Using BEL default namespace
act(p(MGI:Trp53), ma(tscript))

# Using Gene Ontology 
act(p(MGI:Trp53), ma(GO:"nucleic acid binding transcription factor activity"))
```

## Transformation Functions

The following BEL functions represent parametrized biological processes. Currently, BEL parametrizes translocation and degradation processes.

### Translocations

A `translocation(<abundance>, fromLocation(ns1:v1), toLocation(ns2:v2))` or `tloc(<abundance>, fromLoc(ns1:v1), toLoc(ns2:v2))` denotes the process in which a physical entity is moved from one location to another.

For example, endocytosis \(translocation from the cell surface to the endosome\) of the epidermal growth factor receptor \(EGFR\) protein can be represented as:

```text
# Long form
translocation(p(hgnc:3236 ! EGFR), fromLocation(go:0009986 ! "cell surface"), toLocaction(go:0005768 ! endosome))

# Short form
tloc(p(hgnc:3236 ! EGFR), fromLoc(go:0009986 ! "cell surface"), toLoc(go:0005768 ! endosome))
```

In general, the `fromLoc()` and `toLoc()` functions take in an identifier:

```text
toLoc(prefix:identifier [! name])
fromLoc(prefix:identifier [! name])
```

The most reasonable namespaces to use for locations are from the GO cellular components branch and maybe cell types. MeSH also contains locations, but are not recommended because of lack of mappings.

### Cell Secretion

This term represents the event in which human NFE2L2 protein is translocated from the cytoplasm to the nucleus.

```text
# long form
translocation(p(HGNC:NFE2L2), fromLoc(mesh:D003593 ! Cytoplasm), toLoc(mesh:D002467 ! "Cell Nucleus"))

# short form
tloc(p(HGNC:NFE2L2), fromLoc(mesh:D003593 ! Cytoplasm), toLoc(mesh:D002467 ! "Cell Nucleus"))
```

There are also two convenience functions, `cellSurfaceExpression()` and `cellSecretion()`, that are so common that they are part of BEL with pre-defined `toLoc()` and `fromLoc()`.

For example, the following represents secretion of mouse IL6 protein.

```text
# long form
cellSecretion(p(mgi:96559 ! Il6))

# short form
sec(p(mgi:96559 ! Il6))
```

### Cell Surface Expression

`cellSurfaceExpression(<abundance>)` or `surf(<abundance>)` denotes the frequency or abundance of events in which members of `<abundance>` move to the surface of cells. `cellSurfaceExpression(<abundance>)` can be equivalently expressed as:

```text
tloc(<abundance>, fromLoc(go:intracellular), toLoc(go:"cell surface"))
```

The intent of the `cellSurfaceExpression()` function is to provide a simple, standard means of expressing a commonly represented translocation.

For the abundance term A, `cellSecretion(<abundance>)` or `sec(<abundance>)` denotes the frequency or number of events in which members of `<abundance>` move from cells to regions outside of the cells. `cellSecretion(<abundance>` can be equivalently expressed as:

```text
tloc(<abundance>, fromLoc(go:intracellular), toLoc(go:"extracellular space"))
```

The intent of the `cellSecretion()` function is to provide a simple, standard means of expressing a commonly represented translocation.

This term represents cell surface expression of rat Fas protein.

```text
# long form
cellSurfaceExpression(p(rgd:619831 ! Fas))

# short form
surf(p(rgd:619831 ! Fas))
```

### Degradation

Events in which an abundance is degraded can be represented by the `degradation()` or `deg()` function.

`degradation(<abundance>)` or `deg(<abundance>)` denotes the frequency or number of events in which a member of `<abundance>` is degraded in some way such that it is no longer a member of `<abundance>`. For example, `degradation()` is used to represent proteasome-mediated proteolysis.

If can be inferred that:

```text
deg(X) directlyDecreases X
```

This term represents the degradation of MYC RNA. Degradation decreases the amount of the abundance - when degradation statements are compiled, a directlyDecreases relationship edge is added between the degradation term and the degraded entity.

```text
# long form
degradation(rnaAbundance(hgnc:7553 ! MYC))

# short form
deg(r(hgnc:7553 ! MYC))
```

**Note** the degradation relationship is not recommended, because it's more direct to just use the `decreases` relationship to show that the abundance is lowered.

## Cellular Location

Unlike the translocation process, each node can be annotated with the location where it is inside the cell with the `location()` / `loc()` function. It can be used as an argument within any abundance function except `compositeAbundance()` to represent a distinct subset of the abundance at that location. Location subsets of abundances have the general form:

```text
f(ns:v, loc(ns:v))
```

The location should come following all modifications and variants.

For example, the AKT protein in the cytoplasm can be encoded in BEL as:

```text
# long form
p(hgnc:391 ! AKT1, location(mesh:D003593 ! Cytoplasm))

# short form
p(hgnc:391 ! AKT1, loc(mesh:D003593 ! Cytoplasm))
```

While this information is written in the BEL term that is in either the subject or object, the fact that the entity is in a given location is actually metadata that is stored at the statement leve.

#### Example - Endoplasmic Reticulum pool of Ca^2+^

```text
a(chebi:29108 ! "calcium(2+)", loc(go:0005783 ! "endoplasmic reticulum"))
```

## Nested Statements

While most BEL statements take the form of `<subject> <predicate> <object>` where the subject and object may have some of the preceding modifiers attached, it is also possible to use an entire BEL statement as the object. This makes BEL a recursively defined language

Nested statements should only be curated when there is clear transitivity between the two statements and the relationships are casual.

For example, **GATA1** directly increases the process in which the activity of the **ZBTB16** protein directly increases the abundance of RNA designated by **MPL**. This can be encoded in BEL as:

```text
p(hgnc:4170 ! GATA1) => ( act(p(hgnc:12930 ! ZBTB16)) => r(hgnc:7217 ! MPL) )
```

If you are working in a network context, nested statements in the form of

```text
A P1 (B P2 C)
```

can be decomposed into

```text
A P1 B
B P2 C
A P1 * P2 C
```

Where `P1` and `P2` are predicates, and their product `P1 * P2` is increases if both are increases or both are decreases. Their product `P1 * P2` is decreases if one is decreases and the other is increases.

Another example: the CLSPN protein is considered to directly activate the phosphorylation of CHEK1 protein by the kinase activity of ATR, because the CLSPN and ATR proteins physically interact.

```text
p(hgnc:19715 ! CLSPN) => (act(p(hgnc:882 ! ATR), ma(kin)) => p(hgnc:1925 ! CHEK1, pmod(Ph)))
```
