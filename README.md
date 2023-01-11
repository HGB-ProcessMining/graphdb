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
1. Open Neo4j Browser and run the commands from the file CypherCreateGraph.txt (see git-link in point 3). Made a new file in this repository with CypherCreateGraphUpdate.txt because some commands are out of date (like ON, ASSERT, USING PERIODIC COMMIT)


TODO Stopped at point 2 of the .txt file, because Unique is not given...