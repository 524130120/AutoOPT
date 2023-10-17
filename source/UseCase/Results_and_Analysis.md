# 4.3 Results and Analysis

After AutoOptLib running terminates, the best algorithm (termed Alg*) found during design is verified
by the test instances. Alg*’s pseudocode is shown in Algorithm [1](./Use_AutoOptLib_to_the_Problem.html#algorithm1). Interestingly, the niching mechanism
choose_nich is involved, which restricts the following uniform crossover (cross_point_uniform with
crossover rate of 0.1229) to be performed between solutions within a niching area. The reset operation
(search_reset_one that resets one entity of the solution) further exploits the niching area. Finally,
the round-robin selection (update_round_robin) maintains diversity by probably selecting inferior
solutions. All these designs indicate that maintaining solution diversity may be necessary for escaping
local optima and exploring the unstructured and rugged landscape.

To investigate the designed algorithm’s efficiency, the algorithm is compared with baselines, i.e.,
random beamforming, sequential beamforming [[DZS+20]](../References/ref.html#DZS+20)<sup>[3](#3)</sup>, and three classic metaheuristic solvers, i.e., discrete
genetic algorithm (GA), iterative local search (ILS), and simulated annealing (SA)<sup>[4](#4)</sup>. The algorithms
were executed through the Solve mode of AutoOptLib on the five test instances for experimental
comparison. All the metaheuristic algorithms conducted population-based search with a population
size of 50 for a fair comparison. All algorithms terminated after 500000 function evaluations.

The algorithms’ performance is summarized in Table [5](./Use_AutoOptLib_to_the_Problem.html#table5). The performance is measured by final solutions’ fitness (reciprocal of the quality of service of all users). From Table [5](./Use_AutoOptLib_to_the_Problem.html#table5), sequential beamforming
is inferior to most of the metaheuristic solvers. This result confirms the ineligibility of decoupling RIS
elements and the need for global metaheuristic search. Among the metaheuristic solvers, Alg* outperforms others, especially in instances with large numbers of RIS elements (induce high-dimensional
rugged landscape). This performance can be attributed to its diversity maintenance ability. All the
above demonstrates the efficiency of AutoOptLib’s automated design techniques on the problem.

<br>

-------------------------------------------
<a name="3"></a><sup>3</sup> Sequential beamforming refers to exhaustively enumerating the phase shift of each element one-by-one on the basis
of random initial RIS phase shifts.

<a name="4"></a><sup>4</sup> The discrete GA is consisted by tournament mating selection, uniform crossover, random mutation, and round-robin environmental selection; the crossover and mutation rates are both predefined to 0.2. The ILS and SA perform
neighborhood search by randomly resetting one entity of the solution at each iteration.
