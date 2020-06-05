# Annotations

Each BEL Statement can optionally be annotated to express knowledge about the statement itself. Some important uses of annotations are to specify information about the:

* biological system in which the observation represented by the statement

  was made

* experimental methods used to demonstrate the observation
* knowledge source on which the statement is based, such as the citation

  and specific text supporting the statement

Examples of annotations that could be associated with a BEL Statement are the:

* PubMed ID specifying the publication in which the observation was reported
* Species, tissue, and cellular location in which the observations were made
* Dosage, exposure, and recovery time associated with the observation

## Setting Regular Annotations

Annotations always start with `SET <keyword>` where the keyword is either a standard prefix from [https://identifiers.org](https://identifiers.org), or a user-defined category that may encompass several namespaces.

Like identifiers, annotations can look a few different ways. Old-style BEL uses prefixes that correspond to the entity type and names like:

```text
# single
SET Anatomy = "muscle"

# multiple
SET Anatomy = {"muscle", "brain", "liver"}
```

This type of BEL is discouraged, becuase it's neither obvious what to what namespace `Anatomy` refers, nor to which entities `"muscle"` and others refer.

Newer BEL has two options. First, the direct prefix can be used like in

```text
# single
SET go = "0005634"
# single with OBO-style identifier
SET go = "0005634 ! nucleus"


# multiple
SET go = {"0005634", "0009986"}
# multiple with OBO-style identifier
SET go = {"0005634 ! nucleus", "0009986 ! cell surface"}
```

Second, the prefix can be set to a user-defined category, then full CURIEs should be used in the annotation like in:

```text
SET Compartment           = "go:0005634 ! nucleus"
SET CellLine              = "bto:0001938 ! human osteosarcoma cell line"
SET Taxonomy              = "taxonomy:9606 ! Homo sapiens"
SET ExperimentSetupSource = {"mi:0506", "mi:0331"}
SET ExperimentSetupTarget = {"mi:0331", "so:0001679"}
```

This syntax has been recommended in BEP-0013.

### Example - Species

Species annotations indicate the species context for experimental observation represented by the statement. It is good practice to unambiguously assign species context to BEL Statements, even though many BEL Terms are derived from a species-specific namespace \(e.g., HGNC, MGI, RGD\).

```text
SET Species = "taxonomy:9606 ! Homo sapiens."
```

### Other Annotation Types

Other types of annotations can be added to statements to indicate the context of the experimental observation supported by the statement, including cell line, cell type, and cellular location. The MI2CAST recommendations do a good job of outlining what are the preferred keywords for these annotations and what namespaces are appropriate.

## Unsetting Annotations

All annotations, including `Citation` and `Evidence` remain unset until the `UNSET <keyword>` is used. Alternatively, the special line `UNSET ALL` will unset all annotations.

Because most BEL curation begins with a citation, many curators do not unset the annotations and assume that they are reset when a new `SET Citation` is encountered. In some BEL compilers, this is the default behavior \(but it is configurable\).

## Setting the Citation

The most important annotation for each BEL statement is its citation using `SET Citation = ...`.

Citations are a special type of annotation that references the knowledge source that reports the observation that the statement is based on. Citations are composed of a document type, and a document reference ID. For example, the citation for a journal article indexed by PubMed would be encoded as:

```text
SET Citation = {"PubMed", "21533016"}
```

You'll notice that this acts differently than the previous annotations defined with multiple values. This represents old-style BEL. New style BEL will use CURIEs, as shown before. The equivalent new-style BEL will look like:

```text
SET Citation = "pubmed:21533016"
```

This will allow for more granular citations to be used, especially when referencing online resources.

## Setting the Evidence

The textual evidence is the special annotation in BEL. It is set with `SET Evidence = "<text>""` where the `<text>` comes from a research article directly. This is one of BEL's greatest strengths - most knowledge-capturing languages do not enable curators to capture this level of granularity.

```text
SET Support = "The p53 protein activates the transcription of cyclin-dependent kinase inhibitor, p21. p21 inactivates the CyclinE:Cdk2 complexes, and prevent entry of the cell into S phase, leading to G1 arrest."
```

Note: the `\` character can be used to introduce line breaks for long text blocks. Please be careful with whitespace when doing this!

Note: the BEL community isn't exactly sure whether `Evidence`, `Support`, or `SupportingText` is the official keyword for evidence, so all of them can be used interchangably.

