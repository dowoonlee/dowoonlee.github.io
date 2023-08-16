---
title: Data generator
tags: artemis7

---


## Stats

- stats

    - binning

        - sturges

            Sturges' formula
            $$ k = \lceil \log_2 n \rceil + 1 $$

        - doane

            Doane's formula
            $$k = 1+\log_2 (n) + \log_2 (1+\frac{|g_1|}{\sigma_{g_1}})$$

            where $g_1$ is the estimated 3rd-momentum skewness and

            $$ \sigma_{g_1} = \sqrt{\frac{6(n-2)}{(n+1)(n+3)}} $$

        - scott

            Scott's normal reference rule

            bin width $h$ is given by

            $$ h = \frac{3.49\hat{\sigma}}{\sqrt[3]{n}} $$

        - freedman_diaconis

            Freedman-Diaconis' choice

            bin width $h$ is given by
            $$ h = 2\frac{IQR}{\sqrt[3]{n}} $$
            which is based on the interquartile range IQR.

    - frechet_inception_distance

        - Background
        
            $$ d_F(\mu, \nu) := \left(\inf_{\gamma \in \Gamma (\mu, \nu)} \int _{\mathbb{R}\times \mathbb{R}} \Vert x-y\Vert^2 d\gamma(x,y)\right)^{1/2}$$

            Where $\Gamma(\mu, \nu)$ is teh setof all measures on $\mathbb{R}\times \mathbb{R}$ with marginals $\mu$ and $\nu$. In other words, it is the 2-Wasserstein distnce on $\mathbb{R}^n$
        
        - How to use

            ```python
            import numpy as np
            from artemis7.stats.frechet_inception_distanec import FID

            x = np.random.normal(size = 1000)
            y = np.random.normal(size = 1000)
            fid = FID(x, y)
            ```

    - multivariate_sampling

        

    - piecewise_rejection_sampling

    - population_stability_index