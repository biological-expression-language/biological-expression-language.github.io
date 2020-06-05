# Correlative Relationships

These relationship types link abundances and biological processes when
no causal relationship is known. The order of subject and object terms
does not matter in a statement with a correlative relationship, unlike
a statement with a causal relationship.

## Correlation

For terms A and B that are stated to be correlated, but not signified whether
it is positive or negative. This is more specific than the
[association](#association) relationship.

Will be added in BEL v2.3 with [BEP-0012](https://github.com/belbio/bep/pull/33).


## Negative Correlation

For terms A and B, `A negativeCorrelation B` or `A neg B` indicates that
changes in A and B have been observed to be negatively correlated. The order
of the subject and object does not affect the interpretation of the statement,
thus `B negativeCorrelation A` is equivalent to `A negativeCorrelation B`.

## Positive Correlation

For terms A and B, `A positiveCorrelation B` or `A pos B` indicates that
changes in A and B have been observed to be positively correlated. The order
of the subject and object does not affect the interpretation of the statement,
thus `B positiveCorrelation A` is equivalent to `A positiveCorrelation B`.

## No Correlation

For terms A and B that have been measured to not be correlated. The lack
of correlation between A and B can also be used to infer a lack of
causation.

Added in BEL v2.1 with [BEP-0003](http://bep.bel.bio/published/BEP-0003.html)
