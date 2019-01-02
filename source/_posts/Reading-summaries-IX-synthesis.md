---
title: Reading summaries IX -- synthesis
date: 2018-12-31 12:08:56
tags:
- intelligent machinery
categories:
- reading summaries
---
# *<font color = purple>Blaise Agūera y Arcas, [Art in the Age of Machine Intelligence](https://medium.com/artists-and-machine-intelligence/what-is-ami-ccd936394a83), 2016.*</font>

- Art is contrained by technological capabilities and machine intelligence is one of them. 
- Debates about antitechnological concept of art alway exist and will be extended to larger issues. 
- Technology has already been one part of our nature and there is no predetermined human's nature.
- Current cameras are powered by softwares which are coorporating with image-making and information processing like our neurons do, so cameras are not especially artificial.
  - Photographers are cyborgs
  - analogous to the eye $\rightarrow$ also to the brain (deep learning)

# *<font color = purple>Yann LeCun, Léon Bottou, Yoshua Bengio and Patrick Haffner, [Gradient-Based Learning Applied to Document Recognition](http://yann.lecun.com/exdb/publis/pdf/lecun-01a.pdf), 1998.</font>*

## Introduction

- traditional pattern recognition systems = automatic learning techniques + hand-crafted algorithms. 
- Usual method of pattern recognization has two modules
  1. **feature extractor:** raw input $\rightarrow$ feature vectors (contains most prior knowledge)
  2. **classifier:** general-purpose and trainable
- *For a neural network, a good way to incorporate the prior knowledge is to tailor its architecture to the task*
- Most practical pattern recognition system contain modules:
  1. field locator: extract regions of interest
  2. field segmenter: cuts the input image into images of candidate characters
  3. recognizer: classifies and scores each candidate character
