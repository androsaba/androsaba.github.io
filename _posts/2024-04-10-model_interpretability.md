---
layout: distill
title: The Mythos of Model Interpretability
description: Summary of the Zachary C. Lipton's paper with the same title
tags: #distill formatting
giscus_comments: false
date: 2024-04-10
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
_…we should stop acting as if our goal is to author extremely elegant theories, and instead embrace complexity and make use of the best ally we have: the unreasonable effectiveness of data._  
-- Alon Halevy et al, The Unreasonable Effectiveness of Data

Model interpretability means transparency (i.e., how does the model work?) and post hoc explanations (i.e., what else can the model tell me?).

Transparency can be defined at the level of the entire model (simulatability), at the level of individual components such as parameters (decomposability), and at the level of the training algorithm (algorithmic transparency).

Let's characterize each of them:  
Simulatability — an interpretable model is a simple model, easy to simulate. Sufficiently high-dimensional models, unwieldy rule lists, and deep decision trees could all be considered less transparent than comparatively compact neural networks.

Decomposability — each part of the model (input, parameter, and calculation) admits an intuitive explanation. Note that this notion of interpretability requires that inputs themselves be individually interpretable, disqualifying some models with highly engineered or anonymous features. The weights of a linear model might seem intuitive, but they can be fragile with respect to feature selection and preprocessing.

Algorithmic transparency — refers to learning algorithm itself. Deep learning models are less transparent than linear models.

Note that humans exhibit none of these forms of transparency.

**Conclusion**  
Linear models are not strictly more interpretable than deep neural networks. With respect to algorithmic transparency, this claim seems uncontroversial, but given high-dimensional or heavily engineered features, linear models lose simulatability or decomposability, respectively. When choosing between linear and deep models, you must often make a tradeoff between algorithmic transparency and decomposability. This is because deep neural networks tend to operate on raw or lightly processed features. So, if nothing else, the features are intuitively meaningful. To get comparable performance, however, linear models often must operate on heavily hand-engineered features. In some cases, transparency may be at odds with the broader objectives of AI. As a concrete example, the short-term goal of building trust with doctors by developing transparent models might clash with the longer-term goal of improving health care.