Neo4j in docker
Docker desktop öffnen
Folgender command in powershell:
<\br>
docker run --name testneo4j -p7474:7474 -p7687:7687 -d -v $HOME/neo4j/data:/data -v $HOME/neo4j/logs:/logs -v $HOME/neo4j/import:/var/lib/neo4j/import -v $HOME/neo4j/plugins:/plugins --env NEO4J_AUTH=neo4j/letmepass --env NEO4J_dbms_connector_https_advertised__address="localhost:7473" --env NEO4J_dbms_connector_http_advertised__address="localhost:7474" --env NEO4J_dbms_connector_bolt_advertised__address="localhost:7687" --env=NEO4J_dbms_memory_heap_max__size=5G neo4j:latest
<\br>
It might be necessary to add here 20G:
--env=NEO4J_dbms_memory_heap_max__size=20G 
and add:
--memory="21g"
<\br>
in browser
http://127.0.0.1:7474/browser/


username: neo4j
password: letmepass

copy the file ```loan_full.csv``` into C:\Users\[YOUR-USERNAME]\neo4j\import
