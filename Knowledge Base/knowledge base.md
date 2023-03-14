## Forest Structure

Based on the maintainability model defined by ISO/IEC 25010, we construct a forest structure as a knowledge base, combing widely-adopted code-level metrics from the developer side. All the collected metrics correspond to the nodes in the forest structure, where each link between nodes denotes their relation.

![metrics](.//img//metrics.png)

## Metrics

The forest Structure contains four granularity maintainability metrics, and the number of metrics provided by each granularity is as follows:

| granularity | number |
| ----------- | ------ |
| project     | 11     |
| module      | 12     |
| class       | 42     |
| method      | 12     |

The metrics of all granularity are explained as follows.

- project

  | metric | full name                    | description                                                  | source |
  | ------ | ---------------------------- | ------------------------------------------------------------ | ------ |
  | score  | -                            | Module-level metrics are fused to obtain a comprehensive score of maintainability. | [3]    |
  | CHM    | CoHesion at message level    | The average cohesion of all modules in the project at the message level. | [4]    |
  | CHD    | CoHesion at domain level     | The average cohesion of all modules in the project at the domain level. | [4]    |
  | SMQ    | structural modularity        | The degree of structural modularization. The higher SMQ, the higher modularity of the module. | [4]    |
  | ODD    | out-degree dependence        | The average value of odd.                                    | [4]    |
  | IDD    | in-degree dependence         | The average value of idd.                                    | [4]    |
  | SPREAD | -                            | The average value of spread.                                 | [5]    |
  | FOCUS  | -                            | The average value of focus.                                  | [5]    |
  | ICF    | intra co-change frequency    | The average value of icf.                                    | [4]    |
  | ECF    | external co-change frequency | The average value of ecf.                                    | [4]    |
  | REI    | ratio of ecf to icf          | The average value of rei.                                    | [4]    |

- module

  | metric | description                                                  | source |
  | ------ | ------------------------------------------------------------ | ------ |
  | chm    | The larger chm, the higher cohesion of the module at the message layer. | [4]    |
  | chd    | The larger chd, the higher cohesion of the module at the domain level. | [4]    |
  | scoh   | Structural cohesion. The larger scoh, the greater structural cohesion within module. | [4]    |
  | scop   | Structural coupling. The larger scop, the greater structural coupling between modules. | [4]    |
  | odd    | Out-degree dependence. The larger odd, the higher out-degree dependence in the module. | [4]    |
  | idd    | In-degree dependence. The larger idd, the higher in-degree dependence in the module. | [4]    |
  | spread | The number of cross-module co-change clusters in the evolution process.  The smaller spread, the better modularity. | [5]    |
  | focus  | The degree of good modularity.  The larger focus, the better modularity. | [5]    |
  | icf    | The value of co-change frequency intra modules. The higher icf, the more likely entities in the module will evolve together. | [4]    |
  | ecf    | The value of co-change frequency external modules. The lower ecf, the more likely cross-module entities will evolve independently. | [4]    |
  | rei    | The value of the ratio of ecf  to icf. The lower rei, the lower possibility that different modules can be modified together. Each module is more likely to evolve and maintain independently. | [4]    |
  | DSM    | Design size in module. The larger DSM, the module is more complex , and the higher possibility of external coupling. | QMOOD  |

- class

  | metric                 | description                                           | source                     |
  | ---------------------- | ----------------------------------------------------- | -------------------------- |
  | CBC                    | Number of class dependencies                          | CK                         |
  | c_FAN_IN               | Number of class in-degree                             | CK                         |
  | c_FAN_OUT              | Number of class out-degree                            | CK                         |
  | IDCC                   | Direct class coupling  intra module                   | QMOOD                      |
  | IODD                   | Out-degree dependency intra module                    | derived from IDCC in QMOOD |
  | IIDD                   | In-degree dependency intra module                     | derived from IICC in QMOOD |
  | EDCC                   | Direct class coupling external modules                | QMOOD                      |
  | NAC                    | Number of ancestor classes                            | QMOOD                      |
  | NDC                    | Number of descendent classes                          | QMOOD                      |
  | NOI                    | Number of import classes                              | derived from NAC in QMOOD  |
  | NOID                   | Number of imported classes                            | derived from NDC in QMOOD  |
  | c_chm                  | The functional cohesion of class at the message layer | [4]                        |
  | c_chd                  | The functional cohesion of class at the domain layer  | [4]                        |
  | CIS                    | Class interface size                                  | QMOOD                      |
  | NOM                    | Number of methods in the class                        | QMOOD                      |
  | NOP                    | Number of polymorphic methods                         | QMOOD                      |
  | CTM                    | Coupling through Message Passing                      | CK                         |
  | RFC                    | Response for a class                                  | CK                         |
  | NOF                    | Number of fields                                      | CK                         |
  | NOVM                   | Number of visible methods                             | CK                         |
  | NOSI                   | Number of static invocations                          | CK                         |
  | TCC                    | Tight class cohesion                                  | CK                         |
  | LCC                    | Loose class cohesion                                  | CK                         |
  | LCOM                   | Lack of cohesion of methods                           | CK                         |
  | LOCM*                  | Lack of cohesion of methods                           | CK                         |
  | WMC                    | Weight Method Per Class                               | CK                         |
  | c_modifiers            | Class modifiers                                       | CK                         |
  | c_variablesQty         | Number of variables in the class                      | CK                         |
  | privateMethodsQty      | Number of private methods                             | CK                         |
  | protectedMethodsQty    | Number of protected methods                           | CK                         |
  | staticMethodsQty       | Number of static methods                              | CK                         |
  | defaultMethodsQty      | Number of default methods                             | CK                         |
  | abstractMethodsQty     | Number of abstract methods                            | CK                         |
  | finalMethodsQty        | Number of final methods                               | CK                         |
  | synchronizedMethodsQty | Number of synchronized methods                        | CK                         |
  | publicFieldsQty        | Number of public fields                               | CK                         |
  | privateFieldsQty       | Number of private fields                              | CK                         |
  | protectedFieldsQty     | Number of protected fields                            | CK                         |
  | staticFieldsQty        | Number of static fields                               | CK                         |
  | defaultFieldsQty       | Number of default fields                              | CK                         |
  | finalFieldsQty         | Number of final fields                                | CK                         |
  | synchronizedFieldsQty  | Number of synchronized fields                         | CK                         |

- method

  | metric                         | description                                  | source |
  | ------------------------------ | -------------------------------------------- | ------ |
  | startLine                      | Line of code at the beginning of the method  | -      |
  | CBM                            | Coupling between methods                     | CK     |
  | m_FAN_IN                       | Number of method in-degree                   | CK     |
  | m_FAN_OUT                      | Number of method out-degree                  | CK     |
  | IDMC                           | Direct method coupling  intra module         | QMOOD  |
  | EDMC                           | Direct method coupling external modules      | QMOOD  |
  | m_variablesQty                 | Number of variables in the method            | CK     |
  | parametersQty                  | Number of parameters in the method           | CK     |
  | m_modifier                     | Method modifiers                             | CK     |
  | methodsInvokedQty              | Number of methods invocations                | CK     |
  | methodsInvokedLocalQty         | Number of methods local invocations          | CK     |
  | methodsInvokedIndirectLocalQty | Number of methods indirect local invocations | CK     |

## References

[1] S. R. Chidamber and C. F. Kemerer, “A metrics suite for object oriented design,” IEEE Transactions on software engineering, vol. 20, no. 6, pp. 476–493, 1994.

[2] J. Bansiya and C. G. Davis, “A hierarchical model for object-oriented design quality assessment,” IEEE Transactions on software engineering,vol. 28, no. 1, pp. 4–17, 2002.

[3] C. Zhong, S. Li, H. Zhang, and C. Zhang, “Evaluating granularity of microservices-oriented system based on bounded context,” Journal of Software, vol. 30, no. 10, pp. 3227–3241, 2019.

[4] W. Jin, D. Zhong, Y. Zhang, M. Yang, and T. Liu, “Microservice maintainability measurement based on multi-sourced feature space,”Journal of Software, vol. 32, no. 5, pp. 1322–1340, 2021.

[5] L. L. Silva, M. T. Valente, and M. d. A. Maia, “Assessing modularity using co-change clusters,” in Proceedings of the 13th international conference on Modularity, pp. 49–60, 2014.

