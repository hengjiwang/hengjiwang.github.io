---
title: Reading summaries II -- computing machinery
date: 2018-12-18 12:10:56
tags: 
- intelligent machinery
categories:
- reading summaries
---

# <font color=purple>*William James, Psychology (Briefer Course), 1890. [Chapter XVI on Association](https://intelligentmachinerycourse.files.wordpress.com/2018/09/james_psychology_1890p.pdf)*</font>

- **Thoughts have connections**
  - thought-of?
    - cannot be formulated simply
    - every conceivable connection can be thought-of (succession, coexistence, resemblance, contrast ... )
    - proceed from one thought to the other by some intelligible path
  - between thoughts?
- **What determines the particular path?**
  - countless of reasons
  - mode of genesis
- Habit is a sufficient explanation of the sequence of our thoughts
- **Objects are associated, not ideas**
  - association stands for a _cause_, between _processes_ in the brain
  - association determines what successive objects shall be thought
- **The elementary principle**
  - no other elementary causal law than the law of neural habit
  - _When two elementary brain-processes have been active together or in immediate succession, one of them tends to propagate its excitement into the other._
  - _The amount of activity at any given point in the braincortex is the sum of the tendencies of all other points to discharge into it._
- **Spontaneous trains of thought**
  - behind an object there is a combination of objects associated
- **Total recall**
  - _All revivals of a past experience together determine the next thought._
- **Partial recall**
  - _some one brain-process is always prepotent above its concomitants in arousing action elsewhere._
  - **Which associates come up in partial recall?**
    - habit (frequency)
    - recency
    - vividness
    - emotional congruity
- **Focalized recall, or association by similarity**
  - _A small surviving portion will surround itself with its own associates though other portions of the object have faded._
  - _the relation between the new thought’s object and the object of the faded thought will be a relation of similarity._
  - When we affirm the similarity of two compound things, we should always say in what respect it obtains.
- **Voluntary trains of thought**
  - _voluntary:_ describing a process of suggestion of one object by another to be spontaneous
- **Problems**
  - _problem:_ the search for _means_ by which the _end_ shall be attained
  - _end:_ which we desire before we have attained it
  - e.g. mode of recalling a thing forgotten
- **Solution**
  - _will:_  _to emphasize and linger over those which seem pertinent, and ignore the rest_
  - Try to find everything that is associated with the object we desire to recall.
- **Similarity no elementary law**
  - object called up may bear any logical relation whatever to the one which suggested it
  - The similarity itself between the objects has no causal agency in carrying us from one to the other. It is but a result (agent).
  

# <font color=purple>*Warren McCulloch and Walter Pitts, [A logical calculus of the ideas immanent in nervous activity](https://intelligentmachinerycourse.files.wordpress.com/2018/09/mcculloch_pitts_with_intro_1943p.pdf), 1943.*</font>

- McCulloch-Pitts neuron
  - a binary device
  - has a fixed threshold
  - inputs from excitatory synapses, all of which have identical weights
  - inputs from inhibitory synapses, whose action is absolute (when it's active the neuron can't turn on)
  - time quantum for integration of synaptic inputs
- Any finite logical expression can be realized by McCulloch-Pitts neurons. 
- The brain is potentially a powerful logic and computational device.
- Influenced the people who were thinking about the potential of digital computers like John von Neumann.

# <font color=purple>*Walter Pitts and Warren McCulloch, [How we know universals: the perception of auditory and visual forms](https://intelligentmachinerycourse.files.wordpress.com/2018/09/pitts_mcculloch_how_we_know_universals_1947p.pdf), 1947.*</font>

- Pitts and McCulloch refer to a raw sense image as an _apparition_
- Mathematical techniques of differing complexity for transforming an apparition into the constant representation, what they believe were developed by the early nervous system. 
- They suggested we _have anatomically separate layers/substructures do the individual transformations, which are then brought together at another layer to form the final representation._ 
- Time-space trade-off: reusing the neural hardware in a cycle of temporal processing.
- Compared with the 1943 paper, the power of logic has been replaced with the power of spatial representation and analog computation. 

# <font color=purple>*Frank Rosenblatt, [The perceptron: a probabilistic model for information storage and organization in the brain](https://intelligentmachinerycourse.files.wordpress.com/2018/09/rosenblatt_perceptron_1958p.pdf), 1958.*</font>

- _perceptron_ was the first precisly specified, computationally oriented neural network.

- retina -- association area -- A-units -- R-units -- Winner-Take-All
- Rosenblatt felt the appropriate way to view brain operation was a learning associator -- the goal was to couple the classification responses to stimuli.
- The system is very dependent for operation on the internal representation of the world.
- Unable to classify random vectors.

# <font color=purple>*H.D. Block, [The perceptron: a model for brain functioning.](https://intelligentmachinerycourse.files.wordpress.com/2018/09/block_perceptron_1962p.pdf) I, 1962.</font>*

- early thought of SVM
- 4-layers MLP

# <font color=purple>*D. E. Rumelhart, G. E. Hinton, and R. J. Williams, [Learning internal representations by error propagation](https://intelligentmachinerycourse.files.wordpress.com/2018/09/rumelhart_williams_hinton_backprop_1986p.pdf), 1986.*</font>

- _back propogation(backprop)_ is considerably faster than other learning algorithm in MLP/neural network. 
- backprop is a generalization of the Widrow-Hoff error correction rule.
- "generalized delta rule" gives a recipe for adjusting the strengths of synapses on internal units based on the error at the output.
  - However the internal units must be told how large the error is and how strongly the internal units are connected to the output units in error.
  - solution: backprop 
- Real synapses do not run backward. Making a plausible physiological model of back propagation is not easy.
  - The functions of reciprocal cortical connections in physiology are unclear yet.
- Backprop can be used in data compression.