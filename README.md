# graphdb

Git-Link of paper: https://github.com/multi-dimensional-process-mining/graphdb-eventlogs

Step-by-step

see also https://github.com/multi-dimensional-process-mining/graphdb-eventlogs/tree/master/exploration_bpic2017

1. Download BPI Challenge 2017.xes from https://data.4tu.nl/articles/dataset/BPI_Challenge_2017/12696884/1
1. Convert the .xes file into csv with Prom Lite and name it bpiChallenge17.csv
1. Execute the script dataPrepBPIC17full.py from https://github.com/multi-dimensional-process-mining/graphdb-eventlogs/tree/master/exploration_bpic2017
1. Download Neo4j Desktop or use it with Docker.
1. Create a new database in Neo4j Desktop and start it.
1. Open the import folder for the database -> in Neo4j Desktop click on the three dots - Open Folder - Import.
1. Copy the file loan_full.csv in this folder.
1. Click on your database in Neo4j Desktop - at the right side pops up a field. Click on Plugins and install APOC.
1. For more memory: click on the three dots at the database - Open Folder - DBMS - open conf folder - open neo4j.conf.
Change the value at ```dbms.memory.transaction.total.max=``` (in my case it was 256m and changed it to 2g), save the file and restart Neo4j.
1. Open Neo4j Browser and run the commands from the file CypherCreateGraph.txt (see git-link in point 3). Made a new file in this repository with CypherCreateGraphUpdate.txt because some commands are out of date (like ON, ASSERT, USING PERIODIC COMMIT)


TODO Stopped at point 3 of the .txt file, because it didn't work...