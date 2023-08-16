# PyTorch Geometric Example Dataset using Pathway Commons and cBioPortal
This is a dataset that was generated by integrating the breast cancer (BRCA TCGA) dataset from the cBioPortal ([cbioportal.org](https://www.cbioportal.org/)) and a biological network for node connections from Pathway Commons (www.pathwaycommons.org).
      
Data was preprocessed to form one dataset that could be converted to PyTorch Geometric data objects.

This data was retrieved in the CSV format, then processed to form a graph-based dataset for use with Graph Neural Networks (GNN).

The dataset contains the gene features of each patient in graph_features and the overall survival time (in months) of each patient, which are the labels.

