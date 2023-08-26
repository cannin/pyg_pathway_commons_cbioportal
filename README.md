If you make use of this dataset, please cite the Zenodo DOI: https://zenodo.org/record/8251328

This is a project that was carried out during Google Summer of Code(GSoC'23). The main repository for this project is: https://github.com/cannin/gsoc_2023_pytorch_pathway_commons

# PyTorch Geometric Example Dataset using Pathway Commons and cBioPortal

This is a dataset that was generated by integrating the breast cancer (BRCA TCGA) dataset from the cBioPortal ([cbioportal.org](https://www.cbioportal.org/)) and a biological network 
for node connections from Pathway Commons (www.pathwaycommons.org).
      
Data was preprocessed to form one dataset that could be converted to PyTorch Geometric data objects.

This data was retrieved in the CSV format, then processed to form a graph-based dataset for use with Graph Neural Networks (GNN).

The dataset contains the gene features of each patient and the overall survival time (in months) of each patient, which are the labels.

#  Pipeline From Data Collection to Model Building

This is a set of notebooks that shows how data was collected, preprocessed and integrated, then converted to PyTorch Geometric Dataset

## Overview of Repository
1. Data Collection: The Datasets that were collected from cbioportal and Pathway Commons are:
   
   - Reactome subset from Pathway Commons: https://www.pathwaycommons.org/archives/PC2/v12/PathwayCommons12.reactome.hgnc.sif.gz
     
   - brca_tcga_pan_can_atlas_2018(data_clinical_patient.txt, data_clinical_patient.txt and data_mrna_seq_v2_rsem.txt): 
     https://github.com/cBioPortal/datahub/tree/master/public/brca_tcga_pan_can_atlas_2018
     
   To have access to these datasets without having to go through the process needed to download datasets from cBioportal, you can access 
   them on Zenodo: https://zenodo.org/record/8251328

   NB: If you want to do these steps for a different dataset, then you have to download the required data from the sites. You can see how to download from cBioportal here: 
   https://github.com/cBioPortal/datahub/tree/master

2. Data Preprocessing: For the creation of this sample dataset, the data_clinical_patient.txt and data_clinical_patient.txt were merged based on the patient identifier.
   After which, the only columns kept were the sample identifier, patient identifier and overall survival(months) of each patient.
   Next, the merged dataset was merged with the data_mrna_seq_v2_rsem.txt on the sample identifiers. 
   Then this new dataset was splitted into X and y which represents features and labels.
   In this notebook, work was also done on creating training, test and validation splits for modelling using the 60:20:20 rule.

   The final results gotten from these steps include:

   - X_train, y_train, X_val, y_val, X_test, y_test.
   
   - Gene features: graph_idx
     
   - Labels: graph_labels
     
   - edges: edge_index

   All the datasets can be accessed here: https://zenodo.org/record/8251328

   The steps that were followed after downloading the required datasets are shown in the notebook below.
   https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/breast_cancer_preprocesing.ipynb

4. Data Integration: To convert to a PyG Dataset, a list of graphs were created from the preprocessed dataset first.
   Then these graphs were converted to data objects. These steps are shown in the provided notebook.
   For further integration with the PyG provided datasets, the notebook was converted to a python script which can be accessed below.

   Notebook for Integration: https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/InMemoryDataset_Class_with_brca_tcga.ipynb
   
   Python Script for Dataset: https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/breast_invasive_carcinoma_brca.py
   
   The final Result gotten from these have benn uploaded to the Zenodo site and can be downloaded with this link: 

   The zipped file contains of the 3 main datasets used for the integration:

    1. graph_idx: This consists the gene features of the patients. It was gotten by preprocessing the datasets from cBioportal
       
    2. graph_labels: This consists of the overall survival(months) of each patient. It was also gotten from the preprocessing done on cBioportal
       
    3. edge_index: This consists of the total edges. It was gotten from the preprocessing of the Pathway Commons dataset
  
6. Modelling: The dataset was then used for modelling. First a baseline model was created using FLAML, then a Graph Neural Network(GNN) model was built using GCNConv.
   The two notebooks below show the modelling steps that was carried out.

   Baseline model: https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/baseline_model_with_brca_data.ipynb

   GNN model: https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/modelling_with_breast_cancer_data.ipynb

## Please Note:
   Different GNN models were tried out using this dataset and different experiments such as hyperparameter tuning was carried out to determine best model. To see these other changes,
   please refer to the main repository for this GSOC project: https://github.com/cannin/gsoc_2023_pytorch_pathway_commons

