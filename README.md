Compilation environment:

    Intel® Parallel Studio XE Cluster Edition for Linux

To compile the C++ codes, run the following:

    source set_env.sh

    mkdir build

    cd build

    cmake ..

    make
    
**To run the GMM-CorrS**:

    export R_HOME=/usr/lib/R
    
    ./bin/mcmc_multinomial_rd.x n c1 c2 q burnIn iter 1 1 Y_file M_file A_file C1_file C2_file beta_m.ini_file alpha_a.ini_file pi.ini_file Cov_file inv_D_file --no-save

where

n = sample size

c1 = number of covariates in the outcome model

c2 = number of covariates in the mediator model

q = number of mediators

burnIn = iterations for burnIn

iter = total number of iterations

A_file = exposure file containing n-by-1 exposure vector

M_file = mediators file containing n-by-q matrix

Y_file = outcome file containing n-by-1 outcome vector

C1_file = covariate file containing n-by-c1 covariate matrix for the outcome model, with the first column being 1 for the intercept

C2_file = covariate file containing n-by-c2 covariate matrix for the mediator model, with the first column being 1 for the intercept

beta_m.ini_file = initial values for 1-by-q beta_m vector (mediator-outcome coefficients) in the outcome model, 

alpha_a.ini_file = initial values for 1-by-q alpha_a vector (exposure-mediator coefficients) in the mediator model

pi.ini_file = initial values for pi, the proportions of the four Gaussian components

Cov_file = the scale matrix (2-by-2) in the Inverse-wishart prior

inv_D_file = inverse of the estimated D matrix

Please make sure there is no missing or NA values in the above files.

One output file is 'probs_11.txt', which contains the posterior samples of (pi_1, pi_2, pi_3, pi_4) for each j-th mediator, stacked in order.

Another output file is 'results_11.txt', which contains the posterior samples of (beta_mj, alpha_aj, r_j) for each j-th mediator, stacked in order. r_j is the group membership of the j-th mediator.


**To run the GMM-Potts**:

    ./bin/mcmc_potts_rd.x n c1 c2 q burnIn iter 1 1 Y_file M_file A_file C1_file C2_file beta_m.ini_file alpha_a.ini_file pi.ini_file Cov_file theta_0_file theta_1_file neighborMatrix_file

where

n = sample size

c1 = number of covariates in the outcome model

c2 = number of covariates in the mediator model

q = number of mediators

burnIn = iterations for burnIn

iter = total number of iterations

A_file = exposure file containing n-by-1 exposure vector

M_file = mediators file containing n-by-q matrix

Y_file = outcome file containing n-by-1 outcome vector

C1_file = covariate file containing n-by-c1 covariate matrix for the outcome model, with the first column being 1 for the intercept

C2_file = covariate file containing n-by-c2 covariate matrix for the mediator model, with the first column being 1 for the intercept

beta_m.ini_file = initial values for 1-by-q beta_m vector (mediator-outcome coefficients) in the outcome model

alpha_a.ini_file = initial values for 1-by-q alpha_a vector (exposure-mediator coefficients) in the mediator model

pi.ini_file = initial values for pi, the proportions of the four Gaussian components

Cov_file = the rate parameters (2-by-1) in the Inverse-Gamma priors for the variances of the unthresholded beta_m and alpha_a. Both of the shape parameters are set to be 1.1

theta_0_file = initial values for theta_0 (4-by-1)

theta_1_file = initial values for theta_1 (4-by-1)

neighborMatrix_file = estimated q-by-q neighborhood matrix (1 means connected neighbors, 0 means unconnected, non-neighbors)

One output file is 'probs_11.txt', which contains the posterior samples of (pi_1, pi_2, pi_3, pi_4) for each j-th mediator, stacked in order.

Another output file is 'results_11.txt', which contains the posterior samples of (beta_mj, alpha_aj, r_j) for each j-th mediator, stacked in order, r_j is group membership. The following columns contain the posterior samples of beta_a, theta_0, theta_1 and the loglikelihood.



