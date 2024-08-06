# project4-team1: Classifying Ancestry from Genomic Data
Geneticists have identified locations in the human genome that can assess an individual's ancestry, called ancestry-informative single nucleotide polymorphisms (AISNPs). These locations, denoted by rsid numbers, display ancestry-specific variation. However, there is debate as to how many AISNPs are sufficent to determine an individual's ancestry with some researchers, notably Kidd et al (2014) identifying 55 AISNPs, whilst others, notably Seldin et al (2011), identifying 128 AISNPs.

The 1000 Genomes Project provides a unique opportunity to test the discriminatory power of AISNPs for the determination of an individual's ancestry. This project is an international research effort aimed at cataloging human genetic variation by sequencing the genomes of approximately 2,500 persons from various populations worldwide. The recruitment and data collection took place between 2008 and 2015. More information on the overall project can be found in the 1000 Genomes Project reference below.


## Installation and Run Instructions:
You may need to install the following dependencies before commencing:

### Amazon Web Services Command Line Interface:
1. Open **GitBash**
2. Activate your dev environment by typing **conda activate dev**
3. Next, type **pip install awscli**

### Multiple Correspondence Analysis (MCA) package:
1. Open **GitBash**
2. Activate your dev environment by typing **conda activate dev**
3. Next, type **pip install prince**


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

 
This repo also contains the following executable scripts:

1. **Install_1000genomes.ipynb:** a python script, executable in Jupyter Notebook, required to:
    * Download the **1000genomes_populations** and **1000genomes_superpopulations** data from the 1000 Genomes Project AWS S3 Bucket;
    * Convert the **1000genomes_populations** and **1000genomes_superpopulations** data into Pandas DataFrames;
    * Save the **1000genomes_populations** and **1000genomes_superpopulations** data as .csv files into the Resources subfolder;
    * Read the **kidd_test.csv** and **kidd_train.csv**, merging these using the pd.merge() function to create the **kidd_combined.csv** dataset;
    * Read the **seldin_test.csv** and **seldin_train.csv**, merging these using the pd.merge() function to create the **seldin_combined.csv** dataset;
    * Convert the **kidd_combined.csv** and **seldin_combined.csv** datasets into Pandas DataFrames, and;
    * Save the **kidd_combined.csv** and **seldin_combined.csv** datasets as .csv files into the Resources subfolder.
  
2. **PCA.ipynb:** a python script, executable  in Jupyter Notebook, required to:
     * Load the **kidd** and **seldin** .csv files;
     * One-hot encode the features;
     * Explore data saving through generating a sparse matrix;
     * Perform a PCA to evaluate explained variance by principal components;
     * Plot the results of PCA;
     * Calculate an F1-score for a range of PCA principal components;
     * Plot the results of the F1-score calculations;
       
3. **MCA.ipynb:** a python script, executable in Jupyter Notebook, required to:
    * Load the **kidd** and **seldin** .csv files;
    * Define the features (i.e., SNIPS) and labels (i.e., superpopulation);
    * Encode and map the reference and alternate alleles for each SNIP against **dbSNP database** standards;
    * Perform an MCA to identify the optimal number of components to retain;
    * Plot the cumultative explained variance by the number of principal components;
    * Perform an MCA with the optimal number of components;
    * Plot the cumultative explained variance by the number of principal components;
    * Plot the contribution of each SNIP to each principal component;
    * Create Pandas DataFrames of these contributions;
    * Export these contributions as .csv files within the **Exhibits** subfolder as:
       * **kidd_snip_contributions.csv**
       * **seldin_snip_contributions.csv**

4. **NN_Kidd.ipynb** and **NN_Seldin.ipynb:** two python scripts, executable in Jupyter Notebook, required to:
     * Load the **kidd** and **seldin** .csv files;
     * Y
     * Z

5. **Result_counting.ipynb:** a python script to count the interactions between superpopulations
    * Reads in a csv file containing actual superpopulation data and predicted superpopulation data
    * Drops NaN's
    * Calculates a "Path ID" then counts the values when group-by'ing by Path ID
    * Exports to a CSV to drop into Tableau

## Overview of the Analysis:
The overall purposes of this analyses are to:
* Preprocess the datasets using one-hot encoding to prepare for machine learning;
* Perform feature selection to identify the most informative SNPs using unsupervised machine learning techniques.
* Build and train a supervised machine learning model to predict an individual's ancestry;
* Evaluate the performance of this model on the test datasets using accuracy, precision, recall, and the F1-score, and;
* Create a series of plots to visualise the ancestry distributions of individuals in the 1000 Genomes Project.


## Results:
### Data ingestion & storage:
* Data were downloaded from the 1000 Genomes Project AWS S3 Bucket and from Kaggle as .csv files.
* These were converted into Pandas DataFrames, and exported as .csv files to enable further anlysis.

### Data preprocessing:
* Preprocessing was largely ineffective towards the final goal of creating a neural network to predict ancestry based on a range of SNIPs.
* Principal Component Analysis (PCA) generated very low scores for explained variance by 2 or 3 principal components.
* The nature of the data is largely to blame for this, as genomic data is considered to be far too categorical in nature to be effectively handled by PCA.
* Thus, PCA results were not passed on to the final neural network model.

### Dimesionality reduction:
* Given the categorical nature of these data, multiple correspondence analysis (MCA) was used to reduce the number of features.
* Two principal components were identified:
    * The first principal component explained between 61-68% of the variance;
    * The second principal component explained 32-39% of the variance.
* The first principal component contained SNIPs that encode for cardiovascular and diabetes disease risk.
* The second principal component contained SNIPs that encode for cancer risk and obesity.
* Whilst these diseases are known to be linked with ancestry, these components were not considered to be determinitive for ancestry
* Thus, MCA results were not passed on to the final neural network model.

### Classifying ancestry:

### Visualisations:
Visualisations can be seen on the following ![Tableau Dashboard]("https://public.tableau.com/app/profile/violet.bui/viz/shared/WC6BNC323")    
![Screenshot of Tableau Dashboard](TableauScreenshot.png)

## Summary:
The model does well at predicting those of African and South Asian descent. About 5% of the time, the model will predict a European person as a South Asian person instead. The model does not predict those with East Asian heritage or American Heritage well. For someone from East Asia, about 40% of the time, the model will predict that person as South Asian. The model is terrible at predicting heritages from America. It seems to guess an ethnicity at random. If the study considers those who live in North America as American, then this fits as many North Americans have not been in that continent for long enough to be genetically distinct from their possible original continent.


## Data Ethics Statement:
The 1000 Genomes Project Consortium has made this data asset publicly available to all without restrictions (public).


## Credits:
This code was compiled and written by Violet Bui, Elizabeth Dashwood, Mark Peck, and Katrina Witt for project 4 in the 2024 edX Data Analytics Boot Camp hosted by Monash University. Additional credits are declared below:

### 1000 Genomes Project:
The 1000 Genomes Project Consortium. (2015). A Global Refernce for Human Genetic Variation. Nature, 526, 68-74. https://doi.org/10.1038/nature15393 (accessed 25 July 2024).

### 1000 Genomes (Data):
https://www.internationalgenome.org/using-1000-genomes-data/ (accessed 25 July 2024).

### 1000 Genomes Ancestry (Data):
Arvai K. (2024). 1000 Genomes Ancestry. Kaggle. https://kaggle.com/competitions/1000-genomes-ancestry (accessed 29 July 2024).

### dbSNP database (to search for reference/alternate allele combinations by each SNIP):
https://ncbi.nlm.nih.gov/snp/ (accessed 3 August 2024).

### MCA using prince package:
https://pypi.org/project/prince/0.6.2/#multiple-correspondence-analysis-mca (accessed 3 August 2024).

### Kidd et al (2014):
Kidd KK., et al. (2014). Progress toward an efficient panel of SNPs for ancestry inference. Forensic Sci Int Genet, 10: 23-32. https://doi.org/10.1016/j.fsigen.2014.01.002 (accessed 29 July 2024).

### Seldin et al (2011):
Kosoy R., ... Seldin MF. (2011). Ancestry informative marker sets for determining continental origin and admixture proportions in common populations in America. Hum Mutat, 30: 69-78. https://doi.org/10.1002/humu.20822 (accessed 29 July 2024).


