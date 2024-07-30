# project4-team1: [INSERT TITLE HERE]
Geneticists have identified locations in the human genome that can assess an individual's ancestry, called ancestry-informative single nucleotide polymorphisms (AISNPs). These locations, denoted by rsid numbers, display ancestry-specific variation. However, there is debate as to how many AISNPs are sufficent to determine an individual's ancestry with some researchers, notably Kidd et al (2014) identifying 55 AISNPs, whilst others, notably Seldin et al (2011), identifying 128 AISNPs.

The 1000 Genomes Project provides a unique opportunity to test the discriminatory power of AISNPs for the determination of an individual's ancestry. This project is an international research effort aimed at cataloging human genetic variation by sequencing the genomes of approximately 2,500 persons from various populations worldwide. The recruitment and data collection took place between 2008 and 2015. More information on the overall project can be found in the 1000 Genomes Project reference below.




## Installation and Run Instructions:
You may need to install the following dependencies before commencing:

### Amazon Web Services Command Line Interface:
!pip install awscli


## Usage Instructions:
This repo contains the following datasets, saved in the Resources subfolder:
* **1000genomes_populations.csv:** a broadcast table containing data on the population types, population codes, and superpopulation codes for each ancestry group.

* **1000genomes_superpopulations.csv:** a broadcast table containing data on the superpopulation types and codes for each ancestry group.
  
* **kidd_combined.csv:** a dataset combining the test and train datasets from Kidd et al (2014).
  * **kidd_test.csv:** the test dataset from Kidd et al (2014).
  * **kidd_train.csv:** the train dataset from Kidd et al (2014).
    
* **seldin_combined.csv:** a dataset combining the test and train datasets from Seldin et al (2011).
  * **seldin_test.csv:** the test dataset from Seldin et al (2011).
  * **seldin_train.csv:** the train dataset from Seldin et al (2011).

This repo contains the following executable scripts:
1. **Install_1000genomes.ipynb:** a python script, executable in Jupyter Notebook, required to:
    * Download the **1000genomes_populations** and **1000genomes_superpopulations** data from the 1000 Genomes Project AWS S3 Bucket;
    * Convert the **1000genomes_populations** and **1000genomes_superpopulations** data into Pandas DataFrames;
    * Save the **1000genomes_populations** and **1000genomes_superpopulations** data as .csv files into the Resources subfolder;
    * Read the **kidd_test.csv** and **kidd_train.csv**, merging these using the pd.merge() function to create the **kidd_combined.csv** dataset;
    * Read the **seldin_test.csv** and **seldin_train.csv**, merging these using the pd.merge() function to create the **seldin_combined.csv** dataset;
    * Convert the **kidd_combined.csv** and **seldin_combined.csv** datasets into Pandas DataFrames, and;
    * Save the **kidd_combined.csv** and **seldin_combined.csv** datasets as .csv files into the Resources subfolder.

## Overview of the Analysis:
The overall purposes of this analyses are to:
* Preprocess the datasets using one-hot encoding to prepare for machine learning;
* Perform feature selection to identify the most informative SNPs using unsupervised machine learning techniques.
* Build and train a supervised machine learning model to predict an individual's ancestry;
* Evaluate the performance of this model on the test datasets using accuracy, precision, recall, and the F1-score, and;
* Create a series of plots to visualise the ancestry distributions of individuals in the 1000 Genomes Project.


## Results:
Description and screenshots ...


## Summary:
Details here ...


## Credits:
This code was compiled and written by Violet Bui, Elizabeth Dashwood, Mark Peck, and Katrina Witt for project 4 in the 2024 edX Data Analytics Boot Camp hosted by Monash University. Additional credits are declared below:

### 1000 Genomes Project:
The 1000 Genomes Project Consortium. (2015). A Global Refernce for Human Genetic Variation. Nature, 526, 68-74. https://doi.org/10.1038/nature15393 (accessed 25 July 2024).

### 1000 Genomes (Data):
https://www.internationalgenome.org/using-1000-genomes-data/ (accessed 25 July 2024).

### 1000 Genomes Ancestry (Data):
Arvai K. (2024). 1000 Genomes Ancestry. Kaggle. https://kaggle.com/competitions/1000-genomes-ancestry (accessed 29 July 2024).

### Kidd et al (2014):
Kidd KK., et al. (2014). Progress toward an efficient panel of SNPs for ancestry inference. Forensic Sci Int Genet, 10: 23-32. https://doi.org/10.1016/j.fsigen.2014.01.002 (accessed 29 July 2024).

### Seldin et al (2011):
Kosoy R., ... Seldin MF. (2011). Ancestry informative marker sets for determining continental origin and admixture proportions in common populations in America. Hum Mutat, 30: 69-78. https://doi.org/10.1002/humu.20822 (accessed 29 July 2024).


