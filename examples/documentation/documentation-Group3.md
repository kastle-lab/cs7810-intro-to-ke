# Name of the Knowledge Graph
**Authors:** Antrea Christou, Erin Rogers, Sydney Woods

## Use Case Scenario
### Narrative 

Some common goals include:<br>
	*	Improving data organization and management: A knowledge graph can help organize complex and interconnected data, making it easier to understand and manage.<br>
	*	Enabling effective search and retrieval of information: By organizing data in a structured way, a knowledge graph can make it easier to search for and retrieve relevant information.<br>
	*	Supporting data analysis and decision-making: A knowledge graph can help identify patterns, insights, and relationships that might not be visible in traditional data structures, enabling better decision-making.<br>
	*	Facilitating collaboration and communication: By providing a common framework for understanding data, a knowledge graph can facilitate collaboration and communication among teams.<br>

A knowledge graph can also help to streamline communication and collaboration among different stakeholders in the aviation industry, enabling them to make more informed decisions and take actions that improve the overall safety and efficiency of the industry.

In our knowledge graph, we aim to support aircraft owners, pilots, and maintainers. Their end goal is to keep aircraft flightworthy, which means frequent maintenance. Maintenance sometimes means sending parts out for repairs or even replacing them altogether, but a large percentage of aircraft used today is more than fifty years old and their manufacturer may have gone out of business or been subsumed by a competitor. It can be difficult to know what companies are supporting the maintenance for what models based upon service logs and possibly out of date owner’s manuals. Keeping aircraft flightworthy also involves knowing what issues a specific model may be prone to, such as brakes on Cessna 140s leading to the airplanes flipping over on the runway, and knowing when parts are recalled. Recalls can happen decades after an aircraft is no longer in production.<br>

Additionally, there could be potential use by businesses looking to see what companies are their biggest remaining competition in the manufacturing of parts. As previously stated, some manufacturers may have been merged together (a similar situation as has been seen with wireless providers in the USA in the early to mid 2010s).<br>
With the issue of manufacturers going out of business, another possible use would be for owners to see if there are any compatible parts still being made to replace or repair parts no longer being made. This functionality would also be useful should any parts be recalled to figure out what is the next best option to keep the aircraft in a safe condition for flying.<br>
By including details about the most common issues different models of the same parts are prone to, this could allow an individual to make a clear decision on what part they would use. For example if the owner of an aircraft has previously encountered a specific issue and knows how to fix it, they may pick the part that is known to have that issue over a part that they do not know how to fix the issues with. Or if the aircraft owner is looking to expand their knowledge on how to fix issues, they may opt to purchase the part they did not know how to fix and then learn to do so.    

### Competency Questions
* How would you query the knowledge graph to identify all airplane parts manufactured by a specific company?
* Show the top A most common plane models. (This would be the list on length A, of the planes with the highest count of total manufactured / made)  
* What times of year are associated with higher crash ratings that were fatal?
* How many parts each company makes?
* Show the unique plane ID's paired with their corresponding plane model type.
* Show the parts along with their manufactiring company and their airworthiness directive.

### Integrated Datasets
[Crash Types](https://www.kaggle.com/datasets/saurograndi/airplane-crashes-since-1908?resource=download)
[Plane Models](http://aviationdb.net/aviationdb/AircraftQuery#SUBMIT)
[Airworthiness Directives](https://drs.faa.gov/browse/ADFRAWD/doctypeDetails)


### References
* https://gama.aero/facts-and-statistics/statistical-databook-and-industry-outlook/annual-data/ - original access date: 2/16/2023<br>
* https://www.faa.gov/airports/engineering/aircraft_char_database - original access date: 02/16/2023<br>
* Specifically https://www.faa.gov/airports/engineering/aircraft_char_database/data - original access date: 02/16/2023<br>  
* https://www.faa.gov/data_research/aviation_data_statistics - original access date: 02/16/2023<br>
* https://ww2db.com/doc.php?q=399 - original access date: 02/16/2023<br>
* Might be more from the directory one level up found here https://ww2db.com/doc.php - original access date: 02/16/2023<br> 
* https://data.world/data-society/airplane-crashes -original access date: 02/16/2023<br> 
* https://data.world/sanfrancisco/u7dr-xm3v -original access date: 02/16/2023<br> 
* https://www.kaggle.com/code/jiaowoguanren/airplanes-motorbikes-schooners-tf-efficientnet/data -original access date: 02/16/2023<br> 
* https://industry.flightaware.com/ownersandoperators -original access date: 02/16/2023<br> 
* https://drs.faa.gov/browse/ADFRAWD/doctypeDetails -original access date: 03/18/2023<br>


## Modules
<!-- There should be one module section per module (essentially per key-notion) -->
### AirworthinessDirective
**Source Pattern:** [Aggregation]( https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/aggregation)
**Source Data:** [FAA Dynamic Regulatory System](https://drs.faa.gov/browse/ADFRAWD/doctypeDetails)

#### Description
Airworthiness Directives are Part recalls issued by the FAA.

![./schema-diagram.png](https://github.com/cs7810-group3/group3Project/blob/main/schema-diagrams/AirworthinessDirective.png)

#### Axioms
* `isAirworthinessDirectiveFor min 1 Part` <br />
The Airworthiness Directive is for at least one Part.
* `hasDate exactly 1 TemporalEntity` <br />
The Airworthiness Directive is issued on one date.

### CrashType
**Source Pattern:** [Event](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/event)
**Source Data:** [Crashes Since 1908](https://www.kaggle.com/datasets/saurograndi/airplane-crashes-since-1908?resource=download)

#### Description
Binary value identifying if the Plane has had any fatal crashes.

![./schema-diagram.png](https://github.com/cs7810-group3/group3Project/blob/main/schema-diagrams/CrashType.png)

#### Axioms
* `CrashType SubClass Of Plane` <br />
Crash Types are part of the Plane Entity.
* `hasCrashType exactly 1 CrashType` <br />
There is only one Crash Type each time.
* `OccuredOnDate exactly 1 TemporalEntity` <br />
Each Crash Type occurs only once.


### ManufacturingCompany
**Source Pattern:** [Identifier]( https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/identifier) 
**Source Data:** [FAA Dynamic Regulatory System](https://drs.faa.gov/browse/ADFRAWD/doctypeDetails)
#### Description
Manufacturing Companies create Parts for aircraft.

![./schema-diagram.png](https://github.com/cs7810-group3/group3Project/blob/main/schema-diagrams/ManufacturingCompany.png)

#### Axioms
* `manufactures min 1 Part` <br />
A Manufacturing Company must manufacture at least one aircraft Part.


### Part
**Source Pattern:** [Identifier]( https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/identifier)
**Source Data:** [FAA Dynamic Regulatory System](https://drs.faa.gov/browse/ADFRAWD/doctypeDetails)

#### Description
Specific components of an airplane.

![./schema-diagram.png](https://github.com/cs7810-group3/group3Project/blob/main/schema-diagrams/Part.png)

#### Axioms
* `isMadeBy min 1 ManufacturingCompany` <br />
At least one Manufacturing Company must have produced a specific Part, but there can be more than one manufacturer.
* `hasAirworthinessDirective min 0 AirworthinessDirective` <br />
Not all Parts have an AirworthinessDirective, but there is no maximum one Part may have.


### Plane
**Source Pattern:** name of adapted source pattern
**Source Data:** name(s) of dataset(s) which populate this module

#### Description
An individual Plane Entity.

![./schema-diagram.png](https://github.com/cs7810-group3/group3Project/blob/main/schema-diagrams/Plane.png)


### PlaneID
**Source Pattern:** [Identifier]( https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/identifier)
**Source Data:** [Aviation IDs](http://www.csgnetwork.com/aviationtypeid.html)

#### Description
The registration number of an aircraft.

![./schema-diagram.png](https://github.com/cs7810-group3/group3Project/blob/main/schema-diagrams/PlaneID.png)

#### Axioms
* `PlaneID SubClass Of Plane` <br />
Every PlaneID is part of the Plane Entity.
* `hasPlaneID exactly 1 PlaneID` <br />
Every Plane has exactly one PlaneID.


### PlaneModel
**Source Pattern:** [Identifier]( https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/identifier)
**Source Data:** [FAA Dynamic Regulatory System](https://drs.faa.gov/browse/ADFRAWD/doctypeDetails)

#### Description
States the model of the Plane.

![./schema-diagram.png](https://github.com/cs7810-group3/group3Project/blob/main/schema-diagrams/PlaneModel.png)

#### Axioms
* `EndDate max 1 TemporalEntity` <br />
Each PartModel has at most one EndDate.
* `hasIdentifier exactly 1 Identifier` <br />
Each PartModel has exactly one Identifier. 
* `StartDate exactly 1 TemporalEntity` <br />
Each PartModel has exactly one StartDate.


## The Overall Knowledge Graph
### Namespaces
* grair: <https://group3/GenericOntology/Airplanes> .
* kwgr: <http://stko-kwg.geog.ucsb.edu/lod/resource/> .
* xsd: <http://www.w3.org/2001/XMLSchema#> .

### Schema Diagram
![./schema-diagram.png](https://github.com/cs7810-group3/group3Project/blob/main/schema-diagrams/schema_attempt_eight.png)

### Axioms
* `isAirworthinessDirectiveFor min 1 Part` <br />
The Airworthiness Directive is for at least one Part.
* `hasDate exactly 1 TemporalEntity` <br />
The Airworthiness Directive is issued on one date.
* `CrashType SubClass Of Plane` <br />
Crash Types are part of the Plane Entity.
* `hasCrashType exactly 1 CrashType` <br />
There is only one Crash Type each time.
* `OccuredOnDate exactly 1 TemporalEntity` <br />
Each Crash Type occurs only once.
* `manufactures min 1 Part` <br />
A Manufacturing Company must manufacture at least one aircraft Part.
* `isMadeBy min 1 ManufacturingCompany` <br />
At least one Manufacturing Company must have produced a specific Part, but there can be more than one manufacturer.
* `hasAirworthinessDirective min 0 AirworthinessDirective` <br />
Not all Parts have an AirworthinessDirective, but there is no maximum one Part may have.
* `PlaneID SubClass Of Plane` <br />
Every PlaneID is part of the Plane Entity.
* `hasPlaneID exactly 1 PlaneID` <br />
Every Plane has exactly one PlaneID.

### Usage
# Validation

## Competency Question Name
**Competency Question:** How would you query the knowledge graph to identify all airplane parts manufactured by a specific company?

**SPARQL Query:**
```
PREFIX grair:<https://group3/GenericOntology/Airplanes>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX kwgr: <http://stko-kwg.geog.ucsb.edu/lod/resource/> 
SELECT ?part ?partString ?company ?companyString
WHERE {
  ?part a grair:Part ;
        grair:partAsString ?partString ;
        grair:isMadeBy ?company ;
        grair:hasAirworthinessDirective ?directive .
  ?company a grair:ManufacturingCompany ;
           grair:asString ?"Airbus SAS"  .

}

```

**Results:**
|part                                             |partString            |company                                                         |
|-------------------------------------------------|----------------------|----------------------------------------------------------------|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part51|Taperlok Fasteners    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany51|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part52|Taperlok Fasteners    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany52|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part53|Taperlok Fasteners    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany53|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part54|Taperlok Fasteners    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany54|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part55|Taperlok Fasteners    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany55|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part56|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany56|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part57|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany57|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part58|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany58|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part59|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany59|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part60|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany60|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part61|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany61|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part62|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany62|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part63|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany63|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part64|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany64|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part65|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany65|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part66|Angle of Attack Probes|http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany66|



## Competency Question Name
**Competency Question:** Show the top A most common plane models.

**SPARQL Query:**
```
PREFIX grair:<https://group3/GenericOntology/Airplanes>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX kwgr: <http://stko-kwg.geog.ucsb.edu/lod/resource/> 
SELECT ?planeModel (COUNT(?planeModel) AS ?count)
WHERE {
  ?plane grair:isPlaneModelType ?planeModel .
}
GROUP BY ?planeModel
ORDER BY DESC(?count)
LIMIT 10

```

**Results:**
|planeModel                                       |count                 |
|-------------------------------------------------|----------------------|
|Douglas DC-3                                     |334                   |
|de Havilland Canada DHC-6 Twin Otter 300         |81                    |
|Douglas C-47A                                    |74                    |
|Douglas C-47                                     |62                    |
|Douglas DC-4                                     |40                    |
|Yakovlev YAK-40                                  |37                    |
|Antonov AN-26                                    |36                    |
|Junkers JU-52/3m                                 |32                    |
|Douglas C-47B                                    |29                    |
|De Havilland DH-4                                |28                    |

## Competency Question Name
**Competency Question:** What times of year are associated with higher crash ratings that were fatal?

**SPARQL Query:**
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX kwgr: <http://stko-kwg.geog.ucsb.edu/lod/resource/> 
SELECT ?year (COUNT(?crash) AS ?count)
WHERE {
  ?crash a grair:CrashType ;
         grair:isCrashOfType "1" ;
         grair:occuredOnDate ?date .
  BIND(SUBSTR(?date, 7, 4) AS ?year)
}
GROUP BY ?year
ORDER BY DESC(?count)
LIMIT 1

```

**Results:**
Year|Count                                     |
|----|------------------------------------------|
|1972|103                                       |


## Competency Question Name
**Competency Question:** How many parts each company makes?
**SPARQL Query:**
```
PREFIX grair:<https://group3/GenericOntology/Airplanes>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX kwgr: <http://stko-kwg.geog.ucsb.edu/lod/resource/> 
SELECT ?partString ?companyString (COUNT(?part) AS ?count)
WHERE {
  ?part a grair:Part ;
        grair:partAsString ?partString ;
        grair:isMadeBy ?company .
        
  ?company a grair:ManufacturingCompany ;
           grair:asString ?companyString .
  
  ?company grair:manufactures ?part .
}
GROUP BY ?partString ?companyString
ORDER BY DESC(?count)


```

**Results:**
|partString                                       |companyString                |count                                     |
|-------------------------------------------------|-----------------------------|------------------------------------------|
|CF34-8C and CF34-8E Turbofan Engines             |General Electric Company     |13                                        |
|Aft Rudder Control Rods                          |Embraer S.A.                 |12                                        |
|Angle of Attack Probes                           |Airbus SAS                   |11                                        |
|737 Pneumatic Motor                              |The Boeing Company           |9                                         |
|Wing Attach Angles                               |The Boeing Company           |9                                         |
|V2522-A5 Turbofan Engine                         |International Aero Engines AG|7                                         |
|PW4074 Turbofan Engine                           |Pratt & Whitney Division     |7                                         |
|Taperlok Fasteners                               |Airbus SAS                   |5                                         |
|Fuel Pump                                        |The Boeing Company           |5                                         |
|Principle Wing Structure                         |Aero Union Corporation       |4                                         |
|Flight Controls                                  |Cessna Aircraft              |4                                         |
|Wing Structure                                   |Embraer S.A.                 |4                                         |
|Bob-weight Interconnect Link                     |Hawker Textron Aviation Inc  |3                                         |
|Elevator Control System                          |Hawker Textron Aviation Inc  |3                                         |
|Foreward Spar Fasteners                          |Hawker Textron Aviation Inc  |3                                         |
|Lower Rear Bathtub Fitting                       |Hawker Textron Aviation Inc  |3                                         |
|Rear Spar Fasteners                              |Hawker Textron Aviation Inc  |3                                         |
|Rear Wing Lower Spar Caps                        |Hawker Textron Aviation Inc  |3                                         |
|Operational Program Software                     |The Boeing Company           |3                                         |
|TSO-C172 Cargo Restraint Straps                  |The Boeing Company           |3                                         |
|Lower Wing Panel                                 |328 Support Services GmbH    |2                                         |
|Autoflight                                       |Airbus                       |2                                         |
|Skin Bonding Agent                               |Cessna Aircraft              |2                                         |
|Spar Strap                                       |Cessna Aircraft              |2                                         |
|Stabilizers                                      |Mooney Aviation Company Inc  |2                                         |
|Flight Controls                                  |The Boeing Company           |2                                         |
|Center Fuel Tank                                 |Bombardier Inc               |1                                         |
|Battery Charger                                  |Cessna Aircraft              |1                                         |
|Amplifier 38849-001                              |Cirrus Design Corporation    |1                                         |
|Flight Controls                                  |Cirrus Design Corporation    |1                                         |
|Microphone Interface 35809-001                   |Cirrus Design Corporation    |1                                         |
|Pitch Trim                                       |Dassault Aviation            |1                                         |
|Stabilizer Attachment Joint                      |Embraer S.A.                 |1                                         |
|Wing Spar                                        |Frakes Aviation              |1                                         |
|Inboard Vent Tube Hole                           |Gulfstream Aerospace LP      |1                                         |
|Horizontal Stabilizer Actuator                   |Learject Inc                 |1                                         |
|Fuselage Drain Holes                             |Piaggio Aero Industries S.p.A|1                                         |
|Left-Hand Elevator Auxiliary Spar                |Viking Air Limited           |1                                         |

## Competency Question Name
**Competency Question:** Show the unique plane ID's paired with their corresponding plane model type.
**SPARQL Query:**
```
PREFIX grair:<https://group3/GenericOntology/Airplanes>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX kwgr: <http://stko-kwg.geog.ucsb.edu/lod/resource/> 



SELECT  ?planeId ?planeModel
WHERE {
 
  ?plane rdf:type grair:Plane .
  ?plane grair:hasPlaneID ?planeId .
  ?plane grair:isPlaneModelType ?planeModel .
}


```

**Results:**
|planeId                                          |planeModel                              |
|-------------------------------------------------|----------------------------------------|
|1                                                |Wright Flyer III                        |
|100                                              |Dirigible                               |
|1000J                                            |Super Zeppelin (airship)                |
|10051                                            |Junkers F-13                            |
|101TM                                            |Douglas DC-3                            |
|101TQ                                            |Lockheed 18 Lodestar                    |
|101TR                                            |Avro 685 York I                         |
|101TT                                            |Lockheed 18 Lodestar                    |
|101TV                                            |FIAT G-212CP                            |
|101TW                                            |Douglas DC-3                            |
|101TX                                            |Douglas DC-3                            |
|101U                                             |Douglas C-47B                           |
|101UA                                            |Curtiss C-46D-5-CU                      |
|101UD                                            |Lockheed 749-79-33 Constellation        |
|10053                                            |Breguet 14                              |
|101UE                                            |Douglas C-47A-20-DL                     |
|101UK                                            |Lockheed L-749-79-33 Constellation      |
|101UL                                            |Curtiss C-46E-1-CS                      |
|101US                                            |Curtiss C-46F-1-CU                      |
|101UT                                            |Douglas DC-3 -201D/ F-6-F- 5 Hellcat    |
|101UV                                            |Curtiss C-46D-10-CU                     |
|101V                                             |Douglas DC-3                            |
|101VA                                            |Bristol 170 Freighter 21                |
|101VB                                            |Douglas DC-3 (C-54A-DO)                 |
|101VD                                            |Douglas DC-3                            |
|10057                                            |Caudron C-61                            |
|101VK                                            |Consolidated Canso (amphibian)          |
|101VM                                            |Douglas C-47B-5-DK                      |
|101VP                                            |Douglas DC-3                            |
|101VR                                            |Douglas DC-3                            |
|101VS                                            |Douglas C-54A-1-DO                      |
|101VT                                            |Curtiss C-46E-1-CS                      |
|101VU                                            |Lockheed 749-79-33 Constellation        |
|101VW                                            |Douglas C-54B / P-38                    |
|101W                                             |Douglas DC-3                            |
|101WA                                            |Douglas C-47A                           |
|10059                                            |Fokker F-4                              |
|101WB                                            |Douglas DC-4                            |
|101WC                                            |Douglas DC-6                            |
|101WD                                            |Douglas DC-3 (C-47-DL)                  |
|101WE                                            |Douglas DC-3                            |
|101WG                                            |Curtiss C-46D-CU                        |
|101WH                                            |Curtiss C-46D-CU                        |
|101WK                                            |Douglas DC-3                            |
|101WP                                            |Douglas DC-3-313A                       |
|101WR                                            |Douglas DC-3                            |
|101WS                                            |Douglas C-47A-60-DL                     |
|1005B                                            |Junkers F-13                            |
|101WY                                            |Douglas C-54A-DO                        |
|101WZ                                            |Junkers JU-52/3m                        |
|101X                                             |Douglas C-47                            |
|101XL                                            |Douglas C-47A-50-DL                     |
|101XM                                            |Douglas DC-3                            |
|101XT                                            |Douglas C-54D-DC (DC-4)                 |
|101XV                                            |Douglas DC-3                            |
|101XW                                            |Douglas C-47A-15-DK                     |
|101XX                                            |Martin 202                              |
|101Y                                             |Bristol 170 Freighter 21                |
|1005C                                            |Bleriot 155                             |
|101YB                                            |Avro 689 Tudor 5                        |
|101YT                                            |Douglas DC-3                            |
|101YX                                            |Latecoere 631 (sea plane)               |
|101YY                                            |Douglas C-47A                           |
|101ZL                                            |Douglas C-47 (DC-3)                     |
|101ZP                                            |Douglas C-54D                           |
|101ZS                                            |Douglas C-47DL                          |
|101ZW                                            |Boeing B-29                             |
|101ZY                                            |Curtiss C-46D                           |
|1020                                             |Curtiss C-46F-1-CU                      |
|1005D                                            |Sikorsky S-25                           |
|10202                                            |Douglas DC-3                            |
|10205                                            |Curtiss C-46-F-1-CU                     |
|10207                                            |Douglas DC-3-178                        |
|10208                                            |Douglas DC-4-1009                       |
|1020A                                            |Douglas DC-4-1009                       |
|1020D                                            |Douglas DC-4                            |
|1020H                                            |Douglas DC-4-1009                       |
|1020M                                            |Douglas C-54G                           |
|1020P                                            |Douglas DC-3                            |
|1020Q                                            |Douglas DC-3                            |
|1005E                                            |Fokker FG III                           |
|1020S                                            |Douglas DC-3                            |
|1020T                                            |Douglas C-47D                           |
|1020U                                            |Lockheed 049 Constellation              |
|1020V                                            |Bristol 170 Freighter 21                |
|1020W                                            |Boeing B-29MR                           |
|1020X                                            |Douglas C-47B                           |
|1020Z                                            |Lockheed 749A Constellation             |
|1021                                             |Douglas DC-3                            |
|10210                                            |Douglas DC-3                            |
|10211                                            |Douglas R5D-3                           |
|1005F                                            |Handley Page W-10                       |
|10213                                            |Douglas DC-3                            |
|10215                                            |Avro Ninteen I                          |
|10218                                            |Douglas C-54D-DC (DC-4)                 |
|1021B                                            |Douglas DC-3                            |
|1021C                                            |Martin 202                              |
|1021E                                            |Douglas C-47A                           |
|1021G                                            |Vickers 610 Viking-1B                   |
|1021J                                            |Lockheed 749 Constellation              |
|1021K                                            |Martin 202                              |
|1021M                                            |Douglas C-54B-1-DC                      |
|1005H                                            |Breguet 14                              |
|1021P                                            |Douglas DC-3                            |
|1021Q                                            |Douglas DC-3                            |
|1021S                                            |Douglas DC-3                            |
|1021U                                            |Douglas C-47A                           |
|1021V                                            |Douglas DC-3                            |
|1021W                                            |Douglas DC-3                            |
|1021X                                            |Douglas C-54A                           |
|10222                                            |Douglas DC-3                            |
|10225                                            |Douglas DC-3                            |
|1022B                                            |Douglas C-47-DL                         |
|1000L                                            |Zeppelin L-34 (airship)                 |
|1005K                                            |Ryan M-1                                |
|1022D                                            |Douglas C54E-DO (DC-4)                  |
|1022F                                            |Douglas DC-3                            |
|1022G                                            |Douglas DC-3                            |
|1022L                                            |de Havilland Dove 1                     |
|1022M                                            |Douglas DC-3                            |
|1022N                                            |Douglas DC-4-1009                       |
|1022Q                                            |Martin 202                              |
|1022S                                            |Savoia Marchetti SM-95                  |
|1022T                                            |Short Sunderland 9 (flying boat)        |
|1022U                                            |Douglas DC-3                            |
|1005L                                            |Fokker F-VII                            |
|1022X                                            |Douglas C-54                            |
|1022Y                                            |Douglas DC-4                            |
|1023                                             |Curtiss C-46A                           |
|10232                                            |Douglas DC-3                            |
|10235                                            |Douglas DC-4                            |
|10236                                            |Douglas C-47                            |
|1023A                                            |Douglas C-124A Globemaster              |
|1023B                                            |Lockheed C-130B Hercules                |
|1023C                                            |Douglas DC-3                            |
|1023D                                            |Douglas DC-3                            |
|1005N                                            |Breguet 14                              |
|1023E                                            |Douglas DC-3                            |
|1023F                                            |Douglas DC-3                            |
|1023G                                            |Douglas C-47B-DK                        |
|1023K                                            |Douglas DC-3                            |
|1023N                                            |Douglas DC-4 /Beechcraft SMB-1          |
|1023S                                            |Douglas DC-3                            |
|1023W                                            |Convair B-36D                           |
|1023X                                            |Vickers 639 Viking 1                    |
|1023Z                                            |Douglas DC-3                            |
|1024                                             |Fairchild C-82                          |
|1005U                                            |de Havilland DH-9C                      |
|10240                                            |Douglas DC-3D                           |
|10242                                            |Douglas C-47A                           |
|10247                                            |Lockheed 049 Constellation              |
|10248                                            |Junkers 52/3m                           |
|10249                                            |Douglas DC-6B                           |
|1024B                                            |Douglas C-47B                           |
|1024C                                            |Douglas DC-3                            |
|1024D                                            |Fairchild C-82 Packet                   |
|1024F                                            |Vickers Valetta C-1                     |
|1024G                                            |de Havilland DHA-3 Drover II            |
|1005V                                            |NaN                                     |
|1024H                                            |Douglas C-47A                           |
|1024K                                            |Douglas C-54A                           |
|1024L                                            |Douglas DC-3                            |
|1024M                                            |Curtiss C-46A                           |
|1024N                                            |NaN                                     |
|1024P                                            |Douglas DC-3D                           |
|1024Q                                            |Douglas DC-3                            |
|1024R                                            |Douglas DC-6B                           |
|1024S                                            |Douglas DC-3                            |
|1024T                                            |Boeing 377 Stratocruiser 10-34          |
|1005X                                            |Douglas M-4                             |
|1024U                                            |Douglas DC-3                            |
|1024W                                            |Douglas C-47A-30-DK Dakota III          |
|1024Z                                            |Curtiss C-46D-15-CU                     |
|1025                                             |Douglas DC-3                            |
|10250                                            |Douglas DC-3                            |
|10251                                            |Boeing C-97A Stratofreighter            |
|10253                                            |Consolidated PBY-5A Catalina            |
|10254                                            |Douglas DC-3                            |
|10255                                            |Douglas C-47                            |
|10256                                            |Martin 202                              |
|10060                                            |Fokker FG III                           |
|1025A                                            |Douglas DC-3                            |
|1025C                                            |Douglas DC-3                            |
|1025E                                            |Douglas DC-4                            |
|1025G                                            |DC-2-243                                |
|1025M                                            |Douglas DC-3A                           |
|1025N                                            |de Havilland DH-84                      |
|1025T                                            |Curtiss Wright C-46F                    |
|1025V                                            |SNCASE Languedoc                        |
|1025W                                            |Curtiss C-46A-50-CU                     |
|1025X                                            |Curtiss C 46F-CU                        |
|10065                                            |SPCA Meteore 63                         |
|1025Z                                            |Douglas C-47D                           |
|1026                                             |Douglas C-47A                           |
|10260                                            |Junkers JU-52/3m                        |
|10262                                            |Douglas DC-3                            |
|10266                                            |Douglas DC-4                            |
|1026A                                            |Convair CV-240-0                        |
|1026B                                            |Douglas DC-3                            |
|1026C                                            |Boeing B-29                             |
|1026E                                            |Douglas DC-6                            |
|1026F                                            |Douglas C-54B-10-DO                     |
|10067                                            |Junkers F-13                            |
|1026H                                            |Vickers 614 Viking 1                    |
|1026J                                            |Consolidated  32 Liberator II           |
|1026M                                            |Douglas DC-3                            |
|1026N                                            |Douglas DC-3A                           |
|1026S                                            |SNCASE Languedoc                        |
|1026T                                            |Douglas C-47A-35-DL                     |
|1026U                                            |Boeing B-29 / Boeing B-29               |
|1026V                                            |Douglas C-47-DL                         |
|1026W                                            |Douglas DC-6                            |
|1026X                                            |Lockheed 18 Lodestar                    |
|10068                                            |Fokker F-VIII                           |
|1026Y                                            |NaN                                     |
|1027                                             |Douglas DC-3                            |
|10274                                            |Douglas DC-3                            |
|10279                                            |Curtiss C-46F-1-CU                      |
|1027B                                            |Martin 202                              |
|1027C                                            |Douglas C-47A                           |
|1027D                                            |Douglas DC-4                            |
|1027E                                            |Curtiss C-46F-1CU                       |
|1027F                                            |Curtiss C-46D                           |
|1027L                                            |Boeing 377-10-26 Stratocruiser          |
|1000N                                            |Airship                                 |
|10069                                            |Fokker Universal                        |
|1027M                                            |Douglas DC-3                            |
|1027P                                            |Douglas C-47A                           |
|1027T                                            |Douglas DC-3                            |
|1027V                                            |Douglas DC-3                            |
|1027X                                            |Curtiss C-46A                           |
|1027Y                                            |Handley Page HP-81 Hermes IV            |
|10284                                            |Douglas DC-3                            |
|10286                                            |Boeing B-50                             |
|1028A                                            |Avro Shackleton MR-1                    |
|1028C                                            |Boeing 377 Stratocruiser                |
|1006A                                            |Fokker F-VII                            |
|1028E                                            |Douglas DC-3                            |
|1028F                                            |Handley Page HP-81 Hermes 4A            |
|1028G                                            |Bristol 170 Freighter                   |
|1028H                                            |Douglas DC-2-115B                       |
|1028M                                            |de Havilland 110                        |
|1028Q                                            |Curtiss C-46                            |
|1028R                                            |Boeing B-29                             |
|1028S                                            |Douglas C-47A                           |
|1028T                                            |Avro Shackleton MR-1                    |
|1028V                                            |Douglas DC-3                            |
|1006B                                            |BFW M-18                                |
|1028W                                            |Curtiss-Wright C-46D-CU                 |
|10290                                            |Boeing KC-97G Stratofreighter           |
|10293                                            |Douglas C-54B-1-DC                      |
|10294                                            |Fairchild C-119C                        |
|10298                                            |Fairchild C-119C                        |
|1029A                                            |Fairchild C-119C                        |
|1029B                                            |Fairchild C-119C-23-FA Flying Boxcar    |
|1029D                                            |Douglas C-124A Globemaster              |
|1029E                                            |Douglas C-54G (DC-4)                    |
|1029G                                            |Lisunov Li-2                            |
|1006D                                            |Dornier Merkur                          |
|1029H                                            |Douglas DC-4                            |
|1029K                                            |Douglas C-124A Globemaster              |
|1029M                                            |Curtiss C-46D                           |
|1029N                                            |Douglas DC-3                            |
|1029P                                            |Douglas DC-3                            |
|1029R                                            |Douglas DC-3                            |
|1029S                                            |Vickers Viking 610-1B                   |
|1029T                                            |Cessna 402                              |
|1029W                                            |Curtiss C-46                            |
|1029X                                            |Vickers Valetta Mk1 / Avero Lancaster   |
|1006E                                            |Breguet 14                              |
|1029Y                                            |Douglas DC-3                            |
|102AA                                            |Avro 685 York 1                         |
|102AC                                            |Douglas DC-3                            |
|102AD                                            |Douglas DC-4                            |
|102AE                                            |Curtiss-Wright C-46                     |
|102AF                                            |Douglas DC-6                            |
|102AG                                            |de Havilland DH106 Comet 1A             |
|102AH                                            |Curtiss C-46F                           |
|102AK                                            |Convair CV-240-7                        |
|102AL                                            |Douglas DC-3                            |
|1006L                                            |Fairchild FC-2                          |
|102AM                                            |Convair RB-36H                          |
|102AP                                            |Douglas DC-4  (C-54-10-DO)              |
|102AR                                            |de Havilland DH-114 Heron 1B            |
|102AS                                            |Vickers 616 Viking 1B                   |
|102AT                                            |Lockheed 18-56 LodeStar                 |
|102B                                             |Junkers JU-5/-3m                        |
|102BA                                            |Douglas C-47A                           |
|102BB                                            |Douglas DC-3 (C-47-DL)                  |
|102BD                                            |Douglas DC-3                            |
|102BE                                            |Douglas DC-6B                           |
|1006P                                            |Farman F-121 Jabiru                     |
|102BG                                            |de Havilland DH106 Comet 1              |
|102BH                                            |Vickers Valetta T-3                     |
|102BK                                            |Douglas DC-3                            |
|102BL                                            |Consolidated PBY-5A Catalina            |
|102BM                                            |Douglas DC-3                            |
|102BN                                            |Convair CV-240-4                        |
|102BQ                                            |Lockheed 18 Loadstar                    |
|102BR                                            |Douglas DC-3                            |
|102BS                                            |Douglas DC-3                            |
|102BT                                            |Lockheed 049-46-21 Constellation        |
|1006Q                                            |Junkers F-13                            |
|102BZ                                            |Douglas C-124A Globemaster II           |
|102C                                             |Douglas DC-6A                           |
|102CA                                            |Fairchild R4Q-2                         |
|102CC                                            |Ilyushin IL-12                          |
|102CD                                            |Avro 685 York C-1                       |
|102CG                                            |Lockheed L- 749A Constellation          |
|102CJ                                            |Douglas DC-3                            |
|102CL                                            |Boeing B-34                             |
|102CQ                                            |Curtiss C-46A                           |
|102CT                                            |Lockheed 749A Constellation             |
|1006U                                            |Douglas M-4                             |
|102CV                                            |Douglas DC-3                            |
|102CW                                            |Douglas C-47A                           |
|102CZ                                            |Douglas C-47A                           |
|102D                                             |Convair CV-240-0                        |
|102DA                                            |Douglas DC-3                            |
|102DB                                            |Curtiss C-46F-1-CU                      |
|102DD                                            |Convair CV-240-12                       |
|102DE                                            |Douglas C-47B                           |
|102DG                                            |Douglas C-46A-CU ( DC-3)                |
|102DH                                            |Lockheed 749A Constellation             |
|1006V                                            |Breguet 14                              |
|102DL                                            |Douglas DC-6                            |
|102DM                                            |Douglas DC-3                            |
|102DN                                            |Avro Shackleton MR-2                    |
|102DP                                            |Bristol 170 Freighter 21                |
|102DR                                            |Douglas DC-3                            |
|102DS                                            |Convair CV-240                          |
|102DU                                            |Douglas DC-3                            |
|102DV                                            |Douglas DC-3                            |
|102DW                                            |Douglas DC-3                            |
|102DZ                                            |Vickers Valetta                         |
|1000P                                            |Schutte-Lanz S-L-9 (airship)            |
|1006W                                            |Breguet 14                              |
|102EA                                            |de Havilland DH106 Comet 1              |
|102EC                                            |Douglas DC-3                            |
|102ED                                            |F-88 Sabre Jet                          |
|102EL                                            |Douglas DC-6                            |
|102EP                                            |Douglas DC-3 (C-47A-DK)                 |
|102ER                                            |Douglas DC-3A                           |
|102ET                                            |Curtiss-Wright C46D-CU                  |
|102EV                                            |Douglas C-47                            |
|102EX                                            |Avro Shackleton MR-2                    |
|102EY                                            |Douglas DC-3                            |
|1006Y                                            |Latécoère 23                            |
|102EZ                                            |Convair CV-240                          |
|102FA                                            |Douglas C-47A-DL                        |
|102FB                                            |Lockheed 749A-79-33 Constellation       |
|102FC                                            |Douglas C-47A                           |
|102FD                                            |Fairchild C-110F                        |
|102FE                                            |Douglas DC-3                            |
|102FM                                            |Douglas DC-3                            |
|102FP                                            |Douglas C-54A                           |
|102FV                                            |de Havilland DH106 Comet 1              |
|102FW                                            |Canadair C-4-1Argonaut / Harvard Mark II|
|1007                                             |Fairchild FC-2                          |
|102GA                                            |Douglas DC-3                            |
|102GB                                            |Lockheed 18 Lodestar                    |
|102GG                                            |Douglas DC-3                            |
|102GM                                            |Douglas C-47A-30-DK                     |
|102GP                                            |Douglas DC-3                            |
|102GS                                            |Douglas DC-3                            |
|102GW                                            |Douglas C-47A                           |
|102GX                                            |Curtiss C-46A                           |
|102HB                                            |Douglas C-47-DL                         |
|102HK                                            |Convair CV-240-4                        |
|10070                                            |Latecoere 25                            |
|102HL                                            |Lockheed C-28                           |
|102HM                                            |Douglas DC-4                            |
|102HN                                            |Douglas DC-2                            |
|102HQ                                            |Lockheed 749A-79 Constellation          |
|102HS                                            |Douglas DC-3                            |
|102HW                                            |Bristol 170 Freighter 21E               |
|102HY                                            |Douglas DC-3                            |
|102JA                                            |Douglas DC-6B                           |
|102JB                                            |Douglas C-47A                           |
|102JC                                            |Convair RB-36H                          |
|10072                                            |Breguet 14                              |
|102JE                                            |Lockheed 1049C-55-81 S Constellation    |
|102JF                                            |Douglas DC-3                            |
|102JH                                            |Vickers 634 Viking                      |
|102JJ                                            |Douglas C-47A-DL                        |
|102JK                                            |Lockheed R7V-1                          |
|102JL                                            |Lockheed R-7V1                          |
|102JM                                            |Vickers 720 Viscount                    |
|102JP                                            |Douglas DC-3                            |
|102JR                                            |Douglas DC-3                            |
|102JT                                            |Douglas DC-3                            |
|10073                                            |Breguet 14                              |
|102JV                                            |Douglas C-47A                           |
|102JY                                            |Douglas C-47A                           |
|102K                                             |Douglas DC-6B                           |
|102KC                                            |Douglas DC-3                            |
|102KM                                            |Boeing B377-10-28 Stratocruiser         |
|102KR                                            |NaN                                     |
|102KS                                            |Ilyushin 14                             |
|102KT                                            |Avro Shackleton M-2 / Avro Shakleton M-2|
|102KU                                            |Martin 202A / DC-3                      |
|102KW                                            |Convair CV-340                          |
|10074                                            |Breguet 14                              |
|102KY                                            |Consolidated PBY-5 Catalina             |
|102LB                                            |Douglas DC-3                            |
|102LC                                            |Bristol 170 Freighter 21E               |
|102LE                                            |Douglas DC-6                            |
|102LG                                            |Martin 404                              |
|102LJ                                            |Douglas DC-3                            |
|102LL                                            |Douglas DC-3                            |
|102LP                                            |Douglas DC-3                            |
|102LS                                            |Douglas C-47A                           |
|102LT                                            |Convair CV-240-0                        |
|10075                                            |Boeing 40                               |
|102LU                                            |Douglas R6D-1 (C-118B)                  |
|102LW                                            |Boeing 377 Stratocruiser 10-26          |
|102LY                                            |Curtiss C-46A                           |
|102M                                             |Douglas DC-6                            |
|102MA                                            |Lockheed 749A Constellation             |
|102MC                                            |de Havilland DH-114 Heron 1B            |
|102MD                                            |Douglas DC-3                            |
|102ME                                            |Douglas C-47-DL                         |
|102MG                                            |Avro 685 York C-1                       |
|102ML                                            |Douglas C-54A                           |
|10076                                            |NaN                                     |
|102MM                                            |Lockheed 049-46-21 Constellation        |
|102MR                                            |Curtiss C-46                            |
|102MS                                            |Douglas DC-2-243                        |
|102MU                                            |Convair CV-340-32                       |
|102NA                                            |Lockheed 049 Constellation              |
|102NJ                                            |Convair CV-240-0                        |
|102NM                                            |NaN                                     |
|102NN                                            |Fairchild C119G / Fairchild C119G       |
|102NS                                            |Douglas DC-3                            |
|102NT                                            |Douglas C-47A                           |
|10077                                            |Farman F-60 Goliath                     |
|102NY                                            |Douglas DC-3                            |
|102NZ                                            |Douglas DC-3                            |
|102PA                                            |Latecoere 631                           |
|102PB                                            |Bristol 170 Freighter 31                |
|102PC                                            |Canadair C-4                            |
|102PE                                            |Douglas C-54A                           |
|102PF                                            |Douglas C54A                            |
|102PG                                            |Douglas DC-4                            |
|102PH                                            |Convair CV-340-58                       |
|102PJ                                            |Douglas DC-6B                           |
|1000Q                                            |Zeppelin L-22 (airship)                 |
|10078                                            |Boeing 40                               |
|102PK                                            |Douglas C-54                            |
|102PL                                            |Douglas MC-54M                          |
|102PM                                            |Douglas C124-DL Globemaster II          |
|102PR                                            |Boeing RB-52B                           |
|102PS                                            |Douglas DC-3                            |
|102Q                                             |Curtiss C-46A                           |
|102RB                                            |Douglas DC-3                            |
|102RC                                            |Lockheed 749C-79-12 Constellation       |
|102RE                                            |Douglas C-47                            |
|102RF                                            |Douglas DC-3                            |
|10079                                            |Rohrbach Roland                         |
|102RH                                            |Douglas DC-3                            |
|102RJ                                            |Douglas C-47                            |
|102RM                                            |Bristol 170 Freighter 31                |
|102RS                                            |Douglas C-47-DL                         |
|102RV                                            |Douglas R5D2                            |
|102RW                                            |Avro 685 York C-1                       |
|102S                                             |Douglas DC-6B                           |
|102SA                                            |Douglas DC-3                            |
|102SC                                            |Douglas C-47B                           |
|102SD                                            |Douglas DC-3                            |
|1007B                                            |Latecoere 26                            |
|102SG                                            |Douglas C-47B                           |
|102SH                                            |Douglas C-47A                           |
|102SJ                                            |Douglas C-47A                           |
|102SP                                            |Martin 404                              |
|102SR                                            |Boeing 377 Stratocruiser 10-30          |
|102SS                                            |Aero Commander  520                     |
|102ST                                            |Consolidated PBY-5A Catalina            |
|102SU                                            |Avro 685 York C-1                       |
|102SW                                            |Douglas DC-3                            |
|102SX                                            |CF-100 Mark V                           |
|1007F                                            |Ford 4                                  |
|102SY                                            |Douglas DC-3                            |
|102SZ                                            |Lockheed 1049E-55 Super Constellation   |
|102T                                             |Canadair C-4 Argonaut                   |
|102TA                                            |Douglas DC-7 / Lockheed S Constellation |
|102TC                                            |Vickers Viscount                        |
|102TG                                            |Douglas C-118A                          |
|102TH                                            |Douglas DC-3                            |
|102TJ                                            |Douglas DC-3                            |
|102TK                                            |Douglas DC-6B                           |
|102TL                                            |Curtiss C-46A-45-CU                     |
|1007G                                            |Junkers F-13                            |
|102TM                                            |Douglas DC-3 / Cessna 170B              |
|102TN                                            |Stinson AT-19                           |
|102TS                                            |Douglas C188-B                          |
|102TW                                            |Boeing  377 Stratocruiser               |
|102TX                                            |Douglas DC-3                            |
|102TY                                            |Curtiss C-46                            |
|102U                                             |Handley Page HP-1 Hermes                |
|102UC                                            |de Havilland DH-114 Heron 2B            |
|102UM                                            |Douglas C-54A-10-DC                     |
|102UV                                            |Douglas C-47A                           |
|1007L                                            |AEGK                                    |
|102UW                                            |Douglas DC-3                            |
|102VP                                            |Ilyushin IL-12B                         |
|102VR                                            |Douglas DC-6B                           |
|102VS                                            |Lockheed 749-79-34 Constellation        |
|102VT                                            |Consolidated PBY-5A Catalina            |
|102VW                                            |Canadair DC-4M-2 Northstar              |
|102WA                                            |Vickers 708 Viscount                    |
|102WB                                            |Convair CV-340-58                       |
|102WC                                            |Douglas DC-3                            |
|102WD                                            |Lockheed C-121C Super Constellation     |
|1007N                                            |Douglas M-4                             |
|102WH                                            |Convair CV-240-0                        |
|102WK                                            |Vickers 615 Viking 1B                   |
|102WL                                            |Douglas DC-3                            |
|102WM                                            |SNCASE SE.2010 Armagnac                 |
|102WP                                            |Douglas DC-7B / U.S. Air Force F-89J    |
|102WR                                            |Douglas DC-6A                           |
|102WW                                            |Douglas C-124C                          |
|102WY                                            |Douglas C-54B                           |
|102WZ                                            |Blackburn Beverley C Mark 1             |
|102X                                             |Douglas DC-3                            |
|1007P                                            |Junkers F-13                            |
|102XP                                            |Vickers Viscount 701                    |
|102XX                                            |Douglas C-47 Skytrain                   |
|102Y                                             |Douglas DC-3                            |
|102YB                                            |Boeing C-97C                            |
|102YK                                            |Curtiss C-46A-45-CU                     |
|102YM                                            |Douglas DC-3                            |
|102YY                                            |Douglas DC-3                            |
|102Z                                             |Consolidated B-24J                      |
|102ZW                                            |Vickers Valetta C-Mk.1                  |
|102ZX                                            |Lockheed Super Constellation            |
|1007R                                            |Vickers 74 Vulcan                       |
|102ZZ                                            |Vickers Viking 1B                       |
|1030                                             |Douglas C-47A                           |
|10300                                            |Bristol 170 Freighter                   |
|10302                                            |Vickers 615 Viking 1B                   |
|10303                                            |Douglas DC-4                            |
|10305                                            |Douglas DC-3                            |
|1030N                                            |Ilyushin P-14                           |
|1030R                                            |Douglas C-47B                           |
|1030S                                            |Douglas C-47A                           |
|1030T                                            |Douglas DC-3                            |
|1007S                                            |Fokker (KLM) F.III                      |
|1030W                                            |Douglas DC-3                            |
|1030Z                                            |Lockheed 1049C Super Constellation      |
|1031                                             |Convair CV-240                          |
|10310                                            |Douglas DC-4                            |
|10312                                            |Ilyushin IL-14P                         |
|10314                                            |Douglas DC-3                            |
|10315                                            |Douglas DC-3                            |
|10319                                            |Douglas DC-3                            |
|1031B                                            |Douglas DC-3                            |
|1031H                                            |Convair CV-440-62                       |
|1000R                                            |Zeppelin L-43 (airship)                 |
|1007T                                            |Ford 4-AT-B Tri Motor                   |
|1031P                                            |de Havilland DH-114 Heron               |
|1031R                                            |Curtiss C-46A-45-CU                     |
|1031S                                            |Vickers 802 Viscount                    |
|1031V                                            |Douglas DC-3                            |
|1031W                                            |Fairchild C-82A                         |
|1031X                                            |Bristol Britannia 175                   |
|1031Z                                            |Boeing - 377-10-29 Stratocruiser        |
|10324                                            |de Havilland DH-114 Heron 2D            |
|10329                                            |Short Solent 3 (flying boat)            |
|1032D                                            |Bristol 170 Freighter 31                |
|1007U                                            |Bleriot Spad 56                         |
|1032E                                            |Douglas DC-4                            |
|1032F                                            |Douglas C-47A                           |
|1032G                                            |de Havilland Canada DHC-3 Otter         |
|1032H                                            |Avro 685 York C-1                       |
|1032J                                            |Lockheed WV-2                           |
|1032M                                            |Short Sunderland                        |
|1032S                                            |Fairchild C-82A                         |
|1032V                                            |Douglas DC-3                            |
|1032W                                            |Douglas DC-4                            |
|1032X                                            |Convair CV-240-7                        |
|1007W                                            |de Havilland DH.50J                     |
|1032Z                                            |Douglas C-118A / Lockheed P2V-5F        |
|1033                                             |Airspeed Ambassador A5-57               |
|10330                                            |Consolidated PBY-5A  Catalina           |
|10332                                            |Lockheed WV-2                           |
|10334                                            |Bristol 170 Freighter 21                |
|10335                                            |Fairchild R4Q / Dougas AD-6 skyraider   |
|10339                                            |Vickers 628 Viking 1B                   |
|1033A                                            |Lockheed 18 Lodestar                    |
|1033B                                            |Douglas DC-3                            |
|1033C                                            |Douglas DC-7-C                          |
|1007X                                            |Fokker Super Universal                  |
|1033P                                            |Douglas C-124C / Fairchild C-119C       |
|1033Q                                            |Junkers JU-52/3m                        |
|1033T                                            |Vickers Viscount 745D                   |
|1033X                                            |Douglas DC-3                            |
|1033Y                                            |de Havilland DH-114 Heron 2D            |
|1034                                             |Douglas DC-7 / F-100F                   |
|10341                                            |Douglas DC-7C                           |
|10342                                            |Vickers Viscount 745D / T-33A           |
|10349                                            |Avro 685 York C-1                       |
|1034E                                            |Douglas DC-3                            |
|1008                                             |Fokker FG III                           |
|1034H                                            |Curtiss C-46D                           |
|1034K                                            |Boeing 377 Stratocruiser 10-26          |
|1034M                                            |Lockheed 749A Constellation             |
|1034S                                            |Douglas DC-3                            |
|1035                                             |Convair CV-440-59                       |
|10352                                            |Douglas C-47A                           |
|10354                                            |Boeing KC-135A                          |
|10356                                            |Douglas C-47A                           |
|10357                                            |Vickers Viscount 748D                   |
|10358                                            |Douglas DC-3                            |
|10080                                            |Breguet 14                              |
|10359                                            |Douglas DC-4                            |
|1035A                                            |Lockheed 1049H Super Constellation      |
|1035D                                            |Convair CV-240-2                        |
|1035E                                            |Tupolev TU-104-A                        |
|1035H                                            |Lockheed C-130A-II Hercules             |
|1035K                                            |Vickers 621 Viking 1                    |
|1035L                                            |Douglas C-124C Globemaster              |
|1035N                                            |Curtiss C-46A-CU                        |
|1035S                                            |Boeing B-52 / Boeing B-52               |
|1035T                                            |Lockheed L-1049H Super Constellation    |
|10082                                            |Douglas M-4                             |
|1035X                                            |Lockheed C-130A Hercules                |
|10364                                            |Avro 685 York I                         |
|10365                                            |Fairchild C-123 Provider                |
|10366                                            |Lockheed 1049E Super Constellation      |
|10367                                            |Douglas C-47A                           |
|10368                                            |Tupolev TU-104A                         |
|1036C                                            |Lockheed WV-2 Super Constellation       |
|1036E                                            |Vickers Viscount 701C                   |
|1036K                                            |Vickers Viscount 755D                   |
|1036L                                            |Douglas C-47-DL                         |
|10084                                            |Bleriot Spad 56                         |
|1036M                                            |Douglas DC-3                            |
|1036N                                            |Martin Mariner                          |
|1036P                                            |Curtiss C-46F                           |
|1036Q                                            |SNCASE Languedoc                        |
|1036R                                            |Bristol 175 Britannia 312               |
|1036T                                            |Douglas DC-6B                           |
|1036U                                            |Saab Scandia                            |
|1036W                                            |Douglas DC-3                            |
|1036X                                            |Douglas DC-3                            |
|10371                                            |Douglas DC-3                            |
|10085                                            |Latecoere 32                            |
|10372                                            |Lockheed 1049G Super Constellation      |
|10374                                            |Curtiss C-46F                           |
|10375                                            |Curtiss C-46A-50-CU                     |
|10378                                            |Curtiss C-46D-15-CU                     |
|10379                                            |Convair CV-240-2                        |
|1037B                                            |Avro 688                                |
|1037G                                            |Douglas DC-3                            |
|1037J                                            |Beechcraft Bonanza 35                   |
|1037K                                            |Lockheed  188A Electra                  |
|1037L                                            |Vickers Viscount 794D                   |
|10086                                            |Hamilton H-47                           |
|1037M                                            |Curtiss C-46A                           |
|1037N                                            |Douglas DC-4                            |
|1037Q                                            |Vickers Viscount 763                    |
|1037T                                            |Douglas C-47A                           |
|1037V                                            |Bristol 170 Freighter 21E               |
|1037W                                            |Nord 2501 Noratlas                      |
|1037Z                                            |Douglas DC-3                            |
|10380                                            |Curtiss C-46A                           |
|10384                                            |Curtiss C-46F-1-CU                      |
|10385                                            |Avro 688 Super Trader                   |
|1000S                                            |Zeppelin L-23 (airship)                 |
|10089                                            |Douglas M-4                             |
|10387                                            |Douglas DC-3                            |
|10388                                            |Douglas DC-3                            |
|10389                                            |Lockheed C-69 Constellation             |
|1038A                                            |Vickers Viscount 745D                   |
|1038B                                            |Curtiss C-46A                           |
|1038D                                            |Douglas DC-3                            |
|1038E                                            |Curtiss C-46A-50-CU                     |
|1038F                                            |Curtiss C-46                            |
|1038H                                            |Douglas DC-4                            |
|1038J                                            |Lockheed 1649A Starliner                |
|1008A                                            |Travel Air 4000                         |
|1038N                                            |North American F-100D-25NA              |
|1038W                                            |Douglas DC-3                            |
|1038Z                                            |Vickers 815 Viscount                    |
|10392                                            |Boeing 707-123                          |
|10395                                            |Douglas DC-3                            |
|10396                                            |de Havilland DH-106 Comet 4             |
|1039A                                            |Curtiss C-46A                           |
|1039B                                            |Douglas DC-3                            |
|1039D                                            |Douglas DC-4                            |
|1039G                                            |Saab Scandia 90A-1                      |
|1008B                                            |Ford 4-AT-B Tri Motor                   |
|1039J                                            |Douglas DC-7C                           |
|1039K                                            |Douglas C-54B                           |
|1039M                                            |Lockheed 188A Electra                   |
|1039P                                            |Douglas C-47A-DL                        |
|1039S                                            |Douglas DC-3                            |
|1039T                                            |Douglas DC-3                            |
|1039U                                            |Douglas C-54A                           |
|1039W                                            |Douglas DC-7B                           |
|1039X                                            |Antonov AN-10                           |
|103AA                                            |Lockheed L-1049H Super Constellation    |
|1008C                                            |Dornier Wal                             |
|103AC                                            |Martin 202                              |
|103AE                                            |Curtiss C-46A                           |
|103AL                                            |Ilyushin IL-18                          |
|103AM                                            |Consolidated PBY-5A Catalina            |
|103AN                                            |Vickers 785D Viscount                   |
|103AR                                            |Vickers Viscount 827 / Fokker AT-6      |
|103AS                                            |Douglas C-47A                           |
|103AT                                            |Douglas DC-3                            |
|103AV                                            |Douglas C-47A                           |
|103AW                                            |Douglas DC-6B                           |
|1008D                                            |Junkers G24                             |
|103AZ                                            |de Havilland Canada U-1A Otter          |
|103B                                             |Vickers Viscount 745D                   |
|103BA                                            |Sud Aviation Caravelle 1                |
|103BB                                            |Ilyushin IL-18B                         |
|103BC                                            |Lockheed 1049E Super Constellation      |
|103BE                                            |de Havilland DH-114 Heron 2D            |
|103BH                                            |Douglas DC-4                            |
|103BJ                                            |Douglas DC-3 / USN R-6D-1               |
|103BM                                            |Douglas DC-7C                           |
|103BP                                            |Antonov AN-10                           |
|1008E                                            |Junkers G-31                            |
|103BS                                            |Consolidated PBY-5A Catalina            |
|103BU                                            |Douglas DC-3                            |
|103BW                                            |Lockheed 188C Electra                   |
|103BZ                                            |Curtiss C-46                            |
|103C                                             |Curtiss C-46A-40-CU                     |
|103CC                                            |Douglas DC-3                            |
|103CG                                            |Douglas DC-4                            |
|103CH                                            |Douglas C-124C Globemaster              |
|103CL                                            |Curtiss C-46                            |
|103CP                                            |Fairchild F-27 / Cessna 310             |
|1008F                                            |Douglas M-4                             |
|103CR                                            |Douglas C-54B                           |
|103CS                                            |Douglas DC-3                            |
|103CT                                            |Douglas DC-4-1009                       |
|103CW                                            |Douglas DC-6                            |
|103CX                                            |Curtiss C-46                            |
|103D                                             |Convair CV-880                          |
|103DA                                            |Fokker F-27 Friendship 100              |
|103DC                                            |Lockheed 749A-79-32 Constellation       |
|103DF                                            |Convair CV-340-62                       |
|103DG                                            |Goodyear ZPG-3W (airship)               |
|1008J                                            |Fairchild FC-2                          |
|103DJ                                            |Douglas DC-3                            |
|103DM                                            |Douglas C-47B-DK                        |
|103DR                                            |Douglas DC-7C                           |
|103DS                                            |Douglas DC-3                            |
|103DT                                            |Fairchild C-119G                        |
|103DU                                            |Sikorsky S-58C helicopter               |
|103DX                                            |Convair CV-240-4                        |
|103DY                                            |Douglas C-47                            |
|103E                                             |Ilyushin IL-18                          |
|103EA                                            |Avro Lancaster 1                        |
|1008K                                            |Blériot Spad 66                         |
|103EC                                            |Vickers 634 Viking 1B                   |
|103ED                                            |Lockheed 1049G Super Constellation      |
|103EE                                            |Douglas DC-6AB                          |
|103EM                                            |Douglas R5D-3                           |
|103EN                                            |Vickers Viscount 837                    |
|103ER                                            |Douglas DC-3 (C-53-DO)                  |
|103ES                                            |Vickers Viscount 739B                   |
|103EY                                            |Lockheed 188A Electra                   |
|103EZ                                            |de Havilland DH-114 Heron 2             |
|103FB                                            |Curtiss C-46F                           |
|1008L                                            |Fairchild FC-2                          |
|103FE                                            |Tupolev Tu-104A                         |
|103FF                                            |Douglas C-54A-DC                        |
|103FJ                                            |Curtiss C-46F-1-CU                      |
|103FK                                            |Douglas C-47A                           |
|103FP                                            |Fairchild F-27A                         |
|103FR                                            |Douglas DC-3                            |
|103FS                                            |Curtiss C-46A-60-CK                     |
|103FU                                            |Avro 691 Lancastrian IV                 |
|103FV                                            |Douglas DC-3                            |
|103G                                             |Lockheed 1649A Starliner                |
|1000T                                            |Zeppelin L-44 (airship)                 |
|1008M                                            |Stearman C-38                           |
|103GA                                            |Douglas C-124A-DL                       |
|103GB                                            |MD DC-8-11 / Lockheed  1049 S Const     |
|103GC                                            |Convair C-131D (CV-340-79)              |
|103GE                                            |Douglas DC-3                            |
|103GG                                            |Avia 14                                 |
|103GH                                            |Douglas DC-3                            |
|103GL                                            |McDonnell Douglas DC-8-21               |
|103GM                                            |Lockheed WV-2 Super Constellation       |
|103GP                                            |Douglas DC-3                            |
|103GR                                            |Douglas C-118A                          |
|1008N                                            |CMASA Wal                               |
|103GS                                            |Boeing 707-123                          |
|103GT                                            |Douglas DC-3                            |
|103GV                                            |Boeing B-707-320                        |
|103GW                                            |Douglas DC-3                            |
|103HC                                            |Douglas C-47DL                          |
|103HD                                            |Ilyushin IL-18                          |
|103HJ                                            |Handley Page Hastings C-2               |
|103HK                                            |McDonnell Douglas DC-8-53               |
|103HM                                            |Lockheed L-188C Electra                 |
|103HP                                            |Douglas C-54B-1-DC                      |
|1008Q                                            |Travel Air 4000                         |
|103HQ                                            |Curtiss C-46A                           |
|103HS                                            |Tupolev TU-104B                         |
|103HV                                            |McDonnell Douglas DC-8-12               |
|103HY                                            |Ilyushin IL-18B                         |
|103J                                             |Douglas DC-6                            |
|103JA                                            |Douglas DC-6A                           |
|103JC                                            |Douglas DC-3                            |
|103JD                                            |Vickers Viking 3B                       |
|103JF                                            |Curtiss C-46F                           |
|103JG                                            |de Havilland Canada DHC-3 Otter         |
|1008R                                            |Latecoere 26                            |
|103JH                                            |Lockheed 049 Constellation              |
|103JJ                                            |Douglas DC-3                            |
|103JK                                            |Douglas DC-3                            |
|103JL                                            |Douglas DC-3                            |
|103JM                                            |Douglas DC-6B                           |
|103JP                                            |Sud-Aviation Caravelle III              |
|103JR                                            |Douglas DC-6B                           |
|103JS                                            |Lockheed 188C  Electra                  |
|103JT                                            |Fokker F-27 Friendship 100              |
|103JY                                            |Douglas DC-3                            |
|1008W                                            |Ford 5-AT-B Tri Motor                   |
|103KA                                            |Handley Page Hastings C-2               |
|103KC                                            |Silver City Airways                     |
|103KF                                            |Douglas DC-7C                           |
|103KK                                            |Lockheed C-69 Constellation             |
|103KS                                            |Lockheed L-749A Constellation           |
|103L                                             |de Havilland Comet 4                    |
|103LA                                            |Douglas C-54 Skymaster                  |
|103LB                                            |Vickers Viscount 720                    |
|103LC                                            |Boeing 720-030B                         |
|103LF                                            |Fairchild C-119G / Fairchild C-119      |
|1008X                                            |Fokker F-VIIA                           |
|103LH                                            |Curtiss C-46                            |
|103LL                                            |de Havilland Comet 4B                   |
|103LM                                            |Grumman G-21A Goose                     |
|103LN                                            |Curtiss C-46D                           |
|103LS                                            |Antonov AN-10A                          |
|103LT                                            |Douglas DC-3                            |
|103LU                                            |Fairchild F-27                          |
|103MA                                            |Douglas C-47A                           |
|103MB                                            |Boeing B-707-123B                       |
|103MD                                            |Douglas DC-7C                           |
|1008Z                                            |Ford 5-AT-B Tri-Motor / B-PW-9D         |
|103MG                                            |Douglas DC-3                            |
|103MH                                            |Fairchild F-27                          |
|103MJ                                            |Douglas DC-6B                           |
|103MK                                            |Lockheed C-130A Hercules                |
|103MM                                            |Lockheed 1049H Super Constellation      |
|103MN                                            |Lockheed 1049H Super Constellation      |
|103MP                                            |Nord 2501 Noratlas                      |
|103MR                                            |Ilyushin IL-14                          |
|103MS                                            |Douglas C-47                            |
|103MT                                            |Douglas C-47A-1                         |
|1009                                             |Fokker F-III                            |
|103N                                             |Convair CV-440 -62                      |
|103NA                                            |Douglas C-47A                           |
|103NC                                            |Douglas C-47                            |
|103NJ                                            |Convair CV-240-0                        |
|103NN                                            |Consolidated Catalina                   |
|103NS                                            |Douglas DC-3                            |
|103PA                                            |Lockheed C-130A Hercules                |
|103PB                                            |Lockheed C121J                          |
|103PF                                            |Boeing B-707-124                        |
|103PG                                            |Boeing B-707-328                        |
|10091                                            |Cams 53                                 |
|103PH                                            |Tupolev Tu-104B                         |
|103PK                                            |Boeing B-707-328                        |
|103PP                                            |Antonov AN-10A                          |
|103PR                                            |Tupolev TU-104A                         |
|103PS                                            |Ilyushin IL-14                          |
|103PT                                            |McDonnell Douglas DC-8-43               |
|103PW                                            |Douglas DC-4                            |
|103PZ                                            |Douglas C-47A                           |
|103Q                                             |Douglas C-47                            |
|103RA                                            |de Havilland Comet 4C                   |
|10092                                            |Fokker F-X                              |
|103RC                                            |Bristol Britannia 314                   |
|103RD                                            |Antonov An-10A                          |
|103RE                                            |Douglas DC-3                            |
|103RF                                            |Douglas DC-3                            |
|103RH                                            |McDonnell Douglas DC-8-33               |
|103RJ                                            |Douglas DC-3                            |
|103RM                                            |Douglas DC-3                            |
|103RP                                            |Tupolev TU-104A                         |
|103RR                                            |Lockheed P2V-7                          |
|103RS                                            |Lockheed 18 Lodestar                    |
|1000U                                            |Zeppelin L-59 (airship)                 |
|10096                                            |Breguet 14                              |
|103RW                                            |Avia 14                                 |
|103S                                             |Boeing KC-135A                          |
|103SA                                            |Douglas C-47A                           |
|103SE                                            |Douglas C-47A                           |
|103SF                                            |Lockheed 1049H-82 Super Constellation   |
|103SG                                            |Vickers 757 Viscount                    |
|103SH                                            |Fokker F-27 Friendship 100              |
|103SJ                                            |de Havilland DH-125-1A                  |
|103SL                                            |Convair CV-340/440                      |
|103SM                                            |Tupolev TU-104B                         |
|10098                                            |Handley Page W-10                       |
|103SP                                            |Douglas DC-3                            |
|103SS                                            |Vickers 828 Viscount                    |
|103ST                                            |Vickers Viscount 745D                   |
|103SU                                            |Douglas C-54D                           |
|103SV                                            |Ilyushin IL-18D                         |
|103SW                                            |Saab Scandia / Cessna 310               |
|103SY                                            |Boeing B-707-441                        |
|103T                                             |Douglas DC-7B                           |
|103TB                                            |Douglas C-47                            |
|103TD                                            |Lockheed 049-46-21 Constellation        |
|1009A                                            |Ford 5-AT-B Tri-Motor                   |
|103TE                                            |Lockheed 1049H Super Constellation      |
|103TG                                            |Vickers Viscount 804                    |
|103TL                                            |KB-50                                   |
|103TM                                            |Convair CV-240-2                        |
|103TN                                            |Channel Air Bridge                      |
|103TR                                            |Boeing B307-1 Stratoliner               |
|103TS                                            |Bell 74G                                |
|103TT                                            |Beech AT-11                             |
|103TW                                            |Convair CV-240-0                        |
|103TX                                            |Fairchild F-27                          |
|1009C                                            |Domier Delphin III                      |
|103U                                             |Curtiss C-46F                           |
|103UC                                            |Vickers Viscount 812                    |
|103UL                                            |Lockheed P-3A Orion                     |
|103US                                            |Vickers Viscount 754D                   |
|103UV                                            |Lockheed 1049H Super Constellation      |
|103V                                             |Antonov An-10A                          |
|103VK                                            |Boeing B-720-051B                       |
|103VS                                            |Douglas DC-7                            |
|103VT                                            |Douglas DC-3                            |
|103VU                                            |Piper PA-24-250 Comanche                |
|1009D                                            |Travel Air 4000                         |
|103VV                                            |Avro 685 York C1                        |
|103VW                                            |Douglas DC-6B                           |
|103W                                             |de Havilland Comet 4C                   |
|103WA                                            |H-21B                                   |
|103WC                                            |Convair CV-440                          |
|103WD                                            |Douglas DC-3                            |
|103WE                                            |Vickers Viscount 759D                   |
|103WG                                            |Douglas DC-6B                           |
|103WH                                            |Convair CV-340-59                       |
|103WL                                            |Douglas DC-3                            |
|1009E                                            |Lockheed Vega                           |
|103WM                                            |Douglas DC-7CF                          |
|103WW                                            |Douglas C-47                            |
|103X                                             |Douglas DC-3                            |
|103XE                                            |VEB 14P                                 |
|103XS                                            |Douglas C-47A                           |
|103XT                                            |Fairchild C-119                         |
|103YK                                            |Kaiser-Fraser C-119G                    |
|103ZZ                                            |Douglas DC-3                            |
|104                                              |Martin 404                              |
|1040                                             |Douglas DC-3                            |
|1009F                                            |Breguet 14                              |
|10402                                            |Tupolev TU-104B                         |
|10403                                            |Douglas C-47                            |
|10404                                            |Curtiss C-46F                           |
|1040C                                            |de Havilland Comet 4C                   |
|1040D                                            |Avro Shackleton MR3                     |
|1040F                                            |Vickers Viscount 708                    |
|1040H                                            |Curtiss C-46F-1-CU                      |
|1040J                                            |de Havilland DH-114 Heron               |
|1040K                                            |Tupelov Tu-124                          |
|1040P                                            |Boeing KC-135A / Boeing KC-135A         |
|1009G                                            |Kalinin K-4                             |
|1040R                                            |Sud-Aviation Caravelle III              |
|1040T                                            |Vickers Viking 1B                       |
|1040U                                            |Vickers Viscount 768D                   |
|1040V                                            |Douglas C-133A                          |
|1040W                                            |Douglas C-74                            |
|1040X                                            |Boeing Vetrol 107 II helicopter         |
|1040Z                                            |Antonov AN-12                           |
|1041                                             |Ilyushin IL-14                          |
|10410                                            |BAC One-Eleven 200AB                    |
|10416                                            |Douglas DC-3                            |
|1009H                                            |Fokker FG II                            |
|10418                                            |McDonnell Douglas DC-8F-54F             |
|10419                                            |Curtis C-46A-20-CU                      |
|1041A                                            |Boeing B-707-121                        |
|1041C                                            |Douglas C-54A                           |
|1041G                                            |Vickers 634 Viking 1B                   |
|1041H                                            |Douglas DC-6B                           |
|1041L                                            |Douglas DC-3                            |
|1041M                                            |Piper PA-23                             |
|1041P                                            |Douglas C-47A                           |
|1041Q                                            |Beech D18S                              |
|1009L                                            |Lockheed Vega                           |
|1041S                                            |Douglas DC-3                            |
|1041U                                            |Piper PA-23                             |
|1041W                                            |Piper Aero Commander 560E               |
|1041X                                            |Ilyushin IL-14                          |
|1042                                             |Douglas DC-3                            |
|10420                                            |Fairchild C-119                         |
|10421                                            |Beechcraft C35                          |
|10422                                            |McDonnell Douglas DC-8-21               |
|10425                                            |Convair CV-240-0                        |
|1042A                                            |Bristol Britannia 312                   |
|1000V                                            |Zeppelin L-70 (airship)                 |
|1009M                                            |Ford 5-AT-B Tri Motor                   |
|1042B                                            |Lockheed 049 Constellation              |
|1042C                                            |Douglas DC-3                            |
|1042D                                            |Douglas DC-3                            |
|1042E                                            |Douglas DC-4                            |
|1042G                                            |Douglas DC-3C                           |
|1042J                                            |Piper PA-23                             |
|1042K                                            |Vickers Viscount 785D                   |
|1042M                                            |Douglas C-54A-10-DC                     |
|1042P                                            |Douglas DC-3                            |
|1042Q                                            |Sud Aviation Caravelle 3                |
|1009P                                            |de Havilland DH-66 Hercules             |
|1042R                                            |Cessna 185                              |
|1042S                                            |Fairchild F-27A                         |
|1042T                                            |Douglas C-54                            |
|1042U                                            |Douglas C-54                            |
|1042W                                            |Boeing C-135B                           |
|1042X                                            |de Havilland Canada DHC-3 Otter         |
|1042Z                                            |Douglas C-47-DL                         |
|1043                                             |Piper PA-24                             |
|10432                                            |Douglas C-47A                           |
|10433                                            |Aero Commander 680                      |
|1009Q                                            |Latecoere 25-3-R                        |
|10436                                            |Curtiss C-46-CU                         |
|10438                                            |Douglas DC-3                            |
|10439                                            |Lockheed 12A                            |
|1043B                                            |Caravelle VIR                           |
|1043C                                            |Boeing B-707-331                        |
|1043D                                            |Vickers Viscount 745D                   |
|1043F                                            |Piper PA-28                             |
|1043H                                            |Douglas DC-7B                           |
|1043J                                            |Beechcraft 35-B33 Debonair              |
|1043K                                            |Piper PA-18                             |
|1009X                                            |Fairchild 71                            |
|1043N                                            |Piper PA-23                             |
|1043Q                                            |Douglas C-47A-25-DK                     |
|1043S                                            |Ilyushin IL-18B                         |
|1043T                                            |Vickers Viscount 710C                   |
|1043U                                            |Douglas C-47                            |
|1043W                                            |Douglas C-47A                           |
|1043X                                            |Douglas DC-6B                           |
|1043Z                                            |Lockheed L-749A-79 Constellation        |
|10440                                            |Ilyushin IL-14                          |
|10442                                            |Hughes 269B                             |
|1009Z                                            |Pitcairn PA-6 Mailwing                  |
|10443                                            |Ilyushin IL-18                          |
|10444                                            |Beechcraft C45G                         |
|10445                                            |Fairchild F-27A                         |
|10446                                            |Lockheed P-3A                           |
|10448                                            |Beechcraft C-45H                        |
|1044D                                            |Douglas DC-4                            |
|1044E                                            |Cessna 206                              |
|1044F                                            |Douglas DC-3                            |
|1044G                                            |Fairchild C-123                         |
|1044H                                            |Douglas DC-3                            |
|100A                                             |Short Calcutta                          |
|1044J                                            |Douglas DC-3                            |
|1044L                                            |Lockheed L-1049H Super Constellation    |
|1044M                                            |Curtiss C-46                            |
|1044N                                            |Curtis C-46A                            |
|1044Q                                            |Cessna 182B                             |
|1044S                                            |Cessna 180E                             |
|1044T                                            |Boeing KC-135A                          |
|1044V                                            |Curtiss C-46                            |
|1044W                                            |Douglas C-124C                          |
|10450                                            |Curtiss C-46A                           |
|100AB                                            |Stearman C-38                           |
|10452                                            |Douglas DC-6B                           |
|10453                                            |Douglas DC-7B                           |
|10454                                            |Curtiss C-46A                           |
|10455                                            |Douglas DC-3                            |
|10456                                            |Beechcraft B-35                         |
|10457                                            |Lockheed C-130E Hercules                |
|10458                                            |Douglas DC-3                            |
|10459                                            |Tupolev TU-124                          |
|1045A                                            |Handley Page HPR-7 Herald 211           |
|1045C                                            |Douglas C-47                            |
|100AC                                            |Loening C-2C                            |
|1045E                                            |Canadair CP-107 MK-2                    |
|1045F                                            |Douglas C-47                            |
|1045J                                            |Convair CV-440-62                       |
|1045K                                            |Beech C-45H                             |
|1045L                                            |Handley Page Dart Herald 207            |
|1045Q                                            |Douglas C-47B                           |
|1045R                                            |Piper PA-24                             |
|1045S                                            |Douglas DC-6A                           |
|1045W                                            |Lockheed 1049G-55 Super Constellation   |
|1045X                                            |Boeing B-720-040B                       |
|100AE                                            |Lockheed Vega 5                         |
|1045Y                                            |Bell UH-1D / Bell UH1D (helicopters)    |
|10460                                            |Boeing C-135A                           |
|10469                                            |Boeing B-707-321B                       |
|1046B                                            |Boeing B-707-124                        |
|1046E                                            |Fokker F-27 Friendship 200              |
|1046G                                            |Handley Page Hastings C Mark 1          |
|1046K                                            |Antonov AN-12                           |
|1046M                                            |Douglas DC-6B                           |
|1046U                                            |EC-121H (Super Constellation)           |
|1046V                                            |de Havilland 106A                       |
|100AG                                            |Junkers G-24                            |
|1046W                                            |Lockheed P2V-7                          |
|1046X                                            |Douglas C-47                            |
|1046Y                                            |Douglas C-54D                           |
|1046Z                                            |Curtiss C-46A                           |
|1047                                             |Boeing B-727-22                         |
|10470                                            |Vickers 804 Viscount                    |
|10471                                            |Lockheed KC-130F                        |
|10473                                            |Aero Commander 680                      |
|10474                                            |Douglas DC-3A                           |
|10475                                            |Douglas DC-3                            |
|10001                                            |Curtiss seaplane                        |
|1000W                                            |Zeppelin L-53 (airship)                 |
|100AH                                            |Liore et Olivier 190                    |
|10477                                            |Transportes Aéreos Orientales           |
|10478                                            |Douglas DC-3                            |
|1047A                                            |Boeing B-707-121B                       |
|1047B                                            |Douglas C-47                            |
|1047C                                            |Douglas DC-3 / Piper PA-18A             |
|1047E                                            |Douglas C-47A                           |
|1047F                                            |Boeing 307 Stratoliner B-1              |
|1047H                                            |Douglas DC-3                            |
|1047J                                            |Vickers Vanguard 951                    |
|1047L                                            |Douglas C-47A                           |
|100AJ                                            |Stearman M-2 Speedmail                  |
|1047M                                            |Douglas C-54                            |
|1047N                                            |Douglas C-47DL                          |
|1047Q                                            |Boeing B-727-23                         |
|1047U                                            |Tupolev TU-124                          |
|1047V                                            |Boeing B-727-22                         |
|1047W                                            |Beechcraft C-45H                        |
|1047X                                            |Learjet 23                              |
|1047Y                                            |Douglas C-53-DO (DC-3A)                 |
|1047Z                                            |Boeing B-707-131B / L1049C Constellation|
|10480                                            |Curtiss C-46D                           |
|100AK                                            |Douglas M-3                             |
|10481                                            |Douglas DC-3                            |
|10485                                            |Fairchild C-123C                        |
|10487                                            |Cessna 120                              |
|10488                                            |Douglas DC-3A                           |
|1048A                                            |Beechcraft G35                          |
|1048C                                            |Douglas DC-3 / Douglas DC-3             |
|1048D                                            |Douglas DC-6-54B                        |
|1048E                                            |Douglas DC-3                            |
|1048F                                            |Boeing B-707-437                        |
|1048H                                            |Fairchild C-123B                        |
|100AL                                            |Bernard 192                             |
|1048L                                            |Beechcraft B95A                         |
|1048M                                            |Convair CV-440-0                        |
|1048Q                                            |Boeing B-727-81                         |
|1048T                                            |Fokker F-27 Friendship 200              |
|1048X                                            |Beechcraft D35                          |
|1048Y                                            |Sud Aviation SE-210 Caravelle VIN       |
|1049                                             |Douglas DC-6B                           |
|10492                                            |McDonnell Douglas DC-8-43               |
|10493                                            |de Havilland 104-6A                     |
|10495                                            |Boeing B-707-436                        |
|100AM                                            |Arado V1                                |
|10498                                            |Piper PA-32                             |
|10499                                            |Grumman G-21A                           |
|1049A                                            |Douglas DC-6A                           |
|1049C                                            |Antonov AN-24B                          |
|1049D                                            |Curtiss C-46F                           |
|1049F                                            |Cessna 172D                             |
|1049H                                            |Lockheed P-3A Orion                     |
|1049J                                            |Douglas C-47A                           |
|1049K                                            |Lockheed 188C Electra                   |
|1049P                                            |Lockheed 749A Constellation             |
|100AN                                            |Travel Air B6000                        |
|1049S                                            |Boeing CH47A (helicopter)               |
|1049T                                            |Cessna 180                              |
|1049W                                            |Boeing KC-135A                          |
|1049X                                            |Curtiss C-46A                           |
|1049Y                                            |Curtiss C-46E                           |
|1049Z                                            |Douglas DC-3                            |
|104A                                             |Piper PA-23                             |
|104AA                                            |Douglas DC-3                            |
|104AB                                            |Douglas DC-8-52                         |
|104AC                                            |Beechcraft H50                          |
|100AP                                            |Boeing 95                               |
|104AE                                            |Curtiss C-46D                           |
|104AF                                            |BAC One-Eleven 203AE                    |
|104AG                                            |Ilyushin IL-14                          |
|104AH                                            |Douglas DC-8-51                         |
|104AL                                            |Beech C-18S                             |
|104AM                                            |Cessna 310C                             |
|104AP                                            |Chance Vought F-8E                      |
|104AR                                            |Curtiss C-46F-1-CU                      |
|104AS                                            |Grumman G-21 Goose                      |
|104AU                                            |Bristol Britannia 102                   |
|100AR                                            |Farman 190                              |
|104AW                                            |Sud Aviation SE-210 Caravelle           |
|104AZ                                            |Douglas DC-3                            |
|104B                                             |Vickers Viscount 832                    |
|104BA                                            |Douglas DC-4                            |
|104BC                                            |McDonnell Douglas DC-9-14               |
|104BD                                            |de Havilland Canada CV-2B Caribou       |
|104BE                                            |Bell 204B helicopter                    |
|104BK                                            |Antonov AN-24                           |
|104BL                                            |Piper PA-32                             |
|104BM                                            |Beech D18S                              |
|100AS                                            |Ford 5-AT-C Tri Motor                   |
|104BN                                            |Cessna 205A                             |
|104BP                                            |Lockheed EC-121H                        |
|104BR                                            |NAMC-YS-11-111                          |
|104BS                                            |Boeing 727-21                           |
|104BU                                            |Martin 404                              |
|104BV                                            |Douglas DC-3                            |
|104BW                                            |Ilyushin IL-18B                         |
|104BY                                            |Douglas C-47D                           |
|104BZ                                            |PBY-5A Catalina                         |
|104CA                                            |Tupolev TU-114B                         |
|100AT                                            |Latecoere 25                            |
|104CC                                            |Lockheed L-1649A Starliner              |
|104CD                                            |Canadair CL-44D4-1                      |
|104CF                                            |Douglas C-47A-80-DL                     |
|104CH                                            |Beechcraft D18S                         |
|104CL                                            |Curtiss C-46F                           |
|104CM                                            |S2F-1 / HSS-2                           |
|104CP                                            |Piper PA-23                             |
|104CV                                            |Douglas C-54A                           |
|104CX                                            |Douglas DC-3                            |
|104D                                             |Handley Page HPR-7 Herald 214           |
|1000Y                                            |De Havilland DH-4                       |
|100AW                                            |Travel Air A6000A                       |
|104DA                                            |Cessna 210-5A                           |
|104DB                                            |Antonov AN-24                           |
|104DC                                            |Antonov AN-12                           |
|104DD                                            |Convair CV-440                          |
|104DE                                            |Cessna 182                              |
|104DF                                            |Lockheed L-188C Electra                 |
|104DG                                            |Douglas DC-6                            |
|104DJ                                            |Fokker F-27 Friendship 100              |
|104DL                                            |McDonnell Douglas DC-8-33               |
|104DM                                            |Convair CV-380                          |
|100AX                                            |Pitcairn PA-6 Mailwing                  |
|104DN                                            |AT L98 Carvair                          |
|104DP                                            |MD Douglas DC-9-15 / Beechcraft Baron-55|
|104DT                                            |Douglas C-47J                           |
|104DU                                            |Fairchild F-27                          |
|104DV                                            |de Havilland Canada DHC-6 Twin Otter 100|
|104DW                                            |Vickers Viscount 818                    |
|104E                                             |Beechcraft D18S                         |
|104ED                                            |Beechcraft 95-55                        |
|104EE                                            |McDonnell Douglas DC-8-51               |
|104EG                                            |Piper PA-30                             |
|100AZ                                            |Farman F-63                             |
|104EJ                                            |Lockheed 18 Lodestar                    |
|104EK                                            |Beech C-45H                             |
|104EP                                            |Curtiss-Wright C-46                     |
|104ER                                            |Douglas DC-4                            |
|104ES                                            |Lockheed C-130B                         |
|104ET                                            |Bristol Britannia 175                   |
|104EW                                            |EC-121H (Super Constellation)           |
|104FA                                            |Douglas DC-3                            |
|104FD                                            |Fokker F-27 Friendship 400              |
|104FE                                            |Lockheed P-3A Orion                     |
|100BA                                            |Fairchild 71                            |
|104FF                                            |de Havilland DH-104 / Piper PA-28       |
|104FM                                            |Cessna 205                              |
|104FP                                            |Douglas C-47-DL                         |
|104FR                                            |Curtiss C-46T                           |
|104FS                                            |Douglas DC-8-54F                        |
|104GB                                            |Douglas C54A                            |
|104GC                                            |Canadair C-4 Argonaut                   |
|104GD                                            |Lockheed C-130B Hercules                |
|104GF                                            |Douglas DC-3                            |
|104GH                                            |Bristol 170 Freighter 31E               |
|100BB                                            |Latecoere 28                            |
|104GK                                            |Douglas DC-3A-197D                      |
|104GM                                            |Douglas C-47                            |
|104GP                                            |Lockheed C-130E-I Hercules              |
|104GR                                            |Lockheed C-130B                         |
|104GS                                            |Vickers 803 Viscount                    |
|104GT                                            |Lockheed L-1049H Super Constellation    |
|104GX                                            |BAC One Eleven 204AF                    |
|104H                                             |Bell UH-1B / Sikorsky CH53A helicopters |
|104HE                                            |Douglas DC-3                            |
|104HF                                            |Sud Aviation SE-210 Caravelle III       |
|100BC                                            |Ford Tri-Motor 5                        |
|104HH                                            |Fokker F-27 Friendship 100              |
|104HJ                                            |Douglas DC-4-1009                       |
|104HP                                            |Boeing B-727-22 / Cessna 310            |
|104HQ                                            |Douglas DC-3                            |
|104HR                                            |Douglas DC-3                            |
|104HS                                            |Piper PA-32                             |
|104HT                                            |Breguet 1150                            |
|104HY                                            |Fairchild C-123K                        |
|104JA                                            |Ilyushin IL-18                          |
|104JB                                            |Beech C-45H                             |
|100BE                                            |Dornier Wal                             |
|104JC                                            |Lockheed C130B                          |
|104JD                                            |Cessnea 172                             |
|104JF                                            |de Havilland Comet 4B                   |
|104JG                                            |Beechcraft N35                          |
|104JH                                            |Douglas DC-3                            |
|104JK                                            |Aero Commander 560                      |
|104JL                                            |Sud Aviation Caravelle 10R              |
|104JP                                            |Convair CV-880-22M-3                    |
|104JR                                            |Boeing B-707-131                        |
|104JS                                            |Ilyushin IL-18B                         |
|100BF                                            |Lockheed Vega 5                         |
|104JV                                            |Convair CV-880-22-1                     |
|104JW                                            |Hiller FH1100                           |
|104JY                                            |Beech C-45H                             |
|104K                                             |de Havilland Canada C-7A Caribou        |
|104KB                                            |Douglas DC-3                            |
|104KG                                            |Douglas DC-C-54A                        |
|104KJ                                            |Beechcraft 18H                          |
|104KK                                            |Bell 47J-2A                             |
|104KM                                            |Piper PA-32                             |
|104KP                                            |Avro Shackleton MR-3                    |
|100BG                                            |Ford 5-AT-C Tri Motor                   |
|104KV                                            |Douglas C-47A                           |
|104L                                             |Douglas DC-3                            |
|104LA                                            |Antonov AN-24                           |
|104LB                                            |Beechcraft 95-55B                       |
|104LD                                            |Beechcraft E18S                         |
|104LG                                            |Cessna 180H                             |
|104LH                                            |Sikorsky CH-53A (helicopter)            |
|104LJ                                            |Douglas C-54P                           |
|104LN                                            |Douglas DC-3                            |
|104LR                                            |Lockheed P-3A                           |
|100BH                                            |Sabca F-VII                             |
|104LS                                            |Boeing KC-135A                          |
|104LU                                            |de Havilland DH-114 Heron 1B            |
|104LV                                            |Lockheed P-3B Orion                     |
|104LW                                            |Boeing B-707-138B                       |
|104M                                             |Antonov AN-12BP                         |
|104MA                                            |Boeing B-727-92C                        |
|104MB                                            |Cessna 210                              |
|104ME                                            |Douglas DC-3                            |
|104MF                                            |Ilyushin IL-18D                         |
|104MJ                                            |Boeing B-707-328C                       |
|1000Z                                            |De Havilland DH-4                       |
|100BJ                                            |NaN                                     |
|104MK                                            |Fairchild C-123K                        |
|104MM                                            |Fairchild F-27                          |
|104MN                                            |Douglas DC6B                            |
|104MQ                                            |Cessna 182                              |
|104MR                                            |Brantly 305                             |
|104MT                                            |Vickers Viscount 803                    |
|104MX                                            |McDonnell Douglas DC-9 and Cessna 150F  |
|104N                                             |MiG-15 UTI                              |
|104NN                                            |Lockheed P-3B Orion                     |
|104NR                                            |Boeing B-707-465                        |
|100BK                                            |Royal Airship Works R-101               |
|104NS                                            |Douglas DC-3                            |
|104P                                             |Cessna 182                              |
|104PA                                            |Douglas DC-3                            |
|104PB                                            |Avro Shackleton MR-2                    |
|104PC                                            |Bell UH-1H / Bell UH-1H (helicopter)    |
|104PD                                            |Boeing B-707-344C                       |
|104PF                                            |Ilyushin IL-18V                         |
|104PH                                            |Bell 206A                               |
|104PJ                                            |Lockheed Martin L-100-10                |
|104PK                                            |Lockheed L188A Electra                  |
|100BN                                            |Messerschmitt M-20B                     |
|104PP                                            |Armstrong Whitworth Argosy C-1          |
|104PS                                            |Lockheed C-130B Hercules                |
|104PT                                            |Piper PA-23                             |
|104PW                                            |Sikorsky S-61L helicopter               |
|104PZ                                            |Convair CV-990-30A-5                    |
|104Q                                             |Cessna 411                              |
|104QS                                            |Boeing B-707-321C                       |
|104QT                                            |Piaggio PD-808                          |
|104R                                             |Antonov An-12 - Ilyshin IL-14           |
|104RB                                            |Bell UH-1H / Bell UH-1H / Bell UH-1H    |
|100BR                                            |Latecoere 28                            |
|104RC                                            |Douglas DC-3 (C-47-DL)                  |
|104RD                                            |Airspeed AS.57 Ambassador 2             |
|104RF                                            |Piper PA-23                             |
|104RG                                            |Convair CV-340-68B                      |
|104RJ                                            |Boeing 707-329C                         |
|104RL                                            |Curtiss C-46C                           |
|104RN                                            |Curtiss C-46D                           |
|104RR                                            |Douglas C-124C                          |
|104RS                                            |Cessna 182H                             |
|104RT                                            |McDonnell Douglas DC-8                  |
|100BS                                            |Lockheed Vega                           |
|104RV                                            |Convair CV-580 / Cessna 150             |
|104RW                                            |Vickers Viscount 739A                   |
|104SB                                            |Fairchild-Hiller FH-227B                |
|104SC                                            |Douglas DC-4                            |
|104SE                                            |Sikorsky S-61L helicopter               |
|104SF                                            |Antonov AN-24V                          |
|104SG                                            |Hawker Siddeley HS-748-215-2            |
|104SH                                            |Cessna 172                              |
|104SJ                                            |de Havilland Canada DHC-3 Otter         |
|104SK                                            |Ilyushin IL-18                          |
|100BU                                            |Handley Page W-8                        |
|104SP                                            |Cessna 402 / Piper PA-28                |
|104SR                                            |Sud-Aviation Caravelle 3                |
|104ST                                            |Boeing KC-135A                          |
|104SU                                            |Douglas C-54B                           |
|104SW                                            |Beechcraft D50A                         |
|104SX                                            |de Havilland Canada C-7B Caribou        |
|104SY                                            |de Havilland C-7B / Boeing Vertol CH-47A|
|104T                                             |de Havilland DH-104                     |
|104TA                                            |Britten-Norman BN-2 Islander            |
|104TB                                            |Piper PA-23                             |
|100BV                                            |Pitcairn PA-6 Mailwing                  |
|104TC                                            |Avia 14-40                              |
|104TD                                            |Lockheed C-130E Hercules                |
|104TE                                            |Douglas C-47A-25                        |
|104TM                                            |Douglas C-47D                           |
|104TN                                            |Fairchild-Hiller FH227C                 |
|104TP                                            |Aero Commander 680-E                    |
|104TQ                                            |McDonnell Douglas DC-8-62               |
|104TR                                            |de Havilland Canada DHC-6 Twin Otter 200|
|104TT                                            |Curtiss C-46D-20-CU                     |
|104TV                                            |Cessna 185                              |
|100BW                                            |Junkers G-24                            |
|104U                                             |Fairchild F-27B                         |
|104UC                                            |Beechcraft E18S                         |
|104US                                            |Aero Commander 560-F                    |
|104UV                                            |Boeing B-707-321B                       |
|104UW                                            |Convair CV-580                          |
|104VA                                            |Lockheed L-100 Hercules                 |
|104VP                                            |Boeing 707-321CF                        |
|104VR                                            |Douglas DC-3                            |
|104VU                                            |Convair CV-580                          |
|104VV                                            |Lockheed C-130E Hercules                |
|100BY                                            |Boeing 40                               |
|104WB                                            |de Havilland DHC-6                      |
|104WD                                            |Vickers Viscount 720                    |
|104WH                                            |Douglas DC-3                            |
|104WL                                            |Douglas DC-3D                           |
|104WM                                            |Bell 205A                               |
|104WP                                            |Boeing B-727-113C                       |
|104WT                                            |Convair CV-580                          |
|104WW                                            |Douglas DC-3                            |
|104WY                                            |McDonnell Douglas DC-8-62               |
|104X                                             |NaN                                     |
|100BZ                                            |Loening C-W Air Yaht                    |
|104XP                                            |Boeing B-727-22QC                       |
|104Y                                             |Lockheed HC-130H Hercules               |
|104YK                                            |Beechcraft C-45H                        |
|104ZU                                            |Lockheed C-130H                         |
|104ZZ                                            |Douglas DC-3                            |
|105                                              |Handley Page Dart Herald 201            |
|10500                                            |de Havilland DH-114 Heron 2D            |
|10504                                            |McDonnell Douglas DC-9-32               |
|10505                                            |Bell 47G2A1 / Cessna 150H               |
|10507                                            |Ilyushin IL-18D                         |
|1001                                             |De Havilland DH-4                       |
|100C                                             |Fokker F-VII                            |
|10508                                            |Douglas DC-3                            |
|10509                                            |Curtiss C-46F                           |
|1050A                                            |Antonov AN-24V                          |
|1050B                                            |Boeing Vertol CH47C (helicopter)        |
|1050C                                            |Vickers 757 Viscount                    |
|1050F                                            |Lockheed EC-121M                        |
|1050K                                            |Curtiss C-46                            |
|1050Q                                            |de Havilland DHC-2                      |
|1050R                                            |Fokker F-27 Friendship 100              |
|1050T                                            |Douglas DC-3                            |
|100CA                                            |Boeing 40                               |
|1050V                                            |Lockheed EC121R                         |
|10510                                            |Douglas DC-3                            |
|10511                                            |Douglas C-47A                           |
|10516                                            |Boeing Vertol CH47A (helicopter)        |
|10518                                            |Curtiss C-46F                           |
|1051A                                            |Douglas C-47                            |
|1051E                                            |Fokker F-27 Friendship 600              |
|1051H                                            |Boeing B-727-64                         |
|1051K                                            |Cessna 337C                             |
|1051Q                                            |Boeing RC-135E                          |
|100CB                                            |Desoutter II                            |
|1051S                                            |Beechcraft 99                           |
|1051T                                            |Fairchild C-119                         |
|1051V                                            |Beechcraft B-99                         |
|1051X                                            |Douglas DC-3                            |
|1051Y                                            |Grumman G-44A                           |
|1051Z                                            |de Havilland Canada DHC-6 Twin Otter 200|
|10520                                            |Cessna 320                              |
|10522                                            |De Havilland DH-104 Dove                |
|10523                                            |Boeing 707-331C                         |
|10524                                            |Sud Aviation SE-210 Caravelle 6N        |
|100CC                                            |Fokker Universal F-14                   |
|10525                                            |Bell 47G3B1                             |
|10526                                            |Lockheed L-1049H Super Constellation    |
|10528                                            |Bell 47G-2                              |
|1052A                                            |Pilatus Pc-6C                           |
|1052E                                            |Douglas C-47B                           |
|1052F                                            |Ilyushin IL-18                          |
|1052H                                            |Boeing B-707-328B                       |
|1052L                                            |Antonov An-12PL                         |
|1052M                                            |Cessna 172H                             |
|1052T                                            |Douglas C-47                            |
|100CD                                            |Latecoere 32                            |
|1052W                                            |Lockheed EC121R                         |
|1052Y                                            |Douglas DC-3                            |
|1053                                             |MD Douglas DC-9-31/Piper Cherokee PA-28 |
|10532                                            |BAC One-Eleven 402AP                    |
|10534                                            |Douglas DC-3                            |
|1053B                                            |Convair CV-640                          |
|1053D                                            |Douglas DC-4 / USAF F-4E                |
|1053G                                            |Boeing B-727-64                         |
|1053H                                            |Douglas DC-6B                           |
|1053L                                            |Boeing C-97                             |
|100CE                                            |Avro 10                                 |
|1053P                                            |Grumman C-2A                            |
|1053T                                            |Beechcraft 65-B80                       |
|1053W                                            |Douglas C-47B                           |
|1053X                                            |Cessna 180H                             |
|1053Y                                            |Antonov An-12TB                         |
|10547                                            |Fairchild-Hiller FH-227B                |
|10548                                            |BAC VC-10-1101                          |
|1054A                                            |Douglas DC-6B                           |
|1054C                                            |Piper PA-23                             |
|1054D                                            |LTVF-8J                                 |
|100CF                                            |Fokker F10A Trimotor                    |
|1054E                                            |Douglas DC-6B                           |
|1054K                                            |Douglas C-47A-25-DK                     |
|1054M                                            |Cessna 180                              |
|1054Q                                            |Convair CV-990-30A-5                    |
|1054T                                            |Douglas C-47                            |
|1054U                                            |Douglas DC-3                            |
|1054V                                            |Douglas DC-4                            |
|1054W                                            |Beechcraft TC-45J                       |
|1054X                                            |Convair CV-240-2                        |
|1055                                             |Fokker F-27 Friendship 200              |
|100CG                                            |Messerschmitt M-20                      |
|10550                                            |Antonov AN-24                           |
|10551                                            |De Havilland Dove                       |
|10552                                            |Tupolev TU-124                          |
|10554                                            |Hawker Siddeley HS-748 1                |
|10557                                            |Antonov AN-24V                          |
|1055A                                            |Ilyushin IL-18V                         |
|1055C                                            |de Havilland Canada DHC-6 Twin Otter 100|
|1055E                                            |Douglas DC-3 (C-47-DL)                  |
|1055F                                            |McDonnell Douglas DC-9-32               |
|1055H                                            |Cessna 402                              |
|100CJ                                            |Boeing 40                               |
|1055J                                            |Douglas DC-3                            |
|1055M                                            |Convair CV-990-30A-6                    |
|1055R                                            |Handley Page Jetstream 1                |
|1055T                                            |Fairchild-Hiller FH-227B                |
|1055V                                            |Lockheed EC-121P                        |
|1055W                                            |Beechcraft C-45H                        |
|1055X                                            |Piper PA-32                             |
|1055Z                                            |Aerospatiale Caravelle 3                |
|1056                                             |Antonov AN-24V                          |
|10562                                            |Piper PA-32                             |
|100CM                                            |Junkers W-34                            |
|10568                                            |Lockheed AC-130A Hercules               |
|10569                                            |Hawker Siddeley HS-748-209              |
|1056B                                            |Fairchild C-119G                        |
|1056D                                            |de Havilland Canada DHC-6 Twin Otter 100|
|1056E                                            |McDonnell Douglas DC-9-33CF             |
|1056F                                            |Convair CV-240                          |
|1056H                                            |Vickers 785D Viscount                   |
|1056J                                            |Fokker F-27 Friendship 100              |
|1056L                                            |Gates Learjet 23                        |
|1056Q                                            |Antonov AN-10                           |
|10011                                            |De Havilland DH-4                       |
|100CN                                            |Boeing 95                               |
|1056T                                            |Curtiss C-46A-55-CK                     |
|10571                                            |de Havilland DH-114 Heron 1B            |
|10572                                            |Martin 404                              |
|10574                                            |Tupolev TU-104A                         |
|10575                                            |Fokker F-27 Friendship 100              |
|10577                                            |Fokker F-27 Friendship 400M             |
|10578                                            |Douglas DC-3                            |
|10579                                            |de Havilland Comet 4                    |
|1057D                                            |McDonnell Douglas DC-8-63               |
|1057F                                            |Antonov AN-22                           |
|100CR                                            |Fokker F-VIIB                           |
|1057G                                            |Cessna 310J                             |
|1057H                                            |McDonnell Douglas DC-8-63AF             |
|1057J                                            |Nord 2501 Noratlas                      |
|1057K                                            |Lockheed P-3A Orion                     |
|1057N                                            |Fokker F-27 Friendship 200              |
|1057Q                                            |Lockheed 188A Electra                   |
|1057R                                            |NAMC YS-11A-219                         |
|1057T                                            |Boeing Vertol CH47B (helicopter)        |
|1057W                                            |Fokker F-27 Friendship 400              |
|1057X                                            |Britten-Norman BN-2A Islander           |
|100CS                                            |Lockheed Vega 2                         |
|1057Z                                            |Tupolev TU-124                          |
|1058                                             |Yakovlev YAK-40                         |
|10580                                            |McDonnell Douglas DC-8-63CF             |
|10582                                            |Britten-Norman BN-2A Islander           |
|10583                                            |Cessna T337B                            |
|10584                                            |Fokker F-27 Friendship 300              |
|10586                                            |Douglas DC-3-DST                        |
|1058D                                            |Antonov An-12B                          |
|1058F                                            |Martin 404                              |
|1058J                                            |Lockheed C-130E                         |
|100CU                                            |Dornier Merkur                          |
|1058L                                            |Aero Commander 500-B                    |
|1058M                                            |Douglas DC-3                            |
|1058N                                            |Lockheed L-100-20 Hercules              |
|1058R                                            |Piper PA-28R                            |
|1058T                                            |Curtiss C-46D                           |
|1058V                                            |McDonnell Douglas DC-9-31               |
|1058Z                                            |de Havilland RU-6A Beaver /Bell UH-1H   |
|10592                                            |McDonnell Douglas DC-8-63CF             |
|10593                                            |Fairchild C-123K                        |
|10597                                            |Fairchild C-123K                        |
|100CW                                            |Lockheed Vega                           |
|1059A                                            |Canadair CL-44J                         |
|1059B                                            |Douglas DC-3                            |
|1059D                                            |BAC One-Eleven  424EU                   |
|1059E                                            |Antonov AN-22                           |
|1059F                                            |Boeing B-727-2A7                        |
|1059H                                            |Fokker F-27 Friendship 200              |
|1059J                                            |Nord 262E                               |
|1059L                                            |Ilyushin IL-18B                         |
|1059R                                            |de Havilland Comet 4C                   |
|1059S                                            |Boeing B-707-323 / Cessna 150           |
|100CX                                            |Lasco Lascowl                           |
|1059X                                            |Ilyushin IL-18                          |
|1059Y                                            |Nord 262A-34                            |
|1059Z                                            |Curtiss-Wright C-46                     |
|105AA                                            |Antonov AN-12                           |
|105AB                                            |Beech King Air F90                      |
|105AC                                            |Fokker F-27 Friendship 500              |
|105AD                                            |Vickers Viscount 749                    |
|105AF                                            |Antonov AN-10                           |
|105AM                                            |Piper PA-28                             |
|105AP                                            |Curtiss C-46                            |
|100DA                                            |Pitcairn PA-6 Mailwing                  |
|105AS                                            |Douglas DC-3                            |
|105AT                                            |Boeing B-720-047B                       |
|105AV                                            |Antonov An-10                           |
|105AW                                            |Douglas C-47A                           |
|105AZ                                            |Cessna TU206B                           |
|105B                                             |Beech E18S                              |
|105BA                                            |Beechcraft C35                          |
|105BB                                            |de Havilland 104-7X                     |
|105BC                                            |Curtiss C-46A-55-CK                     |
|105BD                                            |Sud Aviation SA 318C                    |
|100DB                                            |Fokker F-VII                            |
|105BE                                            |Tupolev TU-134A                         |
|105BG                                            |Hawker Siddeley HS 125-400B (3)         |
|105BH                                            |Aero Commander 680E                     |
|105BJ                                            |Ilyushin IL-18D                         |
|105BK                                            |Fokker F-27 Friendship 200              |
|105BL                                            |McDonnell Douglas DC-9-31 / F4-B        |
|105BM                                            |Convair CV-580                          |
|105BP                                            |Boeing - EC-135N                        |
|105BW                                            |Douglas DC-6                            |
|105CA                                            |Douglas DC-3                            |
|100DC                                            |Ford 5-AT-C Tri Motor                   |
|105CB                                            |NAMC YS-11A-227                         |
|105CC                                            |Bell 206                                |
|105CD                                            |Douglas DC-3                            |
|105CE                                            |Boeing 707-321CF                        |
|105CH                                            |Tupolev TU-104B                         |
|105CK                                            |Boeing B-727-281 / Air Force F86F       |
|105CM                                            |Boeing B-747-121                        |
|105CN                                            |Nord 2501 Noratlas                      |
|105CP                                            |Tupolev TU-104                          |
|105CT                                            |Sikorsky S-55B                          |
|100DD                                            |Lockheed Vega                           |
|105CW                                            |Boeing Vertol CH-47A (helicopter)       |
|105D                                             |Piper PA-31                             |
|105DA                                            |HAL-748-224 Srs.2                       |
|105DB                                            |Boeing B-727-193                        |
|105DD                                            |BAC One-Eleven 515FB                    |
|105DF                                            |Aero Commander 560-A                    |
|105DM                                            |Douglas DC-3                            |
|105DP                                            |Tupolev TU-134A                         |
|105DR                                            |Douglas DC-3                            |
|105DS                                            |Vickers Vanguard 951                    |
|10013                                            |Curtiss R-4LM                           |
|100DE                                            |Boeing 40                               |
|105DU                                            |Tupolev TU-104B                         |
|105DW                                            |Cessna 402                              |
|105DX                                            |Swearingen SA26AT                       |
|105DY                                            |Douglas C-47A                           |
|105EA                                            |Beech E18S                              |
|105EB                                            |Douglas C-47                            |
|105EC                                            |Beechcraft B99                          |
|105ED                                            |Lockheed C-130K Hercules                |
|105EE                                            |Vickers Viscount 828                    |
|105EJ                                            |Antonov AN-24                           |
|100DF                                            |Heinkel HE-2                            |
|105EL                                            |Sud Aviation SE-210 Caravelle III       |
|105EM                                            |Boeing Vertol CH-47C                    |
|105ER                                            |Antonov AN-24                           |
|105EV                                            |Douglas DC-9-31 /Cessna 206             |
|105F                                             |Antonov AN-26                           |
|105FA                                            |Ilyushin IL-18B                         |
|105FC                                            |Lockheed 188A Electra                   |
|105FE                                            |Hawker Siddeley HS-748-230 Srs. 2A      |
|105FF                                            |Sud-Aviation Caravelle VI-R             |
|105FP                                            |Piper PA-23                             |
|100DK                                            |Dornier Wal                             |
|105FR                                            |MDonnell Douglas DC-9-32                |
|105FS                                            |Vickers Viscount 837                    |
|105G                                             |Douglas C-47                            |
|105GD                                            |McDonnell Douglas DC-9-32               |
|105GH                                            |Douglas DC-6                            |
|105GP                                            |de Havilland Canada C-7A Caribou        |
|105GR                                            |Beechcraft S35                          |
|105GS                                            |Fairchild F-27                          |
|105GX                                            |Douglas DC-4                            |
|105H                                             |Beechcraft D 18S                        |
|100DP                                            |Lockheed Orion 9                        |
|105HC                                            |Lockheed C-130E Hercules                |
|105HF                                            |Beechcraft 65-B80                       |
|105HH                                            |Beechcraft D 18S                        |
|105HK                                            |Fairchild-Hiller FH-227-B               |
|105HM                                            |Boeing KC-135A                          |
|105HP                                            |Aerospatiale Caravelle Super 10B        |
|105HQ                                            |McDonnell Douglas DC-9-32               |
|105J                                             |Lockheed AC-130A Hercules               |
|105JA                                            |Curtiss C-46F                           |
|105JB                                            |NAMC YS-11A-211                         |
|100DQ                                            |De Havilland DH.80                      |
|105JC                                            |Fokker F-27 Friendship 200              |
|105JD                                            |Bell 47J-2                              |
|105JE                                            |BAC Super VC-10 1154                    |
|105JF                                            |Douglas C-47D                           |
|105JG                                            |Pilatus PC6CH2                          |
|105JH                                            |Lockheed C-130E Hercules                |
|105JK                                            |Yakovlev YAK-40                         |
|105JM                                            |McDonnell Douglas DC-8-43               |
|105JR                                            |Douglas C-47B                           |
|105JS                                            |Boeing Vertol CH47A (helicopter)        |
|100DR                                            |Boeing 40                               |
|105JW                                            |Beechcraft 65-B80                       |
|105KA                                            |Fokker F-27 Friendship 200              |
|105KB                                            |de Havilland Canada DHC-6 Twin Otter    |
|105KL                                            |Bell 205A                               |
|105KW                                            |Lockheed 049 Constellation              |
|105L                                             |McDonnell Douglas DC-9-14               |
|105LA                                            |Cessna U206C                            |
|105LB                                            |Beechcraft E18S                         |
|105LC                                            |Lockheed P-3A Orion                     |
|105LG                                            |Curtiss C-46A                           |
|100DS                                            |Stinson                                 |
|105LH                                            |Curtiss C-46D                           |
|105LP                                            |Boeing Vertol CH-47 (helicopter)        |
|105LS                                            |McDonnell Douglas DC-8-53               |
|105LU                                            |Convair CV-880-22M-21                   |
|105LV                                            |Cessna 182N                             |
|105M                                             |Lockheed AC-130A Hercules               |
|105MA                                            |Antonov AN-10A                          |
|105MC                                            |Hawker Siddeley Trident 1C              |
|105MD                                            |de Havilland DH-114 Heron 2B            |
|105MM                                            |Hughes 369HS                            |
|100DT                                            |Boeing 40                               |
|105MR                                            |Convair CV-580/De Hav. Twin Otter 100   |
|105MT                                            |MBB HFB-320 Hansa Jet                   |
|105MU                                            |Beechcraft U206C                        |
|105MV                                            |Boeing 737-200                          |
|105MW                                            |McDonnell Douglas DC-8-52               |
|105NA                                            |Sikorsky CH-53D (helicopter)            |
|105NF                                            |de Havilland Canada DHC-6 Twin Otter 100|
|105NJ                                            |Sud-Aviation SE210 Caravelle            |
|105NK                                            |Douglas DC-3 / Douglas DC-3             |
|105NM                                            |Lockheed C-130E                         |
|100DV                                            |Lockheed Vega 5                         |
|105NN                                            |Fokker F-27 Friendship 100              |
|105NR                                            |Ilyushin IL-62                          |
|105NS                                            |Douglas DC-3 (C-47A-DK)                 |
|105PA                                            |Douglas C-47-DL                         |
|105PB                                            |de Havilland Canada DHC-4 Caribou       |
|105PD                                            |Ilyushin IL-18                          |
|105PF                                            |Shorts SC-7 Skyvan 3-300                |
|105PG                                            |Curtiss C-46A-40-CU                     |
|105PP                                            |Douglas DC-3                            |
|105PR                                            |Douglas C-47                            |
|100DX                                            |Fokker F-VIIb-3M                        |
|105PS                                            |F-86 Sabrejet                           |
|105PW                                            |Douglas C-54D-1-DC                      |
|105PZ                                            |Douglas C-47B                           |
|105RB                                            |Douglas DC-3                            |
|105RC                                            |Ilyushin IL-18B                         |
|105RD                                            |Aero Commander 680E                     |
|105RF                                            |Ilyushin IL-62                          |
|105RG                                            |Fairchild-Hiller FH-227D/LCD            |
|105RH                                            |Cessna 310C                             |
|105RJ                                            |NAMC YS-11A-202                         |
|10015                                            |De Havilland DH-4                       |
|100DY                                            |CAMS 56                                 |
|105RK                                            |Britten-Norman BN-2A-6 Islander         |
|105RL                                            |Vickers Viscount 724                    |
|105RR                                            |Fokker F-27 Friendship 200              |
|105RV                                            |Boeing Vertol CH-47 (helicopter)        |
|105RZ                                            |Ilyushin IL-14P                         |
|105S                                             |Beech G18S                              |
|105SC                                            |McDonnell Douglas DC-8-62               |
|105SD                                            |Beechcraft C-45H                        |
|105SF                                            |Convair CV-990-30A-5 Coronado           |
|105SG                                            |Boeing 707-336C                         |
|100DZ                                            |Fairchild Pilgrim 100A                  |
|105SJ                                            |Lockheed C-130E Hercules                |
|105SK                                            |Douglas C-47B-15-DK                     |
|105SL                                            |Fokker F-27 Friendship 400              |
|105SP                                            |Cessna 320E                             |
|105SS                                            |Boeing B-737-222                        |
|105ST                                            |Learjet 23                              |
|105SU                                            |Convair CV-880 / McDonnell DC-9-31      |
|105SX                                            |Lockheed AC-130A Hercules               |
|105SY                                            |de Havilland Canada DHC-6 Twin Otter 300|
|105T                                             |Fokker F-28 Fellowship 1000             |
|100ED                                            |Stinson SM-2A                           |
|105TB                                            |Lockheed L-1011 TriStar1                |
|105TC                                            |Douglas DC-7CF                          |
|105TD                                            |Boeing 707-321C                         |
|105TF                                            |Vickers 802 Viscount                    |
|105TL                                            |Antonov An-24B                          |
|105TM                                            |Boeing B-707-3D3C                       |
|105TP                                            |Cessna 182B                             |
|105TR                                            |Douglas DC-6A                           |
|105TT                                            |Ilyushin IL-18D                         |
|105TV                                            |Cessna 180H                             |
|100EE                                            |Stinson SM-6000B                        |
|105TW                                            |Tupolev TU-154                          |
|105TX                                            |Bell 206B                               |
|105U                                             |Douglas DC-3                            |
|105UC                                            |Boeing B-727-224                        |
|105UM                                            |Cessna 310J                             |
|105UP                                            |Ilyushin IL-18                          |
|105US                                            |Yakovlev YAK-40                         |
|105UT                                            |Antonov An-24B                          |
|105UV                                            |Antonov AN-24B                          |
|105UW                                            |de Havilland Canada DHC-6 Twin Otter 100|
|100EF                                            |Fairchild                               |
|105VA                                            |Ilyushin IL-18V                         |
|105VB                                            |Sud Aviation SE-210 Caravelle           |
|105VC                                            |MD Douglas DC-9-32/Convair CV-990A      |
|105VE                                            |Fairchild C-123                         |
|105VL                                            |HAL-748-224                             |
|105VP                                            |Lockheed P-3B Orion                     |
|105VT                                            |Douglas C-54D                           |
|105VU                                            |Vickers Vanguard 952                    |
|105VV                                            |Lockheed P-3C / Convair CV-990-30A-5    |
|105VW                                            |Lockheed P-3C Orion /Convair CV-990     |
|100EK                                            |Stearman C-3MB                          |
|105W                                             |de Havilland Canada DHC-6 Twin Otter 100|
|105WA                                            |Beech E18S                              |
|105WB                                            |Cessna 402B                             |
|105WD                                            |Swearingen SA26T                        |
|105WG                                            |Tupolev TU-104A                         |
|105WK                                            |Douglas C-47A                           |
|105WL                                            |Douglas DC-3                            |
|105WM                                            |Boeing B-737-2A8                        |
|105WP                                            |Sud Aviation SE-210 Caravelle VIN       |
|105WS                                            |Tupolev TU-144                          |
|100EL                                            |Boeing 40                               |
|105WT                                            |Boeing 707-327C                         |
|105WZ                                            |McDonnell Douglas DC-9-15               |
|105X                                             |Tupolev TU-134A                         |
|105XP                                            |Boeing B-707-345C                       |
|105XR                                            |Boeing B-707-321B                       |
|105XX                                            |Fairchild-Hiller FH-227B                |
|105YV                                            |Volpar C45G                             |
|105YX                                            |McDonnell Douglas DC-9-31               |
|105ZT                                            |Cessna A185F                            |
|105ZZ                                            |Tupolev TU-104B                         |
|100EM                                            |Latecoere 28                            |
|10601                                            |Sud-Aviation Caravelle 10-R             |
|10602                                            |Norman BN-2A-6                          |
|10604                                            |Antonov AN-24V                          |
|10607                                            |Douglas DC-3                            |
|1060E                                            |Lockheed L-188A Electra                 |
|1060F                                            |Lockheed C-141A                         |
|1060H                                            |Boeing B-707-331B                       |
|1060R                                            |Piper PA-30 / Cessna 337A               |
|1060T                                            |McDonnell Douglas DC-8-63F              |
|1060W                                            |Cessna 310H                             |
|100EN                                            |Stinson SM-6000B                        |
|1061                                             |Aerospatiale Caravelle 6N               |
|10612                                            |Beechcraft E18S                         |
|10613                                            |Cessna 310                              |
|10615                                            |Gates Lear 25                           |
|10617                                            |Convair 600                             |
|10618                                            |Douglas DC-3A                           |
|10619                                            |Tupolev TU-104B                         |
|1061A                                            |Antonov AN-12V                          |
|1061D                                            |Britten-Norman BN-2A-7 Islander         |
|1061E                                            |NAMC YS-11A-211                         |
|100EP                                            |Fokker F-10A                            |
|1061F                                            |Britten-Norman BN-2A-6 Islander         |
|1061G                                            |Cessna 401A                             |
|1061H                                            |Handley Page HPR-7 Herald 101           |
|1061P                                            |McDonnell Douglas DC-10-10              |
|1061Q                                            |Boeing B-707-321C                       |
|1061S                                            |Douglas DC-3                            |
|1061T                                            |Tupolev TU-104B                         |
|1061W                                            |de Havilland DH-125-400A                |
|1061X                                            |Douglas DC-118                          |
|1061Y                                            |Tupolev TU-124                          |
|10018                                            |De Havilland DH.4                       |
|100ER                                            |Northrop Alpha                          |
|10621                                            |Boeing B-707-321B                       |
|10623                                            |Cessna 310L                             |
|10624                                            |Convair CV-440                          |
|10626                                            |Boeing Vertol CH-47 (helilcopter)       |
|10628                                            |Sud-Aviation Caravelle VI-N             |
|10629                                            |Tupolev TU-124                          |
|1062F                                            |Douglas DC-3                            |
|1062G                                            |Fokker F-28 Fellowship 1000             |
|1062K                                            |Curtiss C-46F                           |
|1062N                                            |Beechcraft 99A                          |
|100ES                                            |Farman F-190                            |
|1062Q                                            |Antonov AN-24V                          |
|1062S                                            |Hawker Siddeley HS 748-260              |
|1062U                                            |Douglas C-54                            |
|1062V                                            |Douglas DC-3A                           |
|1062W                                            |Antonov An-24B                          |
|1062Y                                            |Cessna 172L                             |
|10630                                            |Fokker F-28 Fellowship 1000             |
|10631                                            |Beechcraft J-35                         |
|10632                                            |Piper PA-28                             |
|10634                                            |Boeing B-707-321B                       |
|100EU                                            |Boeing 95                               |
|10636                                            |Boeing B-747                            |
|1063B                                            |Transall C-160D                         |
|1063C                                            |Brittonnorman BN-2A6                    |
|1063E                                            |MDonnell Dougals DC-9                   |
|1063G                                            |Curtiss C-46A-45-CU                     |
|1063H                                            |Lockheed C-130E Hercules                |
|1063L                                            |McDonnell Douglas DC-10-10              |
|1063Q                                            |Antonov An-24                           |
|1063S                                            |Robertson 414                           |
|1063T                                            |Convair CV-440                          |
|100EV                                            |Stearman C-3MB                          |
|1063V                                            |Aerospatiale Caravelle 10B3             |
|1063W                                            |Douglas DC-4                            |
|1063Y                                            |Beechcraft H18S                         |
|1063Z                                            |Boeing B-707-321C                       |
|10644                                            |Ilyushin IL-18E                         |
|10645                                            |Ilyushin IL-18B                         |
|10647                                            |Beechcraft 99                           |
|10649                                            |Douglas C-47                            |
|1064C                                            |Douglas DC-6A                           |
|1064D                                            |Lockheed L-100-30 Hercules              |
|100EW                                            |Boeing 40                               |
|1064E                                            |Yakovlev YAK-40                         |
|1064F                                            |Bristol 170 Freighter 31E               |
|1064G                                            |Vickers Viscount 785D                   |
|1064H                                            |Boeing 307B-1 Stratoliner               |
|1064K                                            |Fairchild Hiller FH1100                 |
|1064S                                            |Douglas DC-4                            |
|1064T                                            |Fairchild C-123K                        |
|1064U                                            |Douglas DC-3                            |
|1064V                                            |de Havilland Canada DHC-5 Buffalo       |
|1064X                                            |Ilyushin IL-18B                         |
|100EX                                            |Boeing 40                               |
|10651                                            |Douglas C-47-DL                         |
|10653                                            |de Havilland DHC-2                      |
|10658                                            |Vickers Viscount 749                    |
|10659                                            |Lockheed C-141A                         |
|1065A                                            |Lockheed C-130H                         |
|1065B                                            |Fokker F-27 Friendship 600              |
|1065D                                            |Boeing B-707-331B                       |
|1065E                                            |McDonnell Douglas DC-9-31               |
|1065M                                            |Boeing B-727-121C                       |
|1065N                                            |Piper PA-32                             |
|100F                                             |Ford 5-AT-C Tri Motor                   |
|1065P                                            |Cessna 185                              |
|1065S                                            |Volpar 18                               |
|1065T                                            |Britten-Norman BN-2A Islander           |
|1065U                                            |Bell 205A                               |
|1065V                                            |Tupolev Tu-154                          |
|1065W                                            |Lockheed WC-130H Hercules               |
|1065X                                            |de Havilland DHC-2                      |
|1065Y                                            |Douglas DC-3                            |
|1066                                             |Cessna 172M                             |
|10661                                            |Piper PA-31                             |
|100FA                                            |CAMS 53                                 |
|10662                                            |Cessna 337D                             |
|10663                                            |Piper PA-18                             |
|10669                                            |Lockheed L-100 Hercules                 |
|1066A                                            |Beechcraft 95-B55                       |
|1066B                                            |Lockheed 188PF Electra                  |
|1066C                                            |Britten-Norman BN-2A Islander           |
|1066E                                            |de Havilland DHC-2                      |
|1066H                                            |Douglas C-47A-30                        |
|1066L                                            |Douglas DC-3                            |
|1066M                                            |Boeing B-747-130                        |
|100FB                                            |Junkers G-23                            |
|1066N                                            |Cessna 500 Citation I                   |
|1066P                                            |Boeing B-727-251                        |
|1066Q                                            |Boeing B-727-231                        |
|1066S                                            |McDonnell Douglas DC-8-55F              |
|1066U                                            |Grumman G-21                            |
|1066W                                            |Boeing Vertol CH-47 (helicopter)        |
|1066Y                                            |Yakovlev 40                             |
|10674                                            |McDonnell Douglas DC-9-14               |
|10679                                            |Brittonorman BN-2A                      |
|1067A                                            |Antonov AN-24RV                         |
|100FF                                            |Fokker F-10                             |
|1067E                                            |Tupolev TU-124                          |
|1067F                                            |Fairchild C-123K                        |
|1067G                                            |Cessna TU206D                           |
|1067L                                            |de Havilland Canada DHC-6 Twin Otter 200|
|1067M                                            |Douglas DC-3                            |
|1067N                                            |de Hav Can. DHC-6 Tw Otter 100/ Cessna  |
|1067Q                                            |de Havilland DHC-2                      |
|1067S                                            |Ilyushin IL-18V                         |
|1067W                                            |Antonov AN-12                           |
|1067X                                            |Fokker F-28 Fellowship 1000             |
|10019                                            |De Havilland DH-4                       |
|100FG                                            |Liore-et-Olivier 213                    |
|1067Y                                            |Douglas DC-3-313                        |
|1067Z                                            |Piper PA-31                             |
|10681                                            |Douglas DC-3C                           |
|10682                                            |Hawker Siddeley HS-748 2                |
|10683                                            |Transall C-160                          |
|10686                                            |Douglas DC-6BF                          |
|10687                                            |Canadair CL-44                          |
|10688                                            |Embraer 110C Bandeirante                |
|10689                                            |Beechcraft 95                           |
|1068A                                            |Douglas DC-4                            |
|100FH                                            |De Havilland DH-80                      |
|1068C                                            |Fokker F-27 Friendship 400M             |
|1068D                                            |de Havilland Canada DHC-6 Twin Otter 100|
|1068F                                            |Lockheed C-141A (L.300)                 |
|1068G                                            |Lockheed C-5A Galaxy                    |
|1068H                                            |Cessna 310Q                             |
|1068K                                            |Bell 206                                |
|1068L                                            |Douglas DC-3                            |
|1068M                                            |Bristol 170 Freighter 21E               |
|1068N                                            |Piper PA-23-250                         |
|1068R                                            |Sikorsky CH-53C (helicopter)            |
|100FJ                                            |Latecoere 28                            |
|1068S                                            |BAC One-Eleven 524FF                    |
|1068W                                            |Hawker Siddeley HS-748-235 Srs. 2A      |
|1068X                                            |Boeing B-727-225                        |
|10691                                            |Beechcraft E18S                         |
|10693                                            |Douglas DC-4                            |
|10694                                            |Beechcraft 99                           |
|10699                                            |Douglas C-47A                           |
|1069A                                            |Lockheed L-188AF Electra                |
|1069D                                            |Piper PA-18                             |
|1069E                                            |Bell 206B                               |
|100FL                                            |Ford Tri-motor 5                        |
|1069F                                            |Yakovlev YAK-40                         |
|1069G                                            |Lockheed C-130A Hercules                |
|1069J                                            |Vickers 837 Viscount                    |
|1069K                                            |Boeing B-707-321C                       |
|1069L                                            |Douglas DC-47                           |
|1069P                                            |Boeing B-727-224                        |
|1069V                                            |Yakovlev YAK-40                         |
|1069W                                            |Ilyushin IL-62                          |
|1069X                                            |Piper PA-28                             |
|106AB                                            |Douglas C-47                            |
|100FM                                            |Junkers W-33                            |
|106AC                                            |Fairchild F-27B                         |
|106AE                                            |Tupolev TU-134                          |
|106AF                                            |Douglas C-47-DL                         |
|106AG                                            |Fokker F-28 Fellowship 1000             |
|106AL                                            |Tupolev TU-154B                         |
|106AM                                            |de Havilland Canada DHC-6 Twin Otter 200|
|106AP                                            |Boeing 727-24C                          |
|106AR                                            |de Havilland DH114 Heron 2E             |
|106AS                                            |Piper PA-34                             |
|106AT                                            |Convair CV-440-12                       |
|100FN                                            |Junkers F-13                            |
|106AV                                            |McDonnell Douglas DC-9-32               |
|106B                                             |Bell 212                                |
|106BA                                            |NA Rockwell 112                         |
|106BB                                            |Douglas DC-3                            |
|106BC                                            |Antonov AN-24                           |
|106BD                                            |Yakovlev 40                             |
|106BE                                            |Antonov AN-24B                          |
|106BH                                            |Lockheed C-130 Hercules                 |
|106BJ                                            |Piper PA-23-250 Aztec                   |
|106BL                                            |Cessna 402                              |
|100FP                                            |Travel Air 6000                         |
|106BR                                            |Britten-Norman BN-2A-21 Islander        |
|106BS                                            |Mitsubishi MU-2B                        |
|106BW                                            |Boeing B-720B-023B                      |
|106C                                             |Tupolev TU-124                          |
|106CA                                            |Lear Jet 24A                            |
|106CB                                            |Piper PA-23                             |
|106CC                                            |Britten-Norman BN-2A-21 Islander        |
|106CD                                            |Douglas C-54A                           |
|106CJ                                            |Bellanca 17-30                          |
|106CK                                            |Douglas C-47                            |
|100FR                                            |Ford 5                                  |
|106CM                                            |Hawker Siddeley HS-748-246              |
|106CP                                            |Antonov AN-24                           |
|106CT                                            |Embraer 110C Bandeirante                |
|106D                                             |Ilyushin IL-18V                         |
|106DA                                            |Beechcraft  C-45H                       |
|106DC                                            |Douglas DC-6A                           |
|106DD                                            |Boeing KC-135A                          |
|106DE                                            |Hughes 369HS                            |
|106DK                                            |Douglas DC-6                            |
|106DL                                            |Tupolev TU-104A                         |
|100FV                                            |Boeing 40                               |
|106DN                                            |Grumman G-21A seaplane                  |
|106DR                                            |Ilyushin II-14P                         |
|106DS                                            |IAI Arava 201                           |
|106DU                                            |Ilyushin IL-18D                         |
|106DW                                            |Cessna 207                              |
|106E                                             |Cessna 172M                             |
|106EB                                            |Antonov An-24B                          |
|106EC                                            |Douglas DC-3                            |
|106ED                                            |Boeing B-727-81                         |
|106EJ                                            |Cessna 207                              |
|100FY                                            |De Havilland DH-60                      |
|106EL                                            |Beechcraft A36                          |
|106EM                                            |Hawker Siddeley HS-748 2                |
|106EP                                            |Beech B60                               |
|106ES                                            |Bell 205 A-1 helicopter                 |
|106ET                                            |Cessna 207                              |
|106EW                                            |Boeing B-727-95                         |
|106EX                                            |de Havilland Canada DHC-6 Twin Otter 300|
|106EZ                                            |Britten-Norman BN-2A-21 Islander        |
|106F                                             |NAMC YS-11A-500                         |
|106FA                                            |Boeing B-747-131F                       |
|1001A                                            |De Havilland DH-4                       |
|100FZ                                            |CAMS 53                                 |
|106FB                                            |Antonov AN-24                           |
|106FC                                            |Piper PA-34                             |
|106FE                                            |BAC One-Eleven 527FK                    |
|106FF                                            |Tupolev TU-154A                         |
|106FM                                            |Lockheed 188A Electra                   |
|106FS                                            |GAF Nomad N-22B                         |
|106FW                                            |Bell 47G3B1                             |
|106GA                                            |Airbus A300                             |
|106GB                                            |Douglas C-47                            |
|106GC                                            |Piper PA-28R                            |
|100G                                             |Curtiss Condor 18                       |
|106GG                                            |Piper PA-34                             |
|106GK                                            |Ilyushin IL-18L                         |
|106GL                                            |Beechcraft S35                          |
|106GS                                            |Boeing 707-373                          |
|106GW                                            |Douglas C-54E                           |
|106GX                                            |Vickers Viscount 785D                   |
|106HH                                            |Cessna 185                              |
|106HP                                            |Canadair CL-44                          |
|106HQ                                            |Lockheed C-141A (L.300)                 |
|106HS                                            |Lockheed C-141A (L.300)                 |
|100GA                                            |Stearman 4                              |
|106J                                             |Sud Aviation SE 210 Caravelle III       |
|106JB                                            |Lockheed C-130H                         |
|106JC                                            |de Havilland Canada DHC-3 Otter         |
|106JL                                            |Antonov AN-24 / Yakovlev Yak-40         |
|106JM                                            |McDonnell Douglas DC-9-31 / Trident 3B  |
|106JP                                            |Boeing B-727-2F2                        |
|106JT                                            |de Havilland Canada DHC-6 Twin Otter 100|
|106JW                                            |Sikorsky S-55B                          |
|106K                                             |Boeing KC-135A                          |
|106KA                                            |Douglas DC-7CF                          |
|100GB                                            |Stearman 4                              |
|106KB                                            |McDonnell Douglas DC-8-43               |
|106KH                                            |Piper PA-34                             |
|106KS                                            |Sud-Aviation Caravelle VI-N             |
|106KT                                            |Boeing B-707-31                         |
|106LA                                            |Piper PA-31                             |
|106LB                                            |Douglas C-47DL                          |
|106LC                                            |Embraer 110C Bandeirante                |
|106LH                                            |Fokker F-27 Friendship 100              |
|106LL                                            |Douglas DC-3                            |
|106LS                                            |Piper PA-31T                            |
|100GC                                            |Ford 5-AT-D                             |
|106LU                                            |L-100-20                                |
|106LW                                            |Tupolev TU-104B                         |
|106M                                             |Piper PA-32-300                         |
|106MA                                            |de Havilland Canada DHC-6 Twin Otter 300|
|106MB                                            |Antonov AN-24RV                         |
|106MC                                            |Boeing B-707-366C                       |
|106MG                                            |Piper PA-23-250                         |
|106MH                                            |Douglas C-54A-1-DO                      |
|106MJ                                            |Gates Learjet 24B                       |
|106ML                                            |Tupolev TU-104A                         |
|100GF                                            |Fairchild FC-2W                         |
|106MM                                            |Douglas DC-8                            |
|106MR                                            |de Havilland Canada DHC-6 Twin Otter 300|
|106MS                                            |Vickers Viscount 838                    |
|106MU                                            |Bristol 170 Freighter 31M               |
|106N                                             |Fairchild C-82                          |
|106NA                                            |Avia 14T                                |
|106NJ                                            |Ilyushin IL-18V                         |
|106NK                                            |Douglas DC-3                            |
|106NN                                            |Douglas DC-3                            |
|106PA                                            |Lockheed C-130H                         |
|100GG                                            |Lockheed Orion 9                        |
|106PB                                            |McDonnell Douglas DC-8-63CF             |
|106PC                                            |Lockheed L-188AF Electra                |
|106PE                                            |Pipper PA-23-250 Aztec                  |
|106PF                                            |Boeing B-747-121 / Boeing B-747-206B    |
|106PG                                            |de Havilland Canada DHC-6 Twin Otter 300|
|106PK                                            |Yakovlev YAK-40                         |
|106PS                                            |McDonnell Douglas DC-9-31               |
|106PV                                            |Douglas DC-3-3A                         |
|106PW                                            |Antonov An-24                           |
|106Q                                             |Convair CV-440                          |
|100GH                                            |Armstrong Whitworth Argosy II           |
|106R                                             |Sikorsky CH-53D (helicopter)            |
|106RA                                            |Antonov An-12BP                         |
|106RB                                            |Boeing 707-321C                         |
|106RD                                            |Sikorsky S61L                           |
|106RE                                            |Ilyushin IL-62M                         |
|106RF                                            |Cessna 185                              |
|106RG                                            |Embraer C-95 Bandeirante                |
|106RH                                            |Embraer 110C Bandeirante                |
|106RM                                            |Lockheed EC-130Q                        |
|106RT                                            |Antonov AN-24                           |
|100GJ                                            |Junkers F-13                            |
|106RV                                            |Antonov AN-26                           |
|106RW                                            |Douglas DC-3                            |
|106SB                                            |Britten-Norman BN-2A-6 Islander         |
|106SC                                            |Douglas DC-6B                           |
|106SE                                            |Douglas C-47                            |
|106SH                                            |Piper PA-32R                            |
|106SM                                            |Bell 206B JetRanger                     |
|106SP                                            |de Havilland Canada DHC-6 Twin Otter 200|
|106SR                                            |Cessna U206                             |
|106SU                                            |Beechcraft 58                           |
|100GK                                            |Goodyear-Zeppelin U.S.S. Akron (airship)|
|106SX                                            |Convair CV-880                          |
|106SY                                            |Bell 206B                               |
|106T                                             |Shorts SC-7 Skyvan 3-200                |
|106TD                                            |Canadair CL-44D4-2                      |
|106TG                                            |Helo 295                                |
|106TH                                            |Vickers Viscount 764D                   |
|106TJ                                            |de Havilland Canada DHC-6 Twin Otter 200|
|106TL                                            |de Havilland Canada DHC-6 Twin Otter 300|
|106TM                                            |Douglas DC-7BF                          |
|106TN                                            |Boeing - EC-135K                        |
|10004                                            |Zeppelin L-1 (airship)                  |
|1001B                                            |Curtiss R-4LM                           |
|100GL                                            |Cams 33                                 |
|106TQ                                            |Tupolev TU-134                          |
|106TR                                            |Cessna U206                             |
|106TU                                            |McDonnell Douglas DC-8-62H              |
|106TX                                            |de Havilland DHC-2                      |
|106U                                             |Bell 206B                               |
|106UC                                            |Convair CV-300                          |
|106UV                                            |Sikorksky CH-53 (helicopter)            |
|106V                                             |Boeing B-747                            |
|106VE                                            |Britten-Norman BN-2A-8 Trislander       |
|106VK                                            |Boeing B-727-282                        |
|100GM                                            |Junkers W-34                            |
|106VP                                            |Boeing 707-360C                         |
|106VS                                            |Britten-Norman BN-2A-8 Islander         |
|106VT                                            |BAC One-Eleven 420EL                    |
|106VU                                            |Nord 2501 Noratlas                      |
|106VX                                            |Beechcraft 58                           |
|106W                                             |Tupolev TU-154B                         |
|106WA                                            |Boeing B-737-2H6                        |
|106WB                                            |SNIAS SA330J                            |
|106WD                                            |Antonov AN-24                           |
|106WK                                            |Lockheed P-3B Orion                     |
|100GN                                            |Latecoere 28-1                          |
|106WL                                            |Douglas DC-3                            |
|106WP                                            |Piper PA-34                             |
|106WS                                            |Aerospatiale Caravelle 10R              |
|106WT                                            |Douglas DC-8-54F                        |
|106XX                                            |Britten-Norman BN-2A Islander           |
|106Z                                             |de Havilland Canada DHC-6 Twin Otter 300|
|106ZY                                            |Piper PA-28R                            |
|1070                                             |Piper PA-31-350 Navajo                  |
|10703                                            |Vickers Viscount 764 D                  |
|1070B                                            |Boeing B-747-237B                       |
|100GP                                            |Pitcairns PA-6                          |
|1070D                                            |Cessna 337G                             |
|1070E                                            |Aerostar 601P                           |
|1070H                                            |Douglas DC-3                            |
|1070L                                            |Embraer 110P Bandeirante                |
|1070M                                            |Douglas C-47A-DL                        |
|1070P                                            |Beechcraft 99                           |
|1070V                                            |Boeing B-737-275                        |
|1070W                                            |Beechcraft 58                           |
|1070X                                            |Evangel 4500                            |
|1070Y                                            |Aero Commander 500A                     |
|100GQ                                            |Ford 5-AT-B Tri Motor                   |
|1070Z                                            |McDonnell Douglas DC-10-10              |
|10712                                            |Cessna 337F                             |
|10714                                            |Fokker F-28 Fellowship 1000 / MiG-21    |
|10715                                            |British Aerospace 748 2A                |
|10719                                            |Cessna 310I                             |
|1071A                                            |Beechcraft D18                          |
|1071C                                            |Tupolev TU-134                          |
|1071D                                            |Cessna T207A                            |
|1071E                                            |Fokker F-27 Friendship 200              |
|1071G                                            |Piper Cherokee Arrow  PA-28             |
|100GR                                            |Farman F-306                            |
|1071H                                            |Bell 212                                |
|1071J                                            |Grumman G-21                            |
|1071K                                            |Boeing B-707-321B                       |
|1071L                                            |Piper PA-31                             |
|1071M                                            |Cessna 402B                             |
|1071N                                            |Douglas C-118A                          |
|1071P                                            |de Havilland DHC-2                      |
|1071S                                            |Boeing B-727-235                        |
|1071T                                            |PS-1 amphibious ASW                     |
|1071U                                            |Tupolev TU-154B                         |
|100GS                                            |Boeing 247-D                            |
|1071V                                            |Beech Queen Air A80                     |
|1071W                                            |McDonnell Douglas DC-9-32               |
|1071X                                            |Sikorsky S-61N                          |
|1071Z                                            |Britten Norman BN-2A Trislander Mk.III-2|
|10721                                            |Curtiss C-46                            |
|10725                                            |Grumman G-21 Goose                      |
|10728                                            |Mitsubishi MU-2J                        |
|10729                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1072A                                            |Piper PA-31-350 Chieftain               |
|1072E                                            |Grumman G-21A                           |
|100GT                                            |Farman F-301                            |
|1072F                                            |de havilland Canada Twin Otter 200      |
|1072H                                            |Ilyushin IL-18                          |
|1072J                                            |Vickers Viscount 782D                   |
|1072K                                            |Piper PA-31                             |
|1072L                                            |de Havilland Canada DHC-6 Twin Otter 100|
|1072N                                            |Soloy 12EJ3                             |
|1072Q                                            |Fokker F-27 Friendship 200              |
|1072T                                            |Cessna 411                              |
|1072V                                            |Cessna 310N                             |
|1072X                                            |Boeing B-727-214 / Cessna 172           |
|100GX                                            |Boeing 247                              |
|1072Y                                            |Beech D18AS                             |
|1072Z                                            |Douglas C-47A-1-DK                      |
|10730                                            |Fokker F-27 Friendship 600              |
|10731                                            |Yakovlev YAK-40                         |
|10732                                            |Bell 205-1                              |
|10734                                            |Britten Norman BN-2A Trislander         |
|10737                                            |Antonov AN-24B                          |
|10738                                            |Beechcraft 65-80                        |
|1073A                                            |Cessna 402                              |
|1073E                                            |Douglas DC-3                            |
|100GZ                                            |Northrop Delta                          |
|1073F                                            |Cessna 310J                             |
|1073G                                            |McDonnell Douglas DC-8-Super 63CF       |
|1073L                                            |Beechcraft G18S                         |
|1073M                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1073Q                                            |Antonov An-12                           |
|1073S                                            |Douglas C-47A                           |
|1073T                                            |de Havilland DHC-2                      |
|1073U                                            |Aerostar 601P                           |
|1073V                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1073W                                            |Cessna 421 Golden Eagle                 |
|1001D                                            |Curtiss JN-4H                           |
|100HD                                            |Sinson                                  |
|1073X                                            |Boeing B-737-2A8                        |
|1073Y                                            |Cessna 210L                             |
|10741                                            |Cessna 207                              |
|10742                                            |McDonnell Douglas DC-9-32               |
|10743                                            |Britten Norman BN-2A Islander           |
|10747                                            |McDonnell Douglas DC-8-61               |
|10748                                            |Piper PA-31                             |
|10749                                            |Antonov AN-24N                          |
|1074C                                            |Let 410M                                |
|1074D                                            |Aerostar 601                            |
|100HG                                            |Kalinin K-7                             |
|1074F                                            |Nord 262A-44                            |
|1074G                                            |Fokker F-27 Friendship 500              |
|1074J                                            |Antonov 2PF                             |
|1074K                                            |Embraer 110C Bandeirante                |
|1074L                                            |Nord 262                                |
|1074M                                            |Vickers Viscount 748D                   |
|1074N                                            |Fokker F-27 Friendship 500              |
|1074R                                            |Douglas DC-3                            |
|1074S                                            |Douglas DC-6B                           |
|1074T                                            |Beech 58                                |
|100HJ                                            |Boeing 247                              |
|1074U                                            |Beech BE-70                             |
|1074W                                            |Cessna 310B                             |
|1074X                                            |Fokker F-28 Fellowship 1000             |
|1074Y                                            |Aerospatiale Nord 262A-33               |
|1075                                             |Boeing B-727-2D3                        |
|10750                                            |Hawker Siddeley Trident 2E              |
|10751                                            |Tupolev TU-104B                         |
|10752                                            |Yakovlev YAK-40                         |
|10753                                            |Tupolev 134A                            |
|10754                                            |Cessna U206                             |
|100HK                                            |Focke-Wulf A-17                         |
|10758                                            |Ilyushin IL-18D                         |
|1075A                                            |Fairchild F-27                          |
|1075C                                            |Piper PA-32RT-300                       |
|1075D                                            |Grumman G-21 Goose                      |
|1075E                                            |Sikorsky S61-L                          |
|1075H                                            |Vickers Viscount 785D                   |
|1075J                                            |Antonov AN-26                           |
|1075K                                            |McDonnell Douglas DC-10-10              |
|1075L                                            |Cessna 185                              |
|1075M                                            |de Havilland Canada DHC-4A Caribou      |
|100HL                                            |Junkers W-34                            |
|1075N                                            |de Havilland Canada DHC-5D Buffalo      |
|1075R                                            |de Havilland DHC-6-200                  |
|1075W                                            |Hindustan Aeronautics 748-2M            |
|1075X                                            |Beechcraft 99                           |
|1075Y                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1076                                             |Fokker F-28 Fellowship 1000             |
|10762                                            |Cessna 402B                             |
|10763                                            |Britten Norman BN-2A Trislander         |
|10764                                            |Douglas C-47B                           |
|10765                                            |Boeing 707-327C                         |
|100HM                                            |Avro 10                                 |
|10766                                            |de Havilland DH-114 Heron               |
|10767                                            |Hawker Siddeley HS-748-1                |
|10769                                            |Cessna  501 Citation                    |
|1076D                                            |LET 410M turbojet                       |
|1076F                                            |Hindustan Aeronautics 748 2-224         |
|1076G                                            |Cessna T210M                            |
|1076J                                            |Beechcraft D55                          |
|1076K                                            |Learjet 35                              |
|1076N                                            |Tupolev TU-134A / Tupolev Tu-134A       |
|1076Q                                            |Hawker Siddeley HS-748                  |
|100HP                                            |Dewoitine D-332                         |
|1076V                                            |Antonov AN-12                           |
|1076X                                            |Tupolev TU-124                          |
|1077                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10773                                            |Antonov AN-24                           |
|10774                                            |Aerospatiale Corvette                   |
|10777                                            |Boeing 707-324C                         |
|10779                                            |Douglas DC-7                            |
|1077A                                            |McDonnell Douglas DC-9-32               |
|1077B                                            |Britten Norman BN-7A lslander           |
|1077C                                            |Boeing KC-135A                          |
|100HR                                            |Breguet 280T                            |
|1077D                                            |de Havilland Canada DHC-6 Twin Otter 200|
|1077E                                            |Cessna 207                              |
|1077F                                            |Piper PA-31                             |
|1077G                                            |McDonnell Douglas DC-8-62               |
|1077H                                            |Cessna 207A                             |
|1077J                                            |Cessna 310                              |
|1077L                                            |Beech 200                               |
|1077U                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1077V                                            |McDonnell Douglas DC-10-10              |
|1077W                                            |De Havilland Dash-6                     |
|100HS                                            |Boeing 247                              |
|1077X                                            |Piper PA-31                             |
|1077Y                                            |Cessna T310R                            |
|1078                                             |Boeing B-727                            |
|10780                                            |Yakovlev YAK-40                         |
|10782                                            |Lockheed L-188CF Electra                |
|10784                                            |de Havilland Canada DHC-3 Otter         |
|10785                                            |Boeing B-707-340C                       |
|10787                                            |McDonnell Douglas DC-10-30              |
|1078A                                            |Grumman G-21 Goose                      |
|1078D                                            |de Havilland DHC-6                      |
|100HT                                            |Latécoère 28                            |
|1078E                                            |Antonov AN-26                           |
|1078F                                            |Martin 404                              |
|1078J                                            |Douglas DC-4 (C-54)                     |
|1078L                                            |de Havilland Canada DHC-5 Buffalo       |
|1078M                                            |Fokker F-28 Fellowship 1000             |
|1078N                                            |GAF Nomad 22B                           |
|1078P                                            |Britten Norman BN Islander              |
|1078Q                                            |Cessna 441 Conquest                     |
|1078S                                            |Boeing B-727-86                         |
|1078T                                            |CASA 212 Aviocar 100                    |
|1001E                                            |De Havilland DH-4                       |
|100HU                                            |Fairchild Pilgrim 100A                  |
|1078U                                            |Fairchild FH-227H                       |
|1078Z                                            |Yakovlev YAK-40                         |
|10791                                            |Beechcraft Super King Air 200           |
|10792                                            |Sikorsky S-62A                          |
|10793                                            |Fairchild C-119G                        |
|10797                                            |Boeing B-707-309C                       |
|10798                                            |Ilyushin IL-62                          |
|10799                                            |Lockheed C-130H                         |
|1079A                                            |Piper PA-28-180                         |
|1079B                                            |Sikorsky S-76                           |
|100HW                                            |Sikorsky S-38 Flying Boat               |
|1079D                                            |Cessna 402                              |
|1079E                                            |Britten Norman BN Islander              |
|1079F                                            |Boeing B-727-27C                        |
|1079H                                            |Lockheed EC-130E Hercules               |
|1079K                                            |Boeing B-727-64                         |
|1079L                                            |Hawker Siddeley HS-748-2                |
|1079M                                            |Britten Norman BN Islander              |
|1079P                                            |Ilyushin IL-14                          |
|1079Q                                            |Aerospatiale Caravelle 6R               |
|1079S                                            |Learjet 25D                             |
|100HX                                            |Ford 5-AT-C Tri-Motor                   |
|1079U                                            |Lockheed C-130                          |
|1079V                                            |Fairchild F-27J                         |
|1079Y                                            |Yakovlev YAK-40                         |
|107AB                                            |Swearingen 226TC Metro II               |
|107AC                                            |Yakovlev YAK-40                         |
|107AE                                            |Piper PA-34                             |
|107AF                                            |McDonnell Douglas DC-9-15               |
|107AJ                                            |Embraer 110P1 Bandeirante               |
|107AK                                            |Tupolev TU-154B                         |
|107AM                                            |Cessna 402B                             |
|100HY                                            |Sikorsky S-38BB                         |
|107AP                                            |Cessna 404 Titan II                     |
|107AR                                            |Piper PA-31-350                         |
|107AV                                            |Douglas DC-8-43F                        |
|107AW                                            |de Havilland DHC-3                      |
|107AX                                            |Bell 205A-1 helicopter                  |
|107AZ                                            |Tupolev TU-154B-1                       |
|107B                                             |Britten-Norman BN-2A-6 Islander         |
|107BA                                            |Learjet 35A                             |
|107BB                                            |Lockheed L-1011-200                     |
|107BC                                            |Lockheed C-130E Hercules                |
|100J                                             |Wibault 282T-12                         |
|107BF                                            |Lockheed 1011-200 TriStar               |
|107BH                                            |Vickers Viscount 812                    |
|107BJ                                            |Lockheed L-100-20 Hercules              |
|107BK                                            |Douglas C-47                            |
|107BL                                            |Douglas DC-3                            |
|107BM                                            |Lockheed Hercules C-130                 |
|107BN                                            |Lockheed C-130E                         |
|107BW                                            |de Havilland DHC-5 Buffalo              |
|107BZ                                            |Britten-Norman BN-2A-27 Islander        |
|107C                                             |Antonov AN-12V                          |
|100JA                                            |Liore-et-Olivier 213                    |
|107CA                                            |Beechcraft E18S                         |
|107CB                                            |Lockheed C-130H Hercules                |
|107CD                                            |Lockheed C-141A                         |
|107CG                                            |Britten-Norman BN-2A Trislander         |
|107CH                                            |Boeing B-747-2B5B                       |
|107CK                                            |Douglas C-47A-35-DL                     |
|107CL                                            |Douglas DC-7B                           |
|107CM                                            |Piper PA-42 Cheyenne                    |
|107CT                                            |Beechcraft B90                          |
|107CV                                            |Piper PA-32                             |
|100JC                                            |Curtiss Condor T-32                     |
|107CX                                            |Britten-Norman BN-2A Trislander         |
|107CZ                                            |Vickers Viscount 745D                   |
|107D                                             |Beechcraft 99A                          |
|107DA                                            |Aero Commander 681                      |
|107DD                                            |Tupolev TU-104A                         |
|107DF                                            |Cessna 310R                             |
|107DG                                            |Lockheed 1339                           |
|107DJ                                            |Sikorsky S-62A                          |
|107DK                                            |Embraer 110P Bandeirante                |
|107DM                                            |Cessna 310R                             |
|100JD                                            |Ford 5-AT-C Tri-Motor                   |
|107DN                                            |Lockheed MC-130E-Y                      |
|107DR                                            |Cessna T210N                            |
|107DS                                            |Dassault-Breguet Atlantique             |
|107DU                                            |Boeing RC-135S                          |
|107DW                                            |Antonov AN-24B                          |
|107E                                             |Piper PA-31                             |
|107EA                                            |Cessna 402                              |
|107EC                                            |Douglas C-47A                           |
|107EE                                            |Learjet 23                              |
|107EH                                            |Hadley Page 137Jetstream I / Cessna 206 |
|100JE                                            |Dornier Merkur                          |
|107ER                                            |Douglas C-47A-5-DK                      |
|107ES                                            |Boeing EC-135N                          |
|107EX                                            |BAC One-Eleven 529FR                    |
|107F                                             |Lockheed L-100-20 Hercules              |
|107FB                                            |Convair CV-440-11                       |
|107FC                                            |de Havilland Canada DHC-6 Twin Otter 300|
|107FE                                            |Beech Super King Air 200/DHC6-Twin Otter|
|107FG                                            |Beechcraft 58                           |
|107FH                                            |Lockheed C-130H Hercules                |
|107FM                                            |Ilyushin Il-14                          |
|100JF                                            |Lockheed Orion                          |
|107FT                                            |Britten-Norman BN-2A-8 Islander         |
|107G                                             |Douglas DC-3                            |
|107GB                                            |Hawker Siddeley HS-748                  |
|107GC                                            |Cessna 401                              |
|107GG                                            |Canadair CL-44D4-6                      |
|107GK                                            |Fokker F-27 Friendship 600RF            |
|107GL                                            |Beechcraft 58TC                         |
|107GM                                            |de Havilland Canada DHC-6 Twin Otter 300|
|107GS                                            |Douglas C-53D-DO                        |
|107H                                             |McDonnell Douglas DC-9-32               |
|1001F                                            |De Havilland DH-4                       |
|100JG                                            |Lockheed Vega                           |
|107HJ                                            |Piper PA-32                             |
|107HP                                            |Boeing B-737-222                        |
|107HQ                                            |Antonov AN-24RV / Soviet Air Force TU-16|
|107JA                                            |Yakovlev YAK-40                         |
|107JD                                            |Embraer 110P1 Bandeirante               |
|107JF                                            |Yakovlev YAK-40 / Mil Mi-8              |
|107JG                                            |Lockheed C-130H Hercules                |
|107JH                                            |Northrop F-5A                           |
|107JL                                            |Lockheed C-130H                         |
|107JM                                            |Learjet 24                              |
|100JH                                            |Curtiss AT-32C Condor                   |
|107JP                                            |Fokker F-28 Fellowship 4000             |
|107JS                                            |Cessna 404 Titan                        |
|107JW                                            |Lockheed L-749A Constellation           |
|107KA                                            |de Havilland Canada DHC-6 Twin Otter 300|
|107KB                                            |McDonnell Douglas DC-9-32               |
|107KC                                            |Piper PA-32                             |
|107KM                                            |Tupolev TU-154B-2                       |
|107KP                                            |Pilatus PC-6/B2-H2 Turbo-Porter         |
|107KQ                                            |Douglas DC-6A                           |
|107KR                                            |McDonnell Douglas MD-81                 |
|100JL                                            |Latecoere 26                            |
|107KV                                            |Beech C-45H                             |
|107L                                             |Cessna 207A                             |
|107LB                                            |Cessna 185                              |
|107LC                                            |Aerospatiale Puma                       |
|107LF                                            |de Havilland Canada DHC-6 Twin Otter 300|
|107LH                                            |Cessna 402B                             |
|107LJ                                            |Piper PA-31                             |
|107LM                                            |LET  410M Turbojet                      |
|107LS                                            |Cessna 210                              |
|107LT                                            |Boeing B-737-222                        |
|100JM                                            |Sikorsky S-38B                          |
|107LU                                            |Antonov AN-26                           |
|107M                                             |McDonnell Douglas DC-10-30CF            |
|107MA                                            |Antonov An-24RV                         |
|107MB                                            |Nord 2501 Noratlas                      |
|107MC                                            |Fairchild C-123                         |
|107ME                                            |Fairchild C-119G                        |
|107MJ                                            |McDonnell Douglas DC-8-61               |
|107MK                                            |Douglas DC-3 (C-47A-70-DL)              |
|107ML                                            |Douglas DC-6BF                          |
|107MM                                            |de Havilland DHC -6-100                 |
|100JP                                            |Stinson  SM-6000B                       |
|107MR                                            |de Havilland Canada DHC-6 Twin Otter 300|
|107MS                                            |Boeing B-747                            |
|107MT                                            |Yakovlev YAK-42                         |
|107MU                                            |Beechcraft Bonanza F35                  |
|107MY                                            |Boeing KC-135C                          |
|107NA                                            |Fokker F-28 Fellowship 1000             |
|107ND                                            |Vickers Viscount 745D                   |
|107NG                                            |Hughes 369D                             |
|107NJ                                            |Lockheed C-130H                         |
|107NN                                            |Hawker Siddeley Trident 2E              |
|100JR                                            |de Havilland DH-50A                     |
|107PA                                            |Beechcraft E18S                         |
|107PB                                            |Sikorsky S-76                           |
|107PC                                            |de Havilland Canada DHC-7-103           |
|107PF                                            |Lockheed C-130E Hercules                |
|107PG                                            |Westland Sea King HC-4 (helicopter)     |
|107PH                                            |Boeing B-737-200                        |
|107PJ                                            |Aerospatiale 330G Puma                  |
|107PK                                            |Fairchild C-123                         |
|107PM                                            |Boeing B-727-212A                       |
|107PR                                            |Fairchild-Hiller FH-227B-LCD            |
|100JS                                            |de Havilland DH-86                      |
|107PS                                            |Boeing B-707-437                        |
|107PT                                            |Cessna 404 Titan                        |
|107RA                                            |Ilyushin IL-62M                         |
|107RB                                            |Boeing B-727-235                        |
|107RF                                            |Hawker Siddeley HS-748-209 Srs. 2       |
|107RG                                            |Cessna 172F                             |
|107RH                                            |Bell UH-1B Huey Helicopter              |
|107RM                                            |Cessna A185F                            |
|107RN                                            |Piper PA-28-161                         |
|107RP                                            |Boeing B-747-121                        |
|100JT                                            |De Havilland DH-61                      |
|107RR                                            |de Havilland Canada DHC-6 Twin Otter 300|
|107RT                                            |LeT 410UVP Turbojet / Tupolev TU-134V   |
|107RV                                            |Arava 201                               |
|107RW                                            |Britten-Norman BN-2A Islander           |
|107RZ                                            |Lockheed C-141B                         |
|107S                                             |de Havilland Canada DHC-4A Caribou      |
|107SC                                            |Gates Learjet 25B                       |
|107SD                                            |Boeing Vertol CH-47C (helicopter)       |
|107SE                                            |McDonnell Douglas DC-10-30CF            |
|107SF                                            |Robertson C-U206F                       |
|100JV                                            |de Havilland DH-86                      |
|107SH                                            |de Havilland Canada DHC-3 Otter         |
|107SJ                                            |Cessna U206G                            |
|107SK                                            |Ilyushin IL-62M                         |
|107SL                                            |Piper PA-31                             |
|107SM                                            |Bell 212                                |
|107SP                                            |Beechcraft 95-B55                       |
|107SS                                            |Antonov AN-26                           |
|107ST                                            |de Havilland Canada DHC-6 Twin Otter 310|
|107SX                                            |Piper PA-32-260                         |
|107SY                                            |Swearingen SA.227AC Metro III           |
|100JY                                            |de Havilland DH-86                      |
|107TA                                            |Mil Mi-8 (helicopter)                   |
|107TB                                            |de Havilland DHC-2                      |
|107TC                                            |Fairchild F-27J                         |
|107TD                                            |Cessna T210                             |
|107TF                                            |Piper PA-31-350 Chieftain               |
|107TG                                            |Antonov AN-26                           |
|107TH                                            |Ilyushin IL-18B                         |
|107TJ                                            |Convair 580-11A                         |
|107TL                                            |McDonnell Douglas DC-8-54F37            |
|107TP                                            |Britten Norman BN-2A-20 Trislander      |
|1001J                                            |Armstrong-Whitworth F-K-8               |
|100K                                             |Stinson SM-6000-B                       |
|107TQ                                            |Boeing B-727-2F2                        |
|107TR                                            |Lockheed C-130H Hercules                |
|107TS                                            |Piper PA-32-301                         |
|107TT                                            |Bell 212                                |
|107TU                                            |de Havilland Canada DHC-6 Twin Otter 300|
|107TX                                            |McDonnell Douglas DC-9-32               |
|107US                                            |Mitsubishi MU-2B-60                     |
|107UV                                            |Learjet 25                              |
|107V                                             |Beech Super King Air 200                |
|107VA                                            |Britten-Norman BN-2A-8 Islander         |
|100KA                                            |Junkers F-13                            |
|107VC                                            |Hawker Siddeley HS-748-329 Srs. 2A      |
|107VS                                            |Yakovlev YAK-40                         |
|107VU                                            |Kawasaki C-1 / Kawasaki C-1             |
|107VW                                            |PS-1                                    |
|107WA                                            |Sud Aviation SE-210 Caravelle VIR       |
|107WD                                            |Convair CV-340                          |
|107WF                                            |Fairchild C-123K                        |
|107WK                                            |Lockheed L-1011                         |
|107WM                                            |Fokker F-28 Fellowship 3000RC           |
|107WS                                            |McDonnell Douglas DC-9-32               |
|100KB                                            |Lockheed Vega 5C                        |
|107WW                                            |Fairchild C-199G                        |
|107XL                                            |Lockheed P-3B Orion                     |
|107XR                                            |de Havilland Canada DHC-6 Twin Otter 300|
|107XS                                            |Cessna U206                             |
|107XX                                            |Lockheed C-130H Hercules                |
|107Y                                             |Ilyushin IL-62M                         |
|107YK                                            |Boeing B-737-2V2                        |
|107YY                                            |Sikorsky S-61N-II                       |
|107Z                                             |Boeing B-767-233ER                      |
|107ZA                                            |Cessna 404 Titan                        |
|100KC                                            |Ford 4-AT-E Tri-motor                   |
|107ZC                                            |Britten-Norman BN-2A-21 Islander        |
|1080                                             |Beechcraft G18S                         |
|10804                                            |Piper PA-31-350 Chieftain               |
|10805                                            |Lockheed L-100-30 Hercules              |
|10807                                            |Beech Super King Air 200                |
|10808                                            |Tupolev TU-134A                         |
|1080D                                            |Boeing B-747-230B                       |
|1080F                                            |Britten-Norman BN-2A-21 Islander        |
|1080H                                            |Hawker Siddeley Trident 2E /  II-28     |
|1080J                                            |Boeing B-737-2P6                        |
|100KE                                            |Douglas DC-2-115A                       |
|1080K                                            |Cessna TU206C                           |
|1080M                                            |Britten-Norman BN-2A-26 Trislander      |
|1080N                                            |Yakovlev YAK-40                         |
|1080P                                            |Cessna 182R                             |
|1080R                                            |Embraer 110C Bandeirante                |
|1080S                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1080V                                            |Hawker Siddeley HS-748-FAA              |
|1080W                                            |Shorts 330-200                          |
|1080X                                            |Boeing B-737-200                        |
|1080Z                                            |de Havilland Canada DHC-6 Twin Otter 300|
|100KF                                            |Lockheed Orion 9D                       |
|1081                                             |Beechcraft B-100                        |
|10812                                            |Boeing B-747-283B                       |
|10814                                            |Fokker F-28 Fellowship 2000             |
|10815                                            |Boeing B-727-200 / DC9-32               |
|10816                                            |Cessna 207                              |
|10817                                            |Boeing 707-373C                         |
|10819                                            |de Havilland Canada DHC-6 Twin Otter 200|
|1081A                                            |Antonov AN-24                           |
|1081D                                            |CASA 212-A3 Aviocar 100                 |
|1081F                                            |Douglas DC-3                            |
|100KH                                            |Consolidated Fleetster                  |
|1081H                                            |Tupolev TU-134A                         |
|1081J                                            |Douglas EC-54U                          |
|1081K                                            |CASA 212 Aviocar 200                    |
|1081V                                            |Antonov An-24RV                         |
|1081W                                            |Swearingen SA.226TC Metro II            |
|1081Y                                            |Antonov AN-12                           |
|1082                                             |Bell UH-1H / Bell UH-1H                 |
|10820                                            |Cessna 500 Citation I                   |
|10829                                            |Cessna 404 Titan                        |
|1082D                                            |PS-1                                    |
|100KJ                                            |Junkers JU-52/3m                        |
|1082E                                            |McDonnell Douglas DC-10-30              |
|1082F                                            |Lockheed C-130E                         |
|1082G                                            |Piper PA-31                             |
|1082J                                            |Curtiss C-46A                           |
|1082K                                            |Fairchild F-27M                         |
|1082P                                            |Sikorsky CH-53D                         |
|1082V                                            |Douglas C-54                            |
|1082X                                            |Cessna 402B                             |
|1082Y                                            |PT-LCN                                  |
|1082Z                                            |Embraer 110EJ Band./Embraer 110P Band.  |
|100KL                                            |Rochrbach Roland                        |
|10830                                            |McDonnel F-4E Phantom II                |
|10832                                            |Gates Learjet 35A                       |
|10836                                            |Lockheed L-188AF Electra                |
|10838                                            |Learjet 23A                             |
|10839                                            |Aerospeciale AS-350D                    |
|1083D                                            |Embraer 110C Bandeirante                |
|1083E                                            |Beechcraft 18                           |
|1083F                                            |Bell UH-1H                              |
|1083H                                            |Lockheed C-141B                         |
|1083J                                            |Grumman G-21A                           |
|100KM                                            |de Havilland Dragon 1                   |
|1083L                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1083Q                                            |Cessna 401                              |
|1083R                                            |Britten-Norman BN-2A Islander           |
|1083S                                            |Fokker F-27 Friendship 600              |
|1083T                                            |Antonov AN-12BP                         |
|1083V                                            |Cessna 402A                             |
|1083W                                            |Douglas DC-3                            |
|1084                                             |Douglas C-47A                           |
|10842                                            |Piper PA-31                             |
|10843                                            |Beechcraft C99 / Rockwell 112TC         |
|1001K                                            |De Havilland DH-4                       |
|100KS                                            |Junkers F-13                            |
|10844                                            |Boeing B-737-2H7C                       |
|10846                                            |Britten-Norman BN-2A-20 Islander        |
|10847                                            |Cessna 402C                             |
|10848                                            |Handley Page Dart Herald 202            |
|1084E                                            |Antonov An-2T                           |
|1084F                                            |McDonnell Douglas DC-8F-55              |
|1084G                                            |Antonov AN-12                           |
|1084H                                            |Cessna 500 Citation I                   |
|1084L                                            |Cessna R182                             |
|1084M                                            |de Havilland Canada DHC-6 Twin Otter 100|
|100KU                                            |Farman F-300                            |
|1084U                                            |Tupolev TU-154B                         |
|1084V                                            |de Havilland Canada DHC-6 Twin Otter 100|
|1084W                                            |Ilyushin IL-76M                         |
|1084X                                            |Antonov AN-22                           |
|10851                                            |Douglas C-47B                           |
|10853                                            |Embraer 110P1 Bandeirante               |
|10856                                            |de Havilland Canada DHC-6 Twin Otter 300|
|10859                                            |LET 410 M                               |
|1085B                                            |Embraer 110P1 Bandeirante               |
|1085C                                            |Antonov An-32                           |
|100KW                                            |Fokker F-12                             |
|1085F                                            |PA-23-250                               |
|1085G                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1085J                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1085K                                            |Tupolev TU-154B-2                       |
|1085L                                            |Boeing B-727-225 Adv                    |
|1085M                                            |Lockheed L-188AF Electra                |
|1085N                                            |Antonov AN-24B                          |
|1085P                                            |Ilyushin IL-18D                         |
|1085S                                            |Bell 206 L-1                            |
|1085T                                            |Lockheed L-188A Electra                 |
|100KY                                            |Lockheed Vega                           |
|1085W                                            |Lockheed C-130A                         |
|1085X                                            |Embraer 110P1 Bandeirante               |
|1085Y                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1085Z                                            |Piper PA-31-350                         |
|1086                                             |Tupolev TU-134A                         |
|10860                                            |Beech Queen Air 65-A80                  |
|10865                                            |Cessna 402B                             |
|10866                                            |Ilyushin IL-76MD                        |
|1086A                                            |Gulfstream AC-680F                      |
|1086C                                            |Britten-Norman BN-2A Islander           |
|100KZ                                            |Douglas DC-2-112                        |
|1086E                                            |Boeing B-727-256                        |
|1086F                                            |Boeing B-747-SP-09                      |
|1086H                                            |Antonov AN-24V                          |
|1086J                                            |Boeing RC-135T                          |
|1086L                                            |Lockheed C-130E Hercules                |
|1086M                                            |Fokker F-28 Fellowship 3000             |
|1086Q                                            |HS-125-700B                             |
|1086S                                            |Cessna 320B                             |
|1086T                                            |Boeing B-737-200                        |
|1086U                                            |Boeing B-727-227                        |
|100L                                             |Ford model 4-AT-E                       |
|1086V                                            |Cessna U206G                            |
|1086W                                            |Fokker F-27 Friendship 100              |
|1087                                             |Convair CV-440                          |
|10874                                            |Tupolev TU-134A / Antonov An-26         |
|10876                                            |CH-53D                                  |
|10877                                            |Britten-Norman BN-2 Islander            |
|1087A                                            |Cessna C-207A                           |
|1087C                                            |Cessna 501 Citation I                   |
|1087E                                            |Convair CV-580                          |
|1087J                                            |Grumman G-159 Gulfstream I              |
|100LB                                            |Tupolev ANT-20 / I-5                    |
|1087K                                            |Boeing B-727-231                        |
|1087Q                                            |Embraer 110P Bandeirante                |
|1087S                                            |Boeing B-747-237B                       |
|1087T                                            |Piper PA-42                             |
|1088                                             |Tupolev TU-154B-2                       |
|10880                                            |Aerostar 601                            |
|10881                                            |Douglas DC-6B                           |
|10883                                            |Lockheed L-1011-1 TriStar               |
|10886                                            |Boeing B-747-SR46                       |
|10888                                            |de Havilland Canada DHC-6 Twin Otter 300|
|100LC                                            |Boeing 221                              |
|10889                                            |Boeing 707-336C                         |
|1088D                                            |Learjet 24D                             |
|1088E                                            |Boeing B-737-236                        |
|1088F                                            |Beechcraft 99                           |
|1088H                                            |Boeing KC-135A                          |
|1088J                                            |Britten-Norman BN-2A Islander           |
|1088K                                            |Antonov AN-26                           |
|1088L                                            |McDonnell Douglas DC-9-14               |
|1088M                                            |Antonov AN-12                           |
|1088N                                            |Beechcraft B99                          |
|100LD                                            |Stinson SM6000B Tri-motor               |
|1088R                                            |Antonov An-12                           |
|1088S                                            |Cessna 208 Caravan I                    |
|1088T                                            |Cessna 402B                             |
|1088U                                            |Embraer 110C Bandeirante                |
|1088V                                            |IAI 1124 Westwind                       |
|1088Y                                            |Curtiss C-46D                           |
|1089                                             |Yakovlev YAK-40                         |
|10891                                            |de Havilland Canada DHC-6 Twin Otter 200|
|10894                                            |Fokker F-27 Friendship 600              |
|10895                                            |Learjet 24XR                            |
|100LE                                            |NaN                                     |
|10897                                            |Cessna 208                              |
|10899                                            |Convair CV-340                          |
|1089A                                            |Piper PA-32-300                         |
|1089B                                            |Lockheed C-130H Hercules                |
|1089C                                            |Boeing B-737-266                        |
|1089D                                            |Antonov AN-26                           |
|1089E                                            |McDonnell Douglas DC-8 Super 63PF       |
|1089F                                            |Short SC7- Skyvan                       |
|1089G                                            |Douglas DC-3                            |
|1089J                                            |Sud-Aviation  Caravelle VI-N            |
|1001L                                            |Junkers JL-6                            |
|100LG                                            |Ford Tri-Motor / Ford Tri-Motor         |
|1089M                                            |Bell 296B                               |
|1089P                                            |Boeing B-737-2A1                        |
|1089U                                            |Douglas DC-3A-178                       |
|1089W                                            |Lockheed L-188AF Electra                |
|1089X                                            |Boeing B-737-281                        |
|1089Z                                            |Antonov AN-24B                          |
|108A                                             |Cessna 425 Conquest                     |
|108AB                                            |Embraer 110P1 Bandeirante               |
|108AC                                            |CASA 212 Aviocar 100                    |
|108AD                                            |de Havilland Canada DHC-3 Otter         |
|100LJ                                            |Fokker F-XXII                           |
|108AE                                            |Antonov An-12AP                         |
|108AF                                            |Sepecat Jaguar A                        |
|108AG                                            |Antonov AN-26                           |
|108AH                                            |Boeing B-727-264                        |
|108AJ                                            |Boeing B-727                            |
|108AL                                            |Lockheed HC-130P Hercules               |
|108AM                                            |de Havilland Canada DHC-6 Twin Otter 300|
|108AN                                            |Douglas DC-6                            |
|108AP                                            |Bell UH-1H / Bell UH-1H (helicopters)   |
|108AT                                            |Lockheed L-1011-100                     |
|100LK                                            |General 102-E                           |
|108AV                                            |Yakovlev Yak-40                         |
|108B                                             |Cessna 414A                             |
|108BA                                            |Dassault Breguet Atlantique             |
|108BB                                            |Douglas C-47                            |
|108BD                                            |Fokker F-27 Friendship 500              |
|108BG                                            |de Havilland Canada DHC-6 Twin Otter 300|
|108BJ                                            |Boeing KC-135A                          |
|108BK                                            |de Havilland Can. DHC-6 -300/ Bell 206B |
|108BM                                            |Tupolev TU-134A                         |
|108BT                                            |Tupolev TU-134A                         |
|100LL                                            |Douglas DC-2                            |
|108BZ                                            |Douglas C-47A                           |
|108CB                                            |Piper PA-32-260                         |
|108CC                                            |de Havilland Canada DHC-6 Twin Otter 300|
|108CF                                            |Lockheed C130D                          |
|108CG                                            |Fokker F-27 Friendship 400M             |
|108CH                                            |Cessna T207A                            |
|108CJ                                            |Cessna 441 Conquest                     |
|108CL                                            |Howard 250                              |
|108CM                                            |MD Douglas DC-9-32 / Piper PA-28-181    |
|108CP                                            |Cessna 402                              |
|100LM                                            |Sikorsky S-38B                          |
|108CR                                            |Boeing B-747-121                        |
|108CS                                            |Lockheed C-130A Hercules                |
|108DB                                            |Britten-Norman BN-2A Trislander         |
|108DC                                            |Embraer 120RT Brasilia                  |
|108DF                                            |Shorts SC-7 Skyvan 3-200                |
|108DG                                            |Lockheed L-100-30 Hercules              |
|108DJ                                            |LET 410MT Turbojet                      |
|108DN                                            |Boeing 737-286                          |
|108DQ                                            |Casa 212-M Aviocar 100                  |
|108DS                                            |Piper PA-28-181                         |
|100LN                                            |Stinson Model A                         |
|108DU                                            |Tupolev TU-134A                         |
|108DW                                            |Tupolev TU-134A                         |
|108E                                             |Enstrom F-28F                           |
|108EB                                            |Fokker F-27 Friendship 600              |
|108EC                                            |Mil Mi-17 (helicopter)                  |
|108ED                                            |Lockheed C-130                          |
|108EE                                            |Boeing-Vertol Chinook                   |
|108EH                                            |Ilyushin IL-18                          |
|108ET                                            |Tupolev TU-134A                         |
|108EW                                            |Antonov AN-24RV                         |
|100LR                                            |Waco, model YLC                         |
|108EZ                                            |Boeing B-737-270C                       |
|108F                                             |de Havilland DH-114 Heron 2B            |
|108FB                                            |CASA 212-100                            |
|108FE                                            |Boeing B-707-379C                       |
|108FJ                                            |Britten-Norman BN-2A-20 Islander        |
|108FL                                            |Antonov AN-12                           |
|108G                                             |Swearingen SA-226TC / Mooney M-20C      |
|108GA                                            |Cessna 208 Caravan I                    |
|108GB                                            |Cessna U-27A Caravan I                  |
|108GC                                            |Learjet 55                              |
|100LS                                            |Lockheed Orion 9E Explorer float plane  |
|108GG                                            |Embraer 110P2 Bandeirante               |
|108GL                                            |Antonov AN-26                           |
|108GP                                            |Boeing B-707-323B                       |
|108GW                                            |CASA 212 Aviocar 200                    |
|108GX                                            |Antonov An-26                           |
|108H                                             |Boeing KC-135                           |
|108HF                                            |F-4C Phantom jet fighter                |
|108HG                                            |Learjet 24A                             |
|108HP                                            |Antonov AN-26                           |
|108HQ                                            |Cessna 402                              |
|100LW                                            |Boeing 247                              |
|108HS                                            |Beechcraft King Air C90                 |
|108J                                             |McDonnell Douglas DC-9-32               |
|108JA                                            |Boeing 707-351C                         |
|108JB                                            |Swearingen SA-26TC Metro II             |
|108JC                                            |Cessna 404 Titan II                     |
|108JE                                            |Antonov 12BP                            |
|108JF                                            |CASA 212 Aviocar 200                    |
|108JG                                            |Ilyushin IL-62M                         |
|108JH                                            |Douglas C-47B                           |
|108JK                                            |Piper PA-32-300                         |
|100LY                                            |de Havilland DH-86                      |
|108JL                                            |de Havilland Canada DHC-6 Twin Otter 300|
|108JM                                            |de Havilland Canada DHC-6 Twin Otter 300|
|108JN                                            |de Havilland Canada DHC-6 Twin Otter 100|
|108JR                                            |Cessna 501 Citation                     |
|108JS                                            |Britten-Norman BN-2A Islander           |
|108JT                                            |Antonov AN-26                           |
|108JW                                            |Antonov AN-26                           |
|108K                                             |Yakovlev YAK-40                         |
|108KA                                            |Fokker F-27 Friendship 200              |
|108KB                                            |Hawker Siddeley HS-748-209 Srs. 2       |
|1001M                                            |Junkers F-13                            |
|100M                                             |Boeing 247D                             |
|108KC                                            |Lockheed C-130E Hercules                |
|108KD                                            |McDonnell Douglas DC-10-30              |
|108KF                                            |Boeing B-377 Stratofreighter            |
|108KJ                                            |Learjet 23A                             |
|108KK                                            |Boeing B-737-2A1                        |
|108KM                                            |Ilyushin IL-18D                         |
|108KN                                            |McDonnell Douglas MD-82                 |
|108KP                                            |Piper PA-31-350 Navajo                  |
|108KS                                            |Boeing B-737-2P5                        |
|108KW                                            |Hawker Siddeley HS-125-403B             |
|100MA                                            |Junkers F-13                            |
|108L                                             |Antonov AN-26                           |
|108LA                                            |Airbus A.300B4-203                      |
|108LB                                            |Cessna T210L                            |
|108LC                                            |Fokker F-27 Friendship 500              |
|108LE                                            |de Havilland Canada DHC-6 Twin Otter 310|
|108LF                                            |Aerospatiale Alenia ATR-42-312          |
|108LG                                            |Antonov An-12B                          |
|108LH                                            |Cessna 310 N                            |
|108LJ                                            |Shorts SC-7 Skyvan 3-100                |
|108LK                                            |de Havilland Canada DHC-4A Caribou      |
|100MB                                            |Curtiss AT-32C Condor                   |
|108LL                                            |McDonnell Douglas DC-9-14               |
|108LN                                            |Beechcraft 1900C                        |
|108LT                                            |Cessna 208 Caravan I                    |
|108LU                                            |Britten-Norman BN-2A-26 Trislander      |
|108LV                                            |Swearingen SA.227AC Metro               |
|108LW                                            |Boeing B-747-244B                       |
|108LZ                                            |Boeing B-707-3B5C                       |
|108M                                             |Cessna 404 Titan                        |
|108MA                                            |British Aerospace BAe-146-200A          |
|108MB                                            |Fokker F-27 Friendship 400M             |
|100MC                                            |Boeing B-247-D                          |
|108MC                                            |Britten-Norman BN-2A-2 Islander         |
|108MD                                            |Shorts 360-300                          |
|108ME                                            |Lockheed C-130H                         |
|108MH                                            |Embraer 120 Brasilia                    |
|108MK                                            |Aerospatiale SA-330J                    |
|108MM                                            |Cessna 402C                             |
|108MN                                            |Piper PA-31-350 Navajo                  |
|108MP                                            |Piper PA-31-350 Navajo                  |
|108MQ                                            |de Havilland Canada DHC-6 Twin Otter 300|
|108MR                                            |Boeing B-737-230A                       |
|100MD                                            |Latécoère 28-1                          |
|108MS                                            |Learjet 36A                             |
|108N                                             |Curtiss C-46A-55                        |
|108NB                                            |Tupolev TU 154B-2                       |
|108ND                                            |Yakovlev YAK-40                         |
|108NG                                            |CASA 212 Aviocar 200                    |
|108NM                                            |Cessna 421A                             |
|108NN                                            |Swearingen SA.227AC Metro III           |
|108NS                                            |Swearingen SA227-AC                     |
|108P                                             |Tupolev TU-134A                         |
|108PB                                            |Boeing B-727-2H9A                       |
|100MF                                            |Ford Tri-Motor                          |
|108PC                                            |Embraer 110P1 Bandeirante               |
|108PF                                            |Fairchild FH-227B                       |
|108PH                                            |Rockwell Sabreliner 40                  |
|108PK                                            |Sikorsky UH-60A / Sikorsky UH-60A       |
|108PP                                            |Boeing B-727-21                         |
|108PS                                            |Douglas DC-8-55F                        |
|108PT                                            |Boeing B-747-200                        |
|108RB                                            |Antonov AN-26                           |
|108RC                                            |Douglas DC-3C                           |
|108RD                                            |Mitsubishi MU-2L Marquise               |
|100MG                                            |Lockheed Vega                           |
|108RF                                            |Let 410UVP Turolet                      |
|108RG                                            |Antonov AN-26                           |
|108RH                                            |Learjet 35A                             |
|108RJ                                            |Ilyushin IL-14P                         |
|108RK                                            |Boeing B-737-297                        |
|108RL                                            |de Havilland Canada DHC-7-102           |
|108RM                                            |Piper PA-32-260                         |
|108RP                                            |Boeing B-737-3T0                        |
|108RR                                            |Douglas DC-6                            |
|108RT                                            |Fokker F-27 Friendship 600              |
|100MH                                            |Latecoere 28                            |
|108SA                                            |Military - Ecudorian Air Force          |
|108SC                                            |Lockheed C-130E Hercules                |
|108SF                                            |McDonnell Douglas MD-81                 |
|108SG                                            |Mil Mi-8 (helicopter)                   |
|108SH                                            |Airbus A320-111                         |
|108SM                                            |Airbus A300B2-203                       |
|108SP                                            |Canadair CL-44J                         |
|108SR                                            |Douglas C-118A                          |
|108SS                                            |Boeing 707-328C                         |
|108SU                                            |Cessna CE185                            |
|100MJ                                            |Caudron C-630 Simoun                    |
|108SV                                            |Yakovlev YAK-40                         |
|108SW                                            |CASA 212 Aviocar 200                    |
|108SX                                            |Antonov AN-22                           |
|108SY                                            |Lockheed C-130B                         |
|108T                                             |Partenavia P-68C                        |
|108TA                                            |Douglas DC-4                            |
|108TB                                            |Let 410MU                               |
|108TC                                            |Aermacchi MB-339PAN (3 aircraft)        |
|108TF                                            |Hawker Siddeley HS-121 Trident 2E       |
|108TL                                            |Embraer 110P1 Bandeirante               |
|100ML                                            |Savoia-Marchetti SM73                   |
|108TM                                            |Convair CV-240                          |
|108TR                                            |Boeing B-727-232 Adv                    |
|108TS                                            |Britten-Norman BN-2A Islander           |
|108TT                                            |Tupolev TU-134A                         |
|108TW                                            |Lockheed L-188A Electra                 |
|108TX                                            |BAe-748                                 |
|108UA                                            |Boeing B-737-230                        |
|108UC                                            |Antonov AN-26                           |
|108US                                            |Boeing KC-135A                          |
|108UV                                            |Piper PA-32-300                         |
|1001P                                            |De Havilland DH-4                       |
|100MM                                            |Heinkel He-70                           |
|108UW                                            |Boeing B-707-338C                       |
|108V                                             |Fokker F-27 Friendship 100              |
|108VK                                            |Boeing B-737-2A8                        |
|108VR                                            |Fokker F-28 Fellowship 1000             |
|108VU                                            |Antonov AN-24B                          |
|108VV                                            |Piper PA-28-181                         |
|108VY                                            |Embraer 110P1 Bandeirante               |
|108W                                             |Cessna 441 Conquest                     |
|108WB                                            |Swearingen SA-226TC Metro II            |
|108WD                                            |de Havilland Canada DHC-6 Twin Otter 300|
|100MN                                            |Short Calcutta                          |
|108WG                                            |Let 410UVP                              |
|108WH                                            |Douglas DC-7CF                          |
|108WM                                            |Antonov AN-32                           |
|108WR                                            |Ilyushin IL-76 / Mi-8 (helicopter)      |
|108WS                                            |Boeing B-707-321C                       |
|108WW                                            |Mitsubish MU-2 uise                     |
|108WY                                            |Boeing B-747-121A                       |
|108XX                                            |NAMC YS-11A-300F                        |
|108Y                                             |Boeing B-737-4Y0                        |
|108YG                                            |Hawker Siddeley  Avro 748-215           |
|100MP                                            |Douglas DC-2-120                        |
|108YK                                            |Douglas DC-3(C-47A-DL)                  |
|108YZ                                            |Lockheed CC-130E Hercules               |
|108ZX                                            |Boeing KC-135A                          |
|108ZZ                                            |Fokker F-27 Friendship 600              |
|109                                              |Vickers 952F Vanguard                   |
|1090                                             |Boeing B-707-331B                       |
|10903                                            |Tupolev 154B                            |
|10906                                            |Boeing 747-249F                         |
|10908                                            |Cessna 402B                             |
|10909                                            |Boeing B-747-122                        |
|100MR                                            |Junkers JU-52                           |
|1090E                                            |Douglas DC-6                            |
|1090F                                            |Douglas C-47A                           |
|1090G                                            |Fokker F-28 Fellowship 1000             |
|1090H                                            |Britten Norman BN-2A Trislander         |
|1090J                                            |McDonnell Douglas DC-9-33RC             |
|1090L                                            |Sikorsky CH-53D                         |
|1090M                                            |Boeing B-707-349C                       |
|1090P                                            |Fairchild FH-227B                       |
|1090Q                                            |Pilatus PC-6 Turbo Porter               |
|1090U                                            |Aérospatiale SE-210 Caravelle           |
|100MS                                            |CAMS 53                                 |
|1090V                                            |Britten Norman BN-2A Trislander II      |
|1090W                                            |Embraer EMB-110 Bandeirante             |
|1091                                             |Beechcraft 99                           |
|10911                                            |Bell 412                                |
|10915                                            |McDonnell Douglas DC-8 Super 62         |
|10918                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1091A                                            |Beechcraft H18                          |
|1091C                                            |Ilyushin IL-62MK                        |
|1091D                                            |Antonov AN-26                           |
|1091G                                            |de Havilland Canada DHC-5D Buffalo      |
|100MT                                            |Vultee V-1                              |
|1091H                                            |Cessna 404 Titan Courier II             |
|1091K                                            |Hawker Siddeley HS-748-435 Srs. 2       |
|1091L                                            |Fokker F-27 Friendship 600RF            |
|1091M                                            |Dassault Falcon 20                      |
|1091N                                            |Beech E18S                              |
|1091P                                            |McDonnell Douglas DC-10-10              |
|1091R                                            |Antonov AN-26                           |
|1091S                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1091V                                            |BAC One-Eleven 516FP                    |
|1091Z                                            |Mil Mi-8 / Mil Mi-8                     |
|100MU                                            |Dormier Do-J-Iif Bos Wal                |
|10921                                            |Antonov AN-26                           |
|10922                                            |McDonnell Douglas DC-10-30              |
|10923                                            |Sikorsky S-58T                          |
|10924                                            |Convair CV-580                          |
|10925                                            |Shorts 330-200                          |
|10927                                            |de Havilland DHC-6 Twin Otter 300       |
|1092A                                            |Britten-Norman BN-2A-26 Trislander      |
|1092D                                            |Cessna 177RG                            |
|1092L                                            |Antonov AN-24RV                         |
|1092T                                            |Beechcraft C90                          |
|100MV                                            |Ford 5-AT-D Tri-Motor                   |
|1092U                                            |Fokker F-27 Friendship 200              |
|1092W                                            |Piper PA-31-350 Navajo                  |
|1092X                                            |Ilyushin IL-62M                         |
|1092Y                                            |Boeing B-737-241                        |
|1093                                             |Convair CV-580                          |
|10934                                            |de Havilland Canada DHC-6 Twin Otter 300|
|10936                                            |Beech King Air B100                     |
|10937                                            |McDonnell Douglas DC-10-30              |
|10939                                            |Military - U.S. Air Force               |
|1093A                                            |Boeing B-737-401                        |
|100MW                                            |Ford 5-AT-B Tri Motor                   |
|1093E                                            |Mil Mi-8 (helicopter)                   |
|1093G                                            |Mil Mi-17 ( helicopter)                 |
|1093L                                            |Dornier Do-288-201                      |
|1093X                                            |Swearingen SA.227AC Metro III           |
|1093Y                                            |Cessna 404 Titan II                     |
|1093Z                                            |de Havilland Canada DHC-6 Twin Otter 300|
|10940                                            |Antonov An-32                           |
|10941                                            |Boeing KC-135A                          |
|10942                                            |Cessna 208 Caravan I                    |
|10943                                            |Cessna 402C Utililiner                  |
|100MZ                                            |Stinson Model A                         |
|10944                                            |Agusta A109A MK II                      |
|10945                                            |Ilyushin IL-76TD                        |
|10946                                            |Boeing B-727-224                        |
|10948                                            |Boeing B-737-209                        |
|1094D                                            |Antonov AN-26                           |
|1094E                                            |de Havilland DHC-6 Twin Otter 300       |
|1094F                                            |Britten-Norman BN-2A Islander           |
|1094G                                            |Casa 212 Aviocar                        |
|1094J                                            |Cessna 551 Citation II                  |
|1094M                                            |Antonov AN-24                           |
|1001Q                                            |Salmson 2-A-2                           |
|100NA                                            |Douglas DC-2-112                        |
|1094T                                            |Mil Mi-4 / Mil Mi-4                     |
|1094U                                            |Fokker F-28 Fellowship 4000             |
|1094W                                            |Boeing B-727-21                         |
|1094Z                                            |Lockheed L-100-20 Hercules              |
|1095                                             |Cessna 402                              |
|10951                                            |Britten-Norman BN-2A Islander           |
|10952                                            |CASA 212 Aviocar 200                    |
|10955                                            |Lockheed C-130A                         |
|10956                                            |Grumman G-159 Gulfstream I              |
|10957                                            |British Aerospace 3101 Jetstream 31     |
|100ND                                            |Sikorsky S-42A                          |
|1095A                                            |Antonov An-24RV                         |
|1095B                                            |Cessna 207 / Cessna 207                 |
|1095E                                            |CASA 212 Aviocar 200                    |
|1095F                                            |Tupolev TU-134A                         |
|1095G                                            |CASA 212 Aviocar 200                    |
|1095J                                            |Cessna 208A Caravan I Cargomaster       |
|1095T                                            |Learjet 23                              |
|1095U                                            |CASA 212-200 Aviocar                    |
|1095W                                            |Boeing B-707-321B                       |
|1095X                                            |Hawker Siddeley HS-748-2A               |
|100NE                                            |OFM F-VIIb/3m                           |
|1096                                             |Nord 262C-66                            |
|10961                                            |Cessna 208B Caravan I                   |
|10962                                            |Cessna 208B Caravan I Super Cargomaster |
|10965                                            |Fokker 27 Friendship 200                |
|10966                                            |Airbus A320-231                         |
|10967                                            |DHC-5 Buffalo                           |
|10968                                            |Cessna 208A Caravan I Cargomaster       |
|1096E                                            |MiG-23                                  |
|1096H                                            |Antonov AN-26                           |
|1096J                                            |Aerospatiale 350D                       |
|100NG                                            |Junkers JU-52                           |
|1096K                                            |Sikorsky S-58ET (helilcopter)           |
|1096T                                            |Lockheed L-188CF Electra                |
|1096U                                            |Antonov AN-26                           |
|1096W                                            |Ilyushin IL-76MD                        |
|10971                                            |CASA 212 Aviocar 300                    |
|10972                                            |Learjet 25C                             |
|10975                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1097A                                            |de Havilland Canada DHC-6 Twin Otter 200|
|1097D                                            |Lockheed C-130H                         |
|1097E                                            |Douglas DC-3 (C-47A-30-DK)              |
|100NH                                            |Fokker F-VII                            |
|1097G                                            |Beechcraft C99                          |
|1097H                                            |Avro Shackleton AEW-2                   |
|1097J                                            |Douglas DC-6BF                          |
|1097K                                            |Fairchild F-27                          |
|1097L                                            |Boeing B-737-3Y0                        |
|1097M                                            |Cessna Citation I                       |
|1097N                                            |Transall C-160D                         |
|1097T                                            |Beechcraft 1900C-1                      |
|1097W                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1097Y                                            |Fairchild FH-227B                       |
|100NJ                                            |General Aviation GA-43                  |
|1097Z                                            |BAC One-Eleven 528FL                    |
|10982                                            |Cessna 207A                             |
|10983                                            |Cessna T210L                            |
|10985                                            |Britten-Norman 2B-21 Islander           |
|10987                                            |Britten-Norman BN-2A-8 Islander         |
|10989                                            |Mil Mi-8 (helicopter)                   |
|1098D                                            |Beech King Air B90                      |
|1098E                                            |Yakovlev YAK-40                         |
|1098M                                            |Antonov AN-12                           |
|1098N                                            |Beechcraft 1900C                        |
|100NK                                            |De Havilland DH-60                      |
|1098R                                            |Bell BHT-206-B Helicopter               |
|1098U                                            |Mil Mi 8T (helicopter)                  |
|1098W                                            |Lockheed C-5A                           |
|1099                                             |Piper PA-31-325 Navajo                  |
|10990                                            |Boeing B-727-247                        |
|10992                                            |Cessna 441 Conquest II                  |
|10993                                            |Yakovlev YAK-42                         |
|10996                                            |Embraer 110P1 Bandeirante               |
|10997                                            |Cessna 501 Citation                     |
|1099A                                            |Ilyushin IL-76                          |
|100NM                                            |Fokker F-XXII                           |
|1099C                                            |Boeing B-737-247 / Boeing B-757-21B     |
|1099F                                            |McDonnell Douglas DC-9-31               |
|1099H                                            |Douglas C-47B-40-DK                     |
|1099J                                            |Yakovlev YAK-40                         |
|1099R                                            |Antonov AN-8                            |
|1099S                                            |McDonnell Douglas DC-9-32               |
|1099W                                            |CASA 212 Aviocar 200                    |
|1099Y                                            |Mil Mi-8T                               |
|1099Z                                            |McDonnell Douglas DC-9-15RC             |
|109AA                                            |de Havilland Canada DHC-8-103           |
|100NN                                            |Junkers JU-160                          |
|109AC                                            |Aerospatiale 330J Puma                  |
|109AF                                            |Boeing B-727-251 / MD Douglas DC-9-14   |
|109AG                                            |Boeing B-707-320F                       |
|109AH                                            |IPTN 332C Super Puma                    |
|109AK                                            |Cessna 208 Caravan I                    |
|109AL                                            |CASA 212 Aviocar 200                    |
|109AM                                            |Learjet 25C                             |
|109AP                                            |CASA 212 Aviocar 200                    |
|109AT                                            |Military - U.S. Air Force               |
|109AZ                                            |Boeing B-737-300 / Swearingen SA-227AC  |
|100NR                                            |Junkers JU-52/3m                        |
|109B                                             |Lockheed C-130H                         |
|109BA                                            |Piper PA-31-350                         |
|109BB                                            |Learjet35A                              |
|109BC                                            |de Havilland Canada DHC-6 Twin Otter 300|
|109BD                                            |British Aerospace BAE-146-200A          |
|109BG                                            |Boeing B-737-291                        |
|109BH                                            |McDonnell Douglas DC-9-32               |
|109BJ                                            |Cessna 402B                             |
|109BL                                            |Hawker-Siddeley DH-125-1A/522           |
|109BM                                            |Lockheed L-100-30 Hercules              |
|10006                                            |Zeppelin L-2 (airship)                  |
|1001S                                            |Breguet 14                              |
|100NT                                            |Saro Cloud                              |
|109BR                                            |Gates Learjet 25                        |
|109BS                                            |Cessna 402C                             |
|109BT                                            |Lockheed C-130H                         |
|109BW                                            |Lockheed P-3C / Lockheed P-3C           |
|109BZ                                            |Antonov AN-24B                          |
|109C                                             |Hindustan Aeronautics 748-2             |
|109CA                                            |Cessna 402B                             |
|109CB                                            |Douglas C-47B-15-DK                     |
|109CC                                            |Piper Aerostar 601 / Bell 412SP         |
|109CF                                            |Embraer 120RT- Brasilia                 |
|100NU                                            |Wibault 280                             |
|109CG                                            |Dornier Do-228-212                      |
|109CH                                            |Cessna 404 Titan II                     |
|109CN                                            |Fokker F-27 Friendship 600              |
|109CQ                                            |Cessna 207A                             |
|109CR                                            |Douglas C-47B                           |
|109CT                                            |Tupolev TU-154B-1                       |
|109CW                                            |Ilyushin 76TD                           |
|109CY                                            |Boeing B-767-3Z9ER                      |
|109CZ                                            |GAF Nomad N24A                          |
|109D                                             |Lockheed L-382B Hercules                |
|100NV                                            |Lockheed Orion                          |
|109DA                                            |Douglas DC-6BF                          |
|109DC                                            |Antonov AN-24                           |
|109DG                                            |BAC One-Eleven 402AP                    |
|109DH                                            |de Havilland Canada DHC-6 Twin Otter 300|
|109DJ                                            |CASA 212 Aviocar 200                    |
|109DK                                            |Beechcraft BE-99-C99                    |
|109DL                                            |McDonnell Douglas DC-8 Super 61         |
|109DM                                            |de Havilland Canada DHC-6 Twin Otter 300|
|109DN                                            |Learjet 23                              |
|109DP                                            |Cessna 206                              |
|100NY                                            |Lockheed 10B Electra                    |
|109DR                                            |Britten-Norman BN-2A-6 Islander         |
|109DS                                            |Britten-Norman BN-2A-6 Islander         |
|109DU                                            |Ilyushin IL-18V                         |
|109DV                                            |Piper PA-32                             |
|109DW                                            |Fokker F-27 Friendship 100              |
|109EA                                            |Boeing B-737-2A8                        |
|109EC                                            |Britten-Norman BN-2A-6 Islander         |
|109EH                                            |Aerospatiale 350B1                      |
|109EJ                                            |Shorts SC-7 Skyvan 3-100                |
|109ER                                            |Britten-Norman BN-2A-21                 |
|100P                                             |Junkers F-13                            |
|109EV                                            |Embraer 120RT Brasilia                  |
|109EZ                                            |Antonov AN-72                           |
|109F                                             |Handley Page Dart Herald 400            |
|109FB                                            |Lockheed L-100-30 Hercules              |
|109FC                                            |Convair CV-580                          |
|109FE                                            |Antonov 12BP                            |
|109FF                                            |Antonov AN-26                           |
|109FR                                            |Curtiss C-46A                           |
|109FT                                            |Lockheed C-130H-30                      |
|109GA                                            |Cessna 402A                             |
|100PA                                            |De Havilland DH-86                      |
|109GB                                            |Bell 214 ST                             |
|109GC                                            |Britten-Norman BN2A-III-2 Trislander    |
|109GF                                            |Bell 206B helicopter                    |
|109GL                                            |Lockheed CC-130E                        |
|109GP                                            |Mil Mi-8 (helicopter)                   |
|109GS                                            |Yakovlev YAK-40                         |
|109GU                                            |Embraer 110P1 Bandeirante               |
|109GX                                            |Cessna 208B Caravan I Super Cargomaster |
|109GY                                            |Antonov AN-12V                          |
|109H                                             |Mil Mi-8 (helicopter)                   |
|100PB                                            |Short Kent                              |
|109HB                                            |Bell 206B                               |
|109HF                                            |Yakovlev YAK-40                         |
|109HJ                                            |Douglas C-47B-DK                        |
|109HM                                            |Antonov AN-24                           |
|109HN                                            |Embraer C-95C Bandeirante               |
|109HQ                                            |Piper PA-31-350 Navajo                  |
|109HR                                            |BeechJet 400                            |
|109HW                                            |Douglas DC-3A                           |
|109HY                                            |MDonnell Douglas MD-81                  |
|109J                                             |Piper PA-31-350 Navajo                  |
|100PC                                            |Boulton and Paul P-71                   |
|109JA                                            |Boeing B-747-2R7F                       |
|109JB                                            |Beechcraft 1900C                        |
|109JC                                            |Cessna T210L                            |
|109JD                                            |Airbus A320-111                         |
|109JG                                            |Beech C18S                              |
|109JH                                            |Mil Mi-8 (helicopter)                   |
|109JK                                            |Embraer 110C Bandeirante                |
|109JL                                            |Lockheed C-130B                         |
|109JM                                            |Convair CV- 640                         |
|109JS                                            |McDonnell Douglas DC-8-63F              |
|100PE                                            |Lockheed Vega                           |
|109JT                                            |Boeing B-747                            |
|109JW                                            |Curtiss C-46T                           |
|109K                                             |de Havilland Canada DHC-6 Twin Otter 300|
|109KB                                            |BAe 3101 Jetstream 31                   |
|109KE                                            |Fokker F-28 Fellowship 4000             |
|109KF                                            |Antonov AN-30                           |
|109KG                                            |Boeing 707-321C                         |
|109KM                                            |Let 410UVP                              |
|109KS                                            |Antonov AN-24RV                         |
|109LB                                            |Britten Norman BN-2A-26 Trislander      |
|100PF                                            |Lockheed Vega 5C                        |
|109LD                                            |Embraer 110P1 Bandeirante               |
|109LE                                            |de Havilland DHC-5 Buffalo              |
|109LH                                            |Piper PA-23-250                         |
|109LL                                            |de Havilland Canada DHC-6 Twin Otter 200|
|109LN                                            |Beechcraft E18S                         |
|109LR                                            |Fokker F-27 Friendship 400M             |
|109LS                                            |Lockheed C-130E Hercules                |
|109LT                                            |Boeing B-737-204                        |
|109LU                                            |CASA 212 Aviocar 200                    |
|109MA                                            |Beechcraft C99                          |
|1001T                                            |De Havilland DH-4                       |
|100PM                                            |Lockheed Orion                          |
|109MB                                            |Learjet 25B                             |
|109MC                                            |Beech Baron 95-B55                      |
|109MD                                            |Cessna 402C                             |
|109MG                                            |Boeing 737-2A1C                         |
|109MH                                            |Antonov AN-12                           |
|109MJ                                            |Piper PA-23-250                         |
|109MK                                            |Shaanxi Y-8D                            |
|109ML                                            |Shorts SC-7 Skyvan 3A-200               |
|109MM                                            |Antonov AN-12V                          |
|109MR                                            |Antonov An-12                           |
|100PP                                            |Blackburn B-2                           |
|109MS                                            |Tupolev TU-154B                         |
|109MT                                            |Vickers Viscount 816                    |
|109MY                                            |Antonov 12BK                            |
|109N                                             |Vickers 798D Viscount                   |
|109NA                                            |Learjet 25C                             |
|109NL                                            |Bell 47J-2                              |
|109NN                                            |Airbus A300B4-203                       |
|109NS                                            |Lockheed L-1011                         |
|109P                                             |Airbus A310-304                         |
|109PB                                            |Yakovlev YAK-42D                        |
|100PR                                            |Junkers JU-52                           |
|109PC                                            |Convair CV-440-80                       |
|109PG                                            |Swearingen SA-227AC Metro III           |
|109PL                                            |Tupolev TU-134A                         |
|109PS                                            |de Havilland Canada DHC-4T Caribou      |
|109Q                                             |Fairchild C123K                         |
|109QS                                            |de Havilland Canada DHC-6 Twin Otter 300|
|109R                                             |Douglas DC-3                            |
|109RA                                            |Beechcraft C-45H                        |
|109RB                                            |Fokker F-27 Friendship 500              |
|109RC                                            |Mil Mi-8 (helicopter)                   |
|100PS                                            |Antonov AN-9                            |
|109RD                                            |Aerospatiale AS-350B                    |
|109RF                                            |Douglas C-118A                          |
|109RH                                            |Curtiss C-46F-1-CU                      |
|109RJ                                            |Mil Mi-8 (helicopter)                   |
|109RK                                            |Lockheed C-130H                         |
|109RL                                            |Boeing B-747-258F                       |
|109RM                                            |Lockheed C-130E Hercules                |
|109RS                                            |Avia 14M-40                             |
|109RT                                            |Antonov 32                              |
|109RV                                            |CASA 235-10                             |
|100PT                                            |Junkers JU-52/3m                        |
|109RW                                            |Antonov AN-28                           |
|109S                                             |de Havilland Canada DHC-6 Twin Otter 300|
|109SB                                            |Antonov AN-8                            |
|109SC                                            |Piper PA-42                             |
|109SD                                            |Cessna 402C                             |
|109SF                                            |Antonov AN-22A                          |
|109SG                                            |Mil Mi-8 (helicopter)                   |
|109SJ                                            |Yakovlev YAK-40                         |
|109SR                                            |Ilyushin IL-18D                         |
|109ST                                            |Cessna T207A                            |
|100PU                                            |Fokker F-XII                            |
|109SW                                            |Boeing B-737-3Y0                        |
|109SY                                            |Lockheed C-141B / Lockheed C141B        |
|109T                                             |Britten-Norman BN-2B-27 Islander        |
|109TA                                            |Fokker F-27 Friendship 400M             |
|109TB                                            |McDonnell Douglas DC-10-30CF            |
|109TC                                            |Boeing B-727-2L5 / MiG23UB              |
|109TG                                            |Bell 206B3                              |
|109TJ                                            |de Havilland Canada DHC-8-301           |
|109TK                                            |Hawker Siddeley HS-748-234              |
|109TR                                            |Embraer 110P1 Bandeirante               |
|100PX                                            |Junkers JU-52/3m                        |
|109TS                                            |Douglas C-47A                           |
|109TT                                            |Nord 262A-44                            |
|109TW                                            |Shorts SC-7 Skyvan 3-100                |
|109TY                                            |Tupolev TU-154M / Sukhoi Su-24          |
|109U                                             |Mil Mi-8                                |
|109UA                                            |Convair CV-440                          |
|109US                                            |Dornier 228-201                         |
|109UV                                            |Fokker 100                              |
|109UW                                            |Beechcraft 58                           |
|109V                                             |Beech Super King Air 200                |
|100PY                                            |Latécoère 300                           |
|109VT                                            |Embraer EMB-110 Bandeirante             |
|109W                                             |Boeing B-747-466                        |
|109WA                                            |Fairchild SA227-TT                      |
|109WC                                            |Aerospatiale SA316B                     |
|109WD                                            |McDonnell Douglas DC-9-15               |
|109WE                                            |McDonnell Douglas MD-11                 |
|109WG                                            |Mitsubishi MU-2B-60                     |
|109WH                                            |Antonov AN-26B                          |
|109WJ                                            |Boeing B-737-2A8                        |
|109WK                                            |Antonov AN-32                           |
|100PZ                                            |Douglas DC-2-115E                       |
|109WP                                            |de Havilland  Canada  DHC-5D Buffalo    |
|109WR                                            |Beechcraft C99                          |
|109WT                                            |Britten-Norman BN-2A-6 Islander         |
|109WW                                            |Douglas DC-6BF                          |
|109X                                             |Boeing B-727-46                         |
|109XP                                            |de Havilland Canada DHC-6 Twin Otter 300|
|109XS                                            |Cessna 404 Titan                        |
|109Y                                             |Britten-Norman  BN-2A-20 Trislander     |
|109YK                                            |de Havilland Canada DHC-6 Twin Otter 300|
|109Z                                             |Antonov AN-26                           |
|100Q                                             |Boeing 247D                             |
|109ZA                                            |Fokker F-28 Fellowship 3000             |
|109ZT                                            |Mil Mi-8                                |
|10A                                              |Cessna 402C                             |
|10AA                                             |Helicopter, Hughes 369HS                |
|10AD                                             |British Aerospace 146-300               |
|10AE                                             |Boeing B-737-5L9                        |
|10AF                                             |Shorts SC-7 Skyvan 3-100                |
|10AG                                             |Dornier Do-228-101                      |
|10AJ                                             |Beechcraft C-90                         |
|10AK                                             |McDonnell Douglas DC-8-61               |
|1001V                                            |De Havilland DH-4                       |
|100QB                                            |Lockheed 10 Electra                     |
|10AM                                             |Let 410UVP-E                            |
|10AN                                             |Yakovlev YAK-40                         |
|10AR                                             |Airbus A320-211                         |
|10AS                                             |Tupolev TU-134A                         |
|10AU                                             |Tupolev TU-154B                         |
|10AX                                             |Tupolev 134A                            |
|10AZ                                             |Mil Mi-8 (helicopter)                   |
|10BA                                             |GAF Nomad N-22                          |
|10BB                                             |McDonnell Douglas MD-82                 |
|10BC                                             |de Havilland Canada DHC-6 Twin Otter 300|
|100QS                                            |Douglas DC-2-112                        |
|10BD                                             |Cessna 421B Golden Eagle                |
|10BE                                             |Hawker Siddeley HS-748-234 Srs. 2A      |
|10BF                                             |McDonnell Douglas MD-82                 |
|10BG                                             |Antonov AN-124                          |
|10BH                                             |Yakovlev YAK-42D                        |
|10BJ                                             |Beech Queen Air Model 80                |
|10BL                                             |British Aerospace Jetstream BA-3100     |
|10BM                                             |Britten Norman BN-2A Trislander7        |
|10BN                                             |DHC-6 Twin Otter 300 / NAMC YS-11       |
|10BP                                             |Yunshuji Y-12-II                        |
|100QT                                            |Lockheed 10 Electra                     |
|10BQ                                             |Lockheed C-130H                         |
|10BR                                             |Israel Aircraft Industries 1124A        |
|10BS                                             |Antonov AN-26                           |
|10BT                                             |Tupolev TU-154M                         |
|10BU                                             |Rockwell Turbo Commander 690B           |
|10BV                                             |Beechcraft King Air B90                 |
|10BW                                             |British Aerospace Jetstream 4101        |
|10BX                                             |Learjet 24D                             |
|10BY                                             |Antonov AN-12V                          |
|10BZ                                             |Yakovlev YAK-40                         |
|100RA                                            |Douglas DC-2                            |
|10C                                              |Vickers 813 Viscount                    |
|10CA                                             |McDonnell Douglas MD-82                 |
|10CC                                             |Boeing 737-2R4C                         |
|10CD                                             |Swearingen SA.226AT Merlin IV           |
|10CF                                             |Lockheed C-130H Hercules                |
|10CG                                             |Lockheed Hercules C-130                 |
|10CH                                             |Douglas DC-3C                           |
|10CJ                                             |Grumman G-73T Turbo Mallard             |
|10CK                                             |Britten-Norman BN-2A-21 Trislander      |
|10CL                                             |Cessna 650 Citation VI                  |
|100RB                                            |Boeing 247-D                            |
|10CM                                             |Boeing Vertol Chinook HC-2 (helicopter) |
|10CN                                             |Airbus A310-304                         |
|10CR                                             |GD F-16D / Lockheed C-130E              |
|10CS                                             |Bell 206B3                              |
|10CX                                             |Saab 340B                               |
|10CY                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10CZ                                             |Dassault Falcon 50                      |
|10DB                                             |Sikorsky UH-60 / Sikorsky UH-60         |
|10DC                                             |Britten Norman BN-2A-21 Trislander      |
|10DD                                             |Airbus A300B4-622R                      |
|100RC                                            |Boeing 247B                             |
|10DE                                             |Piper PA-31-350 Navajo                  |
|10DF                                             |Cessna 208 Caravan I                    |
|10DH                                             |Embraer 110 Bandeirante                 |
|10DJ                                             |Pilatus Britten-Norman BN-2B-27 Islander|
|10DK                                             |Douglas DC-3 (C-53D-DO)                 |
|10DL                                             |de Havilland DHC-2                      |
|10DM                                             |Tupolev TU-154M                         |
|10DP                                             |Swearingen SA.226TC Metro II            |
|10DR                                             |Learjet 25D                             |
|10DT                                             |Fokker F-27 Friendship 500F             |
|100RE                                            |Sabca S-73                              |
|10DU                                             |de Havilland DHC-3                      |
|10DV                                             |Fokker F-27 Friendship 400M             |
|10DW                                             |Antonov AN-32                           |
|10DZ                                             |Airbus A330-321                         |
|10E                                              |Fokker F-28 Fellowship 4000             |
|10EA                                             |McDonnell Douglas DC-9-30               |
|10EC                                             |Piper PA-32-301                         |
|10ED                                             |Aerospatiale AS350D                     |
|10EE                                             |Britten-Norman BN-2B-26 Islander        |
|10EF                                             |Yakovlev 40D                            |
|100RF                                            |Douglas DC-3A                           |
|10EG                                             |Embraer 110P1 Bandeirante               |
|10EH                                             |Sikorsky S-58ET                         |
|10EP                                             |Antonov AN-12                           |
|10ER                                             |Airbus A300B4-622R                      |
|10ET                                             |de Havilland DHC-2                      |
|10EV                                             |Bell 206L-4                             |
|10EX                                             |Piper PA-32-260                         |
|10EZ                                             |Aerospatiale ATR-42-300                 |
|10F                                              |Boeing B-737-3B7                        |
|10FA                                             |de Havilland Canada DHC-6 Twin Otter 300|
|100RG                                            |Stinson Model A                         |
|10FB                                             |de Havilland Canada DHC-6 Twin Otter 100|
|10FC                                             |BAC One-Eleven 515FB                    |
|10FF                                             |Lockheed L-100-30 Hercules              |
|10FK                                             |Yakovlev YAK-40                         |
|10FN                                             |Douglas C-47D                           |
|10FP                                             |Rockwell 1121B Jet Commander            |
|10FQ                                             |Antonov AN-8                            |
|10FR                                             |Douglas DC-3                            |
|10FT                                             |Antonov AN-32B                          |
|10FU                                             |Fokker F-28 Fellowship 1000             |
|100RK                                            |Heinkel He-111V2                        |
|10FV                                             |Lockheed C-130E                         |
|10FW                                             |Mil Mi-8MTV (helicopter)                |
|10FY                                             |Antonov AN-2                            |
|10FZ                                             |Antonov AN-12BP                         |
|10G                                              |ATR-72-212                              |
|10GA                                             |Bell 212                                |
|10GC                                             |de Havilland Canada DHC-6 Twin Otter 100|
|10GF                                             |Yakovlev YAK-40                         |
|10GG                                             |Beechcraft C99                          |
|10GH                                             |Britten Norman BN-2A Trislander         |
|1001W                                            |Handley Page HP-16                      |
|100RL                                            |Short  S-23 (flying boat)               |
|10GK                                             |McDonnell Douglas DC-9-82 / Cessna 441  |
|10GL                                             |Mil Mi-17 (helicopter)                  |
|10GN                                             |Boeing B-747-200                        |
|10GP                                             |Cessna 402C                             |
|10GR                                             |British Aerospace Jetstream 3201        |
|10GS                                             |Douglas C-47A-10-DK                     |
|10GT                                             |de Havilland Canada DHC-6 Twin Otter 200|
|10GV                                             |Boeing 737-2D6C                         |
|10GX                                             |Airbus A300B2-1C                        |
|10H                                              |Boeing B-737-4Y0                        |
|100RP                                            |Douglas DC-2-112                        |
|10HC                                             |Lockheed 1329 Jetstar 8                 |
|10HD                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10HG                                             |McDonnell Douglas DC-9-14               |
|10HH                                             |Cessna 208B Caravan I Super Cargomaster |
|10HJ                                             |Learjet 35                              |
|10HK                                             |Cessna 208B Caravan I Super Cargomaster |
|10HL                                             |Cessna 172N                             |
|10HM                                             |Bell 206B                               |
|10HN                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10HP                                             |Let 410UVP                              |
|100RT                                            |Junkers JU-52/3m                        |
|10HT                                             |Dassault Falcon 20E                     |
|10HU                                             |Aerospatiale ATR-72                     |
|10HV                                             |Piper PA-31-350 Navajo                  |
|10HW                                             |McDonnell Douglas DC-8-63F              |
|10HX                                             |Antonov 26B                             |
|10HY                                             |Cessna 208B Caravan I Super Cargomaster |
|10J                                              |Beech Queen Air B80                     |
|10JA                                             |Airbus A310-324                         |
|10JB                                             |Learjet C-21A                           |
|10JC                                             |de Havilland Canada DHC-6 Twin Otter 300|
|100RV                                            |Zeppelin LZ-129                         |
|10JF                                             |Pel Air                                 |
|10JG                                             |Hawker Siddeley HS-748-357/2B SCD       |
|10JH                                             |Swear. SA-227CC Metro 23/Piper Navajo   |
|10JJ                                             |Grumman Gulfstream II                   |
|10JK                                             |Curtiss C-46F                           |
|10JL                                             |Lockheed C-130E Hercules                |
|10JM                                             |Embraer 110 P1 Bandeirante              |
|10JN                                             |Douglas DC-3C                           |
|10JP                                             |Piper PA-31-310 Navajo                  |
|10JR                                             |McDonnell Douglas DC-9-32               |
|100RW                                            |Heinkel He-70                           |
|10JV                                             |de Havilland Canada DHC-8-102           |
|10JW                                             |Antonov 2R                              |
|10JX                                             |Antonov AN-2                            |
|10JZ                                             |CASA 212-200 Aviocar                    |
|10K                                              |Tupolev TU-134A                         |
|10KA                                             |Convair CV-440                          |
|10KE                                             |Piper PA-32-301                         |
|10KF                                             |de Havilland Canada C-7A Caribou        |
|10KG                                             |Piper PA-32R-300                        |
|10KJ                                             |de Havilland Canada DHC-6 Twin Otter 300|
|100RZ                                            |Lockheed 10E Electra                    |
|10KK                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10KL                                             |Douglas C-47A                           |
|10KP                                             |Britten-Norman BN-2A Islander           |
|10KQ                                             |Antonov An-2R                           |
|10KR                                             |Boeing B-737-2H6                        |
|10KS                                             |Hawker Siddeley HS-748 2A               |
|10KX                                             |Embraer 110P1 Bandeirante               |
|10KY                                             |Embraer 120-RT Brasilia                 |
|10KZ                                             |Shorts SC-7 Skyvan                      |
|10L                                              |British Aerospace Nimrod MR-2P          |
|100SA                                            |Douglas DC-2-115L                       |
|10LA                                             |Cessna 421C Golden Eagle                |
|10LB                                             |CASA 212 Aviocar 200                    |
|10LD                                             |Antonov AN-26B                          |
|10LE                                             |Antonov AN-32                           |
|10LF                                             |Cessna 402B                             |
|10LJ                                             |Fokker 50                               |
|10LK                                             |Swearingen SA.227AC Metro III           |
|10LM                                             |Antonov AN-24RV                         |
|10LS                                             |Boeing B-707 (E-3B)                     |
|10LT                                             |Mil Mi-8T                               |
|100SC                                            |Savoia-Marchetti SM73                   |
|10LW                                             |De Havilland Dash-3                     |
|10LX                                             |CASA 212                                |
|10LY                                             |Mil Mi-8MTV-1                           |
|10LZ                                             |Cessna 172RG                            |
|10M                                              |Britten-Norman BN-2A Trislander         |
|10MA                                             |Cessna 208B Caravan                     |
|10MB                                             |Fokker F-27 Friendship 500              |
|10MC                                             |Boeing B-737-2F9                        |
|10MD                                             |Antonov AN-32                           |
|10MG                                             |Bell 412 (helicopter)                   |
|100SD                                            |Sikorsky S-43                           |
|10MH                                             |Boeing 707-323C                         |
|10MJ                                             |Boeing B-737-2K9                        |
|10MK                                             |Tupolev TU-134B-3                       |
|10MM                                             |Tupolev TU-154B                         |
|10MN                                             |Beechcraft 1900D                        |
|10MQ                                             |Antonov AN-24B                          |
|10MR                                             |Lockheed L-188C Electra                 |
|10MS                                             |Boeing B-757-223                        |
|10MV                                             |Britten Norman BN-2A-21 Trislander      |
|10MW                                             |Mil Mi-8T (helicopter)                  |
|100SE                                            |Sikorsky S-43                           |
|10MX                                             |Antonov AN-32B                          |
|10MY                                             |Britten-Norman BN-2A-27 Islander        |
|10N                                              |Hawker Siddeley HS-748                  |
|10NA                                             |Mil Mi-17 (helicopter)                  |
|10NB                                             |Cessna 208 Caravan I                    |
|10NC                                             |McDonnell Douglas DC-8-55F              |
|10NF                                             |ConvairCV-440                           |
|10NG                                             |Boeing B-757-225                        |
|10NH                                             |Cessna 500 Citation                     |
|10NL                                             |NaN                                     |
|1001X                                            |Breguet 14                              |
|100SF                                            |Douglas DC-2                            |
|10NM                                             |GAF Nomad N-24A                         |
|10NN                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10NP                                             |Cessna 550 Citation                     |
|10NR                                             |Lockheed C-130H                         |
|10NS                                             |Antonov 12BP                            |
|10NT                                             |Boeing B-737-222                        |
|10NW                                             |Gates Learjet 25D                       |
|10NX                                             |Mil Mi-17                               |
|10NZ                                             |Cessna 402                              |
|10PB                                             |Cessna U206G                            |
|100SL                                            |Douglas DC-2                            |
|10PC                                             |Boeing B-737-T43                        |
|10PE                                             |Ilyushin IL-76TD                        |
|10PF                                             |Dornier 228-212                         |
|10PG                                             |Cessna 177B                             |
|10PJ                                             |Antonov AN-24                           |
|10PM                                             |de Havilland Canada DHC-3 Otter         |
|10PP                                             |de Havilland Canada DHC-6 Twin Otter 200|
|10PR                                             |Britten Norman BN-2A-20 Trislander      |
|10PS                                             |McDonnell Douglas DC-9-32               |
|10PW                                             |Britten-Norman BN-2A-26 Islander        |
|100SP                                            |Stinson SR-7 Reliant                    |
|10PX                                             |Ilyushin 76MD                           |
|10PZ                                             |Boeing 727-286                          |
|10Q                                              |Sikorsky S-70 / Sikorsky S-70           |
|10QB                                             |McDonnell Douglas DC-10-30              |
|10QG                                             |Harbin Yunshuji Y-12-II                 |
|10QH                                             |McDonnell Douglas MD-88                 |
|10QJ                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10QL                                             |Let 410                                 |
|10QT                                             |Lockheed C-130H                         |
|10QW                                             |Boeing B-747-131                        |
|100SQ                                            |Dewoitine D-338                         |
|10RA                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10RB                                             |Douglas DC-6A                           |
|10RF                                             |Fokker F-27 Friendship 600              |
|10RH                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10RJ                                             |Douglas DC-4                            |
|10RK                                             |Lockheed C-130H Hercules                |
|10RP                                             |de Havilland Canada DHC-3 Turbo Otter   |
|10RQ                                             |Ilyushin IL-76T                         |
|10RR                                             |Tupolev TU-154M                         |
|10RS                                             |Embraer EMB-110 Bandeirante             |
|100SR                                            |Short Empire Flying Boat                |
|10RT                                             |Cessna 206G                             |
|10RV                                             |Douglas DC-3C                           |
|10RX                                             |Boeing B-757-200                        |
|10RZ                                             |de Havilland Canada DHC-6 Twin Otter 200|
|10SB                                             |Antonov 12B                             |
|10SE                                             |Antonov An-124                          |
|10SG                                             |de Havilland DHC-2                      |
|10SH                                             |Piper PA-31-350 Navajo Chieftain        |
|10SL                                             |Boeing B-707-323C                       |
|10SM                                             |Yakovlev YAK-40                         |
|100SU                                            |Douglas DC-3                            |
|10SP                                             |Fokker 100                              |
|10SQ                                             |Embraer 110P1 Bandeirante               |
|10SS                                             |Cessna 421C Golden Eagle                |
|10ST                                             |Antonov AN-12B                          |
|10SU                                             |Boeing B-727-231                        |
|10SW                                             |Boeing B-747-168B / Ilyushin IL-76TD    |
|10SX                                             |Piper PA-31-350 Navajo                  |
|10SZ                                             |Antonov AN-2                            |
|10T                                              |Beechcraft 1900-C / Beech King Air A90  |
|10TA                                             |Lockheed HC-130P Hercules               |
|100SV                                            |Douglas DC-3                            |
|10TC                                             |Boeing B-767-200ER                      |
|10TD                                             |Cessna 208B Caravan I                   |
|10TF                                             |Ilyushin IL-76MD                        |
|10TG                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10TH                                             |CASA 212 Aviocar 100                    |
|10TJ                                             |Douglas C-47A                           |
|10TK                                             |Antonov AN-12                           |
|10TL                                             |Antonov An-32B                          |
|10TP                                             |McDonnell Douglas DC-8-63F              |
|10TR                                             |Hindustan Aeronautics 748-2             |
|100SW                                            |Heinkel He-111                          |
|10TS                                             |Learjet 35A                             |
|10TT                                             |Cessna 208B Grand Caravan               |
|10TU                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10TV                                             |Embraer 120RT Brasilia                  |
|10TX                                             |de Havilland Canada DHC-4A Caribou      |
|10TY                                             |Embraer 110P1A Bandeirante              |
|10U                                              |Hawker Siddeley HS-748-353 Srs.2a       |
|10UA                                             |CASA 212 Aviocar 200                    |
|10UD                                             |Sikorsky CH53D / Sikorsky CH53D         |
|10UH                                             |Boeing B-737-2C3                        |
|100SX                                            |Junkers JU-52/3m                        |
|10UJ                                             |IAI 1124 Westwind                       |
|10UK                                             |Cessna 208B Super Cargomaster           |
|10UL                                             |Cessna 500 Citation I                   |
|10UP                                             |Lockheed C-130HF                        |
|10UR                                             |Antonov AN-24RV                         |
|10US                                             |Lockheed C-130H Hercules                |
|10UX                                             |Aviation Traders ATL-98 Carvair         |
|10V                                              |Cessna 208B Caravan I                   |
|10VA                                             |Fokker F-27 Friendship 600              |
|10VB                                             |Yakovlev 40                             |
|100SY                                            |Junkers JU-52                           |
|10VC                                             |Lockheed C-130H Hercules                |
|10VE                                             |British Aerospace ATP                   |
|10VF                                             |Antonov AN-26                           |
|10VJ                                             |Boeing B-737-31B                        |
|10VN                                             |Vickers Viscount 781D                   |
|10VR                                             |Harbin Yunshuji Y-12 II                 |
|10VU                                             |Fokker F-27 Friendship 200              |
|10VW                                             |de Havilland DHC-2                      |
|10VX                                             |Mil Mi-17 (helicopter)                  |
|10VZ                                             |Fokker 100                              |
|1001Y                                            |De Havilland DH-4                       |
|100TA                                            |Short Empire Flying Boat                |
|10W                                              |Antonov AN-24                           |
|10WA                                             |Piper PA-32                             |
|10WB                                             |Fokker F-27 Friendship 600              |
|10WD                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10WE                                             |Learjet 31                              |
|10WG                                             |BAC One-Eleven 203AE                    |
|10WH                                             |Aerospatiale ATR-42-512                 |
|10WJ                                             |Boeing B-747-300                        |
|10WK                                             |McDonnell Douglas DC-8-61F              |
|10WL                                             |Dornier DO-228-212                      |
|100TB                                            |Potez 621                               |
|10WM                                             |Cessna 180K                             |
|10WN                                             |Cessna 210                              |
|10WP                                             |Cessna 550 Citation II                  |
|10WQ                                             |Pilatus PC-6 Turbo Porter / Cessna 206  |
|10WR                                             |Tupolev TU-134                          |
|10WT                                             |Dornier 228-212                         |
|10WU                                             |de Havilland Canada DHC-6 Twin Otter 300|
|10WX                                             |Tupolev TU-154M / C-141 Starlifter      |
|10WY                                             |Airbus A300-B4-200                      |
|10X                                              |Cessna 208B Caravan I                   |
|100TC                                            |Wibault 283-T12                         |
|10XA                                             |Beech Super King Air 200                |
|10XC                                             |McDonnell Douglas DC-9-32               |
|10XD                                             |Lockheed C-130H Hercules                |
|10XE                                             |Rutan Long EZ (experimental aircraft)   |
|10XG                                             |Yakovlev YAK-40                         |
|10XH                                             |Cessna 206 Seneca                       |
|10XJ                                             |Cessna 208B Caravan I                   |
|10XL                                             |Antonov AN-124-100                      |
|10XN                                             |Embraer 110P1 Bandeirante               |
|10XQ                                             |Swearingen SA-226T Metro II             |
|100TE                                            |Junkers JU-52/3m                        |
|10XR                                             |Tupolev TU-154                          |
|10XS                                             |Cessna 402C                             |
|10XT                                             |Yakovlev YAK-42                         |
|10XV                                             |Boeing B-737-300                        |
|10XX                                             |Lockheed C-130H Hercules                |
|10XZ                                             |Antonov An-72                           |
|10Y                                              |Boeing B-747-122                        |
|10YB                                             |Britten Norman BN-2A Trislander         |
|10YC                                             |Cessna 208B Caravan I                   |
|10YD                                             |Antonov AN-12BP                         |
|100TF                                            |Lockheed 14H Super Electra              |
|10YK                                             |Let 410UVP                              |
|10YM                                             |Fokker F-27 Friendship 600              |
|10YR                                             |McDonnell Douglas DC-9-32               |
|10YS                                             |Grummand EA-6B                          |
|10YT                                             |Antonov 12BP                            |
|10YU                                             |CASA 212-S1 Aviocar 100                 |
|10YV                                             |Antonov AN-32                           |
|10YW                                             |Airbus A300-622R                        |
|10YX                                             |Cessna 208B Caravan I Super Cargomaster |
|10YY                                             |Cessna 208B Caravan I Super Cargomaster |
|100TG                                            |Sikorsky S-42 (flying boat)             |
|10Z                                              |Boeing 707-336C                         |
|10ZB                                             |Saab340B                                |
|10ZE                                             |Boeing B-727-228                        |
|10ZF                                             |Airbus A.320-214                        |
|10ZG                                             |Antonov AN-32                           |
|10ZP                                             |Convair CV-240-53                       |
|10ZR                                             |Boeing B-727-230                        |
|10ZS                                             |Boeing B-737-282                        |
|10ZT                                             |Xian Yunshuji Y-7-100C                  |
|10ZV                                             |Yakovlev YAK-40                         |
|100TH                                            |Stinson Reliant                         |
|10ZW                                             |Bell 206L-3                             |
|11                                               |Harbin Yunshuji Y-12 II                 |
|110                                              |Swearingen SA-226TC Metroliner II       |
|1100                                             |Eurocopter AS-350-BA                    |
|11001                                            |Ilyushin 76MD                           |
|11002                                            |Rockwell Sabreliner 60                  |
|11003                                            |Ilyushin II-76                          |
|11004                                            |Shorts SC-7 Skyvan 3-100                |
|11005                                            |Consolidated PBY-5A Catalina            |
|11006                                            |Swearingen SA.227AC Metro III           |
|100TL                                            |Consolidated PBY-2 / Consolidated PBY-2 |
|11008                                            |Embraer 110 Bandeirante                 |
|1100B                                            |Dornier 228-201                         |
|1100C                                            |Dornier 328-110                         |
|1100D                                            |Beechcraft 1900D / Cessna 177           |
|1100G                                            |de Havilland Dash-2 Beaver              |
|1100H                                            |Antonov An-12BP                         |
|1100K                                            |Cessna 402C                             |
|1100P                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1100S                                            |Cessna 402C                             |
|1100T                                            |DC-3-65TP                               |
|100TM                                            |V6 (airship)                            |
|1100U                                            |Fokker F-27 Friendship 600              |
|1100X                                            |Tupolev TU-154M                         |
|1101                                             |Antonov AN-26                           |
|11011                                            |McDonnell Douglas MD-11                 |
|11016                                            |de Havilland Dash-2 float plane         |
|11018                                            |Lockheed C-130B Hercules                |
|11019                                            |Antonov 12B                             |
|1101A                                            |CASA 212-MP Aviocar 200                 |
|1101B                                            |Cessna 177B Cardinal                    |
|1101C                                            |British Aerospace BAe-146-100           |
|100TN                                            |Lioré-et-Olivier H-242                  |
|1101D                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1101E                                            |Antonov AN-24RV                         |
|1101F                                            |Douglas DC-3C                           |
|1101G                                            |Boeing B-727-30                         |
|1101J                                            |Yakovlev YAK-40                         |
|1101M                                            |Embraer 120RT Brasilia                  |
|1101N                                            |Britten-Norman BN-2A-3 Islander         |
|1101R                                            |Douglas DC-3C                           |
|1101V                                            |Antonov AN-12                           |
|1102                                             |Cessna 207 Skywagon                     |
|10020                                            |Junkers F-13                            |
|100TP                                            |Lockheed 10 Electra                     |
|11022                                            |Burgess RV-6 experimental               |
|11023                                            |Cessna 208B Caravan I Super Cargomaster |
|11025                                            |NaN                                     |
|11026                                            |Cessna 501 Citation I SP                |
|11028                                            |Britten-Norman Trislander               |
|11029                                            |Fokker F-27 Friendship 600              |
|1102A                                            |Airbus A-310-204                        |
|1102C                                            |Antonov AN-12BP                         |
|1102D                                            |Antonov 12                              |
|1102E                                            |Antonov 32B                             |
|100TS                                            |Junkers JU.52                           |
|1102F                                            |Lockheed Martin L-100-30 Hercules       |
|1102G                                            |Lockheed L-100-30 Hercules              |
|1102J                                            |Fokker F-27 Friendship 600              |
|1102L                                            |Boeing KC-135E                          |
|1102M                                            |Douglas DC-3C                           |
|1102N                                            |Britten Norman BN-2A-26                 |
|1102S                                            |Cessna 208 Caravan I                    |
|1102T                                            |Antonov AN-26                           |
|1102V                                            |Antonov AN-12                           |
|1102W                                            |Britten Norman BN-2A Trislander         |
|100TV                                            |Douglas DC-2-112                        |
|1102X                                            |Lockheed L-188A Electra                 |
|1102Y                                            |Beechcraft C99                          |
|1103                                             |Tupolev TU-154                          |
|11031                                            |Antonov AN-32 Transport                 |
|11033                                            |Douglas DC-3C (C-47A-DK)                |
|1103A                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1103C                                            |Learjet 24D                             |
|1103D                                            |Boeing 737-4Q8                          |
|1103E                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1103G                                            |McDonnell Douglas MD-11                 |
|100TW                                            |Potez 621                               |
|1103H                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1103L                                            |de Havilland Canada DHC-4A              |
|1103M                                            |Let 410UVP-E                            |
|1103Q                                            |McDonnell Douglas MD-82                 |
|1103S                                            |Antonov 32                              |
|1103T                                            |Britten-Norman BN-2A-21 Islander        |
|1103V                                            |Eurocopter AS-350BA                     |
|1103X                                            |Embraer 110P2 Bandeirante               |
|1103Y                                            |de Havilland Canada DHC-3 Otter         |
|11041                                            |Beechcraft 99                           |
|100TX                                            |De Havilland DH-60                      |
|11042                                            |Douglas DC-6A                           |
|11043                                            |Boeing 727-243F                         |
|11049                                            |Hawker Siddeley HS-125                  |
|1104A                                            |Piper PA-32-R301 Saratoga II HP         |
|1104B                                            |Cessna 208B Grand Caravan               |
|1104C                                            |Boeing B-747                            |
|1104D                                            |de Havilland Canada DHC-7-102           |
|1104E                                            |Embraer 110P1 Bandeirante               |
|1104F                                            |Beech King Air 65-A90                   |
|1104G                                            |Dornier 228-201                         |
|100TY                                            |Junkers JU-52                           |
|1104H                                            |Beechcraft 1900D                        |
|1104J                                            |McDonnell Douglas MD-11                 |
|1104K                                            |McDonnell Douglas MD-90-30              |
|1104M                                            |Yakovlev YAK-40                         |
|1104N                                            |Boeing B-737-204C                       |
|1104S                                            |Cessna 404 Titan II                     |
|1104T                                            |Cessna 404 Titan Ambassador             |
|1104X                                            |Piper PA-32-260                         |
|1104Z                                            |Hawker Siddeley HS-748-501 Super 2B     |
|11050                                            |Dassault Falcon 900B                    |
|100UD                                            |Lockheed Vega 5B                        |
|11052                                            |Embraer 110 Bandeirante                 |
|11053                                            |Lockheed C-130A Hercules                |
|11054                                            |Piper PA-31-350 Navajo Chieftain        |
|11055                                            |Bell 214ST helicopter                   |
|11056                                            |Learjet 35A                             |
|11059                                            |Arava 201                               |
|1105A                                            |Gates Learjet 35                        |
|1105B                                            |Boeing B-767-366ER                      |
|1105C                                            |Cessna U206F                            |
|1105D                                            |Shaanxi Yunshuji Y-8/Yunshuji Y-8       |
|100UJ                                            |Lockheed 10 Electra                     |
|1105F                                            |McDonnell Douglas DC-9-31               |
|1105H                                            |Aerospatiale Alenia ATR-42              |
|1105J                                            |Cessna 208 Caravan I                    |
|1105Q                                            |Ilyushin 114T                           |
|1105R                                            |Piper PA-31-350                         |
|1105S                                            |Cessna 207                              |
|1105V                                            |Let 410UVP                              |
|1105X                                            |Cessna 525 Citation                     |
|1105Z                                            |Piper PA-31-350                         |
|11061                                            |Lockheed C-130H                         |
|100UK                                            |Lockheed 14-H2 Super Electra            |
|11062                                            |British Aerospace APT                   |
|11063                                            |McDonnell Douglas DC-10-30              |
|11065                                            |Learjet 35A                             |
|11066                                            |Cessna 208B Caravan I                   |
|11067                                            |Boeing 747-2B5F                         |
|11068                                            |Airbus A300B2-101                       |
|1106A                                            |Yakovlev YAK-42D                        |
|1106D                                            |de Havilland Canada DHC-6 Twin Otter    |
|1106E                                            |Antonov 28                              |
|1106G                                            |Embraer 110P1A Bandeirante              |
|100UL                                            |Junkers JU-52/3m                        |
|1106L                                            |Saab 340B                               |
|1106M                                            |Shorts 360-300                          |
|1106P                                            |Let 410UVP-E                            |
|1106Q                                            |Beechcraft King Air C90                 |
|1106S                                            |AirbusA310-304                          |
|1106T                                            |Antonov AN-8                            |
|1106X                                            |GAF Nomad N-22C                         |
|1106Z                                            |McDonnell Douglas MD-83                 |
|1107                                             |Lockheed C-130 Hercules                 |
|11071                                            |Cessna U206G                            |
|10021                                            |Breguet 14                              |
|100UM                                            |Douglas DST-A-207A                      |
|11072                                            |McDonnell Douglas DC-8-71F              |
|11073                                            |Boeing B-737-3T5                        |
|11075                                            |Yakovlev YAK-40                         |
|11076                                            |Douglas C-47A-5-DK                      |
|11077                                            |de Havilland Canada DHC-6 Twin Otter 300|
|11078                                            |CASA 212-DE Aviocar 200                 |
|1107B                                            |Antonov AN-12 (freighter)               |
|1107C                                            |Antonov AN-32                           |
|1107E                                            |Cessna 208 Caravan                      |
|1107F                                            |Learjet 55                              |
|100UP                                            |Heinkel 116                             |
|1107G                                            |Boeing B-737-2H4                        |
|1107H                                            |Britten-Norman BN-2A-20 Islander        |
|1107K                                            |Learjet 35A                             |
|1107N                                            |Britten-Norman BN-2A-9 Islander         |
|1107P                                            |Rockwell Sabreliner 65                  |
|1107Q                                            |Beechcraft 1900C-1                      |
|1107R                                            |BAe Jetstream 3101-31                   |
|1107S                                            |Airbus A.330-301                        |
|1107T                                            |Shorts 330-200                          |
|1107U                                            |Piper PA-31-350 Navajo                  |
|100US                                            |Fairchild 51                            |
|1107V                                            |Fokker F-27 Friendship 600              |
|1107X                                            |Piper PA-31-350 Navajo                  |
|1107Z                                            |Beech Baron                             |
|11081                                            |Xian Yunshuji Y-7-100C                  |
|11082                                            |Kawasaki C-1A                           |
|11085                                            |British Aerospace  BAe Jetstream 32EP   |
|11086                                            |Curtiss C-46A-60-CS                     |
|11087                                            |de Havilland Canada DHC-6 Twin Otter 200|
|1108C                                            |Boeing B-737-2A8 Advanced               |
|1108D                                            |Grumman G-159 Gulfstream I              |
|100UT                                            |De Havilland DH-85                      |
|1108E                                            |Douglas C-47A-10-DK                     |
|1108F                                            |Aerospatiale AS355-F1                   |
|1108H                                            |Aerospatiale BAe Concorde 101           |
|1108J                                            |Lockheed C-130H Hercules                |
|1108M                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1108N                                            |Sikorsky S-76                           |
|1108P                                            |Casa 212-AB10 Aviocar                   |
|1108Q                                            |Piper Navajo PA-31/ Piper Seminole PA-44|
|1108S                                            |Antonov AN-26B                          |
|1108T                                            |Cessna 208 Caravan I                    |
|100UV                                            |Douglas DC-2                            |
|1108W                                            |Piper PA-31-350                         |
|1108X                                            |Airbus A320-212                         |
|11090                                            |Piper PA-31-350 Navajo Chieftain        |
|11092                                            |Cessna 208B Grand Caravan I             |
|11095                                            |Douglas C-47                            |
|11097                                            |Beechcraft SKA 200                      |
|11098                                            |Mil Mi-17                               |
|11099                                            |Piper PA-31-350 Navajo                  |
|1109A                                            |McDonnell Douglas DC-9-31               |
|1109B                                            |Cessna 206                              |
|100UW                                            |Lockheed 14 Super Electra               |
|1109D                                            |Shorts SC.7 Skyvan 3-100                |
|1109J                                            |Cessna 208B Caravan I Super Cargomaster |
|1109K                                            |Canadair CL-600-2B16 Challenger 604     |
|1109M                                            |Cessna 335                              |
|1109S                                            |Harbin Yunshuji Y-12-II                 |
|1109U                                            |Ilyushin IL-18D                         |
|1109W                                            |Boeing B-747-412                        |
|1109X                                            |Antonov AN-26                           |
|1109Y                                            |Antonov 32B                             |
|110A                                             |Swearingen SA.226TC Metro II            |
|100UX                                            |Savoia Marchetti S-66                   |
|110AC                                            |Antonov AN-26                           |
|110AF                                            |Airbus A300-600R                        |
|110AN                                            |Aerospatiale SN-601 Corvette            |
|110AP                                            |Beech A90 King Air                      |
|110AR                                            |Douglas C-47A-30-DK (DC-3C)             |
|110AS                                            |Douglas DC-3C (C47A-DL)                 |
|110AU                                            |Beech King Air 200 Catpass              |
|110AV                                            |Sud Aviation SE-210 Caravelle 10R       |
|110AX                                            |Swearingen SA.227AT Merlin IVC          |
|110AZ                                            |Learjet 35A                             |
|100V                                             |Lockheed 14H Super Electra              |
|110BA                                            |GAF Nomad N24A                          |
|110BB                                            |Shorts 360-100                          |
|110BD                                            |Beech BE-55                             |
|110BE                                            |Boeing B-737-4D7                        |
|110BH                                            |Short 360                               |
|110BJ                                            |Tupolev 154M                            |
|110BK                                            |Beechcraft 1900C                        |
|110BL                                            |de Havilland Canada DHC-6 Twin Otter    |
|110BM                                            |Fokker F-27 Friendship 500F             |
|110BS                                            |Grummand Gulfstream III                 |
|100VA                                            |Curtiss-Wright Hawk                     |
|110BT                                            |Cessna 501 Citation I/SP                |
|110BW                                            |Antonov AN-24                           |
|110BX                                            |Mil Mi-18 Helicopter                    |
|110BZ                                            |Cessna  208B Grand Caravan              |
|110CA                                            |CASA CN-235M-10                         |
|110CB                                            |Fokker F-27 Friendship 400M             |
|110CC                                            |Yakovlev YAK-40                         |
|110CD                                            |Antonov 12MGA                           |
|110CG                                            |Transall C-160NG                        |
|110CN                                            |Tupolev TU-154M                         |
|100VB                                            |Armstrong-Withworth Atlanta             |
|110CP                                            |Sikorsky S-76B helicopter               |
|110CR                                            |Antonov AN-28 PZL-MieleM-28 Sky Truck   |
|110CS                                            |Ilyushin IL-76                          |
|110CT                                            |Piper PA-32-300                         |
|110CW                                            |Dassault Falcon 20C                     |
|110CX                                            |Aerospatiale AS350 Eurocopter  helicoper|
|110DB                                            |Antonov 28                              |
|110DE                                            |Airbus A-330-243                        |
|110DG                                            |Learjet 25                              |
|110DH                                            |Cessna 402B                             |
|10025                                            |De Havilland DH-4                       |
|100VE                                            |Martin M-130 (flying boat)              |
|110DL                                            |CASA  CN-235-200                        |
|110DN                                            |Boeing B-757-222                        |
|110DP                                            |Boeing B-757-223                        |
|110DU                                            |Boeing 767-223ER                        |
|110DW                                            |Boeing B-767-222                        |
|110DX                                            |LET 410UVP                              |
|110E                                             |Fokker 100                              |
|110EA                                            |LET 410UVP-E                            |
|110EC                                            |Cessna 172N                             |
|110ED                                            |Tupolev Tu-154M                         |
|100VF                                            |Douglas DF-151                          |
|110EE                                            |MD-87 / Cessna 525A Citation II         |
|110EH                                            |de Havilland DHC-2 Mk 1 Beaver          |
|110EL                                            |Cessna 208 Caravan                      |
|110EP                                            |Swearingen SA-226AT Merlin IV           |
|110ET                                            |Swearingen SA.226TC Metro I             |
|110EV                                            |EMB 810C Seneca                         |
|110EX                                            |Bell 206L                               |
|110EZ                                            |Airbus A-300-605R                       |
|110F                                             |Ilyushin 18V                            |
|110FB                                            |Learjet 25B                             |
|100VG                                            |Ford Tri-motor                          |
|110FC                                            |Antonov AN-28                           |
|110FD                                            |BAE Avro RJ100                          |
|110FE                                            |Boeing 747-246F                         |
|110FL                                            |Cessna 208B Grand Caravan               |
|110FM                                            |Ilyushin IL- 76TD                       |
|110FP                                            |Cessna 208B Grand Caravan               |
|110FT                                            |Learjet 24D                             |
|110G                                             |Let 410A                                |
|110GC                                            |Let 410UVP-E                            |
|110GD                                            |Cessna 560 Citation V                   |
|100VK                                            |Savoia-Marchetti SM73                   |
|110GK                                            |Britten Norman BN-2B Trislander         |
|110GL                                            |Piper PA-31-250                         |
|110GM                                            |Canadair CL-604                         |
|110GS                                            |Lockheed Hercules KC-130R               |
|110GT                                            |Embraer EMB-120 Brasilia                |
|110GW                                            |de Havilland DHC-6 Twin Otter 300       |
|110HA                                            |Boeing B-737-3Q8                        |
|110HB                                            |Fairchild FH-227E                       |
|110HD                                            |Cessna 207 Skywagon                     |
|110HH                                            |Antonov AN-12                           |
|100VP                                            |Junkers JU-52/3m                        |
|110HL                                            |Boeing B-727-134                        |
|110HN                                            |Learjet C-21A                           |
|110HP                                            |Tupolev TU-154                          |
|110HQ                                            |Antonov 12BP                            |
|110HR                                            |Antonov AN-26                           |
|110HS                                            |MH-47 Chinook helicopter                |
|110JA                                            |Antonov 2TP                             |
|110JB                                            |Antonov AN-2                            |
|110JD                                            |Cessna 208B Caravan I Super Cargomaster |
|110JF                                            |Let 410UVP-E                            |
|100VS                                            |Lockheed 14 Electra                     |
|110JM                                            |Shrike Commander 500S                   |
|110JP                                            |Swearingen SA.227AC Metro III           |
|110JS                                            |Boeing B-767-200ER                      |
|110JW                                            |Cessna U206A                            |
|110JY                                            |Antonov AN-32A                          |
|110K                                             |Cessna 206G                             |
|110KB                                            |Mi-8 helicopter                         |
|110KH                                            |BAC One-Eleven 525FT                    |
|110KM                                            |Boeing B-737-566                        |
|110KT                                            |McDonnell Douglas MD-82                 |
|100VU                                            |Macchi C-94                             |
|110KW                                            |LET 410UVP                              |
|110LA                                            |Boeing B-747-209B                       |
|110LB                                            |de Havilland Canada DHC-6 Twin Otter 300|
|110LE                                            |Hawker Siddeley HS-748-372              |
|110LF                                            |Mi-17                                   |
|110LL                                            |Embraer 721C Sertanejo                  |
|110LM                                            |PA- 31-350 Chieftain                    |
|110LR                                            |Lockheed MC-130H Hercules               |
|110LS                                            |Tupolev TU-154M / Boeing B-757-23APF    |
|110LU                                            |Cessna 310                              |
|100VV                                            |Douglas DC-2                            |
|110LV                                            |Boeing B-707-123B                       |
|110LY                                            |de Havilland DHC-2                      |
|110M                                             |Britten-Norman BN-2A Islander           |
|110MA                                            |Sikorsky S-76A                          |
|110MC                                            |de Havilland Canada DHC-6 Twin Otter 300|
|110ME                                            |Sukhoi Su-27                            |
|110MF                                            |Iluyshin Il-86                          |
|110MK                                            |Lockheed MC-130H Hercules               |
|110MP                                            |Yunshuji Y-8D                           |
|110MR                                            |Mil Mi-26                               |
|100VY                                            |De Havilland DH-84                      |
|110MS                                            |de Havilland Canada DHC-6-300 Twin Otter|
|110MV                                            |Antonov AN-28                           |
|110MW                                            |Learjet 25C                             |
|110MX                                            |Embraer 120ER Brasilia                  |
|110N                                             |Cessna 650 Citation VI                  |
|110NB                                            |PA-34-220T Seneca III                   |
|110NJ                                            |Cessna U206G                            |
|110NP                                            |ATR 42-300                              |
|110NS                                            |de Havilland Canada DHC-3 Otter         |
|110NW                                            |Ilyushin IL-38 / Ilyushin IL-38         |
|100WA                                            |Dornier DO.18                           |
|110NX                                            |Learjet 60                              |
|110P                                             |Cessna 208B Cargomaster I               |
|110PA                                            |Beechcraft King Air A100                |
|110PD                                            |Fokker 50                               |
|110PE                                            |Britten-Norman BN-2A-21                 |
|110PF                                            |IAI 1124A Westwind                      |
|110PK                                            |Fokker F27 Friendship 100               |
|110PL                                            |Let 410UVP-E20                          |
|110PM                                            |Beechcraft 1900C                        |
|110PR                                            |Britten-Norman BN-2A-26 Islander        |
|10026                                            |NaN                                     |
|100WB                                            |Junkers JU-52/3m                        |
|110PS                                            |UH-60 Black Hawk / UH-60 Black Hawk     |
|110PT                                            |Cessna 208B Caravan I Super Cargomaster |
|110PZ                                            |Aérospatiale/Aeritalia ATR-72-202       |
|110Q                                             |Antonov AN-140                          |
|110QS                                            |Cessna 208B Caravan I                   |
|110R                                             |Embraer-110 C-95B Bandeirante           |
|110RD                                            |Let 410UVP                              |
|110RG                                            |BAe Avro RJ-100                         |
|110RH                                            |Beech BE-1900D                          |
|110RJ                                            |Fokker 28 Fellowship 1000               |
|100WD                                            |Savbia-Marchetti  S-73P                 |
|110RK                                            |Antonov 24B                             |
|110RL                                            |Grumman G-159 Gulfstream I              |
|110RM                                            |Ilyushin II-76TD                        |
|110RR                                            |Antonov 12BP                            |
|110RV                                            |Antonov AN-28                           |
|110S                                             |Cessna 421                              |
|110SB                                            |Ilyushin Il-76MD                        |
|110SC                                            |Fokker F-27 Friendship 200              |
|110SD                                            |Let L-410UVP                            |
|110SG                                            |Boeing B-737-2T4                        |
|100WE                                            |Douglas DC-2-112                        |
|110SJ                                            |de Havilland Canada DHC-6 Twin Otter    |
|110SL                                            |Beech A36                               |
|110SM                                            |Illyushin 76                            |
|110SN                                            |Yakovlev 42D                            |
|110SP                                            |Cessna 185                              |
|110SQ                                            |Gates Learjet 45                        |
|110SR                                            |EMB 721C Sertanejo                      |
|110SS                                            |Piper PA-31-350 Navajo Chieftain        |
|110ST                                            |Embraer 820C Navajo                     |
|110SU                                            |McDonnell Douglas 369D                  |
|100WG                                            |Lockheed 14 Electra                     |
|110SW                                            |Canadair CRJ-100ER                      |
|110SX                                            |Lockheed C-130 Hercules                 |
|110SY                                            |Cessna 180H                             |
|110T                                             |Cessna 208B Grand Caravan               |
|110TA                                            |Lockheed C-130H Hercules                |
|110TB                                            |Mitsubishi MU 2B 35                     |
|110TC                                            |Sikorsky  S 76 A                        |
|110TE                                            |Boeing 737-2J8C                         |
|110TF                                            |Cessna 402C                             |
|110TH                                            |Let 410UVP-E                            |
|100WH                                            |de Havilland DH-86                      |
|110TJ                                            |Swearingen SA-226T Metro II             |
|110TK                                            |Bell 206B                               |
|110TL                                            |Gates Learjet 35A                       |
|110TN                                            |Cessna 208B Grand Caravan               |
|110TP                                            |Mi-8 helicopter                         |
|110TS                                            |Let 420UVP-E                            |
|110TT                                            |Beechcraft 1900D                        |
|110TU                                            |Cessna 208B Grand Caravan               |
|110TX                                            |Learjet 25B                             |
|110U                                             |Lockheed C-130A Hercules                |
|100WL                                            |Douglas DC-3                            |
|110UA                                            |Aerospatiale AS350BA                    |
|110UH                                            |Piper PA31-310                          |
|110UL                                            |EMB 721C Sertanejo                      |
|110US                                            |Convair CV-580F                         |
|110UU                                            |Antonov AN-2TP                          |
|110UV                                            |Fairchild Hiller FH-227B                |
|110UW                                            |Hawker 800A                             |
|110V                                             |Cessna 208B Caravan I Super Cargomaster |
|110VC                                            |CH-47 Chinook                           |
|110VE                                            |Shorts SC-7 Skyvan 3M Variant 100       |
|100WN                                            |Lockheed 14 Electra                     |
|110VP                                            |Robertson R44 helicopter                |
|110VT                                            |Swearingen SA227AT Merlin IVC           |
|110VU                                            |Antonov AN-26                           |
|110VV                                            |de Havilland DHC-3 Otter                |
|110W                                             |Douglas DC-9-15F                        |
|110WA                                            |Gates Learjet 24B                       |
|110WB                                            |Boeing B-727-223                        |
|110WD                                            |Boeing B-737-3Q8                        |
|110WE                                            |Yakovlev YAK-40                         |
|110WF                                            |Cessna 208B Grand Caravan               |
|100WP                                            |Junkers JU90V2                          |
|110WG                                            |Beechcraft 1900D                        |
|110WH                                            |Beechcraft Super King Air 200           |
|110WK                                            |Fokker F-50                             |
|110WM                                            |Cessna Citation 500                     |
|110WP                                            |Cessna 172G                             |
|110WR                                            |Ilyushin II-76                          |
|110WS                                            |Cessna UC-35D Citation Encore           |
|110WT                                            |Convair CV-440                          |
|110WW                                            |Beechcraft 1900C                        |
|110WY                                            |Piper PA-32-300                         |
|100WR                                            |Short Empire Flying Boat                |
|110X                                             |Bell 407                                |
|110XP                                            |Rockwell Gulfstream Jetprop 840         |
|110XX                                            |Cessna 208 Grand Caravan I              |
|110XZ                                            |Swearingen SA227AC Metro III            |
|110Y                                             |Let 410UVP                              |
|110YA                                            |Antonov AN-12                           |
|110YD                                            |Embraer 120ER Brasilia                  |
|110YK                                            |PZL-MieleAN-2R                          |
|110YX                                            |Ilyushin II-76TD                        |
|110Z                                             |Let 410UVP                              |
|100WS                                            |Douglas DC 3-A-SB-3-G-14                |
|110ZX                                            |de Havilland DHC-6 Twin Otter 300       |
|111                                              |BAe HS-748-232 Srs 2A                   |
|11102                                            |EMB 820C Navajo                         |
|11103                                            |Mi-8MTV-1                               |
|11104                                            |IAI 1124 Westwind                       |
|11105                                            |Piper PA-31-350 Navajo Chieftain        |
|11106                                            |Sikorsky S 76                           |
|11107                                            |de Havilland DHC-6 Twin Otter 300       |
|11109                                            |Convair CV-580                          |
|1110A                                            |Beechcraft 99                           |
|10007                                            |Zeppelin L-8 (airship)                  |
|10027                                            |De Havilland DH-4                       |
|100WT                                            |Nakajima DC-2                           |
|1110C                                            |Cessna 208B Grand Caravan               |
|1110E                                            |Shorts 360                              |
|1110F                                            |Tupolev 154B-2                          |
|1110J                                            |Tupolev 134A-3                          |
|1110K                                            |de Havilland DHC-3 Otter                |
|1110M                                            |Rockwell CT-39A Sabreliner              |
|1110P                                            |CH-47D Chinook                          |
|1110Q                                            |Pilatus-Britten Norman BN-2A-27 Islander|
|1110R                                            |Antonov AN-12                           |
|1110T                                            |Grumman Gulfstream G3                   |
|100WW                                            |Lockheed 14-WF62 Super Electra          |
|1110W                                            |CASA 212-CC                             |
|1111                                             |Canadair CRJ200LR RegionalJet           |
|11110                                            |Boeing 747-244B-SF                      |
|11111                                            |Douglas DC-3C                           |
|11113                                            |Pilatus Britten-Norman BN-2A-21 Islander|
|11114                                            |Bae Jetstream 3201                      |
|11118                                            |Beech 200 Super King Air                |
|11119                                            |Learjet 35A                             |
|1111A                                            |BAe 3101 Jetstream 31                   |
|1111B                                            |Bambardier CRJ200                       |
|100WX                                            |Short S23 ‘C’ Class flying boat         |
|1111E                                            |Canadair CL-601-2A12 Challenger         |
|1111G                                            |McDonnell-Douglas MD-82                 |
|1111J                                            |HBB HFB-320 Hansa Jet                   |
|1111M                                            |Cesna 208 Caravan                       |
|1111S                                            |Cessna TU206G                           |
|1111T                                            |PZL-MieleM28                            |
|1111Y                                            |Embraer EMB-110 Bandeirante             |
|1111Z                                            |Ilyushin II-76TD                        |
|11121                                            |Black Hawk helicopter                   |
|11124                                            |Antonov AN-2                            |
|100WY                                            |Douglas DC-2-115B                       |
|11125                                            |Embraer EMB-110 Bandeirante             |
|11126                                            |CH53E Sea Stallion                      |
|11127                                            |Let 410UVP-E4                           |
|1112A                                            |Lockheed Hercules C.1                   |
|1112B                                            |Boeing B-737-200                        |
|1112D                                            |Ilyushin 76TD                           |
|1112E                                            |Cessna P210N                            |
|1112G                                            |Cessna 560 Citation V                   |
|1112J                                            |de Havilland DHC-6 Twin Otter 300       |
|1112K                                            |CASA 212 Aviocar                        |
|100XH                                            |Lockheed 14-H Super Electra             |
|1112L                                            |Cessna 500 Citation I                   |
|1112M                                            |Pilatus-Britten Norman BN-2B-26 Islander|
|1112Q                                            |Antonov 24                              |
|1112T                                            |Ilyushin IL-76TD                        |
|1112U                                            |Let-410UVP-E                            |
|1112X                                            |Lockheed Hercules MC-130H               |
|11131                                            |de Havilland Canada DHC-6 Twin Otter 100|
|11132                                            |Boeing B-707-3J9C                       |
|11133                                            |Let 410UVP                              |
|11135                                            |Swearingen SA227AC Metro III            |
|100XK                                            |Junkers JU-52/3m                        |
|11137                                            |Antonov AN-26                           |
|11138                                            |Swearingen SA-227AC Metro III           |
|11139                                            |Beech 65-A80 Queenaire                  |
|1113A                                            |Yunshuji Y-12                           |
|1113B                                            |Antonov AN-12BP                         |
|1113C                                            |Antonov AN-24B                          |
|1113G                                            |Antonov AN-24B                          |
|1113M                                            |Airbus A-340                            |
|1113N                                            |ATR-72-202                              |
|1113R                                            |Sikorsky S-76C                          |
|100XL                                            |Lockheed 14 Electra                     |
|1113S                                            |Boeing 737-31S                          |
|1113T                                            |McDonnell Douglas MD-82                 |
|1113U                                            |Boeing B-737-244                        |
|1113V                                            |Antonov 26B                             |
|1113W                                            |Boeing 737-230                          |
|1113X                                            |Antonov AN-26A                          |
|1114                                             |Cessna 525 CitationJet I                |
|11140                                            |Cessna 207 Skywagon                     |
|11141                                            |Aerospatiale AS-350BA                   |
|11142                                            |Antonov 12V                             |
|100XN                                            |Short S-23 (flying boat)                |
|11144                                            |Cessna 208B                             |
|11145                                            |Boeing B-737-2L9                        |
|11146                                            |Cessna 208B Grand Caravan I             |
|11147                                            |Lockheed C-130B Hercules                |
|1114A                                            |Boeing B-737-7H4                        |
|1114B                                            |McDonnell DC-9-32                       |
|1114C                                            |Grumman G73T Turbo Mallard              |
|1114E                                            |Antonov AN-140-100                      |
|1114F                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1114H                                            |Gates Learjet 35A                       |
|100XP                                            |Junkers JU-52/3m                        |
|1114J                                            |British Aerospace BAe-125-700A          |
|1114K                                            |Antonov 12                              |
|1114L                                            |Dassault Falcon 20                      |
|1114N                                            |Antonov AN-24V                          |
|1114P                                            |Cessna 208B Grand Caravan               |
|1114R                                            |Shorts 360-100 /Shorts 360-300          |
|1114T                                            |Swearingen SA.226TC Metro II            |
|1114V                                            |Cessna 421C Golden Eagle III            |
|1114X                                            |Learjet 35A                             |
|1114Y                                            |Beechcraft C99                          |
|100XR                                            |Junkers JU-52                           |
|1114Z                                            |Cessna 208B Grand Caravan               |
|1115                                             |Let L410UVP-E20                         |
|11150                                            |Harbin Yunshuji Y-12-II                 |
|11151                                            |Antonov 74TK-200                        |
|11153                                            |NaN                                     |
|11155                                            |Antonov AN-32B                          |
|11156                                            |Cessna 208B Grand Caravan               |
|11157                                            |Airbus A320-211                         |
|11159                                            |Convair CV-580                          |
|1115B                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1002C                                            |De Havilland DH-4                       |
|100XS                                            |Junkers JU-86                           |
|1115E                                            |Learjet 35A                             |
|1115F                                            |KJ-2000                                 |
|1115H                                            |Cessna TU206G                           |
|1115M                                            |Lockheed C-130 Hercules                 |
|1115S                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1115T                                            |Cessna 208B Grand Caravan               |
|1115U                                            |de Havilland DHC-2 Beaver               |
|1115Y                                            |Antonov AN-12B                          |
|1115Z                                            |Airbus A-310-324ET                      |
|1116                                             |Fokker F-27 Friendship 200              |
|100XT                                            |Boeing 307 Stratoliner                  |
|11161                                            |Antonov AN-28                           |
|11162                                            |Boeing 727-23F                          |
|11164                                            |Embraer 110 Bandeirante                 |
|11165                                            |Lockheed L-100-30 Hercules              |
|11168                                            |Tupolev Tu-154M                         |
|11169                                            |Canadair CRJ-200ER                      |
|1116A                                            |Tupolev Tu-154M                         |
|1116B                                            |British Aerospace Nimrod MR-2           |
|1116D                                            |Mi-8 helicopter                         |
|1116E                                            |Dornier 228                             |
|100XV                                            |Douglas DC-2-115H                       |
|1116G                                            |Boeing B-737-8EH /EMB-135JB             |
|1116L                                            |BAe 146-200                             |
|1116P                                            |Antonov An-2                            |
|1116R                                            |Boeing 737-2B7                          |
|1116S                                            |Antonov 74T-200                         |
|1116T                                            |Bell 412                                |
|1116W                                            |Piper PA-32-301 Cherokee                |
|1116Z                                            |Cessna 310R                             |
|1117                                             |Boeing B-737-4Q8                        |
|11170                                            |Piper PA-31-310                         |
|100XW                                            |de Havilland DH-84 Dragon               |
|11171                                            |Antonov 26B-100                         |
|11172                                            |Learjet 24F                             |
|11173                                            |Cessna Citation 525                     |
|11176                                            |Sikorsky UH-60L Black Hawk              |
|11177                                            |Fokker 100                              |
|11178                                            |Beechcraft Super King Air B200          |
|11179                                            |Beechcraft Super King Air B200          |
|1117A                                            |Boeing B-737-497                        |
|1117B                                            |Aerospatiale AS350BA Rotocraft          |
|1117C                                            |MDonnell Douglas 369FF Rotocraft        |
|100XX                                            |Douglas DC-2-112                        |
|1117D                                            |Rockwell 500S Shrike Commander          |
|1117E                                            |Tupelov 134AK                           |
|1117F                                            |Ilushin Il-76TD                         |
|1117G                                            |Pilatus Britten Norman BN-2A-27 Islander|
|1117H                                            |Mi 8                                    |
|1117P                                            |Boeing B-737-8AL                        |
|1117T                                            |de Havilland Canada DHC-6 Twin Otter    |
|1117U                                            |Let 410UVP                              |
|1117W                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1117X                                            |Mi-8                                    |
|100Y                                             |Caudron C.635 Simoun                    |
|11181                                            |Cessna 550 Citation II                  |
|11182                                            |Mi-8                                    |
|11183                                            |Cessna 206                              |
|11184                                            |Let 410UVP                              |
|11185                                            |Antonov AN-24V                          |
|11186                                            |Boeing 737-2M2                          |
|11187                                            |North American CT-39A Sabreline         |
|11189                                            |Cessna 208B Grand Caravan               |
|1118A                                            |de Havilland DHC-6 Twim Otter 100       |
|1118B                                            |Airbus A-320-233                        |
|100YA                                            |Short Empire Flying Boat                |
|1118M                                            |Antonov AN-26V                          |
|1118N                                            |de Havilland DHC-2 MK.1 Beaver          |
|1118P                                            |Antonov AN-12BP                         |
|1118Q                                            |Beechcraft King Air E-90                |
|1118S                                            |de Havilland Canada DHC-6 Twin Otter 300|
|1118T                                            |de Havilland Canada DHC-2 Beaver        |
|1118V                                            |UH-60 Blackhawk helilcopter             |
|1118X                                            |Embraer EMB-110P1 Bandeirant            |
|1118Z                                            |Antonov AN-32                           |
|1119                                             |Antonov AN-12BP                         |
|100YB                                            |Dewoitine D-338                         |
|11190                                            |Mi-17 Helicopter                        |
|11191                                            |McDonnell Douglas MD-82                 |
|11192                                            |Let 410                                 |
|11193                                            |Antonov AN-26                           |
|11194                                            |Beechcraft King Air C90A                |
|11196                                            |Cessna 208 Caravan                      |
|11199                                            |Let 410 UVP-E10A                        |
|1119A                                            |Learjet 35A                             |
|1119C                                            |Antonov 12                              |
|1119D                                            |McDonnell Douglas MD-83                 |
|100YC                                            |Curtiss-Wright C-14 Osprey              |
|1119E                                            |Eurocopter Deutschland BK117C1          |
|1119K                                            |Cessna 208B Caravan I Super Cargomaster |
|1119Q                                            |Beechcraft King Air C90B                |
|1119R                                            |Let 410 UVP-E3                          |
|1119T                                            |Piper PA-31-350 Navajo                  |
|1119V                                            |Beechcraft 1900C-1                      |
|1119Y                                            |Boeing 777-236ER                        |
|111A                                             |Beechcraft King Air B200                |
|111AA                                            |CASA C-295M                             |
|111AC                                            |CASA NC-212-200                         |
|100YN                                            |Koolhoven FK.43                         |
|111AD                                            |ATR-42-300                              |
|111AE                                            |Eurocopter  AS332L2 Super Puma          |
|111AF                                            |Mi-17                                   |
|111AH                                            |Beechcraft 1900D                        |
|111AJ                                            |Antonov An-28                           |
|111AL                                            |Swearingen SA227AC Metroliner III       |
|111AM                                            |Antonov An-32                           |
|111AR                                            |McDonnell Douglas DC-9-51               |
|111AS                                            |Antonov An-32B                          |
|111AT                                            |Mil Mi-8T                               |
|1002E                                            |NaN                                     |
|100YP                                            |Junkers JU86 Z-2                        |
|111AW                                            |Beechcraft 1900C                        |
|111AX                                            |de Havilland Canada DHC-2 Mark I Beaver |
|111AZ                                            |Beechcraft 1900C                        |
|111B                                             |Eurocopter AS350D Astar                 |
|111BA                                            |Antonov An-12                           |
|111BB                                            |Bell UN-1N Huey                         |
|111BD                                            |Airbus A-320-233                        |
|111BE                                            |Cessna 208 Grand Caravan                |
|111BF                                            |Bell 407                                |
|111BG                                            |Airbus A-310-324                        |
|100YS                                            |Junkers JU-52/3m                        |
|111BK                                            |de Havilland Canada DHC-6 Twin Otter 100|
|111BL                                            |Bell UH-1N                              |
|111BN                                            |CASA NC-212                             |
|111BT                                            |Antonov 12BK                            |
|111BW                                            |Bell 407 / Bell 407                     |
|111BX                                            |Ilysushin Il-76TD                       |
|111BZ                                            |Douglas DC9-15F                         |
|111C                                             |Boeing B-747-209BSF                     |
|111CA                                            |Beechcraft 99A                          |
|111CC                                            |British Aerospace BAe-125-800A          |
|100YW                                            |Sikorsky S43 (flying boat)              |
|111CD                                            |Grumman G-21A Goose                     |
|111CF                                            |Sikorsky S-61N                          |
|111CG                                            |Bell Huey UH-1H                         |
|111CJ                                            |Fokker F-27 Friendship 500              |
|111CK                                            |McDonnell Douglas MD-82                 |
|111CP                                            |Cessna 208B Grand Caravan               |
|111CQ                                            |Boeing B-737-219                        |
|111CR                                            |Boeing B-737-291                        |
|111CS                                            |Beechcraft 1900C-1                      |
|111CT                                            |Convair CV-580                          |
|100YY                                            |Lockheed 10 Electra                     |
|111CU                                            |Bell 212                                |
|111CV                                            |Boeing B-737-505                        |
|111CW                                            |Learjet 60                              |
|111CX                                            |Aerospatiale SA365N-1 Dauphin II        |
|111CY                                            |de Havilland Canada DHC-6 Twin Otter 300|
|111D                                             |Bell 222                                |
|111DA                                            |Learjet 45                              |
|111DB                                            |Cessna 206                              |
|111DC                                            |Antonov An-12                           |
|111DD                                            |Grumman G-21A Goose                     |
|100YZ                                            |De Havilland D-84                       |
|111DE                                            |Airbus A320-232                         |
|111DF                                            |Rockwell International 690B             |
|111DG                                            |Bell 206-L4 Jet Ranger III              |
|111DH                                            |Britten Norman BN-2A Trislander Mk3     |
|111DJ                                            |Sikorsky S-76C                          |
|111DL                                            |Airbus A320-214                         |
|111DM                                            |Bandeirante EMB-110P1                   |
|111DP                                            |Cessna 650 Citation III                 |
|111DQ                                            |Bombardier DHC-8-402 Q400               |
|111DR                                            |Bell UH-1H                              |
|100ZA                                            |Junkers JU-52/3m                        |
|111DS                                            |Antonov 12V                             |
|111DT                                            |Boeing 737-8F2                          |
|111DU                                            |Ilyushin Il-76T                         |
|111DV                                            |Sikorsky S-92A                          |
|111DW                                            |Pilatus PC-12/45                        |
|111DX                                            |McDonnell Douglas MD-11                 |
|111DY                                            |Eurocopter AS 332L2 Super Puma 2        |
|111E                                             |Fokker F-27 Friendship 400M             |
|111EB                                            |British Aerospace BAe-146-300           |
|111EC                                            |Pilatus PC-6                            |
|100ZP                                            |Douglas DC-3                            |
|111EE                                            |Cessna 208B Grand Caravan               |
|111EH                                            |Boeing B-737-200                        |
|111EJ                                            |Mi-35                                   |
|111EM                                            |Lockheed C-130 Hercules                 |
|111EN                                            |Antonov An-26                           |
|111EP                                            |Airbus A330-203                         |
|111ET                                            |Britten-Norman BN-2A-27 Islander        |
|111EU                                            |Antonov An-32                           |
|100ZT                                            |Airspeed Oxford                         |
|100ZU                                            |Junkers JU-52                           |
|100ZW                                            |Lockheed 14 Super Electra               |
|1002G                                            |De Havilland DH-4                       |
|100ZX                                            |Savoia-Marchetti SM83                   |
|100ZY                                            |Lockheed 14 Super Electra               |
|100ZZ                                            |Handley Page HP-42                      |
|101                                              |Lockheed 14 Super Electra               |
|10100                                            |Douglas DC-3                            |
|10101                                            |Junkers JU-52/3mge                      |
|10105                                            |Dewoitine D-338                         |
|1010A                                            |Dewoitine D-338                         |
|1010D                                            |Lockheed Hudson A16-97                  |
|1010E                                            |Douglas DC-3                            |
|1002H                                            |Breguet 14                              |
|1010F                                            |Douglas DC-3                            |
|1010G                                            |Douglas DC-2                            |
|1010H                                            |Douglas DC-3                            |
|1010L                                            |Douglas DC-3                            |
|1010M                                            |Junkers JU-90                           |
|1010N                                            |NaN                                     |
|1010Q                                            |Farman F-224                            |
|1010R                                            |Douglas DC-3A                           |
|1010V                                            |Savoia-Marchetti SM-75                  |
|1010W                                            |Junkers JU-52/3m                        |
|1002M                                            |Royal Airship Works ZR-2 (airship)      |
|1010X                                            |Ford 5-AT Tri-Motor                     |
|1010Y                                            |Douglas DC-3-3                          |
|1010Z                                            |Lockheed 14-H2 Super Electra            |
|1011                                             |Douglas DC-3                            |
|10111                                            |Junkers JU-52/3m                        |
|10113                                            |Lockheed 18 Lodestar                    |
|10114                                            |Douglas DC-3                            |
|10115                                            |Mitsubishi MC-20                        |
|10116                                            |Consolidated LB-30A Liberator           |
|10117                                            |Consolidated LB-30A Liberator           |
|1002N                                            |Potez IX                                |
|1011A                                            |Lockheed 18 LodeStar                    |
|1011E                                            |Bloch 220                               |
|1011F                                            |Consolidated 32-2 Liberator I           |
|1011H                                            |Sikorsky S-42B (flying boat)            |
|1011J                                            |Junkers JU-53/3m                        |
|1011K                                            |Douglas DC-3                            |
|1011L                                            |Douglas DC-3                            |
|1011M                                            |NaN                                     |
|1011N                                            |Douglas DC-3                            |
|1011R                                            |Lockheed Hudson                         |
|1002Q                                            |Bristol 28 Tourer                       |
|1011S                                            |Douglas DC-3                            |
|1011T                                            |Grumman G-21 Goose                      |
|1011U                                            |Short S-23 (flying boat)                |
|1011V                                            |Douglas DC-2                            |
|1011W                                            |Consolidated Liberator                  |
|1011Z                                            |deHavilland DH-86                       |
|1012                                             |Short S-23 (flying boat)                |
|10120                                            |Consolidated B-24 Liberator             |
|10122                                            |Douglas DC-3                            |
|10123                                            |Douglas DC-3                            |
|1002S                                            |Handley Page O/10                       |
|10124                                            |Douglas DC-2-221                        |
|10125                                            |Lockheed 14 Electra                     |
|10126                                            |Douglas DST-A-207A                      |
|10127                                            |Douglas DC-3-A-269                      |
|10129                                            |Douglas C-49E                           |
|1012A                                            |Lockheed Hudson                         |
|1012B                                            |Lockheed Hudson                         |
|1012C                                            |Liore et Olivier H-246 Air Boat         |
|1012G                                            |Siebel Si-204                           |
|1012H                                            |Lockheed 14 Electra                     |
|1002U                                            |Dirigible Roma (airship)                |
|1012J                                            |Short Sunderland                        |
|1012M                                            |Short Sunderland (flying boat)          |
|1012P                                            |Dewoitine D-342                         |
|1012T                                            |Douglas C-47                            |
|1012X                                            |Douglas C-39-DO  (DC-2)                 |
|1012Y                                            |Sirkorsky 44A (flying boat)             |
|1012Z                                            |Junkers JU-52/3m                        |
|1013                                             |Douglas DC-3 / Boeing B-34              |
|10130                                            |Handley Page HP-57 Halifax              |
|10131                                            |Douglas DC-3A                           |
|10009                                            |Zeppelin L-10 (airship)                 |
|1002Z                                            |de Havilland DH-18 / Farman F-60 Goliath|
|10133                                            |Junkers JU-52/3m                        |
|10134                                            |Short S-26 (flying boat)                |
|10136                                            |Douglas C-54A                           |
|1013A                                            |Consolidated C-87                       |
|1013B                                            |Martin M-130 (flying boat)              |
|1013D                                            |Douglas DC-3A                           |
|1013E                                            |Consolidated 32-3 Liberator II          |
|1013F                                            |Boeing XB-29                            |
|1013H                                            |Boeing B-314 (flying boat)              |
|1013J                                            |Douglas C-53                            |
|10031                                            |NaN                                     |
|1013K                                            |Douglas C-53                            |
|1013L                                            |Douglas C-47-DL                         |
|1013Q                                            |Short S-23                              |
|1013S                                            |Douglas DC-3                            |
|1013U                                            |Douglas C-47A-DL                        |
|1013X                                            |B-17C Flying Fortress                   |
|1013Y                                            |Lockheed Hudson VI                      |
|10140                                            |Lockheed Hudson VI                      |
|10141                                            |Consolidated Liberator B24 C            |
|10142                                            |Short Sunderland 3 (flying boat)        |
|10032                                            |Vickers Viking                          |
|10143                                            |Douglas DC-3                            |
|10144                                            |Consolidated B-24                       |
|10145                                            |Douglas C-47-DL                         |
|10146                                            |Douglas C-53                            |
|10147                                            |Junkers JU-52/3m                        |
|10148                                            |Boeing B-17F / Boeing B-17F             |
|10149                                            |Douglas C-53D-DO                        |
|1014A                                            |Douglas C-53                            |
|1014C                                            |Douglas DC3-G102                        |
|1014E                                            |Consolidated B-24                       |
|10033                                            |De Havilland DH-4                       |
|1014F                                            |Douglas DC-3                            |
|1014G                                            |Douglas C-47-DL                         |
|1014L                                            |NaN                                     |
|1014M                                            |Douglas C-53                            |
|1014N                                            |Douglas C-47                            |
|1014P                                            |Lockheed L-18-56 Lodestar               |
|1014Q                                            |Douglas C-47                            |
|1014S                                            |Douglas C-47A-60-DL                     |
|1014U                                            |Consolidated B-24 / Consolidated B-24   |
|1014W                                            |Junkers JU-52/3m                        |
|10034                                            |Bleriot Spad 27                         |
|1014Y                                            |Douglas DC-3                            |
|1014Z                                            |Douglas C-47                            |
|10150                                            |Junkers JU-52/3m                        |
|10152                                            |Consolidated B-24 Liberator             |
|10155                                            |Pilgrim 100B                            |
|10156                                            |Junkers JU-52/3m                        |
|10157                                            |Douglas DC-3                            |
|10158                                            |Consolidated Liberator                  |
|1015A                                            |Douglas C-47                            |
|1015C                                            |Douglas DC-3                            |
|10036                                            |Breguet 14                              |
|1015D                                            |Douglas C-47A-DL                        |
|1015F                                            |Douglas C-47A                           |
|1015K                                            |Douglas C-47A                           |
|1015L                                            |Douglas C-47                            |
|1015M                                            |Douglas C-47                            |
|1015Q                                            |Lockheed 10C Electra                    |
|1015S                                            |Douglas C-54A-DO (DC-4)                 |
|1015T                                            |Douglas C-47A-DK                        |
|1015V                                            |Consolidated Catalina PB2Y-3R           |
|1015W                                            |Douglas C-47A-DL                        |
|10037                                            |De Havilland DH-4                       |
|1015Z                                            |Sikorsky S-42 (flying boat)             |
|1016                                             |Consolidated PB4Y-1                     |
|10162                                            |Consolidated B-24H                      |
|10165                                            |Douglas C-54A-DC (DC-4)                 |
|10167                                            |Lockheed 18 Lodestar                    |
|10168                                            |Junkers JU52/3m                         |
|10169                                            |C-47 Dakota DT-941                      |
|1016B                                            |Douglas C-47A-90-DL                     |
|1016C                                            |Lockheed 18 Lodestar                    |
|1016D                                            |Focke-Wulf FW 200                       |
|10039                                            |de Havilland DH-9                       |
|1016E                                            |Boeing TB-29A Super Fortress            |
|1016J                                            |Douglas C-47                            |
|1016N                                            |Junkers JU-52/3m                        |
|1016T                                            |Short S-23 (flying boat)                |
|1016U                                            |Junkers JU-52/3m                        |
|1016V                                            |Junkers JU-52/3m                        |
|1016W                                            |Consolidated B24H                       |
|1016X                                            |Douglas DC-3                            |
|1017                                             |NaN                                     |
|10170                                            |Douglas C-47A-DL                        |
|1003A                                            |Breguet 14                              |
|10171                                            |Ford 5-AT-B Tri-Motor                   |
|10175                                            |Lockheed 18 LodeStar                    |
|10176                                            |Focke-Wulf FW 200                       |
|10177                                            |Douglas C-47                            |
|10178                                            |Douglas DC-3                            |
|1017A                                            |Avro 683 Lancaster                      |
|1017C                                            |UC-64A Noorduyn Norseman                |
|1017E                                            |Douglas C-47                            |
|1017F                                            |Martin M-130 (flying boat)              |
|1017G                                            |Douglas DC-3                            |
|1003C                                            |Breguet 14                              |
|1017H                                            |Douglas C-47                            |
|1017J                                            |Douglas C-47                            |
|1017K                                            |Consolidated Liberator                  |
|1017L                                            |Stinson Model A                         |
|1017M                                            |Douglas C-47-DL                         |
|1017P                                            |Douglas C-47 Dakota                     |
|1017Q                                            |Douglas R4D-6                           |
|1017S                                            |Lockheed 18 Loadstar                    |
|1017T                                            |Curtiss C-46A                           |
|1017U                                            |Douglas DC-3                            |
|1000A                                            |Schutte-Lanz S-L-10 (airship)           |
|1003D                                            |Lioré-et-Olivier H-13                   |
|1017W                                            |Douglas C-47A-90-DL                     |
|1017X                                            |Douglas C-47                            |
|10180                                            |Douglas DC-3                            |
|10185                                            |Douglas DC-3                            |
|10186                                            |Junkers JU-53/3m                        |
|10188                                            |Douglas C-47-DL                         |
|10189                                            |Focke-Wulf FW 200                       |
|1018A                                            |B17G Flying Fortress                    |
|1018B                                            |Lockheed 18 Lodestar                    |
|1018C                                            |Douglas C-54E-DO (DC-4)                 |
|1003E                                            |Breguet 14                              |
|1018D                                            |Curtiss-Wright C-46D-CU                 |
|1018E                                            |Avro Lancaster                          |
|1018F                                            |Douglas C-47B-DK                        |
|1018G                                            |Douglas C-47B-dK                        |
|1018H                                            |Douglas C-47                            |
|1018J                                            |de Havilland DH-86A                     |
|1018M                                            |Consolidated LB-30A Liberator           |
|1018P                                            |NaN                                     |
|1018Q                                            |Consolidated LB-30A Liberator           |
|1018R                                            |Douglas C-47                            |
|1003F                                            |De Havilland DH-4                       |
|1018T                                            |Douglas DC-3-201C /  Army A-26          |
|1018U                                            |North American B-25D bomber             |
|1018V                                            |Boeing 247D                             |
|1018W                                            |Sikorsky S-43 (flying boat)             |
|10191                                            |Douglas DC-2-243                        |
|10192                                            |Douglas DC-3                            |
|10194                                            |Douglas C-47A                           |
|10195                                            |Douglas C-47B-DK                        |
|10196                                            |Douglas C-47B-5-DK                      |
|10198                                            |Curtiss C-46D                           |
|1003H                                            |De Havilland DH-4                       |
|10199                                            |Lockheed 18 Lodestar                    |
|1019A                                            |Consolidated LB-40-A Liberator          |
|1019C                                            |Short Stirling IV                       |
|1019E                                            |Consolidated LB-30-A Liberator          |
|1019F                                            |Curtiss-Wright C-46F-CU                 |
|1019J                                            |Douglas C-47B                           |
|1019K                                            |Douglas C-47                            |
|1019M                                            |Douglas C-47B                           |
|1019N                                            |Faucett F-19                            |
|1019S                                            |Curtiss-Wright C-46A-CK                 |
|1003J                                            |Farman F-60 Goliath                     |
|1019T                                            |Douglas C-47A-DK                        |
|1019V                                            |Douglas C-54G                           |
|1019Z                                            |Martin PBM-3S  / Martin PBM-5           |
|101A                                             |Douglas C-47A-DL                        |
|101AB                                            |Boeing B-17G                            |
|101AC                                            |Short Stirling                          |
|101AE                                            |Douglas C-54                            |
|101AF                                            |Douglas C-47 Dakota-DK                  |
|101AG                                            |Consolidated LB-30A Liberator           |
|101AH                                            |Consolidated LB-30A Liberator           |
|1003K                                            |Blériot Spad 46                         |
|101AJ                                            |Five Grumman TBM Avengers               |
|101AK                                            |Douglas C-47                            |
|101AM                                            |Douglas C-47B                           |
|101AN                                            |Lockheed 18 Lodestar                    |
|101AP                                            |Douglas DC-3                            |
|101AR                                            |Douglas DC-3                            |
|101AS                                            |Douglas C-47                            |
|101AT                                            |Douglas C-47 Dakota                     |
|101AW                                            |Douglas DC-3-201E                       |
|101AX                                            |Douglas DC-3 Dakota                     |
|1003L                                            |De Havilland DH-4                       |
|101AZ                                            |Douglas C-47B                           |
|101BA                                            |Douglas DC-3-194H                       |
|101BB                                            |Douglas C-47                            |
|101BC                                            |Consolidated 32-2 Liberator II          |
|101BE                                            |Douglas DC-3-227B                       |
|101BH                                            |Junkers JU-52/3m                        |
|101BJ                                            |Douglas DC-3 (C-47DL)                   |
|101BK                                            |NaN                                     |
|101BM                                            |NaN                                     |
|101BP                                            |Douglas C-47B                           |
|1003Q                                            |de Havilland DH-34                      |
|101BR                                            |Avro 691 Lancastrian 1                  |
|101BS                                            |Vickers Wellington bomber               |
|101BT                                            |NaN                                     |
|101BW                                            |NaN                                     |
|101BY                                            |Douglas C-47A                           |
|101C                                             |PBY4-2 Privateer / PB4Y-2 Privateer     |
|101CA                                            |Douglas DC-3                            |
|101CB                                            |Junkers JU-52/3m                        |
|101CC                                            |Douglas C-54-DO (DC-4)                  |
|101CD                                            |Douglas C-47 Dakota                     |
|1003X                                            |Junkers F-13                            |
|101CE                                            |Douglas C-54D-DC (DC-4)                 |
|101CF                                            |Douglas C-47B                           |
|101CG                                            |Junkers Ju-52/3m                        |
|101CH                                            |Boeing B17G                             |
|101CJ                                            |Lockheed L-049 Constellation            |
|101CL                                            |Curtiss C-46                            |
|101CM                                            |Curtiss C-46D-10-CU                     |
|101CN                                            |Douglas C-47                            |
|101CS                                            |Boeing B-17G / Boeing B-17G             |
|101CU                                            |Douglas C-47 Dakota                     |
|1003Z                                            |De Havilland DH-4                       |
|101CW                                            |Douglas C-47A-10-DK                     |
|101CX                                            |Lockheed 18-56 Lodestar                 |
|101CY                                            |Douglas C-47A                           |
|101D                                             |Avro 691 Lancastrian 1                  |
|101DA                                            |Douglas C-47-DL                         |
|101DB                                            |Avro Anson                              |
|101DC                                            |Douglas DC-3 (C-53D-DO)                 |
|101DF                                            |Douglas DC-3                            |
|101DG                                            |Douglas DC-3 (C-47-A5-DL)               |
|101DH                                            |Avro 685 York I                         |
|1000E                                            |Zeppelin L-32 (airship)                 |
|1004                                             |Zeppelin Dixmunde (airship)             |
|101DJ                                            |Douglas C-47A                           |
|101DK                                            |Douglas C-47A Dakota                    |
|101DL                                            |Douglas C-47-DL                         |
|101DM                                            |Douglas DC-3 ( C-47-DO)                 |
|101DN                                            |Douglas DC-4-1009                       |
|101DP                                            |Avro Lancaster                          |
|101DQ                                            |NaN                                     |
|101DR                                            |Douglas C-47B-25-DK                     |
|101DT                                            |Douglas DC-3A-228D                      |
|101DU                                            |Douglas C-54E-5-DO                      |
|10045                                            |De Havilland DH-4                       |
|101DW                                            |Avro 685 York 1                         |
|101DX                                            |Fairey Firefly MK1                      |
|101DY                                            |Douglas DC-4                            |
|101DZ                                            |Junkers Ju-52/3m                        |
|101EA                                            |Douglas DC-3                            |
|101EB                                            |Douglas C-47B                           |
|101EC                                            |Junkers JU-52/3m                        |
|101ED                                            |AAC-1 Toucan                            |
|101EE                                            |Douglas DC-3 (C-53D-DO)                 |
|101EF                                            |Douglas C-53D-DO (DC-3)                 |
|10048                                            |De Havilland DH-4                       |
|101EG                                            |Douglas DC-3                            |
|101EH                                            |Douglas C-47A-90 DL (DC-3)              |
|101EL                                            |Douglas C-47                            |
|101EM                                            |Douglas DC-3 (C-47A-90-DL)              |
|101EP                                            |Vickers 620 Viking 1                    |
|101ER                                            |Lisunov Li-2                            |
|101ES                                            |Curtiss-Wright R5C-1                    |
|101EX                                            |Curtiss-Wright C-46F-CU                 |
|101F                                             |Douglas DC-3 (C-47-B-1-DK)              |
|101FA                                            |Douglas C-47A                           |
|1004D                                            |Fokker F.III                            |
|101FC                                            |Avro  685 York I                        |
|101FE                                            |Douglas DC-3 ( C-53D-DO)                |
|101FG                                            |Curtiss C-46, C-47, DC-3                |
|101FH                                            |Douglas DC-3 (C-50A-DO)                 |
|101FK                                            |Douglas C-47A                           |
|101FL                                            |Lockheed 049 Consellation               |
|101FM                                            |Sikorsky S-43B (flying boat)            |
|101FR                                            |Douglas DC-3                            |
|101FS                                            |Douglas DC-4                            |
|101FT                                            |Douglas DC-4 (C-54A-DO)                 |
|1004E                                            |Junkers F-13                            |
|101FU                                            |Douglas C-47A-1-DK                      |
|101FY                                            |Douglas DC-3                            |
|101GA                                            |Lockheed C-60 Lodestar                  |
|101GC                                            |Douglas DC-3                            |
|101GD                                            |Douglas C-47 / Douglas DC-3             |
|101GE                                            |Douglas C-47A                           |
|101GJ                                            |Douglas C- C47A-30DK                    |
|101GK                                            |Curtiss C-46                            |
|101GL                                            |Douglas DC-3C                           |
|101GM                                            |Douglas DC-3                            |
|1004F                                            |De Havilland DH-4                       |
|101GN                                            |Douglas C-54B-15-DO                     |
|101GP                                            |Curtiss C-46E                           |
|101GR                                            |Savoia-Marchetti SM-95                  |
|101GT                                            |Douglas DC-4                            |
|101GV                                            |Douglas C-47                            |
|101GW                                            |Douglas C-47B                           |
|101GX                                            |Douglas C-47-DL                         |
|101H                                             |Douglas C-47B                           |
|101HB                                            |Douglas DC-3 (C-47A-90-DL)              |
|101HC                                            |Lockheed 18 Lodestar                    |
|1004G                                            |NaN                                     |
|101HF                                            |Avro York C1                            |
|101HH                                            |Douglas C-47A                           |
|101HJ                                            |Avro 685 York I                         |
|101HL                                            |Douglas DC-3 (C-47DL) /Vultee BT-13     |
|101HM                                            |Douglas C-47                            |
|101HQ                                            |Lockheed 18 Loadstar                    |
|101HS                                            |Lockheed L-049 Constellation            |
|101HT                                            |Douglas DC-3                            |
|101HZ                                            |Douglas C-54D-DC (DC-4)                 |
|101J                                             |Douglas C-54B                           |
|1004H                                            |De Havilland DH-4                       |
|101JA                                            |Douglas C-54B-15-DO                     |
|101JC                                            |Junkers Ju-52                           |
|101JE                                            |Avro Lancaster                          |
|101JF                                            |Douglas DC-4 (C-54-DO)                  |
|101JG                                            |Lockheed 049-46-21 Constellation        |
|101JH                                            |Junkers JU-52/3m                        |
|101JJ                                            |Douglas DC-3                            |
|101JK                                            |Junkers Ju-52/3m                        |
|101JL                                            |Avro 685 York                           |
|101JM                                            |Avro 685 York I                         |
|1004J                                            |de Havilland DH-34B                     |
|101JN                                            |Douglas C-47                            |
|101JP                                            |Avro 691 Lancastrian 3                  |
|101JR                                            |Consolidated PBY-5A Catalina            |
|101JT                                            |Douglas DC-3C                           |
|101JV                                            |Douglas DC-3F                           |
|101JW                                            |Lisunov Li-2                            |
|101K                                             |Curtiss C-46E                           |
|101KC                                            |Short Sandringham 5 (flying boat)       |
|101KF                                            |Short Sandringham (flying boat)         |
|101KG                                            |Douglas DC-4                            |
|1004M                                            |Junkers F-13                            |
|101KK                                            |Douglas DC-3                            |
|101KL                                            |Bristol 170 Freighter I                 |
|101KM                                            |Douglas DC-6                            |
|101KP                                            |Douglas DC-4A                           |
|101KR                                            |Douglas DC-4-1009                       |
|101KS                                            |Douglas C-47B                           |
|101KT                                            |Douglas DC-3                            |
|101KU                                            |Douglas DC-6                            |
|101KW                                            |Junkers Ju-52/3m                        |
|101LB                                            |Bristol 170 Freighter XI                |
|1000H                                            |Zeppelin L-31 (airship)                 |
|1004N                                            |Breguet 14                              |
|101LC                                            |Lockheed L-049-46-26 Constellation      |
|101LE                                            |Lisunov Li-2                            |
|101LG                                            |Douglas DC-3                            |
|101LJ                                            |Douglas DC-3                            |
|101LL                                            |Douglas DC-3                            |
|101LP                                            |Douglas C-47B                           |
|101LU                                            |Douglas C-54A                           |
|101LV                                            |Douglas C-54D-DC (DC-4)                 |
|101LW                                            |Douglas C-47-DK                         |
|101M                                             |Short  S-29 Stirling V                  |
|1004P                                            |Breguet 14                              |
|101MA                                            |Douglas DC-3 (C-47)                     |
|101MB                                            |Douglas DC-2-172                        |
|101MC                                            |Douglas DC-3D                           |
|101ME                                            |Vickers 610 Viking 1B                   |
|101MF                                            |Douglas DC-3                            |
|101MG                                            |Douglas DC-3                            |
|101MH                                            |Douglas DC-3                            |
|101MJ                                            |Douglas DC-3-201F                       |
|101ML                                            |Curtiss C-46                            |
|101MN                                            |Douglas C-47B                           |
|1004Q                                            |Fokker (KLM)  F.III                     |
|101MP                                            |Douglas DC-3 (C-47B-DK)                 |
|101MR                                            |Avro 688 Tudor I                        |
|101MT                                            |Lockheed L-649 Constellation            |
|101MU                                            |Douglas DC-3                            |
|101MV                                            |Douglas C-47-DL                         |
|101MW                                            |Latecoere 631                           |
|101MX                                            |Douglas DC-3                            |
|101MZ                                            |Douglas C-47A                           |
|101N                                             |Douglas C-47                            |
|101NC                                            |Junkers Ju-52/3m                        |
|1004S                                            |Lioré-et-Olivier H-13                   |
|101ND                                            |Douglas DC-3                            |
|101NE                                            |Avro Anson                              |
|101NL                                            |Douglas DC-4                            |
|101NM                                            |Douglas DC-4 (C-54G-1-DO)               |
|101NN                                            |Douglas DC-3                            |
|101NS                                            |Douglas DC-3 (C47-DL)                   |
|101NW                                            |Vickers 604 Viking 1B                   |
|101NX                                            |Vickers Viking 1B & Soviet YAK-3 fighter|
|101NY                                            |Lockheed L-049-46 Constellation         |
|101NZ                                            |Douglas C-47                            |
|1004V                                            |Breguet 14                              |
|101P                                             |Douglas DC-4-1009                       |
|101PA                                            |de Havilland Dove 1                     |
|101PE                                            |Douglas DC-3-455                        |
|101PF                                            |Curtiss C-46E                           |
|101PG                                            |Douglas C-47A                           |
|101PK                                            |Handley Page Halifax C-8                |
|101PL                                            |de Havilland DH-89A Dragon Rapide       |
|101PM                                            |Douglas DC-6                            |
|101PQ                                            |Douglas DC-3                            |
|101PR                                            |Fiat G.212CP                            |
|1004X                                            |Potez IX                                |
|101PS                                            |Douglas DC-6 / RAF York MW248           |
|101PT                                            |Douglas DC-3                            |
|101PV                                            |Douglas C-47A                           |
|101PZ                                            |Consolidated OA-10 Catalina             |
|101QS                                            |Douglas DC-3                            |
|101R                                             |Short Sandringham 2 (flying boat)       |
|101RA                                            |Curtiss C-46D-20-CU                     |
|101RB                                            |Latecoere 631 (flying boat)             |
|101RC                                            |Avro 691 Lancastrian                    |
|101RD                                            |Douglas C-47B                           |
|1004Y                                            |Dirigible ZR-1 Shenandoah (airship)     |
|101RE                                            |Douglas C-47A                           |
|101RF                                            |Douglas C-47                            |
|101RG                                            |Martin 202                              |
|101RH                                            |Douglas DC-3 (Douglas C-47A-10-DK)      |
|101RJ                                            |Douglas DC-3                            |
|101RK                                            |Short Sandringham 6 (flying boat)       |
|101RL                                            |Lockheed 049-46-25 Constellation        |
|101RM                                            |Lockheed 10A Electra                    |
|101RP                                            |Douglas C-54A                           |
|101RR                                            |Boeing B-29 Superfortress               |
|1004Z                                            |NaN                                     |
|101RT                                            |Douglas DC-3                            |
|101RV                                            |Douglas DC-3                            |
|101RW                                            |de Havilland DH-89A Dragon Rapide       |
|101RX                                            |Douglas DC-3                            |
|101RZ                                            |Curtiss C-46                            |
|101SA                                            |Douglas C-47                            |
|101SB                                            |Douglas DC-3                            |
|101SC                                            |Douglas C-47                            |
|101SG                                            |Douglas DC-3                            |
|101SH                                            |Douglas C-54B-5-DO                      |
|1005                                             |Farman F-60 Goliath                     |
|101SJ                                            |Douglas DC-3 (C-47-DL)                  |
|101SK                                            |Douglas DC-3                            |
|101SL                                            |Douglas DC-3                            |
|101SM                                            |Douglas DC-3 (C-47A-DL)                 |
|101SN                                            |Avro 685 York 1                         |
|101SP                                            |Douglas C-47A                           |
|101SS                                            |Lockheed 18 Lodestar                    |
|101ST                                            |Douglas C-54 Skymaster                  |
|101SV                                            |Douglas DC-3                            |
|101SX                                            |Avro 688 Tudor 4B                       |
|10050                                            |Curtiss Carrier Pigeon                  |
|101SY                                            |Boeing B-29A Superfortress              |
|101T                                             |Douglas DC-3C                           |
|101TA                                            |Lockheed L-749 / Cessna 140             |
|101TB                                            |Avro Anson                              |
|101TC                                            |Douglas C-54A-1-DO Skymaster            |
|101TD                                            |Consolidated PBY-5A Catalina            |
|101TF                                            |Vickers 628 Viking 1B                   |
|101TH                                            |Douglas DC-3                            |
|101TJ                                            |Douglas DC-3 / Avro Anson               |
|101TK                                            |Douglas DC-3                            |

## Competency Question Name
**Competency Question:** Show the parts along with their manufactiring company and their airworthiness directive.
**SPARQL Query:**
```
PREFIX grair:<https://group3/GenericOntology/Airplanes>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX kwgr: <http://stko-kwg.geog.ucsb.edu/lod/resource/> 

SELECT ?part ?partString ?company ?companyString ?directive ?directiveString WHERE {
  ?part a grair:Part ;
        grair:partAsString ?partString ;
        grair:isMadeBy ?company ;
        grair:hasAirworthinessDirective ?directive .
  ?company a grair:ManufacturingCompany ;
           grair:asString ?companyString .
  ?directive a grair:AirworthinessDirective ;
              grair:directiveAsString ?directiveString .
}



```

**Results:**
|part                                             |partString                              |company                                                          |companyString                |directive                                                           |directiveString|
|-------------------------------------------------|----------------------------------------|-----------------------------------------------------------------|-----------------------------|--------------------------------------------------------------------|---------------|
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part0 |Autoflight                              |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany0  |Airbus                       |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective0  |2022-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part1 |Autoflight                              |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany1  |Airbus                       |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective1  |2022-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part10|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany10 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective10 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part100|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany100|The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective100|2005-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part101|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany101|The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective101|2005-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part102|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany102|The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective102|2005-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part103|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany103|The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective103|2005-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part104|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany104|The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective104|2005-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part105|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany105|The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective105|2005-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part106|Flight Controls                         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany106|Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective106|2005-05-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part107|Flight Controls                         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany107|Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective107|2005-05-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part108|Flight Controls                         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany108|Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective108|2005-05-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part109|Flight Controls                         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany109|Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective109|2005-05-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part11|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany11 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective11 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part110|Spar Strap                              |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany110|Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective110|2005-05-52     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part111|Spar Strap                              |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany111|Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective111|2005-05-52     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part112|Foreward Spar Fasteners                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany112|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective112|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part113|Rear Spar Fasteners                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany113|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective113|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part114|Lower Rear Bathtub Fitting              |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany114|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective114|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part115|Foreward Spar Fasteners                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany115|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective115|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part116|Rear Spar Fasteners                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany116|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective116|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part117|Lower Rear Bathtub Fitting              |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany117|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective117|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part118|Foreward Spar Fasteners                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany118|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective118|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part119|Rear Spar Fasteners                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany119|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective119|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part12|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany12 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective12 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part120|Lower Rear Bathtub Fitting              |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany120|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective120|2004-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part121|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany121|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective121|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part122|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany122|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective122|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part123|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany123|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective123|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part124|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany124|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective124|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part125|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany125|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective125|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part126|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany126|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective126|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part127|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany127|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective127|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part128|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany128|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective128|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part129|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany129|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective129|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part13|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany13 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective13 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part130|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany130|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective130|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part131|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany131|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective131|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part132|Aft Rudder Control Rods                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany132|Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective132|2004-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part133|Horizontal Stabilizer Actuator          |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany133|Learject Inc                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective133|2003-06-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part134|Elevator Control System                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany134|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective134|2003-03-18     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part135|Elevator Control System                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany135|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective135|2003-03-18     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part136|Elevator Control System                 |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany136|Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective136|2003-03-18     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part137|Center Fuel Tank                        |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany137|Bombardier Inc               |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective137|2003-02-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part14|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany14 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective14 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part15|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany15 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective15 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part16|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany16 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective16 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part17|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany17 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective17 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part18|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany18 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective18 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part19|CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany19 |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective19 |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part2 |Left-Hand Elevator Auxiliary Spar       |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany2  |Viking Air Limited           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective2  |2022-21-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part20|V2522-A5 Turbofan Engine                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany20 |International Aero Engines AG|http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective20 |2021-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part21|V2522-A5 Turbofan Engine                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany21 |International Aero Engines AG|http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective21 |2021-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part22|V2522-A5 Turbofan Engine                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany22 |International Aero Engines AG|http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective22 |2021-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part23|V2522-A5 Turbofan Engine                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany23 |International Aero Engines AG|http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective23 |2021-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part24|V2522-A5 Turbofan Engine                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany24 |International Aero Engines AG|http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective24 |2021-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part25|V2522-A5 Turbofan Engine                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany25 |International Aero Engines AG|http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective25 |2021-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part26|V2522-A5 Turbofan Engine                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany26 |International Aero Engines AG|http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective26 |2021-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part27|PW4074 Turbofan Engine                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany27 |Pratt & Whitney Division     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective27 |2021-05-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part28|PW4074 Turbofan Engine                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany28 |Pratt & Whitney Division     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective28 |2021-05-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part29|PW4074 Turbofan Engine                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany29 |Pratt & Whitney Division     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective29 |2021-05-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part3 |Wing Structure                          |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany3  |Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective3  |2022-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part30|PW4074 Turbofan Engine                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany30 |Pratt & Whitney Division     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective30 |2021-05-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part31|PW4074 Turbofan Engine                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany31 |Pratt & Whitney Division     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective31 |2021-05-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part32|PW4074 Turbofan Engine                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany32 |Pratt & Whitney Division     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective32 |2021-05-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part33|PW4074 Turbofan Engine                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany33 |Pratt & Whitney Division     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective33 |2021-05-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part34|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany34 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective34 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part35|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany35 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective35 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part36|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany36 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective36 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part37|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany37 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective37 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part38|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany38 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective38 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part39|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany39 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective39 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part4 |Wing Structure                          |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany4  |Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective4  |2022-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part40|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany40 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective40 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part41|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany41 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective41 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part42|737 Pneumatic Motor                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany42 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective42 |2020-16-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part43|Amplifier 38849-001                     |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany43 |Cirrus Design Corporation    |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective43 |2020-03-50     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part44|Microphone Interface 35809-001          |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany44 |Cirrus Design Corporation    |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective44 |2020-03-50     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part45|TSO-C172 Cargo Restraint Straps         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany45 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective45 |2019-25-55     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part46|TSO-C172 Cargo Restraint Straps         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany46 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective46 |2019-25-55     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part47|TSO-C172 Cargo Restraint Straps         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany47 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective47 |2019-25-55     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part48|Flight Controls                         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany48 |Cirrus Design Corporation    |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective48 |2019-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part49|Flight Controls                         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany49 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective49 |2018-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part5 |Wing Structure                          |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany5  |Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective5  |2022-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part50|Flight Controls                         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany50 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective50 |2018-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part51|Taperlok Fasteners                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany51 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective51 |2014-26-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part52|Taperlok Fasteners                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany52 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective52 |2014-26-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part53|Taperlok Fasteners                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany53 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective53 |2014-26-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part54|Taperlok Fasteners                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany54 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective54 |2014-26-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part55|Taperlok Fasteners                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany55 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective55 |2014-26-53     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part56|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany56 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective56 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part57|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany57 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective57 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part58|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany58 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective58 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part59|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany59 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective59 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part6 |Wing Structure                          |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany6  |Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective6  |2022-11-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part60|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany60 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective60 |2014-25-52     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part61|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany61 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective61 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part62|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany62 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective62 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part63|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany63 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective63 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part64|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany64 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective64 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part65|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany65 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective65 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part66|Angle of Attack Probes                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany66 |Airbus SAS                   |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective66 |2014-25-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part67|Stabilizer Attachment Joint             |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany67 |Embraer S.A.                 |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective67 |2014-15-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part68|Inboard Vent Tube Hole                  |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany68 |Gulfstream Aerospace LP      |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective68 |2014-13-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part69|Stabilizers                             |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany69 |Mooney Aviation Company Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective69 |2012-03-52     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part7 |CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany7  |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective7  |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part70|Stabilizers                             |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany70 |Mooney Aviation Company Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective70 |2012-03-52     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part71|Principle Wing Structure                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany71 |Aero Union Corporation       |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective71 |2012-03-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part72|Principle Wing Structure                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany72 |Aero Union Corporation       |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective72 |2012-03-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part73|Principle Wing Structure                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany73 |Aero Union Corporation       |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective73 |2012-03-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part74|Principle Wing Structure                |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany74 |Aero Union Corporation       |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective74 |2012-03-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part75|Bob-weight Interconnect Link            |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany75 |Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective75 |2011-27-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part76|Bob-weight Interconnect Link            |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany76 |Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective76 |2011-27-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part77|Bob-weight Interconnect Link            |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany77 |Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective77 |2011-27-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part78|Battery Charger                         |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany78 |Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective78 |2011-21-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part79|Pitch Trim                              |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany79 |Dassault Aviation            |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective79 |2011-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part8 |CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany8  |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective8  |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part80|Fuselage Drain Holes                    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany80 |Piaggio Aero Industries S.p.A|http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective80 |2011-09-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part81|Skin Bonding Agent                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany81 |Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective81 |2010-26-54     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part82|Skin Bonding Agent                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany82 |Cessna Aircraft              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective82 |2010-26-54     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part83|Fuel Pump                               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany83 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective83 |2008-24-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part84|Fuel Pump                               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany84 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective84 |2008-24-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part85|Fuel Pump                               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany85 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective85 |2008-24-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part86|Fuel Pump                               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany86 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective86 |2008-24-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part87|Fuel Pump                               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany87 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective87 |2008-24-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part88|Lower Wing Panel                        |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany88 |328 Support Services GmbH    |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective88 |2008-10-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part89|Lower Wing Panel                        |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany89 |328 Support Services GmbH    |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective89 |2008-10-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part9 |CF34-8C and CF34-8E Turbofan Engines    |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany9  |General Electric Company     |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective9  |2021-23-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part90|Rear Wing Lower Spar Caps               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany90 |Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective90 |2006-18-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part91|Rear Wing Lower Spar Caps               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany91 |Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective91 |2006-18-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part92|Rear Wing Lower Spar Caps               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany92 |Hawker Textron Aviation Inc  |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective92 |2006-18-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part93|Wing Spar                               |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany93 |Frakes Aviation              |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective93 |2006-01-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part94|Operational Program Software            |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany94 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective94 |2005-18-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part95|Operational Program Software            |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany95 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective95 |2005-18-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part96|Operational Program Software            |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany96 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective96 |2005-18-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part97|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany97 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective97 |2005-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part98|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany98 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective98 |2005-12-51     |
|http://stko-kwg.geog.ucsb.edu/lod/resource/Part99|Wing Attach Angles                      |http://stko-kwg.geog.ucsb.edu/lod/resource/ManufacuringCompany99 |The Boeing Company           |http://stko-kwg.geog.ucsb.edu/lod/resource/AirworthinessDirective99 |2005-12-51     |



