# CYBELE Common Semantic Model Profiles

The CYBELE Common Semantic Model (CCSM) re-uses existing models and vocabularies such as DCAT, StatDCAT, GeoDCAT, INSPIRE, SSN ontology, QB vocabulary and PROV-O. 

The main class is derived from DCAT, dcat:Dataset, so the CCSM can be described as a profile of DCAT, however it will draw on a range of standard vocabularies, each of which can be used to profile DCAT in a project-independent fashion.

This directory contains a profile-oriented view of the CCSM derived from the authoritative CCSM OWL model and additional statements about profiling intent.

## Derivation methodology

The CCSM is refactored into a minimal profile using the [ProfileWiz toolkit] (https://github.com/RDFLib/profilewiz).

```cd /path/to/cybele/repo/profiles

python $PROFILEWIZ_REPO_PATH/profilewiz/profilewiz/profilewiz.py -n -a -q -p=lib/profile_cat.ttl -e -j -b https://w3id.org/cybele/model/proxy/ ../cybele-semantic-model.ttl```

This uses the prior extraction and caching of imported ontologies and any refactoring imposed on the imported ontologies - for example we could force a profile of GeoDCAT to be used if one was available with a canonical ontology, SHACL, JSON-LD context etc ready for re-use.

The steps to build the profile model from scratch are:

+ run profilewiz over the CCSM in interactive mode to build (or update) a profile catalog and cache local copies of imports
+ edit the profile catalog to
	* add any authoritative canonical forms  - e.g. JSON-LD context, for imported vocabularies.
	* declare the target profile hierarchy - *in this case we will declare new profiles of DCAT for PROV, QB, StatDCAT and GeoDCAT in an experimental OGC managed namespace, and declare that the target profile inherits from these.*
+ run this methodology over OWL files where available for each parent profile to build up an accurate model of which profile declares or constrains which object definitions.
+ run profilewiz in extraction mode to extract profile
+ refactor - move reusable constraints from extracted profile to imported general profiles where no master profile ontology exists (build up the reusable profiles)
+ rerun profilewiz using -ho and -hd ( HTML for OWL and HTML for profile ) mode to generate documentation using the refactored profile hierarchy.

## Why is this so complicated?

Because this is the complexity normally passed on to the ontology user to work out where all the pieces are and how a model relates to other similar profiles of common standards...


## TODO

1. update pyLODE to use and import closure and rdfs:isBefinedBy to style imported content differently
2. Generate SHACL shape constraints
3. Generate RDF-QB dimensional models (in interactive mode) or consume these in automated mode
