---
description: How to encode physical entities in BEL
---

# Entities

Throughout this tutorial, most functions have both a long and short form. For brevity, the long forms will be introduced, but thereafter the short forms will be used.

Two general categories of biological entities are represented as BEL Terms: **abundances** and **processes**.

### Physical Entities

Life science experiments often measure the abundance of a type of thing in a given sample or set of samples. BEL Abundance Terms represent classes of abundance, the abundances of specific types of things. Examples include the **protein abundance of TP53**, the **RNA abundance of CCND1**, the **abundance of the protein AKT1 phosphorylated at serine 21**, or the **abundance of the complex of the proteins CCND1 and CDK4**.

### Process Entities

BEL Process Terms represent classes of complex phenomena taking place at the level of the cell or the organism, such as the biological process of **cell cycle** or a disease process such as **Cardiomyopathy**. In other cases, BEL Terms may represent classes of specific molecular activities, such as the kinase activity of the AKT1 protein, or a specific chemical reaction like conversion of superoxides to hydrogen peroxide and oxygen.

Measurable biological parameters such as **Blood Pressure** or **Body Temperature** are represented as process BEL Terms. These BEL Terms denote biological activities that, when measured, are reduced to an output parameter.

### Reified Entities

BEL also allows for some kinds of entities to be defined based on other types, such as transient
complexes, chemical reactions, and composites (the logical AND operator in BEL).
