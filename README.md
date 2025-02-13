# QRISK3 R Package

**Update**

This repository has been updated to version 0.6 as the CRAN version.

**Introduction**

This package provides a function to calculate 10-year individual cardiovascular disease (CVD) risk using the QRISK3-2017 model. The QRISK3 model, developed by ClinRisk Ltd., estimates the likelihood of developing CVD over a decade based on various health factors.

**Model Information:**

The original QRISK3 model formula, including variable names and model beta coefficients, is licensed under LGPL and copyrighted to ClinRisk Ltd.

    Copyright 2017 ClinRisk Ltd.

QRISK3-2017 is free software: you can redistribute and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

QRISK3-2017 is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with QRISK3-2017. If not, see http://www.gnu.org/licenses/.

**Additional Terms**

The following disclaimer must be included with any risk score generated by this code. If the score is displayed, the disclaimer must be displayed or made easily accessible, such as by a prominent link alongside it:

The initial version of this file, available at http://svn.clinrisk.co.uk/opensource/qrisk2, faithfully implements QRISK3-2017. ClinRisk Ltd. released this code under the GNU Lesser General Public License to allow others to implement the algorithm faithfully. However, due to the nature of the GNU Lesser General Public License, we cannot prevent errors such as altered coefficients, incorrect inputs, or poor programming. ClinRisk Ltd. emphasizes that it is the responsibility of the end user to verify that the implementation produces the same results as the original code found at https://qrisk.org. Inaccurate implementations may lead to incorrect patient treatment.

**Installation**

To install the package, you can use one of the following methods:

- **From CRAN:**

    install.packages("QRISK3")

- **From GitHub:**

    install.packages("devtools")
    library(devtools)
    install_github("YanLiUK/QRISK3")

**Example Usage**

    data(QRISK3_2019_test)
    test_all <- QRISK3_2019_test

    test_all_rst <- QRISK3_2017(data=test_all, patid="ID", gender="gender", age="age",
        atrial_fibrillation="b_AF", atypical_antipsy="b_atypicalantipsy",
        regular_steroid_tablets="b_corticosteroids", erectile_disfunction="b_impotence2",
        migraine="b_migraine", rheumatoid_arthritis="b_ra", 
        chronic_kidney_disease="b_renal", severe_mental_illness="b_semi",
        systemic_lupus_erythematosis="b_sle",
        blood_pressure_treatment="b_treatedhyp", diabetes1="b_type1",
        diabetes2="b_type2", weight="weight", height="height",
        ethnicity="ethrisk", heart_attack_relative="fh_cvd", 
        cholesterol_HDL_ratio="rati", systolic_blood_pressure="sbp",
        std_systolic_blood_pressure="sbps5", smoke="smoke_cat", townsend="town")

    test_all_rst$"QRISK_C_algorithm_score" <- test_all$"QRISK_C_algorithm_score"
    test_all_rst$"diff" <- test_all_rst$"QRISK3_2017_1digit" - test_all_rst$"QRISK_C_algorithm_score"
    print(test_all_rst$"diff")
    print(identical(test_all_rst$"QRISK3_2017_1digit", test_all_rst$"QRISK_C_algorithm_score"))

**References**

- [QRISK3 Model Information](https://qrisk.org/src.php)
- [Paper on QRISK3 Variables](https://f1000research.com/articles/8-2139)
- DOI: [10.12688/f1000research.21679.1](https://doi.org/10.12688/f1000research.21679.1)
