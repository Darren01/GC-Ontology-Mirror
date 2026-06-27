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

This repository contains a copy of the Gainesville Core Ontology that was developed by Chemical Semantics in 2015.
We had to create this repo in order to be able to ingest this ontology for research purposes within the [NFDI4Chem Terminology Service](https://terminology.nfdi4chem.de), since the original IRI does not resolve anymore.
The ontology was taken from this snapshot of the internet archive: https://web.archive.org/web/20221005233201fw_/http://ontologies.makolab.com/gc/gc07.owl
Since this archived version imports outdated and unresolvable versions of BFO and QUDT, the associated import statements where commented out (see: https://github.com/NFDI4Chem/GC-Ontology-Mirror/blob/main/gc07_without_imports.owl#L20-L22).  

