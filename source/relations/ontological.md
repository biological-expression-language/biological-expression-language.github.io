# Ontological Relationships

In most cases, these relationships will be introduced by the BEL Namespace
resources, and are not needed for creation of BEL Statements and BEL Scripts.

## Parent/Child

For terms A and B, `A isA B` indicates that A is a subset of B.

All terms in BEL 1.0 represent classes, but given that classes implicitly have
instances, `A isA B` is interpreted to mean that any instance of A must also be
an instance of B. This relationship can be used to represent GO and MeSH
hierarchies:

```
pathology(MESH:Psoriasis) isA pathology(MESH:"Skin Diseases")
```

## Whole/Part

For terms A and B, `A partOf B` indicates that A is a part of B.

```
p(HGNC:CHUK)  partOf complex(GO:"IkappaB kinase complex")
p(HGNC:IKBKB) partOf complex(GO:"IkappaB kinase complex")
p(HGNC:IKBKG) partOf complex(GO:"IkappaB kinase complex")
```

## Equivalence

For terms A and B, `A equivalentTo B` / `A eq B` indicates that A and B are equivalent.
This relationship is two-way.
