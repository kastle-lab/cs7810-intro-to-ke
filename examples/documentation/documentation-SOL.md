# SOL of Life
**Authors:** Dave, Brandon Daniel, Miller, Ryan E., Noble, Megan T.

## Use Case Scenario
### Narrative 
The rich minerals on Earth remain a non-renewable resource for humans as they continue to refine the currently available resources to build products from everyday use items to hardware for technological advances. Due to the limited availability of rich minerals, humans will eventually need to branch out from Earth to other planetary bodies for mineral excavations. SOL Of Life plans to support the missions of space exploration and research by providing a tool to query collected data of asteroids within Sol, our solar system. Users of our tool could range anywhere from government entities, researchers, analysts, other space research institutions, and space enthusiasts. 

The available research and data can be cumbersome to navigate through. A knowledge graph is interesting in the case of mining in space because it is an uncharted frontier. There are so many questions that are difficult to answer surrounding the viability and cost. A knowledge graph would provide a method for answering those questions without the need for a specialized analyst to go out and make the various connections themselves from the existing research and data.

Our focus is on asteroids that can be found within approximately 2AU of Earth because of their potential for containing valuable minerals and a wealth of existing data. As defined by NASA, an asteroid exists as a space rock that orbits the sun with a size between 10 meters and 530 kilometers. 

Open source data provided by researchers and institutions such as Neil deGrasse Tyson, NASA, and Space Force, can be re-purposed into a knowledge graph to provide insight into excavation missions. With all of the data gathered together, the knowledge graph helps to filter the information into a readable state. Data that includes celestial body mineralogy predicted from infrared readings combined with data of the body’s trajectory path could be used together for humans to plan space missions in order to send out spacecrafts for mining expeditions. We also hope to serve humans of Planet Earth against celestial bodies that may be on a course for impact into the planet.  

### Competency Questions
1. What are the top 5 most frequently occuring minerals within 1.5 astronomical units from Earth in 2024?
2. What are the top 3 most occuring asteroid types within 1.5au from Earth in 2025?
3. Which is the closest asteroid to Earth in the next 24 months and when does that occur?
4. What are the 5 closest asteroids that may contain iron?
5. What are the 3 most potentially profitable asteroids within 0.75au of Earth in 2024?  
6. When will 162173 Ryugu be within 1au of Earth?
7. How long will 162173 Ryugu be within 1au of Earth?
8. Based on current trajectory of 162173 Ryugu, how far from Earth will 162173 Ryugu be in 8 months?
9. How much time is available until the 162173 Ryugu is within 1au of Earth?
10. Which asteroid is the first to come within 0.5au of Earth that contains iron?

### Integrated Datasets
Source: [Asterrank](https://www.asterank.com/)
- Asterank is built atop Nasa's Small Body Database to provide asteroid orbital data as well as estimates for asteroid value and distance metrics.  SOL of Life will contain a subset of Asterrank's data focusing on asteroid worth and distance metrics.

Source:  [Asteroid Spectral Types](https://en.wikipedia.org/wiki/Asteroid_spectral_types)
- Overview of the various Asteroid SMASSII classes and their properties.

Source: [MP3C](https://mp3c.oca.eu/)
- Similar to the Nasa-JPL Small Body Database, MP3C Asteroid Database also serves as a source for physcial and orbital data on asteroids.  MP3C's database is maintained by the Observatoire de la Côte d'Azur and includes measurements and observations on the orbital and physical properties of asteroids.  SOL of Life will utilize the MP3C's database as a secondary source for orbital data on asteroids.  

Source:  [Nasa-JPL: SBDB](https://ssd.jpl.nasa.gov/tools/sbdb_query.html)  
- Nasa-JPL Small Body Database (SBDB) serves as a well established and primary source for data on asteroids as well as other "small bodies".  The SBDB includes extensive information on orbital, physical, and historical properties.  SOL of Life will utilize the SBDB for data relating to orbital properties for asteroids.  

Source:  [Sky Live](https://theskylive.com/)
- Historical and Predictive measurements of celestial bodies given their orbital trajectory can be recorded from the Sky Live tool.


## Modules
<!-- There should be one module section per module (essentially per key-notion) -->

### Asteroid
**Source Pattern:** SOSA Feature of Interest  
**Source Data:** Asterank, MP3C, NASA_JPL  

#### Description
The domain of space objects are broken into three subcategories: Artificial Space Objects, Space Weather Phenomena, and Natural Space Objects.  Asteroids exist as a Natural Space Object where object can be further defined as a material object.  An Asteroid is represented by NASA as an object that orbits the sun of the Sol Solar System measuring 33 feet (10 meters) to 329 miles (530 kilometers).  For the SOL of Life, the only celestial body to be concerned with is Asteroid; therefore, the derived understanding begins with an OWL Thing consisting of multiple properties; such as, labeled naming conventions and quantitative measurable components of velocity, semi-major axis, and minimum orbit intersection distance.  Researchers have also predicted properties that benefit exomining operations such as the average profit gained after a mining excavation with consideration of the available valuable materials.  A subsumption is made for Asteroids into Near-Earth Asteroids when their semi-major axis measurement is within a threshold.  The SOSA pattern best reflects the usage of SOL of Life's knowledge graph with respect to the layer of Observations. Asteroids can be represented as a Feature of Interest with a Observations, a Classification, and a Distance Record.  
![Asteroid](https://github.com/meganthehorse/CS7810/tree/main/schema-diagrams/asteroid/asteroid.jpg)  

#### Axioms
1. * `Asteroid SubClassOf FeatureOfInterest` <br />
Every Asteroid is a Feature of Interest.
2. * `NearEarthAsteroid SubClassOf Asteroid` <br />
Every NearEarthAsteroid is an Asteroid.
3. * `Asteroid SubClassOf hasNumericID only xsd:int` <br />
The scoped range of hasNumericID, scoped by Asteroid, is an xsd:integer.
4. * `Asteroid SubClassOf hasNumericID exactly 1 xsd:int` <br />
Every Asteroid has exactly 1 Numeric ID. 
5. * `Asteroid SubClassOf hasCommonName only rdfs:Literal` <br />
The scoped range of hasCommonName, scoped by Asteroid, is an rdfs:Literal
6. * `Asteroid SubClassOf hasCommonName max 1 rdfs:Literal` <br />
Every Asteroid has at maximum 1 Common Name. 
7. * `Asteroid SubClassOf hasDiscoveryName only rdfs:Literal` <br />
The scoped range of hasDiscoveryName, scoped by Asteroid, is an rdfs:Literal
8. * `Asteroid SubClassOf hasDiscoveryName exactly 1 rdfs:Literal` <br />
Every Asteroid has exactly 1 Discovery Name.
9. * `Asteroid SubClassOf hasAsteroidClassification only AsteroidClassification` <br />
The scoped range of hasAsteroidClassification, scoped by Asteroid, is AsteroidClassification
10. * `Asteroid SubClassOf hasAsteroidClassification exactly 1 AsteroidClassification` <br />
Every Asteroid has exactly 1 AsteroidClassification.
11. * `Asteroid SubClassOf hasDistanceRecord only DistanceRecord` <br />
The scoped range of hasDistanceRecord, scoped by Asteroid, is DistanceRecord
12. * `Asteroid SubClassOf hasDistanceRecord min 0 DistanceRecord` <br />
Every Asteroid has at minimum 0 DistanceRecord.
13. * `Asteroid SubClassOf hasObservation only Observation` <br />
The scoped range of hasObservation, scoped by Asteroid, is Observation
14. * `Asteroid SubClassOf hasObservation min 1 Observation` <br />
Every Asteroid has at minimum 1 Observation.

### Asteroid Classification
**Source Pattern:** No Source Pattern  
**Source Data:** Asterank, Asteroid Spectral Types  

#### Description
The derived elemental composition of an Asteroid is a prediction based from infrared readings, as traveling to each individual asteroid remains an unrealistic task. As such, infrared reflections and readings are compared for similarities against known Earth elements and denote the components from the Asteroid's surface. The infrared data has been collected to formulate classifications among clusters of all asteroids for similarities of readings. The infrared readings and cluster family of similar asteroids result in a SMASSII classification which can be represented as a label. For our use case, we're only interested in the asteroid type as a label and decided to disregard the initial observation that lead to the classification.  
![Asteroid Classification](https://github.com/meganthehorse/CS7810/tree/main/schema-diagrams/asteroid-classification/asteroid-classification.jpg)

#### Axioms
1. * `AsteroidClassification SubClassOf EntityWithProvenance` <br />
Every AsteroidClassification is an Entity With Provenance .
2. * `AsteroidClassification SubClassOf hasSMASSIIClass only SMASSIIClass` <br />
The scoped range of hasSMASSIIClass, scoped by AsteroidClassification, is SMASSIIClass.
3. * `AsteroidClassification SubClassOf hasSMASSIIClass exactly 1 SMASSIIClass` <br />
Every AsteroidClassification has exactly 1 SMASSII Class.
4. * `ElementalComposition SubClassOf derivesFrom min 1 SMASSIIClass` <br />
Every ElementalComposition is derived from at minimum 1 SMASSII Class.
5. * `ElementalComposition SubClassOf hasElement only dbo:ChemicalElement` <br />
The scoped range of hasElement, scoped by ElementalComposition, is dbo:ChemicalElement.
6. * `ElementalComposition SubClassOf hasElement min 1 dbo:ChemicalElement` <br />
Every ElementalComposition has at minimum 1 Element.
7. * `SMASSIIClass SubClassOf hasElementalComposition only ElementalComposition` <br />
The scoped range of hasElementalComposition, scoped by SMASSIIClass, is ElementalComposition.
8. * `SMASSIIClass SubClassOf hasElementalComposition exactly 1 ElementalComposition` <br />
Every SMASSIIClass has exactly 1 ElementalComposition.
9. * `SMASSIIClass SubClassOf hasLabel only rdfs:Literal` <br />
The scoped range of hasLabel, scoped by SMASSIIClass, is an rdfs:Literal.
10. * `SMASSIIClass SubClassOf hasLabel exactly 1 rdfs:Literal` <br />
Every SMASSIIClass has exactly 1 Label.

### Distance Record
**Source Pattern:** MODL's Record  
**Source Data:** SkyLive  

#### Description
The end-goal of SOL of Life is to provide insight at a specific point of time for whether an Asteroid is within a means of distance for exomining companies to travel to for mineral extraction operations. As such, the spatial coordinates of an Asteroid is less important than the actual distance from Earth, which acts as a baseline for exomining operations. We used the Record pattern for distance from Earth because it accounts for some Event that occurs at a specific point in time. For our ontology, the Event is simplified as a result for a quantifiable metric for distance from Earth.  
![Distance Record](https://github.com/meganthehorse/CS7810/tree/main/schema-diagrams/distance-record/distance-record.jpg)

#### Axioms
1. * `DistanceRecord SubClassOf EntityWithProvenance` <br />
Every DistanceRecord is an Entity With Provenance.
2. * `DistanceRecord SubClassOf hasResult exactly 1 Result` <br />
Every DistanceRecord has exactly 1 Result.
3. * `DistanceRecord SubClassOf hasTemporalExtent only TemporalExtent` <br />
The scoped range of hasTemporalExtent, scoped by DistanceRecord, is TemporalExtent.
4. * `DistanceRecord SubClassOf hasTemporalExtent exactly 1 TemporalExtent` <br />
Every DistanceRecord has exactly 1 Temporal Extent.
5. * `TemporalExtent SubClassOf recordedAt only xsd:dateTime` <br />
The scoped range of recordedAt, scoped by TemporalExtent, is an xsd:date.  
6. * `TemporalExtent SubClassOf recordedAt exactly 1 xsd:dateTime` <br />
Every TemporalExtent has exactly 1 xsd:date.  

### Entity With Provenance
**Source Pattern:** MODL's Entity With Provenance  
**Source Data:** Asterank, MP3C, NASA_JPL, Skylive

#### Description
Attributes of asteroids can fit into the Entity With Provenance pattern provided by MODL. Most of our data is gathered by experts in astronomy, such as NASA and MP3C. Using this pattern allows for our end users to trace our data back to a source and the agent or organization that performed the data collection.  
![Entity With Provenance](https://github.com/meganthehorse/CS7810/tree/main/schema-diagrams/entity-with-provenance/entity-with-provenance.jpg)

#### Axioms
1. * `EntityWithProvenance SubClassOf generatedBy only ProvenanceActivity` <br />
The scoped range of generatedBy, scoped by EntityWithProvenance, is ProvenanceActivity.
2. * `EntityWithProvenance SubClassOf generatedBy exactly 1 ProvenanceActivity` <br />
Every EntityWithProvenance is generated by exactly 1 Provenance Activity.
3. * `EntityWithProvenance SubClassOf attributedTo only Agent` <br />
The scoped range of attributedTo, scoped by EntityWithProvenance, is Agent.
4. * `EntityWithProvenance SubClassOf attributedTo exactly 1 Agent` <br />
Every EntityWithProvenance is attributed to by exactly 1 Agent.
5. * `ProvenanceActivity SubClassOf performedBy only Agent` <br />
The scoped range of performedBy, scoped by ProvenanceActivity, is Agent.
6. * `ProvenanceActivity SubClassOf performedBy exactly 1 Agent` <br />
Every ProvenanceActivity is performed by exactly 1 Agent.
7. *  `ProvenanceActivity SubClassOf hasDescription only xsd:string` <br />
The scoped range of hasDescription, scoped by ProvenanceActivity, is an xsd:string.
8. *  `ProvenanceActivity SubClassOf hasDescription exactly 1 xsd:string` <br />
Every ProvenanceActivity has exactly 1 Description.
9. *  `Agent SubClassOf hasName only xsd:string` <br />
The scoped range of hasName, scoped by Agent, is an xsd:string.
10. *  `Agent SubClassOf hasName exactly 1 xsd:string` <br />
Every Agent has exactly 1 Name.

### Observation
**Source Pattern:** SOSA Observation  
**Source Data:** Asterank, MP3C, NASA_JPL  

#### Description
Data that describes Asteroids can be represented as Observations from the SOSA pattern which consists of the property that describes the observation along with the quantifiable value. The description of the property follows SOSA's ObservableProperty pattern, and the value follows the aforementioned Result pattern.  With that in mind, the measurable data; such as, mass, value, and velocity are represented as an instance of an Observation.  
![Observation](https://github.com/meganthehorse/CS7810/tree/main/schema-diagrams/observation/observation.jpg)  

#### Axioms
1. * `Observation SubClassOf hasFeatureOfInterest only Asteroid` <br />
The scoped range of hasFeatureOfInterest, scoped by Observation, is Asteroid.
2. * `Observation SubClassOf hasFeatureOfInterest exactly 1 Asteroid` <br />
Every Observation has exactly 1 Feature of Interest, which is an Asteroid.
3. * `Observation SubClassOf hasObservableProperty only ObservableProperty` <br />
The scoped range of hasObservableProperty, scoped by Observation, is ObservableProperty.
4. * `Observation SubClassOf hasObservableProperty exactly 1 ObservableProperty` <br />
Every Observation has exactly 1 ObservableProperty.
5. * `Observation SubClassOf hasResult exactly 1 Result` <br />
Every Observation has exactly 1 Result.
6. * `Observation SubClassOf EntityWithProvenance` <br />
Every Observation is an Entity With Provenance.
7. * `EconomicProperty SubClassOf ObservableProperty` <br />
Every EconomicProperty is an Observable Property.
8. * `OrbitalProperty SubClassOf ObservableProperty` <br />
Every OrbitalProperty is an Observable Property.
9. * `PhysicalProperty SubClassOf ObservableProperty` <br />
Every PhysicalProperty is an Observable Property.

### Result
**Source Pattern:** MODL's Result and Quantity  
**Source Data:** Asterank, MP3C, NASA_JPL  

#### Description
A Result pattern is used to describe the quantifiable values in the properties of an Asteroid. In our case, the Result notion has a Quantity associated with it, which is a pattern in MODL. A Quantity consists of a Quantity Kind, which is the description indicating the Result's usage, along with the quantifiable value and unit of measurement. Similarly to how controlled vocabularies are used in the Enslaved Ontology, we implement them as a means of scalability of our ontology. They are considered to be separate from the actual ontology yet complement it. A Quantity Kind as controlled vocabulary can consist of, but is not limited to mass, distance from Earth, and velocity. A Unit as controlled vocabulary can consist of, but is not limited to km/s, kg, and AU.  
![Result](https://github.com/meganthehorse/CS7810/tree/main/schema-diagrams/result/result.jpg)

#### Axioms
1. *  `Quantity SubClassOf hasQuantityValue only QuantityValue` <br />
The scoped range of hasQuantityValue, scoped by Quantity, is QuantityValue.
2. *  `Quantity SubClassOf hasQuantityKind only QuantityKind` <br />
The scoped range of hasQuantityKind, scoped by Quantity, is QuantityKind.
3. *  `Quantity SubClassOf hasQuantityKind exactly 1 QuantityKind` <br />
Every Quantity has exactly 1 Quantity Kind.
4. *  `Result SubClassOf hasQuantity only Quantity` <br />
The scoped range of hasQuantity, scoped by Result, is Quantity.
5. *  `Quantity SubClassOf hasQuantityValue exactly 1 QuantityValue` <br />
Every Quantity has exactly 1 Quantity Value.
6. *  `Result SubClassOf hasQuantity exactly 1 Quantity` <br />
Every Result has exactly 1 Quantity.
7. *  `QuantityValue SubClassOf hasNumericValue only xsd:double` <br />
The scoped range of hasNumericValue, scoped by QuantityValue, is an xsd:double.
8. *  `QuantityValue SubClassOf hasNumericValue exactly 1 xsd:double` <br />
Every QuantityValue has exactly 1 Numeric Value.
9. *  `QuantityValue SubClassOf hasUnit only Unit` <br />
The scoped range of hasUnit, scoped by QuantityValue, is Unit.
10. *  `QuantityValue SubClassOf hasUnit exactly 1 Unit` <br />
Every QuantityValue has exactly 1 Unit.
11. *  `Result SubClassOf  inverse (hasResult) exactly 1 (Observation or DistanceRecord)` <br />
Every Result belongs to exactly 1 Observation or DistanceRecord.

#### Remarks
* A result can be associated with a DistanceRecord or an Observation

## The Overall Knowledge Graph
### Namespaces
* @base <http://www.soloflife.org> .
* @prefix sol-ont: <http://soloflife.org/lod/ontology/> .
* @prefix sol-qk: <http://soloflife.org/lod/quantitykinds> .
* @prefix sol-unit: <http://soloflife.org/lod/units> .
* @prefix solr: <http://soloflife.org/lod/resource/> .

### All-Together
![image](https://github.com/meganthehorse/CS7810/tree/main/schema-diagrams/all-together/all-together.jpg)

# Materialization
The following directory contains all scripts used throughout the triplification of datasets and the materialization of the knowledge graph.  Triplification is done separately for each dataset used.

[Scripts for Triplification and Materialization](https://github.com/meganthehorse/CS7810/tree/main/code/)

# Validation

## 1. Top 5 Most Frequently Occurring Minerals
**Competency Question:** "What are the top 5 most frequently occuring minerals within 1.5 astronomical units from Earth in 2024?"

**Bridged Datasets:** 
sbdb_jpl_asteroids_with_constraints.csv, Asterank.csv, Summary_of_Asteroid_Taxonomic_Classes.csv

**SPARQL Query:**
```sql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX so: <http://schema.org/>
PREFIX time: <http://www.w3.org/2006/time#>
PREFIX sol-ont: <http://soloflife.org/lod/ontology/>
PREFIX solr: <http://soloflife.org/lod/resource/>

SELECT (?e as ?Element) (count(?e) as ?CountOfElement)
WHERE {
  {
    ?asteroid a sol-ont:Asteroid .
    ?asteroid sol-ont:hasCommonName ?name .
    ?asteroid sol-ont:hasDistanceRecord ?record .
    ?record sol-ont:hasTemporalExtent ?te .
    ?te sol-ont:recordedAt ?time .
    ?asteroid sol-ont:hasAsteroidClassification ?type .
    ?type sol-ont:hasSMASSIIClass ?class.
    ?class sol-ont:hasElementalComposition ?EC .
    ?EC sol-ont:hasElement ?e .
    ?record sol-ont:hasResult ?r. 
    ?r sol-ont:hasQuantity ?q.
    ?q sol-ont:hasQuantityValue ?qv .
    ?qv sol-ont:hasNumericValue ?distance .
    FILTER(
      ?distance < 1.5 &&
      (?time >= "2024-01"^^xsd:gYearMonth &&
      ?time < "2025-01"^^xsd:gYearMonth)
    )
  } 
}
GROUP BY ?e
ORDERBY DESC (?CountOfElement)
LIMIT 5
```

**Results:**
|Element |CountOfElement|
|--------|--------------|
|iron    |10            |
|ammonia |7             |
|hydrogen|7             |
|nitrogen|7             |
|cobalt  |6             |

## 2. Top 3 Most Occurring Asteroid Types
**Competency Question:** "What are the top 3 most occuring asteroid types within 1.5au from Earth in 2025?"

**Bridged Datasets:** sbdb_jpl_asteroids_with_constraints.csv, Asterank.csv, Summary_of_Asteroid_Taxonomic_Classes.csv

**SPARQL Query:**
```sql
SELECT (?class as ?AsteroidType) (count(?class) as ?CountOfTypes)
WHERE {
  {
    ?asteroid a sol-ont:Asteroid ;
		sol-ont:hasCommonName ?name.
    ?asteroid sol-ont:hasAsteroidClassification ?type .
    ?type sol-ont:hasSMASSIIClass ?class.
    ?asteroid sol-ont:hasDistanceRecord ?record .
    ?record sol-ont:hasTemporalExtent ?te .
    ?te sol-ont:recordedAt ?time .
    ?record sol-ont:hasResult ?r. 
    ?r sol-ont:hasQuantity ?q.
    ?q sol-ont:hasQuantityValue ?qv .
    ?qv sol-ont:hasNumericValue ?distance .
    FILTER(
      (?time >= "2025-01"^^xsd:gYearMonth &&
      ?time < "2026-01"^^xsd:gYearMonth) &&
      ?distance < 1.5
    )
  } 
}
GROUP BY ?class
ORDERBY DESC (?CountOfTypes)
LIMIT 3
```
**Results:**
|AsteroidType|CountOfTypes|
|------------|------------|
|< http://soloflife.org/lod/resource/Cg >|4           |
|< http://soloflife.org/lod/resource/B >|3           |
|< http://soloflife.org/lod/resource/Xk >|1           |

## 3. Closest Asteroids In 2 Years Window
**Competency Question:** "Which is the closest asteroid to Earth in the next 24 months and when does that occur?"

**Bridged Datasets:** sbdb_jpl_asteroids_with_constraints.csv, Asteroid_Distances.csv 

**SPARQL Query:**
```sql
SELECT ?name ?time ?distance ?unit
WHERE {
  {
    SELECT *
    WHERE {
    ?asteroid a sol-ont:Asteroid .
    ?asteroid sol-ont:hasCommonName ?name .
    ?asteroid sol-ont:hasDistanceRecord ?record
    }
  } . 
  {
    SELECT *
    WHERE {
      ?record a sol-ont:DistanceRecord .
      ?record sol-ont:hasTemporalExtent ?te .
      ?te sol-ont:recordedAt ?time .
      ?record sol-ont:hasResult ?r .
      ?r sol-ont:hasQuantity ?q .
      ?q sol-ont:hasQuantityValue ?qv .
      ?qv a sol-ont:QuantityValue;
         sol-ont:hasNumericValue ?distance;
         sol-ont:hasUnit ?unit .
      FILTER( 
        ?time >= "2023-01"^^xsd:gYearMonth &&
        ?time <= "2025-05"^^xsd:gYearMonth
      )
    }
    ORDERBY ASC(?distance)
  }
}
```
**Results:**
| name    | time    | distance | unit |
|---------|---------|----------|------|
| Didymos | 2023-01 | 0.27677  | au   |
| Bennu   | 2024-05 | 0.42804  | au   |
| Ryugu   | 2025-05 | 0.44189  | au   |
| Bennu   | 2025-01 | 0.52983  | au   |
| Bennu   | 2023-08 | 0.5301   | au   |
| Bennu   | 2024-08 | 0.54087  | au   |
| Ryugu   | 2024-11 | 0.55874  | au   |
| Didymos | 2025-01 | 0.56544  | au   |
| Didymos | 2024-08 | 0.61461  | au   |
| Bennu   | 2025-05 | 0.64079  | au   |
| Didymos | 2024-11 | 0.64674  | au   |
| Ryugu   | 2025-01 | 0.66498  | au   |
| Bennu   | 2024-11 | 0.7039   | au   |
| Bennu   | 2023-11 | 0.71025  | au   |

* Remarks:  
Additional results are listed to better represent a query on our knowledge graph.  The appropriate answer for the above question would be the first result with `Didymos` with distance at 0.27677.  A Limit can be added to only show the `Didymos` result.  

## 4. Top 5 Closest Iron Asteroids
**Competency Question:** "What are the 5 closest asteroids that may contain iron?"

**Bridged Datasets:** sbdb_jpl_asteroids_with_constraints.csv, Asteroid_Distances.csv, Summary_of_Asteroid_Taxonomic_Classes.csv
```sql
SELECT Distinct ?name
WHERE {
  ?asteroid a sol-ont:Asteroid;
  	sol-ont:hasCommonName ?name;
    sol-ont:hasAsteroidClassification ?class;
  	sol-ont:hasDistanceRecord ?record.
  ?record sol-ont:hasResult ?r. 
  ?r sol-ont:hasQuantity ?q.
  ?q sol-ont:hasQuantityValue ?qv .
  ?qv sol-ont:hasNumericValue ?distance .
  ?class a sol-ont:AsteroidClassification;
    sol-ont:hasSMASSIIClass ?smassii.
  ?smassii sol-ont:hasElementalComposition ?ec.
  ?ec sol-ont:hasElement ?e.
  FILTER(?e = "iron"^^sol-ont:ChemicalElement)
}
ORDERBY ASC(?distance)
```

**Results:**
| name |  
| :----: | 
| Didymos |
| Ryugu |
| Bennu |

## 5. Top 3 Profitable Asteroids in 2024
**Competency Question:** "What are the 3 most potentially profitable asteroids within 0.75au of Earth in 2024?"

**Bridged Datasets:** Asteroid_Distances.csv, Asterank_Dataset.csv

```sql
SELECT distinct ?name 
WHERE{
  {
	?asteroid sol-ont:hasCommonName ?name ;
    	sol-ont:hasDistanceRecord ?record ;
    	sol-ont:hasObservation ?obs .
    ?obs sol-ont:generatedBy ?activity .
    ?obs sol-ont:hasResult ?result .
    ?result sol-ont:hasQuantity ?q .
    ?q sol-ont:hasQuantityValue ?qv .
    ?qv sol-ont:hasNumericValue ?profit .
    ?record sol-ont:hasResult ?recordResult .
    ?record sol-ont:hasTemporalExtent ?te .
    ?te sol-ont:recordedAt ?time .
  	?recordResult sol-ont:hasQuantity ?recQ .
    ?recQ sol-ont:hasQuantityValue ?recQV .
    ?recQV sol-ont:hasNumericValue ?distance .
  }  
FILTER(
    ?activity=<http://soloflife.org/lod/resource/ProfitMeasurementActivity> &&
    (?time >= "2024-01"^^xsd:gYearMonth &&
      ?time <= "2024-11"^^xsd:gYearMonth)&&
    ?distance < 0.75
)
}
ORDERBY DESC(?profit)
```
**Results:** 
|name   |
|-------|
|Ryugu  |
|Didymos|
|Bennu  |

## 6. Ryugu Arriving
**Competency Question:** "When will 162173 Ryugu be within 1au of Earth?"

**Bridged Datasets:** sbdb_jpl_asteroids_with_constraints.csv, Asteroid_Distances.csv

**SPARQL Query:**
```sql
SELECT ?distance ?time
WHERE {
  {
    ?asteroid a sol-ont:Asteroid ;
  				sol-ont:hasCommonName "Ryugu".
    ?asteroid sol-ont:hasDistanceRecord ?record .
    ?record sol-ont:hasTemporalExtent ?te .
    ?te sol-ont:recordedAt ?time .
    ?record sol-ont:hasResult ?r. 
    ?r sol-ont:hasQuantity ?q.
    ?q sol-ont:hasQuantityValue ?qv .
    ?qv sol-ont:hasNumericValue ?distance .
    FILTER(
      ?distance < 1)
  }}
```

**Results:**
| distance | time    |
|----------|---------|
| 0.8274   | 2024-08 |
| 0.55874  | 2024-11 |
| 0.66498  | 2025-01 |
| 0.44189  | 2025-05 |
| 0.6127   | 2025-08 |
| 0.83492  | 2029-05 |
| 0.3926   | 2029-08 |
| 0.67229  | 2029-11 |
| 0.69894  | 2030-01 |
| 0.66023  | 2030-05 |

## 7. Ryugu Length of Stay
**Competency Question:** "How long will 162173 Ryugu be within 1au of Earth?"

**Bridged Datasets:** sbdb_jpl_asteroids_with_constraints.csv, Asteroid_Distances.csv

**SPARQL Query:**
```sql
SELECT ?timeStart ?timeEnd ?duration
WHERE {  
  {
    SELECT ?timeStart 
    WHERE{
        ?asteroid sol-ont:hasCommonName ?name ;
              sol-ont:hasDistanceRecord ?record .
        ?record sol-ont:hasTemporalExtent ?te .
        ?te sol-ont:recordedAt ?timeStart .
        ?record sol-ont:hasResult ?r .
        ?r sol-ont:hasQuantity ?q .
        ?q sol-ont:hasQuantityValue ?qv .
        ?qv a sol-ont:QuantityValue;
        sol-ont:hasNumericValue ?distance;
        sol-ont:hasUnit ?unit .      
        Filter(
            ?name="Ryugu"
            && ?distance < 1
        ) 
      }ORDERBY(?timeStart) LIMIT 1
  }
  .
  {
    SELECT ?timeEnd
    WHERE{
        ?asteroid sol-ont:hasCommonName ?name ;
                sol-ont:hasDistanceRecord ?record .
        ?record sol-ont:hasTemporalExtent ?te .
        ?te sol-ont:recordedAt ?timeEnd .
        ?record sol-ont:hasResult ?r .
        ?r sol-ont:hasQuantity ?q .
        ?q sol-ont:hasQuantityValue ?qv .
        ?qv a sol-ont:QuantityValue;
        sol-ont:hasNumericValue ?distance;
        sol-ont:hasUnit ?unit .      
        Filter(
            ?name="Ryugu"
            && ?distance > 1
        )
      } 
  }
  FILTER(?timeEnd>?timeStart)
  BIND((?timeEnd-?timeStart) as ?duration)
} LIMIT 1
```

**Results:**
| timeStart | timeEnd | duration         |
|-----------|---------|------------------|
| 2024-08   | 2025-11 | P457DT0H0M0.000S |

## 8. Ryugu Distance After Range
**Competency Question:** "Based on current trajectory of 162173 Ryugu, how far from Earth will 162173 Ryugu be in 8 months?"

**Bridged Datasets:** sbdb_jpl_asteroids_with_constraints.csv, Asteroid_Distances.csv


**SPARQL Query:**
```sql
SELECT ?Asteroid ?distance ?Unit
WHERE {
      ?Asteroid a sol-ont:Asteroid .
      ?Asteroid sol-ont:hasCommonName "Ryugu" .   
      ?Asteroid sol-ont:hasDistanceRecord ?d .
      ?d sol-ont:hasTemporalExtent ?time .
      ?time sol-ont:recordedAt "2024-01"^^xsd:gYearMonth .
      ?d sol-ont:hasResult ?r .
      ?r sol-ont:hasQuantity ?q .
      ?q sol-ont:hasQuantityValue ?qv .
      ?qv sol-ont:hasNumericValue ?distance .  
  		?qv sol-ont:hasUnit ?Unit .
} 
```
**Results:**
| Asteroid | distance | Unit |
| :----: | :----: | :----: |
| Ryugu | 2.06539e0 | au |


## 9. Planning for Ryugu
**Competency Question:** "How much time is available until the 162173 Ryugu is within 1au of Earth?"

**Bridged Datasets:** sbdb_jpl_asteroids_with_constraints.csv, Asteroid_Distances.csv

**SPARQL Query:**
```sql
SELECT ?timeEnter ?distance1 ?timeArrive ?distance2 ?TimeRemaining
WHERE {  
  {
    SELECT ?timeEnter ?distance1
    WHERE{
        ?asteroid sol-ont:hasCommonName ?name ;
              sol-ont:hasDistanceRecord ?record .
        ?record sol-ont:hasTemporalExtent ?te .
        ?te sol-ont:recordedAt ?timeEnter .
        ?record sol-ont:hasResult ?r .
        ?r sol-ont:hasQuantity ?q .
        ?q sol-ont:hasQuantityValue ?qv .
        ?qv a sol-ont:QuantityValue;
        sol-ont:hasNumericValue ?distance1;
        sol-ont:hasUnit ?unit .      
        Filter(
            ?name="Ryugu"
            && ?distance1 > 1
        ) 
      }ORDERBY(?timeEnter) LIMIT 1
  }
  .
  {
    SELECT ?timeArrive ?distance2
    WHERE{
        ?asteroid sol-ont:hasCommonName ?name ;
                sol-ont:hasDistanceRecord ?record .
        ?record sol-ont:hasTemporalExtent ?te .
        ?te sol-ont:recordedAt ?timeArrive .
        ?record sol-ont:hasResult ?r .
        ?r sol-ont:hasQuantity ?q .
        ?q sol-ont:hasQuantityValue ?qv .
        ?qv a sol-ont:QuantityValue;
        sol-ont:hasNumericValue ?distance2;
        sol-ont:hasUnit ?unit .      
        Filter(
            ?name="Ryugu"
            && ?distance2 < 1
        )
      } LIMIT 1
  }
  FILTER(?timeArrive>?timeEnter)
  BIND((?timeArrive-?timeEnter) as ?TimeRemaining)
}  
```
**Results:**
| timeEnter | distance1 | timeArrive | distance2 | timeRemaining     |
|-----------|-----------|------------|-----------|-------------------|
| 2023-01   | 2.38984e0 | 2024-08    | 0.8274e0  | P577DT23H0M0.000S |

* Remarks:  
An improvement for the query would include additional results that included differing time ranges and the respective time remaining durations for an Asteroid's orbital length of stay within 1au of Earth.  

## 10. Iron Arrival
**Competency Question:** "Which asteroid is the first to come within 0.5au of Earth that contains iron?"

**Bridged Datasets:** sbdb_jpl_asteroids_with_constraints.csv, Asteroid_Distances.csv, Summary_of_Asteroid_Taxonomic_Classes.csv

**SPARQL Query:**
```sql
SELECT ?name ?distance ?time
WHERE {
  ?asteroid a sol-ont:Asteroid;
  	sol-ont:hasCommonName ?name;
    sol-ont:hasAsteroidClassification ?class;
  	sol-ont:hasDistanceRecord ?record.
  ?record sol-ont:hasResult ?r. 
  ?record sol-ont:hasTemporalExtent ?te .
  ?te sol-ont:recordedAt ?time .
  ?r sol-ont:hasQuantity ?q.
  ?q sol-ont:hasQuantityValue ?qv .
  ?qv sol-ont:hasNumericValue ?distance .
  ?class a sol-ont:AsteroidClassification;
    sol-ont:hasSMASSIIClass ?smassii.
  ?smassii sol-ont:hasElementalComposition ?ec.
  ?ec sol-ont:hasElement ?e.
  FILTER(
    ?e = "iron"^^sol-ont:ChemicalElement
  &&?distance < 1
  )
}
ORDERBY ASC(?time)
```
**Results:**
| name    | distance | time    |
|---------|----------|---------|
| Didymos | 0.27677  | 2023-01 |
| Bennu   | 0.5301   | 2023-08 |
| Bennu   | 0.71025  | 2023-11 |
| Bennu   | 0.85044  | 2024-01 |
| Bennu   | 0.42804  | 2024-05 |
| Didymos | 0.61461  | 2024-08 |
| Ryugu   | 0.8274   | 2024-08 |
| Bennu   | 0.54087  | 2024-08 |
| Didymos | 0.64674  | 2024-11 |
| Ryugu   | 0.55874  | 2024-11 |
| Bennu   | 0.7039   | 2024-11 |
| Didymos | 0.56544  | 2025-01 |
| Ryugu   | 0.66498  | 2025-01 |
| Bennu   | 0.52983  | 2025-01 |
| Ryugu   | 0.44189  | 2025-05 |

* Remarks:  
Additional results are listed to better represent a query on our knowledge graph.  The appropriate answer for the above question would be the second result with `Bennu` with distance at 0.5301.  A Filter can be included to limit the time range from only showing dates after the current MonthYear (2023-04), and a Limit can be added to only show the `Bennu` result.

### Remarks
- `Asterank_Dataset.csv`:  refers to the `JPL_SBDB` dataset with Asterank's evaluation on Asteroid value and profitability
- `Asteroid_Distances.csv`:  refers to a subset of available Asteroids from `SkyLive`
- `sbdb_jpl_asteroids_with_constraints.csv`: refers to large set of sbdb_jpl dataset 
- `Summary_of_Asteroid_Taxonomic_Classes.csv`:  refers to the [Asteroid Spectral Types](https://en.wikipedia.org/wiki/Asteroid_spectral_types)
- `mp3c_dataset.csv`:  refers to a subset of MP3c's dataset of Asteroids
- `nasajpl_sbdl.csv`:  refers to a subset of NASA's JPL_SBDB dataset of Asteroids
