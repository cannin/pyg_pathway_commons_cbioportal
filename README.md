If you make use of this dataset, please cite the Zenodo DOI: https://zenodo.org/record/8251328

# PyTorch Geometric Example Dataset using Pathway Commons and cBioPortal

This is a dataset that was generated by integrating the breast cancer (BRCA TCGA) dataset from the cBioPortal ([cbioportal.org](https://www.cbioportal.org/)) and a biological network for node connections from Pathway Commons (www.pathwaycommons.org).
      
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

NB: If you want to do these steps for a different dataset, then you have to download the required data from the sites. You can see how to download from cBioportal here: https://github.com/cBioPortal/datahub/tree/master

2. Data Preprocessing: The steps that were followed after downloading the required datasets are shown in the notebook below.
   https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/breast_cancer_preprocesing.ipynb

3. Data Integration: To convert to a PyG Dataset, a list of graphs were created from the preprocessed dataset first. Then these graphs were 
    converted to data objects. These steps are shown in the python script below.
    https://github.com/cannin/pyg_pathway_commons_cbioportal/blob/main/breast_invasive_carcinoma_brca.py

