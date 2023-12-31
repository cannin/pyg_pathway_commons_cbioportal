If you make use of this dataset, please cite the Zenodo DOI: https://zenodo.org/record/8251328

This is a project that was carried out during Google Summer of Code(GSoC'23). The main repository for this project is: https://github.com/cannin/gsoc_2023_pytorch_pathway_commons

# PyTorch Geometric Example Dataset using Pathway Commons and cBioPortal

This is a dataset that was generated by integrating the breast cancer (BRCA TCGA) dataset from the cBioPortal ([cbioportal.org](https://www.cbioportal.org/)) and a biological network for node connections from Pathway Commons (www.pathwaycommons.org). 

Data was preprocessed to form one dataset that could be converted to PyTorch Geometric data objects.

This data was retrieved in the CSV format, then processed to form a graph-based dataset for use with Graph Neural Networks (GNN).

The dataset contains the gene features of each patient and the overall survival time (months) of each patient, which are the labels.

#  Pipeline From Data Collection to Model Building

This is a set of notebooks that shows how data was collected, pre-processed and integrated, then converted to PyTorch Geometric Dataset

## Overview of Repository
1. Data Collection: The datasets are from cBioPortal and Pathway Commons:
   
   - Reactome subset from Pathway Commons: https://www.pathwaycommons.org/archives/PC2/v12/PathwayCommons12.reactome.hgnc.sif.gz
   - brca_tcga_pan_can_atlas_2018 (data_clinical_patient.txt, data_clinical_patient.txt and data_mrna_seq_v2_rsem.txt): 
     https://github.com/cBioPortal/datahub/tree/master/public/brca_tcga_pan_can_atlas_2018
     
   The above files have been archived on Zenodo: https://zenodo.org/record/8251328

   NOTE: The data on cBioPortal uses a consistent format, you can pre-process other datatests from the cBioportal DataHub: https://github.com/cBioPortal/datahub/tree/master

3. Data Preprocessing: For the sample dataset, data_clinical_patient.txt and data_clinical_patient.txt were merged based on the patient identifier. After which, the only columns kept were the sample identifier, patient identifier and overall survival (months) of each patient. Then, the gene expression features (N=9288) that overlapped with biological network data from Pathway Commons were extracted from the data_mrna_seq_v2_rsem.txt dataset, this was then merged with the first merged data based on the sample identifiers. Additionally, overall survival time in months was extracted as the value to be predicted. Then this new dataset was splitted into X and y which represents features and labels. In this stage, work was also done on creating training, test and validation splits for modelling using a 60:20:20 split.

   The final results gotten from these steps include:

   - X_train, y_train, X_val, y_val, X_test, y_test
   - Gene features: graph_idx
   - Labels: graph_labels
   - edges: edge_index

   Processed datasets are here: https://zenodo.org/record/8251328

   The steps that were followed after downloading the required datasets are shown in the notebook below.
   https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/breast_cancer_preprocesing.ipynb

4. Data Integration: In this stage, an edge index (N=271771 edges) was generated using Pathway Commons v12 data in a tabular format. To convert to a PyG Dataset, a list of graphs were created from the pre-processed dataset first. Then, these two data types were integrated which resulted in patient-specific graphs which were then converted into PyG data objects. 
   These steps are shown in the provided notebook. Finally, these graphs are wrapped using the InMemoryDataset class for use with PyG.
   For contribution to PyG Github, the notebook was converted to a python script which can be accessed below.

   Notebook for Integration: https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/InMemoryDataset_Class_with_brca_tcga.ipynb
   
   Python Script for Dataset: https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/breast_invasive_carcinoma_brca.py
   
   The final Result can be downloaded with this link: https://zenodo.org/record/8251328/files/brca_tcga.zip?download=1

   The zipped file contains of the 3 main datasets used for the integration:

    1. graph_idx: gene features of the patients; it was by produced by pre-processing datasets from cBioportal
    2. graph_labels: overall survival(months) of each patient. It was also gotten from the preprocessing done on cBioportal
    3. edge_index: This consists of the total edges; it was by produced by the Pathway Commons dataset
  
6. Modelling: The dataset was then used for modelling. First a baseline model was created using FLAML, then a Graph Neural Network (GNN) model was built using GCNConv.
   The two notebooks below show example modelling
   * Baseline model: https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/baseline_model_with_brca_data.ipynb
   * GNN model: https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/modelling_with_breast_cancer_data.ipynb

## Note: 
Different GNN models were tried out using this dataset and different experiments such as hyperparameter tuning was carried out to determine best model. To see these other changes, please refer to the main repository for this GSOC project: https://github.com/cannin/gsoc_2023_pytorch_pathway_commons

