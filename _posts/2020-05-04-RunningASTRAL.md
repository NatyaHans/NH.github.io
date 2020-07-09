---
title: ‘Gene discordance analysis using ASTRAL on HiPerGator'
date: 2020-07-09
permalink: /posts/2019/05/RunningASTRAL/
tags:
  - hipergator
  - bash
  - aliases
  - linux
--- 

Really brief background 
--------

[ASTRAL](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2129-y)is a method used for inferrring species tree from an input of gene trees.
The algorithm takes into account discordance among genes, by using dynamic programming. It splits the input gene tree into set of quartets and then searches for a 
species tree that has maximum number of each of these quartet topologies, assigning support values to each. The algorithm is really fast (takes about 2-4seconds to run) as there are predetermined 
partitions instead of searching for new ones.

ASTRAL III  is the faster version that reduces the run time as compared to the older versions [ASTRAL](https://academic.oup.com/bioinformatics/article/30/17/i541/200803) and [ASTRAL II](https://pubmed.ncbi.nlm.nih.gov/26072508/). 
Both of these method can still be found on Hipergator. The ASTRAL III paper compares and contrasts the accuracy with ASTRAL II, results are presented in a [table](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2129-y/tables/1).
and are worth glancing over even if you are not a method developer. The results in the table indicate improved quartet scores. 
There is a new paper in bioRxiv on [ASTRAL-PRO](https://www.biorxiv.org/content/10.1101/2019.12.12.874727v2) that deals with gene duplication and gene loss.
If you want to learn more gene discordance theory start [here](https://academic.oup.com/sysbio/article/46/3/523/1651369) and [here](https://www.cell.com/trends/ecology-evolution/fulltext/S0169-5347(09)00084-6?)


Using ASTRAL on Hipergator
---------
Astral uses gene trees as input, and gives a species tree as output. To be specific, the gene trees must be in newick format, can have missing taxa, and/or polytomies.
After you log in to Hipergator, type

        module spider astral 
        
This gives the version number of Astral, currently on hipergator, the latest version is astral/5.6.2. Let's load astral now. Note we can skip the previous step, and type "module load astral" and it will default to the latest version usually.
It is always a good idea to double check and make sure the version is correct especially when reporting the version in manuscripts.

        module load astral/5.6.2
        

Let's assume all of your gene trees are in a single file labeled INPUTGENETREES.tre (again note that it is in newick format). For a sample input file click [here]().For the simplest ASTRAL run, type the following command
 
        astral -i INPUTGENETREES.tre -o OUTTREE.tre 2 > out.log
 
 
-i is flag for input file name
-o is flag for output file name, user specified name
2 defines the format
> out.log saves the detailed information about the run into a log file instead of printing it on the screen, user specified name
 
 
 For more detailed notes [click](https://github.com/smirarab/ASTRAL/blob/master/README.md)
 
 Multi locus bootstrapping using ASTRAL
 ----------

