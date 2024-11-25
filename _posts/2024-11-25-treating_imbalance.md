---
layout: distill
title: To SMOTE or not to SMOTE?
description: Summary of the paper https://arxiv.org/pdf/2201.08528.pdf
tags: #distill formatting
giscus_comments: false
date: 2024-11-25
featured: false

#post_image: "assets/img/treatment_effect_estimation/churn.png"


authors:
  - name: Andro Sabashvili
    affiliations:
      name: Myself #IAS, Princeton
  

#bibliography: 2018-12-22-distill.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).


# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
   .footnote {
    font-size: 80%;
    }    
---

This paper discusses the scenarios when balancing techniques (SMOTE, under/over sampling) are beneficial.
- When the objective metric is proper: <d-footnote> A metric is proper when it is optimized by a classifier predicting the true class probabilities. For example, it is easy to see that Brier score is proper and even though AUC is generally not proper under the i.i.d assumption it is proper.</d-footnote> 
    - One can empirically show that balancing could improve prediction performance for weak classifiers such as MLP, SVM, decision tree, Adaboost and LGBM  but not for the SOTA classifiers (XGBoost and Catboost). The strong classifiers (without balancing) yield better prediction quality than the weak classifiers with balancing. 

- When the objective is a label metric:
    - Fixed threshold:
        - balancing considerably improved prediction performance for all classifiers.
    - Optimized threshold:
        - strong and medium classifiers: Balancing and optimizing the decision threshold provide similar prediction quality. However, optimizing the decision threshold is recommended due to simplicity and lower compute cost.
        - very weak classifiers (MLP and SVM): balancing the data is significantly beneficial over the optimizing the decision threshold. Nevertheless, the resulting prediction quality will be significantly worse compared to using a strong classifier (without oversampling).
    - When balancing (instead of optimizing the decision threshold) SMOTE-like methods were not significantly better than the simple random oversampler.

- scenarios for which SMOTE-like oversampling can improve prediction performance and should be applied:
    - Proper metric:
        - balancing is significantly effective when using a weak classifier 
    - Label metric:
        - When Optimize threshold is possible
            - balancing was beneficial (over optimization of decision threshold) only for the weak MLP and SVM classifiers. best prediction for them was achieved by oversampling with SMOTE. 
        - When not possible to optimize decision threshold