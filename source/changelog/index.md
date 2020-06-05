# Changelog

## Summary of Changes for BEL v2.2

See [https://medium.com/bel-news/bel-v2-2-enhancements-cfb4b27b22cb](https://medium.com/bel-news/bel-v2-2-enhancements-cfb4b27b22cb)

## Summary of Changes for BEL v2.1

See [https://medium.com/bel-news/bel-2-1-enhancements-ac79b078ad5a](https://medium.com/bel-news/bel-2-1-enhancements-ac79b078ad5a)

## Summary of Changes for BEL v2.0

These additions and modifications enhance the BEL language by providing new representation capability \(e.g., DNA and RNA variants, protein cleavage fragments, cellular location of abundances\) and enabling the use of external vocabularies \(post-translational modifications, activities\).

### Variants

* Now represents sequence variants at DNA, RNA, and protein levels.
* Now represents multiple substitutions within the same gene/RNA/protein
* New BEL abundance modifier function`variant("")` / `var("")` is used for most variant types,

  replacing `substitution()` / `sub()` and `truncation()` / `trunc()`.

  [Human Genome Variation Society \(HGVS\)](http://www.hgvs.org/rec.html) nomenclature adopted to describe variants

  [Dunnen and Antonarakis, 2000](http://onlinelibrary.wiley.com/doi/10.1002/%28SICI%291098-1004%28200001%2915:1%3C7::AID-HUMU4%3E3.0.CO;2-N/pdf)

  within the `var("")` modifier function, expanding supported types of variation to include insertions,

  deletions, duplications as well as non-specific variants.

* Usage of [http://wiki.openbel.org/display/BLVD/Other+Functions\[\`fus\(\)\`](http://wiki.openbel.org/display/BLVD/Other+Functions[`fus%28%29`)\] changed. Instead of a modifier function for a gene/RNA/protein abundance, `fus()` is used to compose new entities that can be used in place of a namespace value for abundance functions.

### Protein Cleavage Fragments

* New abundance modifier function `fragment()` / `frag()` to be used within protein abundances

  to specify protein fragments based on amino acid sequence range.

### Post-Translational Protein Modifications

* The `proteinModification()` / `pmod()` abundance modifier function can now

  use external vocabularies \(e.g., [PSI-MOD](http://psidev.cvs.sourceforge.net/viewvc/psidev/psi/mod/data/PSI-MOD.obo)\)

  for modification types, enabling users to add types without requiring a language change.

* Now multiple `pmod()` expressions can be used within a protein abundance.

### Translocations and Cellular Location

* New abundance modifier function to specify location - `location()` / `loc()`.
* Change in [http://wiki.openbel.org/display/BLVD/Transformation+Functions\[\`translocation\(\)\`](http://wiki.openbel.org/display/BLVD/Transformation+Functions[`translocation%28%29`)\] / [http://wiki.openbel.org/display/BLVD/Transformation+Functions\[\`tloc\(\)\`](http://wiki.openbel.org/display/BLVD/Transformation+Functions[`tloc%28%29`)\] function format, to explicitly add BEL location functions to location arguments.

### Activity Functions

* The ten distinct BEL activity functions, e.g., `kinaseActivity()` / `kin()`, `catalyticActivity()` / `cat()`, `transcriptionalActivity()` / `tscript()`, are consolidated to a single activity function [http://wiki.openbel.org/display/BLVD/Process+Functions\#ProcessFunctions-act\(\)\[\`activity\(\)\`](http://wiki.openbel.org/display/BLVD/Process+Functions#ProcessFunctions-act%28%29[`activity%28%29`)\] / [http://wiki.openbel.org/display/BLVD/Process+Functions\#ProcessFunctions-act\(\)\[\`act\(\)\`](http://wiki.openbel.org/display/BLVD/Process+Functions#ProcessFunctions-act%28%29[`act%28%29`)\].
* New modifier function [http://wiki.openbel.org/display/BLVD/Process+Modifier+Function\[\`molecularActivity\(\)\`](http://wiki.openbel.org/display/BLVD/Process+Modifier+Function[`molecularActivity%28%29`)\] / [http://wiki.openbel.org/display/BLVD/Process+Modifier+Function\[\`ma\(\)\`](http://wiki.openbel.org/display/BLVD/Process+Modifier+Function[`ma%28%29`)\] can be used to specify specific activity types, using external vocabularies, e.g., [http://www.geneontology.org/GO.function.guidelines.shtml\[GO](http://www.geneontology.org/GO.function.guidelines.shtml[GO) Molecular Function\], or a default BEL vocabulary.

### Regulates Relationship

* New causal relationship `regulates` to represent cases where A is reported to affect B, but it cannot be determined if A increases or decreases B.

### BEL Script Format Changes

* Citation annotation requirement removed for **Name** field
* Citation annotation **DOI** and **URL** added as accepted types
* **BEL Script Evidence** Annotation renamed to **Support**
* BEL version set in document header

