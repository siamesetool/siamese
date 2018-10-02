# Siamese
Siamese (**S**calable, **i**ncremental, **a**nd **m**ulti-repr**ese**ntation) is a code clone search engine.

## Why it's good?
It works with multiple representations of source code to capture code
similarity at different structural levels and mines token frequencies in a code
corpus on-the-fly and automatically adjusts a query's length to improve the
search speed and accuracy. The tool is scalable to a corpus of hundreds million lines of code and return the results within seconds. It also allows incremental updates to its index to support changes in the software project being analysed.

## Downloads
* **Tool**:
    * **Siamese:** Siamese executable can be downloaded here: [Siamese v. 0.6](https://drive.google.com/open?id=1lQX4SvQbxi9WYH4ndRilc_s45gBsi0Sx). Please make sure you have Java 8 installed on your machine. 
    
        1\. To execute Siamese, unzip the file and follow the steps below:
        ```bash
        $cd siamese
        $./elasticsearch-2.2.0/bin/elasticsearch -d
        $java -jar siamese-0.0.5-SNAPSHOT.jar
        ```
        Then you'll see the usage and example of how to use Siamese.
        ```
        usage: (v 0.5) $java -jar siamese.jar -cf <config file> [-i input] [-o output] [-c command] [-h help]
          Example: java -jar siamese.jar -cf config.properties
          Example: java -jar siamese.jar -cf config.properties -i /my/input/dir -o /my/output/dir -c index
           -c,--command <arg>        [optional] command to execute [index, search].
                                     This will override the configuration file.
           -cf,--configFile <arg>    [* requried *] a configuration file
           -h,--help                 <optional> print help
           -i,--inputFolder <arg>    [optional] location of the input files (for
                                     index or query). This will override the
                                     configuration file.
           -o,--outputFolder <arg>   [optional] location of the search result file.
                                     This will override the configuration file.
        ```
        2\. An example of running Siamese to index a project "foo".
    
        ```bash
        java -jar siamese-0.0.6-SNAPSHOT.jar -c index -i /my/dir/foo -cf config.properties
        ```
    
        3\. Then, tell Siamese to search for clones of "foo" in "bar".
        ```bash
        java -jar siamese-0.0.6-SNAPSHOT.jar -c search -i /my/dir/bar -o /my/output/dir -cf config.properties
        ```

        4\. After Siamese finishes its execution, the output file (clone classes) will be located at ```/my/output/dir```.
        The file will be using the pattern ```data_qr_<timestamp>.xml```.

        5\. If you want to enforce similarity threshold on the search results, 
        modify the ```config.properties``` file to enable fuzzywuzzy or tokenratio (recommended) similarity.
        Choose any similarity thresholds you like for the four code representations (r0, r1, r2, r3) respectively.
    
        ```bash
        computeSimilarity : tokenratio
        simThreshold      : 50%,50%,50%,50%
        ```
    
    * **BigCloneEval:** BigCloneEval is a tool for automated recall evaluation based on BigCloneBench data set. It can be downloaded from: [BigCloneBench](https://github.com/jeffsvajlenko/BigCloneEval)
* **Data sets**: the data sets that we used to evaluate Siamese are listed below:
    * **OCD (Obfuscation/Compilcation/Decompilation)** data set. The OCD data set is from a study by Ragkhitwetsagul et al. and can be found here: [OCD data set](http://crest.cs.ucl.ac.uk/resources/cloplag/).
    * **SOCO (SOurce COde Re-use)** data set. The SOCO data set was created for the detection of source code reuse competition and can be downloaded here: [SOCO](http://users.dsic.upv.es/grupos/nle/soco/). However, the clone oracle has some issues which Ragkhitwetsagul et al. found and fixed. Please download the corrected clone oracle from: [Fixed clone oracle](http://crest.cs.ucl.ac.uk/fileadmin/crest/cloplag/soco_train_clones_fixed.txt).
    * **BigCloneBench** data set. The BigCloneBench is created by Svajlenko et al., it is one of the largest clone benchmarks available to date. It is created from IJaDataset 2.0 of 25,000 Java systems. The benchmark contains 2.8 million files with 8 million manually validated clone pairs of type-1 up to type-4. The data set and the clone oracle can be downloaded here: [BigCloneBench](https://github.com/jeffsvajlenko/BigCloneEval).
    * **GitHub** data set. We used 131,307 GitHub Java projects to evaluate Siamese's incremental update module. Since the projects are all open source, you can download the GitHub projects from [GitHub](https://github.com) directly.
