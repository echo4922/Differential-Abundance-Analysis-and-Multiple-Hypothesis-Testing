# Differential-Abundance-Analysis-and-Multiple-Hypothesis-Testing

Differential abundance analysis (DAA) is one of the statistical analyses performed in metagenomics studies for microbiome data (Source: original paper by Yang & Chen). Consequently, the CoDA is applied to the DAA. Given the study utilizes the compositional approach, the DAA was performed for the statistical analysis to test significance between two amyloid beta peptides. The figure below shows the workflow:

![DAA](https://github.com/echo4922/Differential-Abundance-Analysis-and-Multiple-Hypothesis-Testing/assets/112420424/a3526703-5014-41e6-8952-b0d358e216a1)

Because the assumptions of parametric statistical methods are not satisfied in sequencing data, nonparametric statistics should be considered. Also known as the Mann-Whitney U test, the Wilcoxon rank-sum test is a nonparametric alternative to a two-sample t-test. The Wilcoxon rank-sum test uses ranking of observations (hence, the name “rank”). While the t-test is used to test whether the means of two populations are equal, in the Wilcoxon rank-sum test, medians of populations are used to test the hypothesis.

The following is the null hypothesis (H0) and the alternative hypothesis (H1): <br />
H0= The medians of two populations are equal.	<br />
H1= The medians of two populations are NOT equal. <br />

In the Wilcoxon rank-sum test, one of the ways to obtain the p-value is the z approximation method to determine the p-value; the z-score is converted to the p-value.  The other method of obtaining the p-value is an exact method. The Wilcoxon rank-sum test is a six-step process (Source: datatab.net). First, samples or observations of data are ranked from smallest to largest. Second, the ranks are added for each group. The test statistic, W, is calculated for each group using a ranked sum. Third, the expected value is calculated. Fourth, the standard error is obtained. If the p-value is obtained with the z-score, then it is computed using the test statistic W, the expected value of W, and the standard error of W. The z-score is lastly converted to the p-value. For the exact method to obtain the p-value, the last step is determined from the distribution of the Wilcoxon rank-sum statistic (Source: University of Virginia Library).

In statistics, 0.05 is commonly used as the p-value to determine the significance. In other words, there is a 1 in 20 chance of obtaining significance by chance. To correct this issue, the Benjamini-Hochberg (BH) correction is applied to the p-value. The BH correction applied p-values are called adjusted p-values. This procedure is important in multiple hypothesis testing where multiple hypothesis tests are performed simultaneously (Source:  Columbia University Mailman School of Public Health). This inherently increases a type I error; the null hypothesis is rejected when it should not be rejected. The type I error leads to false positive statistical results. The BH procedure is a four-step process. First, original p-values are sorted from smallest values to largest values. Second, a rank is assigned to the sorted list; the smallest p-value is given rank 1. Third, the Benjamini-Hochberg (B-H) critical value is calculated. The false discovery rate (FDR) is defined as the “expected proportion of discoveries which are falsely rejected” (Source: original paper by Korthauer et al). The “discoveries” refer to the significant results. Lastly, the original p-values are compared to the B-H critical values and the biggest p-value smaller than the B-H critical value becomes the adjusted p-value (Source: LibreTexts Statistics). 

In the study, 20 genes of interest were handpicked for the DAA. The list was selected as genes of interest originated from differential gene expression analysis (DESeq2) with minimum 0.5 log fold changes (base 2). This is equivalent with 40% of increased gene expressions in DESeq2. Once the list was chosen, the raw features of the genes were used for the CLR transformation then the Wilcoxon rank-sum test was performed because the DAA works based on the CoDA. T The count matrix needed to be transposed such that the first column designates groups (control or condition), and the rest of the columns designates each gene to properly perform the Wilcoxon rank-sum test. In R programming, each gene ID was used for the dependent variable while the groups were used for the independent variable.



References: <br />
Paper by Yang Chen: https://doi.org/10.1186/s40168-022-01320-0 <br />
Mann-Whitney U Test: https://datatab.net/tutorial/mann-whitney-u-test <br />
Wilcoxon Rank Sum Test: https://library.virginia.edu/data/articles/the-wilcoxon-rank-sum-test <br />
False discovery rate (Columbia University Mailman School of Public Health): https://www.publichealth.columbia.edu/research/population-health-methods/false-discovery-rate <br />
Paper by Korthauer et al: https://doi.org/10.1186/s13059-019-1716-1 <br />
Multiple Hypothesis Testing: https://stats.libretexts.org/Bookshelves/Applied_Statistics/Biological_Statistics_(McDonald)/06%3A_Multiple_Tests/6.01%3A_Multiple_Comparisons
