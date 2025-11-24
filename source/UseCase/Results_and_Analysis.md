# 4.3 Results and Analysis

After AutoOptLib running terminates, the best algorithm (termed Alg*) found during design is verified
by the test instances. Alg*’s pseudocode is shown in [Algorithm 1](#algorithm1). Interestingly, the niching mechanism choose_nich is involved, which restricts the following uniform crossover (cross_point_uniform with
crossover rate of 0.1229) to be performed between solutions within a niching area. The reset operation
(search_reset_one that resets one entity of the solution) further exploits the niching area. Finally,
the round-robin selection (update_round_robin) maintains diversity by probably selecting inferior
solutions. All these designs indicate that maintaining solution diversity may be necessary for escaping
local optima and exploring the unstructured and rugged landscape.

<a name="algorithm1"></a>
```matlab
Algorithm 1 Pseudocode of Alg*
1: S = initialize() // initialize solution set S
2: while stopping criterion not met do
3: S = choose_nich(S)
4: Snew = cross_point_uniform(0.1229, S)
5: Snew = search_reset_one(Snew)
6: S = update_round_robin(S, Snew)
7: end while    
```

To investigate the designed algorithm’s efficiency, the algorithm is compared with baselines, i.e.,
random beamforming, sequential beamforming [[DZS+20]](../References/ref.html#DZS+20)<sup>[3](#3)</sup>, and three classic metaheuristic solvers, i.e., discrete
genetic algorithm (GA), iterative local search (ILS), and simulated annealing (SA)<sup>[4](#4)</sup>. The algorithms
were executed through the Solve mode of AutoOptLib on the five test instances for experimental
comparison. All the metaheuristic algorithms conducted population-based search with a population
size of 50 for a fair comparison. All algorithms terminated after 50000 function evaluations.

The algorithms’ performance is summarized in [Table 5](#table5). The performance is measured by final solutions’ fitness (reciprocal of the quality of service of all users). From [Table 5](#table5), sequential beamforming
is inferior to most of the metaheuristic solvers. This result confirms the ineligibility of decoupling RIS
elements and the need for global metaheuristic search. Among the metaheuristic solvers, Alg* outperforms others, especially in instances with large numbers of RIS elements (induce high-dimensional
rugged landscape). This performance can be attributed to its diversity maintenance ability. All the
above demonstrates the efficiency of AutoOptLib’s automated design techniques on the problem.

<br>
<a name="table5"></a>
<div style="text-align: center;">Table 5: Average and standard deviation of performance on the beamforming problem. Best results are in bold.</div>
<br>

<table>
   <tr>
        <td rowspan="2" style="font-weight: bold">Algorithm</td> 
        <td colspan="5" style="font-weight: bold">Number of RIS elements in the problem instances</td>    
   </tr>
   <tr>
        <td style="font-weight: bold">120</td> 
        <td style="font-weight: bold">160</td>
        <td style="font-weight: bold">280</td> 
        <td style="font-weight: bold">320</td> 
        <td style="font-weight: bold">400</td>     
   </tr>
    <tr>
        <td style="font-weight: bold">Alg*</td>  
        <td >0.0332±5.05E-04</td>  
        <td >0.0312±4.84E-04</td>  
        <td >0.0281±1.57E-04</td>  
        <td >0.0272±6.76E-04</td>
        <td >0.0260±1.11E-04</td>  
    </tr>
    <tr>
        <td style="font-weight: bold">Random</td> 
        <td >0.0442±7.94E-04</td>  
        <td >0.0425±6.56E-04</td>   
        <td >0.0402±8.30E-04 </td>  
        <td >0.0390±6.67E-04</td>
        <td >0.0390±6.67E-04</td>  
    </tr>
    <tr>
        <td style="font-weight: bold">Sequential</td>  
        <td >0.0382±6.19E-04</td>  
        <td >0.0387±6.75E-04</td>  
        <td >0.0374±4.17E-04</td>  
        <td >0.0369±4.38E-04</td>
        <td >0.0369±4.38E-04</td>  
    </tr>
    <tr>
        <td style="font-weight: bold">GA</td>  
        <td >0.0369±3.30E-04</td>  
        <td >0.0356±1.00E-04</td>  
        <td >0.0337±4.26E-04</td>  
        <td >0.0333±1.04E-04</td>
        <td >0.0322±6.96E-04</td>  
    </tr>
    <tr>
        <td style="font-weight: bold">ILS</td>  
        <td >0.0333±3.74E-04</td>  
        <td >0.0314±2.49E-04</td>  
        <td >0.0314±2.49E-04</td>  
        <td >0.0279±1.82E-04</td>
        <td >0.0278±1.15E-04</td>  
    </tr>
    <tr>
        <td style="font-weight: bold">SA</td>  
        <td >0.0398±5.59E-04</td>  
        <td >0.0388±7.75E-04</td>
        <td >0.0369±3.27E-04</td>  
        <td >0.0360±4.18E-04</td>
        <td >0.0355±9.50E-04</td>  
    </tr>
</table>

<br>

<br>

-------------------------------------------
<a name="3"></a><sup>3</sup> Sequential beamforming refers to exhaustively enumerating the phase shift of each element one-by-one on the basis
of random initial RIS phase shifts.

<a name="4"></a><sup>4</sup> The discrete GA is consisted by tournament mating selection, uniform crossover, random mutation, and round-robin environmental selection; the crossover and mutation rates are both predefined to 0.2. The ILS and SA perform
neighborhood search by randomly resetting one entity of the solution at each iteration.
