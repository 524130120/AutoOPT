# 2.1 What is automated algorithm design?

Given a target problem, through algorithm design, we would like to find an algorithm(s) with the best performance on the problem [[BK09]](../References/ref.html#BK09):

[formulation 1]

where A is the designed algorithm; S is the design space, from where A can be instantiated; i ∈ I is an instance of the target problem domain I; P : S × I → R is a performance metric that measures the performance of A in I. The design aims to find algorithm(s) with the maximum expected performance in I.

In reality, the distribution of problem instances in I is often unknown, and one cannot exhaust all the instances during the design process. The common practice of settling for the reality is to consider a finite set of instances from I. Consequently, Eq. (1) can be reformulated as

[formulation 2]

where It is the finite set of instances that are target at time (i.e., iteration<sup>[1](#note1)</sup>) t of the design process.
The target problem instances can either be fixed (i.e., I1 = I2 = · · · = IT ) or dynamically changed during the design process.
The output of solving Eq. (2) is algorithm(s) with the best performance on the considered instances.
To avoid the designed algorithms overfitting, the design process can be followed by validation 
to investigate the generalization of the designed algorithms to instances from I\{I1, I2, · · · , IT }.

The general process of automated design of metaheuristic optimizers can be abstracted into four
parts, as shown in [Fig. 1](#Fig1). first, the design space collects of candidate primitives or components
for instantiating metaheuristic algorithms. It regulates what algorithms can be found in principle.
Second, the design strategy provides a principle way to design algorithms by selecting and combining
the primitives or components from the design space. Third, the performance evaluation strategy defines
how to measure the performance of the designed algorithms. The measured performance guides the
design strategy to find desired algorithms. Finally, because the design aims to find algorithms with
promising performance on solving a target problem, the target problem acts as external data to support
the performance evaluation. This survey is organized according to the above four parts of automated
design.

<a name="Fig1"></a>
![图片标题](../_static/Fig1.png)
<div style="text-align: center;">Figure 1: Process of automated design of metaheuristic optimizers.</div>


**Note:**

<a id="note1"></a>1. Since Equation 2 is a black-box problem, it is often solved in an iterative manner.