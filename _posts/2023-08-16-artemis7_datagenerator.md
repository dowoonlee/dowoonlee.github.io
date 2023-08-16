---
title: Data generator
tags: artemis7

---


## Datagenerator

- Virtual Drift generator

    - Initialization

        Between (time_range[0]~time_range[1]), Drifts take place at `drfit_time_sequence`.
        `time_range` and `drift_time_sequence` support float (mjd) and string (datetime64, yyyy-mm-dd).
        CDG only support continuous columns and 2type drift mode (base<->drift) (2023-01-06).
        CDG can support continous and discrete columns (2023-01-12)
        CDG supports regression prob type (2023-01-19)

    - Generation

        X (Data set) is randomly sampled with Gamma distribution (https://en.wikipedia.org/wiki/Gamma_distribution).
        Gamma distribution has two parameters (k, theta). The parameters follow normal distribution in this class.

        generate() methods supports 2 types of drift modes `real`/`virtual` and 3types of drift patterns `sudden`/`incremental`/`gradual`.
        In case of drift mode, **real** is the drift in p(y|X) which is the case that X doesn't change but label y change only.
        For **virtual**, p(y|X) doesn't change but the distribution of X changes.
        you can control the strength of the drift with parameter `strength`. `strength` works linearly in **real** and logarithmic in **virtual**.
        Drift pattern depends on the time interval of `drift_start`, `drift_end`.
        `sudden` make drift with time interval=0.
        `Incremental` and `gradual` have same time interval of `[0.3*dT_bef, 0.3*dT_aft]`.
        The difference between them is that `incremental` has gentle drift in time interval and `gradual` has abrupting dirft.

    - How to use
        - import
            ```python
            from artemis7.datagenerator.virtual_drift_generator import VirtualDriftGenerator as VDG
            ```
        - generation
            ```python
            vdg = VDG(
                time_range = ["2012-01-01", "2018-01-01"],
                drift_time_sequence = ["2014-01-01"],
                prob_type = "regression",
                n_cont = 5,
                n_disc = 5,
                dt = 1)
            df = vdg.generate(
                drift="real",
                time_format="mjd",
                drift_type="sudden",
                strength=10, 
                noise=0.1)
            vdg.save_to_csv(
                path = "./",
                file_name = None,
                time_format="mjd",
                file_info=True)
            ```
            