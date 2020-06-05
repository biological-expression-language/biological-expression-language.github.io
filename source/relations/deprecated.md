# Deprecated Relationships

These BEL v1.0 relationships are supported in BEL v2.0, but are slated to be
removed in the next major version.

## analogous

For terms A and B, `A analogousTo B` indicates that A and B represent
abundances or molecular activities which function in a similar manner, but do
not share sequence similarity or a common ancestor.

## biomarkerFor

For term A and process term P, `A biomarkerFor P` indicates that changes in or
detection of A is used in some way to be a biomarker for pathology or
biological process P.

## prognosticBiomarkerFor

For term A and process term P, `A prognosticBiomarkerFor P` indicates that
changes in or detection of A is used in some way to be a prognostic biomarker
for the subsequent development of pathology or biological process P.

## hasMember

For term abundances A and B, `A hasMember B` designates B as a member class of
A. A member class is a distinguished sub-class. A is defined as a group by all
of the members assigned to it. The member classes may or may not be overlapping
and may or may not entirely cover all instances of A. A term may not appear in
both the subject and object of the same hasMember statement.

## hasMembers

The `hasMembers` relationship is a special form which enables the assignment
of multiple member classes in a single statement where the object of the
statement is a set of abundance terms. A statement using `hasMembers` is
exactly equivalent to multiple `hasMember` statements. A term may not appear
in both the subject and object of the same `hasMembers` statement.

For the abundance terms A, B, C and D, `A hasMembers list(B, C, D)`
indicates that A is defined by its member abundance classes B, C and D.

## hasComponent

For complex abundance term A and abundance term B, `A hasComponent B`
designates B as a component of A, that complexes that are instances of A have
instances of B as possible components. Note that, the stoichiometry of A is not
described, nor is it stated that B is a required component. The use of
`hasComponent` relationships is complementary to the use of functionally
composed complexes and is intended to enable the assignment of components to
complexes designated by names in external vocabularies. The assignment of
components can potentially enable the reconciliation of equivalent complexes
at knowledge assembly time.

## hasComponents

The `hasComponents` relationship is a special form which enables the assignment
of multiple complex components in a single statement where the object of the
statement is a set of abundance terms. A statement using `hasComponents` is
exactly equivalent to multiple `hasComponent` statements. A term may not appear
in both the subject and object of the same +hasComponents+ statement.

For the abundance terms A, B, C and D, `A hasComponents list(B, C, D)`
indicates that A has components B, C and D.

## subProcessOf

For process, activity, or transformation term A and process term P,
`A subProcessOf P` indicates that instances of process P, by default, include
one or more instances of A in their composition. For example, the reduction
of HMG-CoA to mevalonate is a subprocess of cholesterol biosynthesis:

```bel
rxn( \
 reactants(a(CHEBI:"(S)-3-hydroxy-3-methylglutaryl-CoA"), a(CHEBI:NADPH), a(CHEBI:hydron)), \
 products(a(CHEBI:mevalonate), a(CHEBI:"CoA-SH"), a(CHEBI:"NADP(+)")) \
) subProcessOf bp(GOBP:"cholesterol biosynthetic process")
```
