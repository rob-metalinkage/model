Definitions extracted per namespace from profiled ontologies where configured library, imports and namespaces cannot be used to locate ontology resource.

Generated if -e (--extract) flag set

These will be expressed as a profile of the referenced namespace, and consist of a tTL file containing just the declarations used and other resources, such as a JSON-LD context for the profile.

This step allows for JSON-LD contexts to be be created in a modular fashion and accessible even when original ontology does not support this.

If a canonical context file is available, then this should be preconfigured in a profile catalog graph (-p {profile_cat1}.ttl,... )