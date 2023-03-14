# Identifying Code Changes for Architecture Decay via a Metric Forest Structure

This repository illustrates data and the tool demo video of our TechDebt2023 under-reviewing work —— `Identifying Code Changes for Architecture Decay via a Metric Forest Structure`. The directory is organized as follows.



The whole directory goes like the following:

```
├─README.md
│	
├─Data         
│  │─Setup
│  │  ├─Subjects
│  │ 
│  └─Results
│     ├─Maintainability Evaluation Results    
│     ├─Architecture Decay Detection Results
|
└─Demo Video 
|
└─Knowledge Base  
│	
├─Scripts
│  ├─Setup
|
└─References  
```

## Data

### Setup

This directory contains the preliminary data to conduct the following experiments.

- #### Subjects

This directory contains a csv file named `Subjects.csv`. This file shows the information about all projects mentioned in the paper. We selected projects with diverse sizes and diverse do-mains(android-based projects, microservice-based projects and other projects studied by related work).So in this file, it includes `loc` , `#files`, `#commits`, `#modules`, `#classes` , `#methods` and `source` of the project (the latest version is obtained for all multi-version projects).Please note that our experiments focus on Java projects.



### Results

This directory contains all experimental results.

- #### Maintainability Evaluation Results


We conducted measurements for the latest versions for all of the collected projects, using the metrics integrated into our dbMIT. This directory contains a csv file named `evaluation results.csv` and 5 sample results. 

​	***evaluation results.csv**:* The SCORE and DL values of all projects are counted in the file. Since dbMIT considered multiple metrics, we computed the SCORE to obtain a weighted average measurement. We also computed the DL for these projects, a metric proposed by Mo et al.[1] to assess the architectural maintainability. A bigger value of DL or SCORE indicates a better maintainability of the software. Based on the results by DL and SCORE, we observed how the measurements will distribute over all of the subjects.

​	**sample results:** We use `apollo`, `argouml`, `LineageOS`, `piggymetrics` and `servicecomb-java-chassis` as samples to show our evaluation results. In addition to piggymetrics , the other four projects are multi-version projects. In their folder, all versions evaluated are included. 

The evaluation results of each project or version contain two csv files: `measure_result_class.csv` 和`measure_result_method.csv`. There are 67 columns in `measure_result_class.csv`, including the calculation results of all project-level, module-level and class-level metrics. `measure_result_method.csv` contains 15 columns, including the calculation results of all method-level metrics.

- #### Architecture Decay Detection Results


This directory contains two files: `detection results.csv` and `maintenance cost.csv`.

​		***detection results.csv**:* This file contains statistical number of all root causes entities.We executed the dbMIT on multiple versions of the collected subjects. The problematic methods or classes can be detected by using detection rules defined in Section II of the paper. 

​		***maintenance cost.csv**:* This file contains the maintenance cost of 6 projects. We employed three measures: `#commit`, `#changeLoc`, and `#author` as the ground-truth maintenance cost. 

`#commit` evaluates the number of commits that file entities participated in the software evolution.

`#author` computes the number of developers by which a file entity was modified. 

`#changeLoc` counts the code churn (added or deleted code lines) of a file in the revision history. A bigger value indicates a higher maintenance cost. 

`mc(A)` denotes the result of the three measures averaged on a set of problematic entities, which are detected by dbMIT. 

`mc(B)`denotes the results by the three measures averaged on a set of non-problematic entities. 

`P = mc(A)/mc(B)` denotes the rate of `mc(A)` to `mc(B)`. If the value of P is bigger than 1.0, it means that the problematic code reported by dbMIT indeed incurred more maintenance efforts.

## Demo Video

This directory contains the demo video of our tool-dbMITPlus.dbMITplus is a web system, developed and implemented based on our dbMIT approach. It aims to localize the cause of software architecture decay by using the metric forest and metric rules.

In this video, LineageOS is used as a case to introduce the four modules of dbMITPlus: Entity and Dependency Extraction, Module Clustering, Architecture Evaluation, Design Problem Detection, and the corresponding visualization.

- **The first module: Entity and Dependency Extraction.** This module extracts syntax dependencies such as method invocation, class inheritance, package import, and historical dependency information such as co-change from source code and commit history.

  When a user inputs basic information of analyzed project , the system  starts the entity and dependency extraction. The system UI will also display the extraction progress. After the progress reaches 100%, the information extraction is completed.

  Users can also view the code package structure of the current software through Project Size TreeMap. TreeMap displays the size of “modules” in a hierarchical structure.

- **The second module: Module Clustering.** Module Clustering reveals the “as-implemented” architecture based on historical dependency.

  The system provides SKM,DBSCAN,SpectralClustering and other clustering algorithms. For example, users can select SKM algorithm for clustering.

- **The third module: Architecture Evaluation.** It evaluates the software maintainability at different granularities with  77 metrics.

  Taking LineageOS as an example, users can observe the project's maintainability level among all projects through the "population distribution" .

  Through the "growth curve" , users can observe the quality changes of 6 versions during the evolution from LineageOS-16.0 to LineageOS-19.1.

  Through the "current profile", users can click on the LineageOS-17.1 to view maintainability measurements of the module in three dimensions.

- **The fourth module: Design Problem Detection.** It pinpoints potential architecture decay causes using a set of pre-defined detection rules. 

  Take LineageOS as an example. In the growth curve of the previous step, LineageOS-16.0 to LineageOS-17.1 experienced a decline in maintainability quality.

  "com.android.server.stats" is the module with the most severe issue. We then detect problematic classes inside this module via class-level metrics of CBC, EDCC, c_FAN OUT. The results suggest that the class "com.android.server.stats.StatsCompanionServicem" frequently invokes the methods across module boundary, leading to a measurement increase. 

  Next, We continue to pinpoint method-level code changes to explain the issue of this class. Method-level maintainability measures indicates that  "StatsCompanionService.pullAppOps" and "StatsCompanionService.pullRoleHolde" are the most severe entities, and each of them depends on more than 10 other modules to implement functionalities. 

  The system can display the information of the two problematic methods that incur heavier maintainability issues. Users can employ this information to fix the issue.
  

## Knowledge Base

The key of dbMIT is the forest structure of code-level metrics, making it easy for developers to understand the measurements (i.e.,comprehensibility), explain why the detected code changes are potential contributors to the decay (i.e., interpretability), and indicate how to resolve them (i.e., indicative-lity). In the `knowledge base.md`, the forest structure and metrics are described in detail.

## Scripts

### Setup

This directory contains a python script `get_github_projects.py`.It can automatically search microservice systems via Github Restful API.

## References

[1] R. Mo, Y. Cai, R. Kazman, L. Xiao, and Q. Feng, “Decoupling level: a new metric for architectural maintenance complexity,” in 2016 IEEE/ACM 38th International Conference on Software Engineering(ICSE), pp. 499–510, IEEE, 2016.
