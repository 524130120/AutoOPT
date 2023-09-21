# 1.1 Introduction

AutoOptLib is a Matlab library for automatically designing metaheuristic optimizers. It provides:
+ Rich library of design choices - Over 40 representative metaheuristic components for designing algorithms for continuous, discrete, and permutation problems with/without constraints and uncertainties.

<a name="table1"></a>
<div style="text-align: center;">Table 1: Metaheuristic algorithm components in AutoOptLib.</div>

| Component                        | Description                                                                                                                      |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| **Continuous search:**           | -                                                                                                                                |
| cross\_arithmetic                | Whole arithmetic crossover                                                                                                       |
| cross\_sim\_binary               | Simulated binary crossover [[DA+95]](../References/ref.html#DA+95)                                                               |
| cross\_point\_one                | One-point crossover                                                                                                              |
| cross\_point\_two                | Two-point crossover                                                                                                              |
| cross\_point\_n                  | n-point crossover                                                                                                                |
| cross\_point\_uniform            | Uniform crossover                                                                                                                |
| search\_cma                      | The evolution strategy with covariance matrix adaption                                                                           |
| search\_eda                      | The estimation of distribution                                                                                                   |
| search\_mu\_cauchy               | Cauchy mutation   [[YLL99]](../References/ref.html#YLL99)                                                                        |
| search\_mu\_gaussian             | Gaussian mutation [[Fog98]](../References/ref.html#Fog98)                                                                        |
| search\_mu\_polynomial           | Polynomial mutation [[DA+96]](../References/ref.html#DA+96)                                                                      |
| search\_mu\_uniform              | Uniform mutation                                                                                                                 |
| search\_pso                      | Particle swarm optimization's particle fly and update [[SE98]](../References/ref.html#SE98)                                      |
| search\_de\_random               | The "random/1" differential mutation    [[SP97]](../References/ref.html#SP97)                                                    |
| search\_de\_current              | The "current/1" differential mutation                                                                                            |
| search\_de\_current\_best        | The "current-to-best/1" differential mutation                                                                                    |
| reinit\_continuous               | Random reinitialization for continuous problems                                                                                  |
| **Discrete search:**             | -                                                                                                                                |
| cross\_point\_one                | One-point crossover                                                                                                              |
| cross\_point\_two                | Two-point crossover                                                                                                              |
| cross\_point\_n                  | n-point crossover                                                                                                                |
| cross\_point\_uniform            | Uniform crossover                                                                                                                |
| search\_reset\_one               | Reset a randomly selected entity to a random value                                                                               |
| search\_reset\_rand              | Reset each entity to a random value with a probability                                                                           |
| search\_reset\_creep             | Add a small positive or negative value to each entity with a probability, for problems with ordinal attributes                   |
| reinit\_discrete                 | Random reinitialization for discrete problems                                                                                    |
| **Permutation search:**          |                                                                                                                                  |
| cross\_order\_two                | Two-order crossover                                                                                                              |
| cross\_order\_n                  | n-order crossover                                                                                                                |
| search\_swap                     | Swap two randomly selected entities                                                                                              |
| search\_swap\_multi              | Swap each pair of entities between two randomly selected indices                                                                 |
| search\_scramble                 | Scramble all the entities between two randomly selected indices                                                                  |
| search\_insert                   | Randomly select two entities, insert the second entity to the position following the first one                                   |
| reinit\_permutation              | Random reinitialization for permutation problems                                                                                 |
| **Choose where to search from:** | -                                                                                                                                |
| choose\_roulette\_wheel          | Roulette wheel selection                                                                                                         |
| choose\_tournament               | K-tournament selection                                                                                                           |
| choose\_traverse                 | Choose each of the current solutions to search from                                                                              |
| choose\_cluster                  | Brain storm optimization's idea picking up for choosing solutions to search from [[Shi15]](../References/ref.html#Shi15)         |
| choose\_nich                     | Adaptive niching based on the nearest-better clustering                                                                          |
| **Select promising solutions:**  | -                                                                                                                                |
| update\_always                   | Always select new solutions                                                                                                      |
| update\_greedy                   | Select the best solutions                                                                                                        |
| update\_pairwise                 | Select the better solution from each pair of old and new solutions                                                               |
| update\_round\_robin             | Select solutions by round-robin tournament                                                                                       |
| update\_simulated\_annealing     | Simulated annealing's update mechanism, i.e., accept worse solution with a probability [[KGJV83]](../References/ref.html#KGJV83) |
| **Archive:**                     | -                                                                                                                                |
| archive\_best                    | Collect the best solutions found so far                                                                                          |
| archive\_diversity               | Collect most diversified solutions found so far                                                                                  |
| archive\_tabu                    | The tabu list [[Glo89]](../References/ref.html#Glo89)                                                                            |



+ Flexibility to designing diverse algorithms - Design algorithms with diverse structures in a single run, enables great possibility to find novel and efficient algorithms.
 Fair benchmark of various design objectives and techniques. 
  + Various design objectives, e.g., solution quality, runtime, and anytime performance.
    
    <a name="table2"></a>
    <div style="text-align: center;">Table 2: Design objectives involved in AutoOptLib.</div>

  + Different design techniques, e.g., racing, intensification, and surrogate.
    
    <a name="table3"></a>
    <div style="text-align: center;">Table 3: Algorithm performance evaluation methods provided in AutoOptLib.</div>

+ Good accessibility - Graphical user interface (GUI) for users to input problems, manage the algorithm design process, make experimental comparisons, and visualize results with simple one-clicks.
+ Easy extensibility - Easily add new algorithmic components, objectives, and techniques by a uniform interface.
