# 2.2 AutoOptLib Architecture

## 2.2.1 File Structure

<a name="Figure2"></a>

![图片标题](../_static/Figure2.png)
<div style="text-align: center;">Figure 2: File structure of AutoOptLib.</div>
<br>

The file structure of AutoOptLib is given in [Figure 2](#Figure2). As shown in [Figure 2](#Figure2), source files of the library
are organized in a clear and concise structure. One interface function `AutoOpt.m` and three folders
are in the root directory. The folder `/Utilities` contains public classes and functions. Specifically, the
subfolder `/@DESIGN` stores the class and functions for designing algorithms for a target problem,
including functions for initializing, searching, and evaluating algorithms. `/@SOLVE` contains the
class and functions for solving the target problem by the designed algorithms, e.g., functions for
inputting algorithms, executing the algorithms, and repairing solutions. `/Others` involves miscellaneous
functions, e.g., sources of the GUI, functions of experimental tools, etc. The `Space.m` function is for
constructing the design space by algorithmic components.

The `/Components` folder contains the algorithmic components for constructing the design space.
We package each component with ranges of its endogenous parameter values in a single `.m` file. For
example, in [Figure 2](#Figure2), `choose_tournament.m` and `search_mu_gaussian.m` are the functions of the tournament selection [[ES+03]](../References/ref.html#ES+03) and Gaussian mutation [[Fog98]](../References/ref.html#Fog98), respectively. All the component functions are
written in the same structure, so users can easily implement and add new components to the library
according to existing ones.

Finally, the `/Problems` folder is for the target problems. A problem template, i.e., the `prob_template.m`
in [Figure 2](#Figure2), is given to guide users to easily implement and interface their problems with the library.


<br>

## 2.2.2  Classes

<a name="Figure3"></a>

![图片标题](../_static/Figure3.png)
<div style="text-align: center;">Figure 3: Class diagram of AutoOptLib.</div>
<br>

We involve only two classes in AutoOptLib, namely `DESIGN` and `SOLVE`, which manage the process of
designing algorithms for a target problem and solving the target problem by the designed algorithms,
respectively. The class diagram is given in [Figure 3](#Figure3). An object of the `DESIGN` class is a designed algorithm with several properties, e.g., `operator` (components that constitute the algorithm), `parameter`
(endogenous parameters of the algorithm), and `performance` (performance of the algorithm). The
class have some methods to be invoked by the objects. For example, the method `Initialize()` works
on initializing the designed algorithms; `Evaluate()` is for evaluating the algorithms’ performance
according to a design objective.

An object of the `SOLVE` class is a solution to the target problem. It has several properties, including
`dec` (decision variables), `obj` (objective value), `con` (constraint violation), etc. The class has several
methods for achieving the solutions, such as `InputAlg()` (preprocessing and inputting the designed
algorithm) and `RunAlg()` (running the algorithm on the target problem).


<br>
<br>

## 2.2.3 Operating Sequence

<a name="Figure4"></a>

![图片标题](../_static/Figure4.png)
<div style="text-align: center;">Figure 4: Sequence diagram of AutoOptLib.</div>
<br>

AutoOptLib’s sequence diagram is depicted in [Figure 4](#Figure4). To begin with, the interface function `AutoOpt.m` invokes `DESIGN.m` to instantiate objects (the designed algorithms) of the `DESIGN` class.
In detail, firstly, `DESIGN.m` uses the `Initialize()` method to initialize algorithms over the design
space. Then, the algorithms’ performance on solving the “training” instances <sup>[1](#note1)</sup> of the target problem
is evaluated by the `Evaluate()` method. To get the performance, the `Evaluate()` method invokes
the `SOLVE` class, and `SOLVE` further calls functions of the algorithms’ components and function of the
target problem. Finally, the initial algorithms are returned to AutoOpt.m.

After initialization, AutoOptLib goes into iterative design. In each iteration, firstly, `AutoOpt.m` invokes `DESIGN.m`. Then, `DESIGN.m` instantiates new objects (new algorithms) of the `DESIGN` class based on the current ones by the `Disturb()` method. Next, the new algorithms' performance is evaluated in the same scheme as in the initialization. After that, the new algorithms are returned to `AutoOpt.m`. Finally, the `Select()` method of the `DESIGN` class is invoked to select promising algorithms from the current and new ones.

After the iteration terminates, `AutoOpt.m` invokes the `Evaluate()` method of the `DESIGN` class to test the final algorithms' performance on the test instances of the targeted problem. Then, the final algorithms are returned in `AutoOpt.m`.

The above operating sequence has some significant advantages. Firstly, we keep functions of algorithmic components not interactive with each other but invoked independently by the `SOLVE` class. This independence provides great flexibility in designing various algorithms and extensibility to new components. Furthermore, we package design techniques in different methods (e.g., `Evaluate()`, `Select()`) of the `DESIGN` class. Such packaging brings good understandability and openness to new techniques without modifying the library's architecture. In addition, we enclose the targeted problem separately and do not directly interact it with algorithmic components and design techniques. This separation allows users to easily interface their problems with the library and use the library without much knowledge of metaheuristics and design techniques, thereby ensuring the accessibility of the library to researchers and practitioners from different communities and domains.

<br>
<br>

-------
<a id="note1"></a>1. Since the distribution of instances of a real problem is often unknown, one has to sample some of the problem
instances and target these instances (training instances) during the algorithm design procedure. To avoid the designed
algorithms overfit on the training instances, some other instances (test instances) of the target problem are then employed
to test the final algorithms after the design procedure terminates.