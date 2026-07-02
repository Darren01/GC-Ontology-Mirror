## About this fork

This is a maintained fork of the Gainesville Core Ontology (GNVC v0.7), 
originally developed by Chemical Semantics, Inc. and mirrored by NFDI4Chem.

GNVC is a valuable ontology for publishing computational chemistry results, 
but v0.7 contains several structural defects that prevent clean import and 
use with current OWL tooling. This fork aims to repair those defects while 
preserving the original term IRIs and conceptual structure, and to extend 
coverage where gaps have been identified.

If you are the original author or a stakeholder in GNVC, we would welcome 
contact. The goal is to bring this ontology back into active maintenance, 
not to replace or compete with any future official release.

---

## Repairs in v0.8.0

The working file is `gc07_without_imports.owl`. The following structural 
defects from GNVC v0.7 have been repaired:

### Fix 1 — DAML periodic table import removed
GNVC v0.7 imported the DAML periodic table 
(http://www.daml.org/2003/01/periodictable/PeriodicTable.owl), a 2003-era 
precursor to OWL that is no longer resolvable. This import was removed and 
replaced with a local `gc:Element` stub class with a `rdfs:seeAlso` reference 
to ChEBI (http://purl.obolibrary.org/obo/CHEBI_33250).

### Fix 2 — QUDT namespace updated
GNVC referenced QUDT unit classes via the old NASA namespace 
(http://data.nasa.gov/qudt/owl/qudt#) which is no longer active. All 
references have been updated to the current QUDT namespace 
(http://qudt.org/schema/qudt/).

### Fix 3 — gc:Bond class/individual collision resolved
A cardinality restriction was incorrectly applied to gc:Bond as a named 
individual rather than as a class axiom. This has been corrected by moving 
the restriction to a proper owl:subClassOf axiom on the class.

### Fix 4 — gc:RHF/UHF/ROHF modelling corrected
gc:RHF was simultaneously declared as a class and a named individual. 
gc:RHF, gc:UHF, and gc:ROHF are now consistently modelled as subclasses 
of gc:SpinType, consistent with the dominant pattern used for methodology 
classes elsewhere in GNVC.

### Fix 5 — gc:hasFloatValue class/property collision resolved
gc:hasFloatValue was declared as both a datatype property and a class. 
The spurious class declaration was removed. The range of gc:hasMass was 
corrected from gc:hasFloatValue (a property) to gc:FloatValue (the 
correct class).

### Fix 6 — Meta-level domain/range declarations removed
gc:hasMolecularProperty and gc:hasAtomProperty had rdfs:Class and 
owl:ObjectProperty as domain/range values respectively. These meta-level 
constructs have been removed. The stray owl:ObjectProperty and rdfs:Class 
class declarations have also been removed.

### Fix 7 — UTF-8 encoding errors corrected
String literals containing non-ASCII characters were corrupted due to 
double-encoding. Affected terms: Schrödinger, Møller-Plesset.

### Fix 8 — gc:hasSystemMultiplicity consolidated
gc:hasSystemMultiplicity existed as both an object property and a datatype 
property with conflicting axioms. These have been consolidated into a single 
datatype property with correct domain (gc:MolecularSystem), range 
(xsd:positiveInteger), and complete annotations.

### Fix 9 — Ontology metadata updated
The ontology version has been bumped to 0.8.0 with a proper owl:versionIRI. 
dc:modified and dcterms:contributor annotations have been added. Stale 
commented-out import statements and encoding errors in the description have 
been removed.

---

## Quality improvements in v0.8.0

Beyond structural repairs, the following quality improvements have been made:

- Duplicate rdfs:label values resolved across 15 terms
- Missing rdfs:label annotations added to 13 terms
- QUDT unit class declarations given proper labels
- Multiple label conflicts resolved
- dcterms:license added in ROBOT-compatible form
- UTF-8 encoding errors fixed throughout

---

## Formal definitions (IAO:0000115) — work in progress

Formal OBO Foundry definitions have been added for the following terms, 
sourced from the IUPAC Gold Book (https://goldbook.iupac.org) and IUPAC 
PAC recommendations:

- gc:BasisSet — Gold Book BT06999
- gc:Atom — Gold Book A00493
- gc:Molecule — Gold Book M03986
- gc:Orbital — Gold Book O04317
- gc:WaveFunction — Gold Book W06659
- gc:DensityFunctional — PAC 1999, 71, 1919

Definitions for remaining terms are in progress. Contributions welcome — 
see open issues labelled `good first issue`.

The following review informed the design decisions in this fork:
https://doi.org/10.26434/chemrxiv-2024-fvzpq

---

## Original NFDI4Chem mirror note

This repository contains a copy of the Gainesville Core Ontology that was 
developed by Chemical Semantics in 2015. The NFDI4Chem terminology service 
created the original mirror because the original IRI no longer resolves.
The ontology was taken from this snapshot of the internet archive:
https://web.archive.org/web/20221005233201fw_/http://ontologies.makolab.com/gc/gc07.owl
Since this archived version imports outdated and unresolvable versions of 
BFO and QUDT, the associated import statements were commented out in the 
original mirror (see gc07_without_imports.owl).

---

## Contributing

If you would like to contribute definitions, bug fixes, or extensions:

1. Open an issue describing what you want to add or fix
2. Fork this repository
3. Make your changes to `gc07_without_imports.owl`
4. Verify with `xmllint --noout gc07_without_imports.owl` and 
   `robot convert --input gc07_without_imports.owl --output test.ttl`
5. Open a pull request

Issues labelled `good first issue` are suitable for new contributors and 
typically involve adding a formal IAO:0000115 definition to an existing term.
