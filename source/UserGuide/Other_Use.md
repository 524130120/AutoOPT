# 2.4 Other Uses

Beyond the primary use of automatically designing algorithms, AutoOptLib provides functionalities of hyperparameter configuration, parameter importance analysis, and benchmark comparison.

## 2.4.1 Hyperparameter Configuration

In many scenarios, users may have a preferred algorithm and only need to configure endogenous parameters (hyperparameters). In essence, hyperparameter configuration is equivalent to designing an algorithm with predefined component composition but unknown endogenous parameter values. Thus, it is easy to perform hyperparameter configuration in AutoOptLib by fixing the component composition and leaving the endogenous parameters tunable in the design space. Following the steps below to conduct hyperparameter configuration: 

 + Implement the target problem as illustrated in Section [2.3.1](../UserGuide/Use_AutoOptLib.html#implement-problem).

 + Define the design space as illustrated in Section [2.3.2](../UserGuide/Use_AutoOptLib.html#define-design-space). In particular, the design space should only involve the components of the preferred algorithm. The components can be existing ones in the library or user implemented with the same interface as existing ones. Turn `Setting.TunePara` to `true` in `space.m`.

```matlab
 Setting.TunePara = true; % true/false, true for hyperparameter configuration
```

 + Run AutoOptLib as illustrated in Section [2.3.3](../UserGuide/Use_AutoOptLib.html#run-autooptlib).


## 2.4.2 Parameter Importance Analysis

Users can further conduct parameter importance analysis by leaving only one tunable parameter in the design space. That is, users can define the design space with one tunable parameter and fix the component composition and other parameter values. Then, AutoOptLib runs and returns the algorithms found during the design process. These algorithms only differ in the values of the tunable parameter. Users can compare the performance of different parameter values and analyze the impact of parameter changes on the algorithm performance. 

Furthermore, by leaving different parameters tunable in different AutoOptLib runs, users can collect and compare the trends of each parameter's changes versus algorithm performance, subsequently getting insight into each parameter's importance to the algorithm performance.


## 2.4.3 Benchmark Comparison

As illustrated in Section [2.2](../UserGuide/AutoOptLib_Arch.html), different design objectives ([Table 2](../GettingStart/Introduction.html#table2)) and techniques ([Table 3](../GettingStart/Introduction.html#table3)) in AutoOptLib are implemented with the same architecture; more objectives and techniques can be added by the same interface. This ensures fair and reproducible comparisons among the objectives or techniques. The comparison can be conducted by assigning different objectives or techniques to different AutoOptLib runs on the same targeted problem instances.

AutoOptLib can also be used to benchmark comparisons among different algorithms. Users can set `AlgN`>1 in the running command or GUI, such that AutoOptLib will design multiple algorithms in a single run. These algorithms are built and evaluated in a uniform manner during the design process. Such uniformity ensures a fair comparison among the algorithms.



