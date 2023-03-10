# graphdb

Git-Link of paper: https://github.com/multi-dimensional-process-mining/graphdb-eventlogs

## Step-by-step

see also https://github.com/multi-dimensional-process-mining/graphdb-eventlogs/tree/master/exploration_bpic2017

### Get the data
* Download the loan_full.csv from https://drive.google.com/drive/folders/1kinMug9OzNg5RiwhyfZ5aiF5ksUEAMXI?usp=sharing


* OR prepare the original data:
1. Download BPI Challenge 2017.xes from https://data.4tu.nl/articles/dataset/BPI_Challenge_2017/12696884/1
1. Convert the .xes file into csv with Prom Lite and name it bpiChallenge17.csv
1. Execute the script dataPrepBPIC17full.py from https://github.com/multi-dimensional-process-mining/graphdb-eventlogs/tree/master/exploration_bpic2017

Then work with Neo4j Desktop or with Neo4j with Docker

### Hardware
* Prozessor: AMD Ryzen 7 3800X 8-Core Processor     3.90 GHz
* RAM: 32,0 GB

### Neo4j Desktop

1. Download Neo4j Desktop and create a new database in Neo4j Desktop and start it.
1. Open the import folder for the database -> in Neo4j Desktop click on the three dots - Open Folder - Import.
1. Copy the file loan_full.csv in this folder.
1. For more memory: click on the three dots at the database - Under Settings change the value at ```dbms.memory.heap.max_size=``` to example ```20g```, save the file and restart database.

### Neo4j with Docker

1. Neo4j in docker Docker desktop öffnen Folgender command in powershell: 
<br> docker run --name testneo4j -p7474:7474 -p7687:7687 -d -v $HOME/neo4j/data:/data -v $HOME/neo4j/logs:/logs -v $HOME/neo4j/import:/var/lib/neo4j/import -v $HOME/neo4j/plugins:/plugins --env NEO4J_AUTH=neo4j/letmepass --env NEO4J_dbms_connector_https_advertised__address="localhost:7473" --env NEO4J_dbms_connector_http_advertised__address="localhost:7474" --env NEO4J_dbms_connector_bolt_advertised__address="localhost:7687" --env=NEO4J_dbms_memory_heap_max__size=5G neo4j:latest <\br> It might be necessary to add here 20G: --env=NEO4J_dbms_memory_heap_max__size=20G and add: --memory="21g" <\br> in browser http://127.0.0.1:7474/browser/
- username: neo4j password: letmepass
2. copy the file loan_full.csv into C:\Users[YOUR-USERNAME]\neo4j\import

### For execution (tried in Neo4j Desktop):
1. Follow the steps in ![import/Readme.md](https://github.com/HGB-ProcessMining/graphdb/blob/main/import/readme.md)
1. For the queries change the setting in Neo4j Browser: Go to settings scroll to the bottom and disable ```Connect result nodes```
1. Run the ![statements.md](https://github.com/HGB-ProcessMining/graphdb/blob/main/statements.md)


## useful links
1. Paper "Multi-Dimensional Event Data in Graph Databases" from Stefan Esser and Dirk Fahland: https://link.springer.com/article/10.1007/s13740-021-00122-1
1. Git from Stefan Esser and Dirk Fahland: https://github.com/multi-dimensional-process-mining/graphdb-eventlogs
1. prepared data from the students: https://drive.google.com/drive/folders/1kinMug9OzNg5RiwhyfZ5aiF5ksUEAMXI?usp=sharing

