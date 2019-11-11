---
title: Hyak Manual
date: 2019-02-18 21:59:53
tags:
- hyak
categories:
- tutorials
---

# Get started

Log into Hyak:

    $ ssh username@mox.hyak.uw.edu

Now you are in **home** directory, of which the path is 

    $ pwd
    /usr/lusers/hengjw

Since **home** directory only has 10GB for storage, maybe you want to use **work** directory where you share 45500GB with all other users. To enter it just type in 

    $ cd /gscratch/stf/username

The files in **home** directory will never be deleted, but the files in **work** directory will be cleaned in 30 days after the last modification time. 

# File transfer

There are two methods to upload/download files between local directory and Hyak. Both of them should be operated on local directory. 

## 1. scp

Upload files into Hyak

`$ scp myfile username@mox.hyak.uw.edu:path/of/destination`

Download files from Hyak

`$ scp user@mox.hyak.uw.edu:path/of/remote/file .`

## 2. sftp

First off, connect a local directory to Hyak

`$ sftp user@mox.hyak.uw.edu`

Upload file into Hyak

`$ put filename`

Upload folder into Hyak

`$ put -r foldername`

Download file from Hyak

`$ get filename`

Download folder from Hyak

`$ get -r foldername`

List files in Hyak directory

`$ ls`

List files in local directory 

`$ lls`





# Before running scripts

Check how many nodes are available

`$ hyakalloc stf`

or check which users are running or waiting

`$ squeue -p stf`

If there is no available nodes in **stf**, you can check another partition **stf-int**

`$ hyakalloc stf-int`

# Run scripts

Two methods for running a script in Hyak.

## 1. srun

If you only plan to use one node

`$ srun -p stf -A stf --time=1:00:00 --mem=10G --pty /bin/bash`

The maximum of memory in one memory is around 120GB, some GB should be left for operating system; setting smaller memory may increase your priority in partition **stf-int**.

## 2.

Create a bash script in **home** directory (mine is named **myslurm**). Save the following texts in it:

    ```shell
    #!/bin/bash

    #SBATCH --job-name=test_nodes

    #SBATCH --account=stf

    #SBATCH --partition=stf

    #SBATCH --nodes=1

    #SBATCH --ntasks-per-node=28

    #SBATCH --time=0:02:00

    #SBATCH --mem=10G

    #SBATCH --workdir=/gscratch/stf/username

    #SBATCH --mail-type=ALL

    #SBATCH --mail-user=username@uw.edu

    python filename.py
    ```

Each time to run a script, just change the numbers after ```#SBATCH --nodes=``` to the nodes number you want and ```#SBATCH --mem=``` to the memory you want to use, and replace the last line to another run command. 

# Check node usage

To enter the current node from a new terminal 

`$ ssh nodeid`

Check the usage status of node

`$ top -u username`

Press ```q``` to quit.

To check free memory in current node

`$ free -g`

To check disk space of current node

`$ dh -f`