
<H1>Property Offer, Application oder Workflow einfügen</H1>

MATCH (c:Class) <br>
WHERE c.Name =~ "O_.*" <br>
SET c.AWO = "Offer" <br>
RETURN c <br>

 ![grafik](https://user-images.githubusercontent.com/62024017/214136894-d196d971-25f1-49f4-8e0c-f7ffbc84ad70.png)

MATCH (c:Class) <br>
WHERE c.Name =~ "A_.*" <br>
SET c.AWO = "Application" <br>
RETURN c <br>

![grafik](https://user-images.githubusercontent.com/62024017/214137666-c8d1108f-f0a3-4878-a42a-79cf6b9092c8.png)

MATCH (c:Class) <br>
WHERE c.Name =~ "W_.*" <br>
SET c.AWO = "Workflow" <br>
RETURN c <br>

![grafik](https://user-images.githubusercontent.com/62024017/214137760-25b0e866-e9ba-430a-a6b2-0c624e44b132.png)



MATCH (c:Class) <br>
WITH DISTINCT c.AWO AS AWO, collect(DISTINCT c) AS class <br>
CALL apoc.create.addLabels(class, [AWO]) YIELD node <br>
RETURN *  <br>

![grafik](https://user-images.githubusercontent.com/62024017/214137951-4f382f5b-4f14-42b2-8bcd-f12c80ce1564.png)



<H1>Property for Relations between each other and themselves: Offer, Application oder Workflow einfügen</H1>

MATCH (o1:Offer)-[dfco:DF_C]->(o2:Offer) <br>
SET dfco.connection = "OO"; <br>
MATCH (a1:Application)-[dfca:DF_C]->(a2:Application) <br>
SET dfca.connection = "AA"; <br>
MATCH (w1:Workflow)-[dfcw:DF_C]->(w2:Workflow) <br>
SET dfcw.connection = "WW"; <br>
MATCH (a:Application)-[dfc:DF_C]->(o:Offer) <br>
SET dfc.connection = "AO"; <br>
MATCH (a:Application)-[dfc:DF_C]->(w:Workflow) <br>
SET dfc.connection = "AW"; <br>
MATCH (w:Workflow)-[dfc:DF_C]->(o:Offer) <br>
SET dfc.connection = "WO"; <br>
<br>
MATCH (w1:Workflow)-[dfc:DF_C]->(w2:Workflow) <br>
CREATE (w1)-[ww:DF_C_WW]->(w2) <br>
SET ww.EntityType = dfc.EntityType, ww.count = dfc.count <br>
RETURN w1, dfc, w2, ww LIMIT 30 <br>
<br>
![grafik](https://user-images.githubusercontent.com/62024017/214142452-a57c6495-0def-4cb7-bbf7-608371092b71.png)
<br>
MATCH (a1:Application)-[dfc:DF_C]->(a2:Application) <br>
CREATE (a1)-[aa:DF_C_AA]->(a2) <br>
SET aa.EntityType = dfc.EntityType, aa.count = dfc.count <br>
RETURN a1, dfc, a2, aa LIMIT 30 <br>
<br>
![grafik](https://user-images.githubusercontent.com/62024017/214142722-89c6c9f5-f2bc-4b16-b3c3-58873227c26a.png)
<br>
MATCH (o1:Offer)-[dfc:DF_C]->(o2:Offer) <br>
CREATE (o1)-[oo:DF_C_OO]->(o2) <br>
SET oo.EntityType = dfc.EntityType, oo.count = dfc.count <br>
RETURN o1, dfc, o2, oo LIMIT 30 <br>
<br>
![grafik](https://user-images.githubusercontent.com/62024017/214142811-fe69bfaa-f11d-4d3c-b8af-99b51e83f6ae.png)





<H1>Cool Statements</H1>

MATCH p=()-[dfc:DF_C]-(c:Class)  <br>
WHERE dfc.count > 10000 AND (c.Name =~ "O_.*") <br>
RETURN c, dfc LIMIT 300<br>
<br>
![grafik](https://user-images.githubusercontent.com/62024017/214140635-6daf612d-33ea-498d-bcb9-d9431f052d4a.png)
<br>
MATCH p=()-[dfc:DF_C]-(c:Class) <br>
WHERE dfc.count > 10000 <br>
RETURN p LIMIT 300 <br>
<br>
 
MATCH  (e1:Event {activity: "O_Created"})<-[:O_DF]-(e2:Event {activity: "O_Cancelled"}) -[:EVENT_TO_OFFER]-> (o:Offer) -[rel:OFFER_TO_CASE]-> (c:Case) <br>
WITH  c AS c, count(o) AS ct  <br>
WHERE ct > 1  <br>
MATCH (:Event {activity: "O_Created"})<-[:O_DF]-(e:Event {activity: "O_Cancelled"}) -[:EVENT_TO_OFFER]-> (o:Offer) -[rel:OFFER_TO_CASE]-> (c) <br>
WITH c AS c, e AS O_Cancelled, o AS o <br>
MATCH p = (A_Created:Event {activity: "A_Create Application"}) <-[:DF*]-(O_Cancelled:Event {activity: "O_Cancelled"}), (O_Cancelled) -[:EVENT_TO_CASE]-> (c) <br>
RETURN p,c,o <br>
![grafik](https://user-images.githubusercontent.com/62024017/214145227-d4682236-2322-4eed-95bd-7d84d6b78043.png) 


/ Q6
MATCH (o: Entity {EntityType : "Offer"})<-[:CORR]-(e1:Event {Activity :"O_Created"}) -[df :DF {EntityType: "Offer"}]-> (e2:Event {Activity : "O_Cancelled"})-[:CORR]->(o) <br>
MATCH (e2)-[:CORR]->(c: Entity {EntityType :"Case_AWO"})<-[:CORR]-(e1)-[:CORR]->(o) <br>
WITH c , count(o) AS ct <br>
WHERE ct > 1 <br>
MATCH (o: Entity {EntityType : "Offer"})<-[:CORR]-(e1:Event {Activity :"O_Created"}) -[df :DF {EntityType: "Offer"}]-> (e2:Event {Activity : "O_Cancelled"})-[:CORR]->(o) <br>
MATCH (e2)-[:CORR]->(c)<-[:CORR]-(e1)-[:CORR]->(o) <br>
WITH e2 AS O_Cancelled, c <br>
MATCH (A_Created:Event {Activity : "A_Create Application"})-[:CORR]->(c)<-[:CORR]-(O_Cancelled:Event {Activity : "O_Cancelled"}) <br>
MATCH p = (A_Created) -[:DF* {EntityType: "Case_AWO"}]-> (O_Cancelled) <br>
RETURN p LIMIT 3 <br>
<br>
![grafik](https://user-images.githubusercontent.com/62024017/214144238-c1362b56-8374-4935-9582-7cc3e8993715.png)


<h5>Hier starke limitierung vor Ausgabe </h5>
MATCH p=()-[dfc:DF_C]-(c:Class) <br>
WHERE dfc.count > 1000 <br>
RETURN p LIMIT 300 <br>

![grafik](https://user-images.githubusercontent.com/62024017/214144543-5bf42e98-5bbf-454b-a887-c21a87b3fd51.png)



MATCH p=()-[dfc:DF_C]-(c:Class) <br>
WHERE dfc.count > 500 AND ((dfc.connection = "WW" AND dfc.EntityType = "Workflow") OR (dfc.connection = "AA" AND dfc.EntityType = "Application") OR (dfc.connection = "OO" AND dfc.EntityType = "Offer") OR (dfc.connection IN ["AO", "AW", "WO"] AND dfc.EntityType = "Case_AWO" AND dfc.count > 20000))
RETURN p <br>

 ![grafik](https://user-images.githubusercontent.com/62024017/214143612-f8d8d8f3-3d44-44d0-aa4b-179adc857d8b.png)
 
 <h5>Hier weniger starke limitierung vor Ausgabe; dafür mehr Rules (doppelte Kanten verschwinden) </h5>
  
MATCH p=()-[dfc:DF_C]-(c:Class) <br>
WHERE dfc.count > 500 AND ((dfc.connection = "WW" AND dfc.EntityType = "Workflow") OR (dfc.connection = "AA" AND dfc.EntityType = "Application") OR (dfc.connection = "OO" AND dfc.EntityType = "Offer") OR (dfc.connection IN ["AO", "AW", "WO"] AND dfc.EntityType = "Case_AWO")) <br>
RETURN p <br>

![grafik](https://user-images.githubusercontent.com/62024017/214146082-8fb264d8-42da-4950-8097-64eae8213942.png)


