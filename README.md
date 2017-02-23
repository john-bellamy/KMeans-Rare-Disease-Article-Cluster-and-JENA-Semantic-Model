# RDOST-app
Rare Disease Ontology and Search tool is a Jena-model-driven application for article retrieval.

You will need to move the fuseki-server.jar to RDOST/fuseki first. Then follow instructions in README.

How to Run (also see documentation in unzipped file):
1) Requires Jena 3.0.1
2) Requires OpenCsv jarfile, which I included in this same directory. Both of these items need to be on build path.
3) The main class is JenaModelCreationMain. Run this class after adding above to build path. This will run the other methods and classes and create the TDB database.
4) Run the bootstrap.sh file to load the Fuseki Server.
5) Navigate to localhost:3030 on your browser, then select pubmedArticles to query.
