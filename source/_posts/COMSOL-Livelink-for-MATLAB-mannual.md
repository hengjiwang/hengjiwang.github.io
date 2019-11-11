---
title: COMSOL Livelink for MATLAB mannual
date: 2019-11-11 11:50:30
tags:
- COMSOL
- MATLAB
categories:
- Mannual
---
A mannual for COMSOL Livelink for MATLAB on Ubuntu 18.04.3 LTS.
<!-- more -->

# Get Started

In Terminal, open COMSOL Server

    $ comsol server

After it displays

    COMSOL Multiphysics server 5.3a (Build: 180) started listening on port 2036
    Use the console command 'close' to exit the program

Open a new Terminal, then open matlab

    $ matlab

In MATLAB Command Window

```matlab
>> addpath('/usr/local/comsol53a/multiphysics/mli');
>> mphstart;
```

Then it should display

    MATLAB is now connected to a COMSOL Multiphysics Server at localhost:2036

    Run the commands below to access the COMSOL ModelUtil commands:
    import com.comsol.model.util.*
