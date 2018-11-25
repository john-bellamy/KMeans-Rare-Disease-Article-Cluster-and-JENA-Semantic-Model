# Interactive KMeans+ Rare Disease Article Cluster and JENA Semantic Model

# PART I--Cluster:

To see outcome, look at sbma.html in Cluster Analysis folder.
(Scroll past project description to read install instructions)

# Abstract— 

Rare disease researchers often have a difficult time retrieving articles relating to their research subject. Problems with retrieval stem from a lack of unique subject headings (indexes) in databases, which would otherwise help with an inconsistent vocabulary of disease names and with the apparent absence of disease names in-lieu of pathophysiological terms.  To further compound this problem, rare diseases like Spinal (and) Bulbar Muscular Atrophy (SBMA) and Hunter’s Syndrome, have several names. Thus, if the disease name is not enough to retrieve only a fraction of the articles, and the abstract of these articles are not available, researchers are left searching only the title, and presumably searching primarily for the disease name.

# Methodology—

Why can we only retrieve only approximately 60% of rare disease articles using the various disease names? Are we missing additional naming conventions? Is disease naming responsible for difficulty in retrieving these articles? If we remove the articles containing  the disease names we know about and cluster the articles, what happens? What do we see?

751 Articles were collected for the rare disease Spinal Bulbar Muscular Atrophy-- a rare disease primarily affecting males. Articles were searched on PubMed using various known names for the disease. The results were uploaded from a csv file into a python environment, where titles were then cleaned of stop-words, like: and, or, but, the, and so forth. 

Cluster analysis using a TF-IDF matrix:

Once the stop-words--both common and custom-- were removed, words lowered, numbers removed, and punctuation removed using my software available in my GIT Library, a TF-IDF matrix was formed with SKLEARN. Then, K-Means+ was used to find articles that were similar.

Finally, mpld3 was used to generate a visualization using matplotlib.

# Outcome—

In the cluster that was created we find some surprises. There is a large grey cluster in the top left. After reading the description of SBMA, I realized the terms that are appearing in the title are pathophysiological terms! Indeed, we see Polyglutamine Expansion/Expanded and Androgen Receptor. Compare this to the pathophysiological definition from WikiPedia:

"The mechanism behind SBMA is caused by expansion of a CAG repeat in the first exon of the androgen receptor gene (trinucleotide repeats). The CAG repeat encodes a polyglutamine tract in the androgen receptor protein. The greater the expansion of the CAG repeat, the earlier the disease onset and more severe the disease manifestations. The repeat expansion likely causes a toxic gain of function in the receptor protein, since loss of receptor function in androgen insensitivity syndrome does not cause motor neuron degeneration."

We also see the terms trinucleotide and CAG Repeat. Maybe we are on to something. It appears that pathophysiological terms that are distinct for a disease can be used to improve article retrieval, but how?

# PART II--Jena Model:

# Abstract— 
At Indiana University, I had carte blanche in choosing data and topics. I took a Semantic Web Technology class and was exploring JENA, RDF, OWL and XML, etc. Could a semantic web application increase article retrieval? Spoiler: Yes it can!
# Methodology— 
In Part I we found that almost 40% of article titles from the SBMA articles contained pathophysiological terms. These terms we extracted from the cluster analysis were then "attached" to each article title, if the term was contained in the title. Once this was done, a java program was used to turn each set of article title, and phrase into an xml file.
Protégé was used to develop an ontology for the model. owl:sameAs was used to link all of the disease names. Then Jena (a semantic web application) was used to reason over the rdfs and owl file.
# Outcome— 
Once the Fuseki server was running, we could return 100% of the articles using the disease name alone. It didn’t matter which name. Furthermore, on PubMed, if we search for the disease name SBMA, we get 67 results. In our model we get all 546 that we were able to find pathophysiological terms for.

# Installation Cluster Analysis in Jupyter:
Requirements:
You need to have the following python packages installed either by pip or conda install:
1) mpld3
2) nltk
3) sklearn and matplotlib, if not using Anaconda.

Navigate to Cluster Analysis folder and open WIAN cluster_analysis.ipynb in your Jupyter/Ipython environment.

# Installation Ontology Search Tool:
Rare Disease Ontology and Search tool is a Jena-model-driven application for article retrieval. 

How to Run (also see documentation in unzipped file):

Requirements:
1) Requires Jena 3.0.1
2) Requires OpenCsv jarfile, which I included in this same directory. Both of these items need to be on build path.

The main class is JenaModelCreationMain. Run this class after adding above to build path. This will run the other methods and classes and create the TDB database.

1) Download RDOST.zip and extract files.
2) Download fuskei-server.jar file.
3) You will need to move the fuseki-server.jar to RDOST/fuseki. Then follow instructions in README in zip file, reproduced below.
Run the bootstrap.sh file to load the Fuseki Server.
Navigate to localhost:3030 on your browser, then select pubmed. Articles to query.
