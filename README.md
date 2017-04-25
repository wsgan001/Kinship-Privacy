# hierclustering_opensnp.r 
 R code that applies hierchical clustering on opensnp data (VCF format).
# hide_snps.r
R code that generates kinship and outlier constraints. It can solve the optimization model if outlier constraints are relaxed.  If kinship constraints are relaxed, those constraints become non-linear. Unfortunately, Rcplex cannot solve non-linear constrainted integer programming problems, so this R code only generates the constraints and writes to txt files and then ga_lp2.m code is used to find minimum phi value that satisfies given non-linear constraints. We replace the optimal phi value into non_linear kinship constraints and make them linear. When the problem becomes linear with found phi value, we can solve original problem in Rcplex.
These cases are denoted as choice variable:
If choice = 0 , solve the problem where outlier constraints are relaxed and kinship constraints are satisfied. (This is linear integer programming problem). Also minimize slack variables (quantity of being outliers.)
If choice = 1, Solution is based on relaxing kinship constraints and satisfying outlier constraints. Generate constraints to find optimal phi value. (This is a non-linear constrained integer problem). Use those constraints in Matlab.
If choice = 2, solve the original problem by replacing optimal phi value found in the previous step. (This is linear integer programming problem). 
