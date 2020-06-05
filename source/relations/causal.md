# Causal Relationships

These relationship types denote a causal relationship, or the absence of a
causal relationship between a subject and an object term.

## Regulates

For terms A and B, `A regulates B` or `A reg B` indicate that A is reported to
have an effect on B, but information is missing about whether A increases B or
A decreases B. This relationship provides more information than association,
association, because the upstream entity (source term) and downstream entity
(target term) can be assigned.

This relationship is equivalent to RO:0002211.

There isn't currently a differentiation between direct regulation and indirect
regulation, so right now this should be considered as indirect.

## Increases

For terms A and B, `A increases B` or `A -> B` indicate that increases in A
have been observed to cause increases in B.

Depending on the terms A and B, this relationship can be used to describe a
phosphorylation event, the increase in the amount of a protein, the activation
of a protein, the transportation of a protein, or several other things.

## Directly Increases

For terms A and B, `A directlyIncreases B` or `A => B` indicates that increases
in A have been observed to cause increases in B and that the mechanism of the
causal relationship is based on physical interaction of entities related to A
and B. This is a Direct Relationships, direct version of the increases
relationship.

## Decreases

For terms A and B, `A decreases B` or `A -| B` indicate that increases in A
have been observed to cause decreases in B.

Depending on the terms A and B, this relationship can be used to describe a
dephosphorylation event, the decrease in the amount of a protein, the 
deactivation of a protein, the inhibition of the transportation of a protein,
or several other things.

## Directly Decreases

For terms A and B, `A directlyDecreases B` or `A =| B` indicates that increases
in A have been observed to cause decreases in B and that the mechanism of the
causal relationship is based on physical interaction of entities related to A
and B. This is a Direct Relationship, direct version of the decreases
relationship.

For example, the inhibition of the Patched 1 receptor signaling activity by
Hedgehog is represented as direct, because Hedgehog and Patched 1 physically
interact:

```bel
# long form
p(fplx:Hedgehog) directlyDecreases act(p(hgnc:9585 ! PTCH1))

# short form
p(fplx:Hedgehog) =| act(p(hgnc:9585 ! PTCH1))
```

### Example - Transcription Factors

In the case of transcriptional activity, if the protein performing the
transcriptional activity interacts with the gene that the RNA is transcribed
from, the relationship is considered direct. For example, repression of the
transcription of miR-21 by FOXO3 protein transcriptional activity is
represented as direct because FOXO3 binds the miR-21 promoter:

```bel
act(p(hgnc:3821 ! FOXO3), ma(tscript)) =| r(hgnc:31586 ! MIR21)
```

### Example - Self-referential relationships

Self-referential causal relationships are generally represented as direct.
For example, phosphorylation of GSK3B at serine 9 inhibiting the kinase
activity of GSK3B can be represented as:

```
p(hgnc:4617 ! GSK3B, pmod(Ph, Ser, 9)) =| act(p(hgnc:4617 ! GSK3B), ma(kin))
```

## Rate Limiting Step

For process, activity, or transformation term A and process term P,
`A rateLimitingStepOf P` indicates both:

```bel
A partOf bp(B)
A -> bp(B)
```

For example, the catalytic activity of HMG CoA reductase is a
rate-limiting step for cholesterol biosynthesis:

```bel
act(p(hgnc:5006 ! HMGCR), ma(go:0003824 ! "catalytic activity")) rateLimitingStepOf bp(go:0006695 ! "cholesterol biosynthetic process")
```

## Causes No Change

For terms A and B, `A causesNoChange B` or `A cnc B` indicate that B was
observed not to change in response to changes in A.

Statements using this relationship correspond to cases where explicit
measurement of B demonstrates lack of significant change, not for cases
where the state of B is unknown.
