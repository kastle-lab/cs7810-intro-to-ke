# Deliverable 6: Materialization of the Knowledge Graph
There are two components to this deliverable: materialization of the graph and executing SPARQL queries to test the graph.

### Materialization
* Deploy a triplestore. Choose one of [GraphDB](https://www.ontotext.com/products/graphdb/), [Stardog](https://www.stardog.com/), or [Apache Jena Fuseki](https://jena.apache.org/documentation/fuseki2/)
* Load `schema.ttl` into the triplestore.
* Modify the [materialization starter code][../templates/rdflib-starter.py] to ingest your data. It is recommended to have a series of these scripts which will run for each dataset that needs to be integrated.
* For each triplified dataset, load the respective `.ttl` into the triplestore

### Validation
* Create a `validation.md` file from the [template](../templates/validation.md).
* Take the list of competency questions from the `use-case.md` document. 
* For each competency question, generate a SPARQL query which will return the answer-set for that competency question.
* Execute each SPARQL query against the triplestore.
* Note the answer-set.