# TFM_scripts

The **aim** of this scripts is to perform a statistical analysis of untargeted metabolomics data obtained from a sample analysis performed with the Orbitrap<sup>TM</sup> QExactive<sup>TM</sup> Plus and the analysis software Compound Discover<sup>(R)</sup>. These scripts have been optimized to study Ochratoxin A (OTA)-associated metabolites  by using RStudio, with packages "Limma" and "mixOmics".

## Using these scripts you will be able to pass form dataset with Areas Under the Curve values to a complete Univariate and Multivariate Statistical Analyses results. 

### Targeted metabolomic analysis:

This preliminary step consists of identifying the conditions under which OTA occurrence was detected throughout the sampling days. This information can be used to prepare the following comparisons. 

### Raw data pretreatment:

The first step consist in prepare raw dataset obatined from software Compound Discover<sup>(R)</sup> to datasets with the structure needed in the statistical analyses. This preparation step is performed with the script "Prepare_Datasets_to_Statistical_Analysis.Rmd". 

### Univariate and Multivariate Statistical Analyses:

After preparation of the data sets, the script "Metabolomic_analysis.Rmd" will be used, which will perform the following tasks:

1. Read the raw data files from the input folder.
2. Normalize data set with the package "NormalyzerDE" without the need of a design input (it is created with the information given in the input files).
3. After the **review and evaluation of the normalization report by the researcher**, the _**selected data normalized is uploaded by changing line 183**_ with the corresponding file. You can choose among the following options: _CycLoess-normalized.txt, GI-normalized.txt, log2-normalized.txt, mean-normalized.txt, median-normalized.txt, Quantile-normalized.txt, RLR-normalized.txt, VSN-normalized.txt_. If you do not want to use any normalized file, then set it as _"None"_.
4. Exploratory analysis before and after the normalization with box plot from "NormalyMets" package. Principal Component Analysis (PCA) and Hierarchical Cluster Analysis (HCA) from packages "FactoMineR" and "factoextra" for normalized dataset to check the right group differentiation and a possible batch effect.
   
#### Univariate Statistical Analysis:
5. Statistical analysis, using the "Limma" package, performed to extract the **p-values** and **log2 fold change values (LFC)** for every metabolite in the conducted comparative analysis. Additionally, p-value adjustment methods, such as Benjamini-Hochberg, Bonferroni, and q-values were applied. Tables with the results are given, as well as plots displaying the original p-values and q-values, which are available for visualization.
6. The identification of significant metabolites will be based on the statistical thresholds set at point 4 of the usage instructions. A message will be displayed indicating the number of decreased and increased metabolites for each adjustment method, taking into account the linear model used in the Limma analysis. This will provide insights into the directionality of differential expression for the identified metabolites. _[As the test model was set up as_"contrast <- paste0(group[2],"-",group[1])". _This instruction represent the measures difference in expression levels between Group 2 and Group 1. A positive LFC indicates higher expression in Group 2 compared to Group 1, while a negative LFC indicates higher expression in Group 1 compared to Group 2. The magnitude of the LFC represents the change in expression between the two groups.]_ The number of significant differences will be represented by venn-diagrams ("ggVennDiagram" package) and upset plot ("UpSetR" package).
7. After having **selected a p-value adjustment method in line 750**, the significant metabolites based on the statistical thresholds will be plotted by Mean-Average plots and Volcano plots, also a dynamic volcano plot is displayed where you can see the information for each dot (metabolite). Tables with the 10 most significant metabolites for each comparative will be displayed.

#### Multivariate Statistical Analysis:
8. Finally, a sparse Partial Least Squares Discriminant Analysis (sPLS-DA) will be conducted using the "mixOmics" package. This analysis uses 2 components and 25 variables. The results for the sPLS-DA analysis include a loadings plot, individual samples plot, variable plot, and a prediction essay. Additionally, predictions results and the top 10 most important variable predictors for each comparative will be presented in tables, providing valuable insights into the predictive power of the model and the variables driving the differences between the comparatives.

### Additional scripts:

With the additional scripts you can use the data obtained in the previous analysis to compare the results of the studied comparisons. And also with the results obtained from a MetaboAnalyst study: https://www.metaboanalyst.ca/MetaboAnalyst/ModuleView.xhtml.

