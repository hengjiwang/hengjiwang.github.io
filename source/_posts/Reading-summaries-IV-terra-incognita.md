---
title: Reading summaries IV -- terra incognita
date: 2018-12-29 12:24:02
tags:
- intelligent machinery
categories:
- reading summaries
---
# <font color = purple>*Manuel DeLanda, Philosophy and Simulation: The Emergence of Synthetic Reason, 2011.*</font>

## [Introduction: Emergence in History](https://intelligentmachinerycourse.files.wordpress.com/2018/10/delanda_philosophy_and_simulation_2011_introduction_p1.pdf)

- Between today and early 20th century on emergence:
    - Different:
      - epistemological (认识论的): brute fact $\rightarrow$ can be explained away
    - Same:
      - ontological (本体论的): irreducible
- What concrete emergent wholes can we believe in?
  - *Wholes the identity of which is determined historically by the processes that initiated and sustain the interactions between their parts.*
  - *The historically contingent identity of these wholes is defined by their emergent properties, capacities, and tendencies*
- Simulations play the role of laboratory experiments in the study of emergence

## [Chapter 6: Neural Nets and Insect Intelligence](https://intelligentmachinerycourse.files.wordpress.com/2018/10/delanda_philosophy_and_simulation_2011_chapter_6_p1.pdf)

- Hydra can perform two ancient forms of learning:
  - habituation: gradually decrease its response to a stimulus; transforms a significant stimulus into an insignificant one
  - sensitization: transform a irrelevant stimulus as a relevent one
- Classical conditioning shows that animal's brain is creating a simplified model of stimulus based on those emergent properties
- Local assemblies of neurons rather than the entire nervous systens sustain the capacity for classical conditioning
- The more surprising the stimulus the larger the conditioning effect
- To simulate classical conditioning, two improvements need to be made: 
  - increasing computational power: needed because animal should be able to predict from different stimuli, which need to learn some elementary logical functions
  - giving it capacity to generalize: animals should be able to response to similar stimuli in same categories
  
    Both improvements can be achieved by adding intermediate layers (hidden layers)
- The pattern in the hidden layer is emergent and its composition is influenced by similarities in the different sensory patterns included in the training set
- Simulating classical conditioning with two MLP:
  - first plays a role of an inherited reflex (继承反射) of which the configuration of weights are fixed (unconditioned stimuli)
  - second is able to learn from experience (conditioned stimuli)

    The two nets should be connected with each other laterally; after training, conditioned stimuli can result in a representation of unconditioned one and vice versa
- Pure neural net is not enough -- should embody the simulated neurons and situate them in a space that provides them with opportunities and risks. 

## [Chapter 7: Neural Nets and Mammalian Memory](https://intelligentmachinerycourse.files.wordpress.com/2018/10/delanda_philosophy_and_simulation_2011_chapter_7_p1.pdf)

- categories of memory:
  - declarative memory: content is accessible
    - episodic memory: have experienced
    - semantic memory: consists of linguistically expressed facts
- two capacities:
  - object recognition
  - scence analysis

object recognition

- how to capture an objective category without using any linguistic resources?
  - mapping of relations of similarity into relations of proximity
- **Instrumental conditioning:** different with classical conditioning, it starts with spontaneous behaviors rather without conditioned stimuli, and control the frequencies by reward and punishment. 
  - successive approximation
- Difficulty of instrumental conditioning: hard to control the extent a reiforcer can affect an animal. Methods:
  - four nets corresponding to pleasure/pain (internal reinforcement), approach/avoid (motor behavior), each pair is laterally inhibited; external reinforcement connected to the internal reinforcement through fixed connections
  - obtain the degree of hunger or thirst from the output activation

scence analysis

- Current simulations of human episodic memory use **propositionss**, which are component parts of **scripts**
- The scripts implemented by neural nets are learned by example extracted from statistical regularities in actual stories -- emergent
- methods to implement scripts:
  - recurrent neural network (RNN)
  - self-organizing map (SOM)
- *Discern*: a machine simulating memory combining RNN and SOM

# <font color = purple>*Michael Graziano, The Spaces Between Us, 2018.</font>*

## [Chapter 12: The First Smile.](https://intelligentmachinerycourse.files.wordpress.com/2018/10/graziano_the_spaces_between_us_smile_ch12_2017.pdf)

- smile is an social signal emerged from defensive actions. 
- smile is an evolutionary mimic. 
- survival advantage of any social signal is to manipulate the behavior of the receiver