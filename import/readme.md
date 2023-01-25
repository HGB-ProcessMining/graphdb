The files ```bpic17_import.py``` and ``` bpic17_prepare.py``` were taken from the GitHub [repository](https://github.com/multi-dimensional-process-mining/graphdb-eventlogs) of the original authors.

The file ```bpic17_import.py``` was modified to be compatible with neo4j version 5.2.0.


## Data
The BPIC17 data can be found on [zenodo](https://zenodo.org/record/4708117).

## Import and prepare
The import and prepare script was executed with Python version 3.7

### Step 1
Install the python libraries listed inside the requiremts.txt

### Step 2
Check the configurations inside the python scripts and adapt them to your needs. 

Configurations ``` bpic17_prepare.py```:
+ ```inputpath```
	+ path to the directory containing the BPIC17 dataset
+  ```path_to_neo4j_import_directory```
	+ neo4j import directory


Configurations ```bpic17_import.py```:
+ ```DB_HOST```
+  ```DB_PORT```
+  ```DB_USER```
+ ```DB_PASSWORD```
+ ```path_to_neo4j_import_directory```
	+ neo4j import directory

### Step 3
1. Ensure that a neo4j database is running and check if the connection parameters in ```bpic17_import.py``` match those from the database.
2. Execute ``` bpic17_prepare.py```.
3. Execute ```bpic17_import.py```

### Need further informations?
Checkout the GitHub [repository](https://github.com/multi-dimensional-process-mining/graphdb-eventlogs) of the original authors.
