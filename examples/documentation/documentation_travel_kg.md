# Travel Knowledge Graph 
**Authors:** 
* Chaitanya Anumula
* Skyler Gentner
* Calvin Greenewald
* Rakesh Kandula

## Use Case Scenario
### Narrative 
The topic of travel and vacations comes up frequently for many individuals and families across the world. Especially with the rise in social media marketing of travel destinations, the interest in traveling around Europe has gained global attention. After the effect of COVID deminished, and tourism gained popularity again, Europe saw tourists spend an astonishing 2.72 billion nights in Europe in 2022 [1]. These tourists largely used social media or travel blogs to determine their destinations and other vacation plans. These listed means of determining travel destination and details have weaknesses and limitations in providing the traveler with adequate information necessary for planning the entire trip. The portrayal of popular destinations on social media often deceives viewers and lead them to believe a false narrative about the destination [2]. Images of destinations are usually overly photoshopped, hiding all the flaws which then catch tourists off guard or ruin trips [2]. Travel blogs often highlight what worked for the writer and all the activities that they did. Therefore, they are not a good means for one to determine the best trip for them or their families, as the blogs are not able to be personalized. A creation of a knowledge graph could help give the tourist all the necessary details for structuring their entire trip.

This project would support many people from all walks of life and help them experience new destinations and cultures. Travel influencers across various social media platforms could grow their following and footprint on social media by using this project to determine new travel destinations or details of a trip. On TikTok, a popular social media platform, the hashtag “‘travel’ boasts 74.4 billion views [2].” Additionally, roughly 60% of Gen Zs and 40% of millennials use social media” to get inspiration for their vacation trips [2]. These statistics show that this project could support individuals and families alike, regardless of economic status, to plan budget friendly short trips or long extravagant vacations for themselves and their families. Users could consider all the popular spots that match their interests, as well as all the details regarding transportation, stay, and food.

The goal of this project is to identify tourist destinations based on personal preferences and recommend possible destinations for users. This project would ideally consider budget, length of time, destination interests, destination reviews, transportation options, and activities. Users would not have to scour the internet searching for the best reviewed, most picturesque, destinations. They would have all the information needed for planning their trip all in one place.

A knowledge graph on travel recommendations would positively impact the tourism industry. Tourists from across the world would be encouraged to visit destinations across Europe that would be a best fit for them, and consequently tourism across Europe would increase. This would also help travel agencies or travel blogs come up with best fit destinations for users and their families.

### References
[1] "Tourism in 2022 approaches pre-pandemic levels." EuroStat, 18 January 2023. https://ec.europa.eu/eurostat/web/products-eurostat-news/w/DDN-20230118-1. [Accessed 6 November 2023].

[2] Chelsea Ong. “People are Getting Travel Ideas From Social Media – Often With Hilarious Results.” CNBC, 26 April 2022. https://www.cnbc.com/2022/04/26/what-happens-when-people-use-tiktok-and-instagram-to-make-travel-plans.html. [Accessed 27 September 2023].

### Competency Questions
* What are the details and specifications of a location that is to be visited ?
* What can be the mode of transport for a given range of budget?
* What kind of activities can be performed in a given location?
* What are the locations that facilitate one particular activity, sorted from low to high based on price range?
* What are the different tourist spots for a given location?
* What type of accommodations are available in a budget range for a given location ?
* Which locations offers multi-cuisine restaurants?

### Added to scope
* What are the top-rated accommodations, attractions, modes of transport & restaurants ?

### Descoped Competency Questions
* What are the nearby places/tourist attractions?
* What are the preferred activities for the current season?
* Which are the destinations that offer water activities ?


### Integrated Datasets
Source: [Tourist Information](http://tour-pedia.org/about/datasets.html)
- A complete dataset containing a large amout of data describing the actions that we are covering, locations, reviews, and prices. 

Source: [AirBnB](https://data.world/datasets/berlin)
- Overview of AirBnB data from Berlin.

Source: [Restaurant Data] (https://www.kaggle.com/datasets/damienbeneschi/krakow-ta-restaurans-data-raw/)
- Dataset showing descriptive information regarding important restaurant information. 


## Modules
### Transport
**Source Pattern:** Part-whole, Hierarchial-cell-features <br />
**Source Data:** Tour Dataset

#### Description
The mode of transportation can affect the enjoyment the traveller experiences during their trip. They may not want to ride in public transportation and would rather drive themselves to anywhere they want to go at their destination. The traveller could also want their primary transportation to come in the form of walking so it would be better to know that so they can take a trip in a walkable city instead of a place where everything is far away from each other. Recognizing these transportation preferences helps travelers select modes that align with their comfort and travel style, ultimately enhancing their overall travel experience.

![Transport](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/Transport.jpg)

#### Axioms
* `Transport SubClassOf hasName some xsd:string` <br />
"A Transport has a name represented by a string value"
* `Transport SubClassOf hasReview some Review` <br />
"A Transport has some Review"
* `Transport SubClassOf hasCategory exactly 1 Category` <br />
"A Transport has exactly one Category"
* `Transport SubClassOf hasCost exactly 1 FinancialResource` <br />
"A Transport has exactly one cost of FinancialResource"
* `Transport SubClassOf SpatialObject` <br />
"Every Transport is a SpatialObject"

### Financial Resource
**Source Pattern:** QuantityPattern <br />
**Source Data:** Tour Dataset

#### Description
Depending on how high or low the user's budget is they will be provided with more or fewer options to travel to. Providing options that are available for a particular range of budget makes it possible to plan for a trip despite the constraints. Recognizing the budgetary limitations of travelers helps in tailoring recommendations that not only fit their financial capabilities but also ensure that their travel plans are realistic and enjoyable.

![FinancialResource](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/FinancialResource.png)

#### Axioms
* `FinancialResource SubClassOf hasCurrency some xsd:string` <br />
"FinancialResurce has a currency represented by a string value"
* `FinancialResource SubClassOf hasCurrencyValue some xsd:integer` <br />
"FinancialResurce has a currency value represented by an integer value"
* `Restaurant SubClassOf hasCost some FinancialResource` <br />
"Restaurant has a cost represented by FinancialResource"
* `Activity SubClassOf hasCost some FinancialResource` <br />
"Activity has a cost represented by FinancialResource."
* `Accommodation SubClassOf hasCost some FinancialResource` <br />
"Accommodation has a cost represented by FinancialResource."
* `Transport SubClassOf hasCost some FinancialResource` <br />
"Transport has a cost represented by FinancialResource."

### Activity
**Source Pattern:** SpatioTemporalExtent, Temporal extent <br />
**Source Data:** Tour Dataset

#### Description
Some users would like to plan their trip around certain activies that they can do while travelling. This could also help other users know what sorts of activities are available so that if needed they can make reservations ahead of time so they do not have to miss out on something they might want to do. Recognizing the significance of activities in travel planning allows users to align their travel experiences with their interests and also ensures that they can make necessary arrangements to fully enjoy the activities they desire during their trip. Given the users activity interest they could choose from different locations that offer some or all of the activities. This approach empowers travelers to select destinations that are tailored to their preferred activities, enhancing their overall travel experience by ensuring that their chosen location aligns with their activity interests and enabling them to make the most of their trip.

![Activity](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/Activity.png)

#### Axioms
* `Activity SubClassOf hasCost exactly 1 FinancialResource` <br />
"Activity has a cost of exactly one FinancialResource"
* `Activity SubClassOf hasName some xsd:string` <br />
"Activity has a name that is represented by some string value"
* `Activity SubClassOf hasLocation exactly 1 Location` <br />
"Activity has exactly one Location"
* `Activity SubClassOf hasEnvironment some Environment` <br />
"Activity has some Environment"
* `Environment SubClassOf hasType either Outdoor or Indoor` <br />
"Environment is either Outdoor or Indoor"

### Location
**Source Pattern:** SpatialObject or SpatialExtent <br />
**Source Data:** Tour Dataset

#### Description
Tourist spots would be things such as historical monuments, artistic statues, or a particular sight from a mountain that people like to see that the traveller might also want to see while on vacation. This could be important to someone who wants to plan a trip to see both the Colosseum and the statue of David on the same trip to Italy. Understanding the availability and significance of tourist spots aids travelers in creating well-rounded itineraries that encompass cultural, historical, and scenic attractions, ensuring that they can maximize their exploration of the chosen destination. And knowing the specifications of a travel location can help the traveller go to a place that they would enjoy. The traveller has in mind general information on a location that they want to go to. It would be important that someone who wants to go to the beach got there instead of ending up on the ski slopes of a mountain.These specifications can include details about the geographical features, climate, topography, and primary attractions of the location, ensuring that travelers can choose destinations that align with their preferences and expectations.

![Location](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/LocationSchema.png)

#### Axioms
* `Location SubClassOf hasAccommodation some Accommodation` <br />
"Location has some Accommodation"
* `Location SubClassOf hasRestaurant some Restaurant` <br />
"Location has some Restaurant"
* `Location SubClassOf hasTransport some Transport` <br />
"Location has some Transport"
* `Location SubClassOf hasAttraction some Attraction` <br />
"Location has some Attraction"
* `Location SubClassOf hasName some xsd:string` <br />
"Location has max one name represented by a string value"
* `Attraction SubClassOf hasName some xsd:string` <br />
"An Attraction has max one name represented by a string value"
* `Attraction SubClassOf hasReview some Review` <br />
"An Attraction has some Review"
* `Attraction SubClassOf hasCategory exactly 1 Category` <br />
"An Attraction has exactly one Category"
* `Attraction SubClassOf hasCost exactly 1 FinancialResource` <br />
"An Attraction has exactly one cost of FinancialResource"
* `Attraction SubClassOf SpatialObject` <br />
"Every Attraction is a SpatialObject"

### Accommodation
**Source Pattern:** Part-whole, Quantity, SpatioTemporalExtent <br />
**Source Data:** Berlin Airbnb Dataset, Tour Dataset

#### Description
Housing is important while on a vacation. This is where your belongings will be kept and where you will be sleeping. If your housing is in a bad part of town you may be worrying your entire trip whether or not something will get stolen. Also, if you can not sleep well in whatever housing you choose it will impact your experience as you most likely will not feel as good as you could if you got a full rest each night. Recognizing the significance of suitable accommodations in travel planning ensures that travelers have a secure and comfortable base during their journey, reducing concerns about safety and the quality of their rest, ultimately enhancing the overall travel experience.

![Accommodation](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/Accommodation.jpg)

#### Axioms
* `Accommodation SubClassOf hasName some xsd:string` <br />
"An Accommodation has max one name represented by a string value"
* `Accommodation SubClassOf hasReview some Review` <br />
"An Accommodation has some Review"
* `Accommodation SubClassOf hasLocation exactly 1 Location` <br />
"An Accommodation has exactly one Location"
* `Accommodation SubClassOf hasCategory exactly 1 Category` <br />
"An Accommodation has a exactly one Category"
* `Accommodation SubClassOf hasCost exactly 1 FinancialResource` <br />
"An Accommodation has exactly one cost of FinancialResource"
* `Accommodation SubClassOf SpatialObject` <br />
"Every Accommodation is a SpatialObject"

### Restaurant
**Source Pattern:** Provenance, Temporal extent <br />
**Source Data:** Restaurant info, Tour Dataset

#### Description
Different destinations offer diverse culinary experiences. Understanding the food options available in a location allows travelers to explore and savor the local cuisine, which for food lovers is often a highlight of the trip. For travelers who appreciate culinary adventures, discovering the local cuisine is a significant aspect of their journey. Different destinations provide unique and diverse culinary traditions. Understanding the food options available in a location ensures that food enthusiasts can indulge in the flavors and culinary delights of the region, enhancing their overall travel experience by savoring the local gastronomy.

![Restaurant](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/Restaurant.png)

#### Axioms
* `Restaurant SubClassOf hasName some xsd:string` <br />
"A Restaurant has a name represented by a string value"
* `Restaurant SubClassOf hasReview some Review` <br />
"A Restaurant has some Review"
* `Restaurant SubClassOf hasCategory exactly 1 Category` <br />
"A Restaurant has exactly one Category"
* `Restaurant SubClassOf hasLocation exactly 1 Location` <br />
"A Restaurant has exactly one Location"
* `Restaurant SubClassOf hasCost exactly 1 FinancialResource` <br />
"A Restaurant has exactly one cost of FinancialResource"
* `Restaurant SubClassOf SpatialObject` <br />
"Every Restaurant is a SpatialObject"

### SpatialObject
![SpatialObject](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/GeometrySpatialObject.jpg)

#### Axioms
* `SpatialObject SubClassOf hasGeometry some Geometry` <br />
"SpatialObject has some Geometry"
* `Geometry SubClassOf asWKT some geo:wktLiteral` <br />
"Geometry is represented as WKT by some wktLiteral value"
* `Transport SubClassOf SpatialObject` <br />
"Every Transport is a SpatialObject"
* `Attraction SubClassOf SpatialObject` <br />
"Every Attraction is a SpatialObject"
* `Restaurant SubClassOf SpatialObject` <br />
"Every Restaurant is a SpatialObject"
* `Accommodation SubClassOf SpatialObject` <br />
"Every Accommodation is a SpatialObject"

### Category
![Category](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/Category.png)

#### Axioms
* `Transport SubClassOf hasCategory exactly 1 Category` <br />
"A Transport has exactly one Category"
* `Accommodation SubClassOf hasCategory exactly 1 Category` <br />
"An Accommodation has exactly one Category"
* `Restaurant SubClassOf hasCategory exactly 1 Category` <br />
"A Restaurant has exactly one Category"
* `Attraction SubClassOf hasCategory exactly 1 Category` <br />
"An Attraction has exactly one Category"

### Review
![Review](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/Review.jpg)

#### Axioms
* `Review SubClassOf hasURL some xsd:stringURI` <br />
"Review has min 0 URL represented by a string URI"
* `Review SubClassOf hasSource some Source` <br />
"Review has min 0 Source some Source"
* `Source SubClassOf hasName some xsd:string` <br />
"Source has a name represented by a string value"
* `Source SubClassOf hasText some xsd:string` <br />
"Source has a text represented by a string value"
* `Source SubClassOf hasRating some xsd:integer` <br />
"Source has a rating represented by an integer value"

## The Overall Knowledge Graph
### Namespaces
    prefix geo: <http://www.opengis.net/ont/geosparql#> 
    
    prefix kl-ont: <https://kastle-lab.org/lod/ontology/> 
    
    prefix kl-res: <https://kastle-lab.org/lod/resource/> 
    
    prefix xsd: <http://www.w3.org/2001/XMLSchema#>

### Schema Diagram
![CombinedSchema](https://github.com/Rakesh-Sri/cs7810_Group1/blob/main/deliverables/images/Combined_Schema.jpg)


### Usage
* What can be the mode of transport for a given range of budget?

        PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
        PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
        PREFIX geo: <http://www.opengis.net/ont/geosparql#> 
        PREFIX kl-ont: <https://kastle-lab.org/lod/ontology/> 
        PREFIX kl-res: <https://kastle-lab.org/lod/resource/> 
        PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
        
        
        SELECT ?transport ?category  ?price
        WHERE {
          ?transport a kl-ont:Transport ;
                  kl-ont:hasName ?name;
                  kl-ont:hasLocation ?location;
                  kl-ont:hasCategory ?category;
                  kl-ont:hasCost ?financialRes .
            ?financialRes kl-ont:hasCurrency ?currencyType ;
                  kl-ont:hasCurrencyValue ?price .
          FILTER(?price < 30)
        } LIMIT 10
* What kind of Activities can be performed at the given location?

        PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
        PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
        PREFIX geo: <http://www.opengis.net/ont/geosparql#> 
        PREFIX kl-ont: <https://kastle-lab.org/lod/ontology/> 
        PREFIX kl-res: <https://kastle-lab.org/lod/resource/> 
        PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
        
        
        SELECT ?locName ?attraction  ?category
        WHERE {
          ?location a kl-ont:Location;
          kl-ont:hasName ?locName;
          kl-ont:hasAttraction ?attraction .
          ?attraction kl-ont:hasCategory ?category
          
          FILTER (?location = kl-res:Amsterdam)
          
        } LIMIT 10
* What type of Accommodation options available in a budget range for given location?

        PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
        PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
        PREFIX geo: <http://www.opengis.net/ont/geosparql#>
        PREFIX kl-ont: <https://kastle-lab.org/lod/ontology/>
        PREFIX kl-res: <https://kastle-lab.org/lod/resource/>
        PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
        SELECT ?locName ?accomodationName ?currencyType  ?price
        WHERE {
          ?location a kl-ont:Location;
          kl-ont:hasName ?locName;
          kl-ont:hasAccomodation ?accomodation .
          ?accomodation kl-ont:hasName ?accomodationName;
          kl-ont:hasCost ?financialRes .
          ?financialRes kl-ont:hasCurrency ?currencyType ;
                        kl-ont:hasCurrencyValue ?price .
          FILTER (?location = kl-res:London && ?price > 110 && ?price < 150)
        } LIMIT 10
  
* What are locations that facilitate a particular activity, sorted from low to high based on price range?
  
        PREFIX owl: <http://www.w3.org/2002/07/owl#>
        PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
        PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
        PREFIX geo: <http://www.opengis.net/ont/geosparql#> 
        PREFIX kl-ont: <https://kastle-lab.org/lod/ontology/> 
        PREFIX kl-res: <https://kastle-lab.org/lod/resource/> 
        PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
        
        
        SELECT ?locName ?attraction  ?category ?currencyType ?price
        WHERE {
          ?location a kl-ont:Location;
          kl-ont:hasName ?locName;
          kl-ont:hasAttraction ?attraction .
          ?attraction kl-ont:hasCategory ?category;
                      kl-ont:hasCost ?financialRes .
          ?financialRes kl-ont:hasCurrency ?currencyType ;
                        kl-ont:hasCurrencyValue ?price .
          
          FILTER (?category = kl-res:Skydiving)
          
        }
        ORDER BY ASC(?price)
        LIMIT 10
  
* What are the top rated accomodation in a particular location, along with its price?
  
        PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
        PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
        PREFIX geo: <http://www.opengis.net/ont/geosparql#> 
        PREFIX kl-ont: <https://kastle-lab.org/lod/ontology/> 
        PREFIX kl-res: <https://kastle-lab.org/lod/resource/> 
        PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> 
        
        
        SELECT ?locName ?accomodationName  ?rating ?currencyType ?price
        WHERE {
          ?location a 	kl-ont:Location;
                  kl-ont:hasName ?locName;
                  kl-ont:hasAccomodation ?accomodation .
          ?accomodation kl-ont:hasName ?accomodationName;
                        kl-ont:hasReview ?review;
                  kl-ont:hasCost ?financialRes .
          ?financialRes kl-ont:hasCurrency ?currencyType ;
                        kl-ont:hasCurrencyValue ?price .
          ?review kl-ont:hasRating ?rating.
          FILTER(?location = kl-res:London)
        } 
        ORDER BY DESC(?rating)
        LIMIT 10
