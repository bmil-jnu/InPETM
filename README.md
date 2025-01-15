# InPETM

**An integrated analysis using association rule mining and network pharmacology to identify therapeutic combinations of herbal materials and compounds in traditional medicine.**

Traditional medicine (TM) has been used to treat a variety of symptoms and diseases through the combination of herbal materials, and it also contributes to the pharmaceutical industry with several advantages such as fewer side effects and significant cost reductions. However, the rules for combining ingredients are not well organized, and complex multi-compound characteristics make it difficult to understand the pharmacological mechanisms among the herbal materials used in TM. *In silico* approaches that have been proposed to analyze TM and herbal materials require large amount of high-quality structural information or physicochemical properties or have limitations due to ease of interpretation or scope of analysis.

In this work, we proposed an approach named InPETM, that integrates association rule mining (ARM) and network pharmacology analyses to identify polypharamcological effects of herbal materials and compounds from TM. Specifically, InPETM performs analyses combining ARM and network pharmacology-based method at the herb-level and compound-level, respectively, and identifies potential herbal material combination and compound candidates for the phenotype. InPETM provided results of pharmacological effects of herbal material combination and compound and identification of mechanism of action in human protein interactome network, which were confirmed by further structural network analysis and literature review analysis. These results indicate that InPETM can contribute to drug development in TM through better understanding of polypharmacological features of herbal materials. 

## Installation

This source code was tested on the basic environment with:
* python==3.9.7
* conda==4.10.3

It is also recommended to use the following versions of packages:
* numpy==1.24.3
* pandas==2.0.3
* scipy==1.13.1

## Data Statistics

Note: In the full_data and data directories, you can see the raw files used for the preprocessing. The entities and amounts of data provided by each raw file are shown in the following table. Also for COCONUT, herbal material data with biological classifications higher than species are included because they are standardized based on taxonomy identifiers from the NCBI taxonomy database. Therefore, when standardizing the collected herbal material data, all biological classifications were considered and assigned identifiers, but only species and infraspecies were used in the experiment.

* full_data 

|File name|Entity|Amount of data|Note|
|-----|-----|-----|-----|
|prescription.csv|prescription|16260||
|herb_lev_data.csv|herbal material|870|herb-level analysis|
|comp_lev_data.csv|herbal material|9088|compound-level analysis|
|compound.csv|compound|48991||
|gene.csv|gene|25344||
|phenotype.csv|phenotype|17519||
|prescription_phenotype.csv|precription-phenotype|66291|interaction|
|prescription_herb.csv|precription-herb|110497|interaction|
|herb_phenotype.csv|herb-phenotype|407204|interaction|
|herb_compound.csv|herb-compound|1628746|interaction|
|compound_gene.csv|compound-gene|3933224|interaction|
|gene_phenotype.csv|gene-phenotype|2990372|interaction|

* full_ARM_file - preprocessed

|File name|Amount of data|Note|
|-----|-----|-----|-----|
|ARM_herb_dataframe.csv|16260 (prescriptions) x 628 (herbal materials)||
|ARM_compound_dataframe.csv|5187 (herbal materials) x 43454 (compounds)||
|herb_level_DF.csv|16260|dataframe for preprocessing|
|comp_level_DF.csv|5187|dataframe for preprocessing|


* data (Sample)

|File name|Entity|Amount of data|Note|
|-----|-----|-----|-----|
|prescription.csv|prescription|100||
|herb_lev_data.csv|herbal material|100|herb-level analysis|
|comp_lev_data.csv|herbal material|100|compound-level analysis|
|compound.csv|compound|102||
|gene.csv|gene|755||
|phenotype.csv|phenotype|100||
|prescription_phenotype.csv|precription-phenotype|200|interaction|
|prescription_herb.csv|precription-herb|163|interaction|
|herb_phenotype.csv|herb-phenotype|200|interaction|
|herb_compound.csv|herb-compound|31123|interaction|
|compound_gene.csv|compound-gene|3291|interaction|
|gene_phenotype.csv|gene-phenotype|9467|interaction|

* full_ARM_file - preprocessed

|File name|Amount of data|Note|
|-----|-----|-----|-----|
|ARM_herb_dataframe.csv|17 (prescriptions) x 77 (herbal materials)||
|ARM_compound_dataframe.csv|7 (herbal materials) x 49 (compounds)||
|herb_level_DF.csv|17|dataframe for preprocessing|
|comp_level_DF.csv|7|dataframe for preprocessing|



## Getting Started
* In order to get InPETM, please clone this repo:
  
  ```yaml
  git clone git@github.com:lapis423/InPETM.git
  cd InPETM
  ```


* Then unzip the "InPETM.zip", "envs.zip" files into the current directory (\InPETM), and create environment using the 'InPETM.yaml' file.
  
  ```yaml
  unzip InPETM.zip
  unzip envs.zip
  conda env create --file InPETM.yaml
  conda activate InPETM
  ```


* Use the following code to run the integrated analysis for the phenotype. 
  
  ```yaml annotate
  python main.py phenotype_name True  # In 'phenotype_name', write the phenotype you want to analyze. (e.g., asthma, diabetes)
  python main.py phenotype_name False  # False means to use full data instead of sample data.
  ```
Note: Analyzing with full data rather than sample data can take at least several hours, depending on your computer's specifications. If the full_ARM_file directory does not exist, the first run may take even longer. 

## Examples
Try out the following examples:
* **Asthma**

  ```yaml annotate
  # Sample analysis for asthma
  python main.py asthma True  # For sample data, there may be herbal materials or compounds that do not yield results.
  ```
  
  ```
  >>> Inferred Herb combination:  ['Aster tataricus', 'Paeonia lactiflora']
  ```
  
  ```
  >>> * * * Herb-level Network Analysis Results * * *
  >>>              herb                       related disease target genes  ...   z-score proximal
  0  Paeonia lactiflora  [BCL2, SMAD3, RANBP6, SLC25A46, IKZF4, GAB1, G...  ... -3.322159      Yes
  ```

  ```
  >>> * * * Compound-level Network Analysis Results * * *
  >>> compound                       related disease target genes  average distance  ...   z-score  proximal is_in_arm
  0  catechin  [BCL2, SMAD3, RANBP6, SLC25A46, IKZF4, GAB1, G...          1.925926  ... -3.279547       Yes        No
  ```


* **Stroke**

  ```yaml annotate
  # Sample analysis for stroke
  python main.py stroke True  # For sample data, there may be herbal materials or compounds that do not yield results.
  ```
  
  ```
  >>> Inferred Herb combination:  ['Glycyrrhiza uralensis', 'Paeonia suffruticosa']
  ```
  
  ```
  >>> * * * Herb-level Network Analysis Results * * *
  >>>                 herb                       related disease target genes  ...   z-score proximal
  0   Paeonia suffruticosa  [SOD1, MTHFR, ITGA2B, TRIM29, ITGAV, VKORC1, T...  ... -3.581544      Yes
  1  Glycyrrhiza uralensis  [ITGA2B, ITGB3, ALDH2, PLAT, IL1B, ALB, TRIM29...  ... -4.223914      Yes
  ```

  ```
  >>> * * * Compound-level Network Analysis Results * * *
  >>>  compound                       related disease target genes  average distance  ...   z-score  proximal is_in_arm
  1  apigenin  [ITGA2B, ITGB3, ALDH2, PLAT, IL1B, ALB, TRIM29...          1.717949  ... -4.176682       Yes       Yes
  0  catechin  [SOD1, MTHFR, ITGA2B, TRIM29, ITGAV, VKORC1, T...          1.818182  ... -3.422604       Yes        No
  ```


* **Try it on your own**

  Create a txt file in the same format as the files in the UMLS_code directory. Write the UMLS identifiers (starting with C) of the phenotypes you want to analyze in the txt file, line by line, and save it as the name of the phenotype. Use the name of the file to perform your analysis.

  ```yaml annotate
  python main.py phenotype_name False  # For sample data, there may be herbal materials or compounds that do not yield results.
  ```
