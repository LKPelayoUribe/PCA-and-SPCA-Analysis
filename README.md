# PCA-and-SPCA-Analysis
High Dimensional Data Learning &amp; Visualization Project - Applying PCA and SPCA methods to a cancer dataset and PCA to a dataset containing spam email. 

# STAT 437 - Project 2
This research paper studies cancer prediction from gene expression data using PCA (Principal component analysis) and SPCA (Sparse principal component analysis) methods, and a data set containing spam email was analyzed with PCA. 

### By: Shawn Petersen and Laura K. Pelayo Uribe

# Datasource, approach and cleaning.
- The first data set was the Gene Expression Cancer RNA-Seq Data Set which is hosted by the UC Irvine Machine Learning Repository. This data set consists of 801 cancer patients, each exhibiting one of five types of cancer. For each patient, 20,531 gene expressions are recorded as real-valued features.
gene expression cancer RNA-Seq. (2016). UCI Machine Learning Repository, https://archive-beta.ics.uci.edu/ml/datasets/gene+expression+cancer+rna+seq
- The second data set used in this analysis was the Spam Data Set, which is also hosted by the UC Irvine Machine Learning Repository. This data set has 4,601 emails which are described by 57 real-valued features, each of which is labeled (tagged) spam or non-spam.
Hopkins,Mark, Reeber,Erik, Forman,George & Suermondt,Jaap. (1999). Spambase. UCI Machine Learning Repository, https://archive-beta.ics.uci.edu/dataset/94/spambase

PCA was used as a tool for finding patterns in high-dimensional data, such as the dataset provided for this project on the cancer gene and email spam.

For this project, genes that contained less than 300 values of 0’s were selected for the data set. From the remaining set, 1000 genes were randomly selected for a more manageable data set to analyze with the various techniques. The data was also scaled to minimize the effects that relatively large values have on clustering metrics.

# PCA & SPCA for Patterns in Cancer Data
PCA and SPCA are applied to the sub-data set to analyze patterns in cancer genes. The resulting dataset was used for the following analyses with PCA and SPCA. PCA was applied to the data resulting in 801 principal components in total, one per sample. The variance was calculated for each of the principal components, ordered by eigenvalues. A plot of the first two principal component scores was created. Looking at the visualization of the scores for the first two components class clusters we can clearly see, which KIRC and COAD appear to be the most distinct, with the other 3 classes, BRCA, LUAD, and PRAD, having a significant amount of overlap. Both of these plots can be seen below in **Figure 1** and **Figure 2**: 
**Figure 3** is a graph of the PCA eigenvalues, which is telling how much variance there is in the data in that direction for each PCA. The plot shows the first 10 PCA dimensions, the first two PCAs have a total of 21.9% of the variation. 

<img src="https://raw.githubusercontent.com/LKPelayoUribe/PCA-and-SPCA-Analysis/main/Cancer_PCA_Scores.PNG">
<img src="https://raw.githubusercontent.com/LKPelayoUribe/PCA-and-SPCA-Analysis/main/Cancer_PCA_Eigenvalues.PNG">

The first 8 principal components (of 801) were calculated at %49 of the total explained variance. The graph shows a significant amount of the information that characterizes the cancer gene data is present in relatively few principal components. Observation:
- The cancer gene score plot visualized clusters for each of the cancer classes. KIRC and COAD gene samples were the most distinct clusters of all the gene classes, having little overlap with other classes.
- The other three classes, BRCA, LUAD, and PRAD overlap heavily.
- The class with the largest dispersion was BRCA which spanned the largest range across positive and negative PC2 scores.

SPCA was also calculated by the elasticnet::spca function for comparison with the PCA results. For this calculation, the adjusted partial variance explained as well as the adjusted cumulative partial variance explained were computed and plotted. A score plot of the first 2 sparse principal components was also created, similar to that which was constructed for the PCA section. Both of these plots can be seen below in **Figure 4** and **Figure 5**:

<img src="https://raw.githubusercontent.com/LKPelayoUribe/PCA-and-SPCA-Analysis/main/Cancer_SPCA.PNG">

Comparing the results between PCA and SPCA, we see that even though the first 6 sparse PCs account for less than 40% of the variance explained, which was less than that of classical PCA at 49% for the same number of components. The score plots are still very similar for the PCA and SPCA plots. It can be seen clearly clusters of the cancer gean class with KIRC samples being the most distinctly different.

# PCA for Spam Detector
For the spam experiment, PCA was applied to email data to determine whether emails can be reliably classified as spam or non-spam. The first step of this section was to load the data and remove the *testid* column which contained sample labels predicted during a previous analysis. The data were checked for missing values, and none were found. 
**Figure 6** shows the highly correlated features in the form of a correlation matrix.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/PCA-and-SPCA-Analysis/main/Corr_SPAM.PNG">

The cumulative variance of each principal component was computed and plotted, as seen in figures **Figure 7** and **Figure 8**. The first two principal components only accounted for 18.5% of the spam variance. The score plot of these principal components shows a clear pattern where each class label, spam vs. non-spam. Both were clustered and visually separated. The samples with TRUE PC1 scores and FALSE PC2 scores were clearly labeled as spam.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/PCA-and-SPCA-Analysis/main/SPAM_PCA_Scores.PNG">

**Figure 9** is a graph of the PCA eigenvalues, which is telling how much variance there is in the data in that direction for each PCA. The plot shows the first 10 PCA dimensions, the first two PCAs have a total of 18.7% of the variation. 

<img src="https://raw.githubusercontent.com/LKPelayoUribe/PCA-and-SPCA-Analysis/main/SPAM_PCA_Eigenvalues.PNG">

# Conclusion
High-dimensional data is becoming increasingly common in many fields. Often, the presentation of high dimensional data can be inadequate. We find a redundancy of information and it is not always easy to process big data effectively. A common approach is to apply a dimension reduction technique that will model our data in a lower dimensional setting, that captures the core importance of our data. Principle component analysis (PCA) tries to explain the variance found in our data. PCA helps us remove noise from our data and we are also able to efficiently create consistent 2-D visualizations. PCA is an important place to start with any unsupervised learning, but not all datasets will work well with PCA. 

With our cancer dataset, PCA and SPCA were not very helpful. KIRC and COAD gene samples had the clearest clusters compared to the other three classes, BRCA, LUAD, and PRAD. Looking at our eigenvalues chart **figure 3**, it is easy to understand why. The variance of our data is evenly spread and there isn’t specifically one or two components that explain the majority of how our data is behaving. On the other hand, for our SPAM dataset, there is some overlap with TRUE and FALSE, but overall, there is a clear distinction between an email that is classified as spam or not when we look at our graph **figure 7**. If we also look at our eigenvalues chart **figure 9**, we can see that the majority of variance is explained with the first two principal components.
