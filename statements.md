
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


MATCH p=()-[dfc:DF_C]-(c:Class)
WHERE dfc.count > 500 AND ((dfc.connection = "WW" AND dfc.EntityType = "Workflow") OR (dfc.connection = "AA" AND dfc.EntityType = "Application") OR (dfc.connection = "OO" AND dfc.EntityType = "Offer") OR (dfc.connection IN ["AO", "AW", "WO"] AND dfc.EntityType = "Case_AWO" AND dfc.count > 20000))
RETURN p


