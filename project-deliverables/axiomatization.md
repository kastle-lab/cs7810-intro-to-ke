# Conduct Systematic Axiomatization
This deliverable is comprised of two artifacts: `axioms.md` and `axioms.owl`.

1. Create an `axioms.md` file using the [template](../templates/axioms.md) and place in the `deliverables` directory.
2. Use the schema diagrams produced in the previous deliverable and iterate through each node-edge-node construction.
    * Identify from the list of axiom patterns provided during lecture which axioms apply for that construction.<br>
    **Note:** Patterns may already have these axioms provided.
    * Provide a natural language description of the instantiated axiom pattern.
    * Provide reasoning for why the axiom pattern has been selected as applicable in this case.
3. Consider if there are any axioms which must be addressed outside of the scope of the axioms patterns. 
    * These generally have a complex structure using `if...then` formulation or have `and`s or `or`s in them.
4. Use [Protégé](https://protege.stanford.edu/) to encode these axioms.
    * Choose an appropriate base URI for your ontology.
    * Render the ontology (i.e., the collection of axioms) in Turtle syntax with the name `schema.ttl` and place in the `schema` directory.

**Note:** Ensure that each member contributes to the artifact via explicit commits. Do not squash commits; the `git` history will serve as a record of participation and contribution.
