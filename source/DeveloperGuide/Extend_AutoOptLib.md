# 3.1 Extend AutoOptLib

AutoOptLib follows the open-closed principle [[Mey97](../References/ref.html#Mey97), [Lar01](../References/ref.html#Lar01)]. Users can implement their 
algorithmic components, design objectives, and algorithm performance evaluation techniques based on the current
sources, and add the implementations to the library by a uniform interface. Taking Listing 1 as an
example, new algorithmic components can be added as follows.

<a name="listing1"></a>
<div style="text-align: center;">Listing 1: Implementation of the uniform mutation operator.</div>

```matlab
function [output1,output2] = search_mu_uniform(varargin)
mode = varargin{end};
switch mode
    case 'execute'
        Parent  = varargin{1};
        Problem = varargin{2};
        Para    = varargin{3};
        Aux     = varargin{4};
        if ~isnumeric(Parent)
            Offspring = Parent.decs;
        else
            Offspring = Parent;
        end
        Prob  = Para;
        [N,D] = size(Offspring);      
        Lower = Problem.bound(1,:);
        Upper = Problem.bound(2,:);
        ind = rand(N,D) < Prob;
        Temp = unifrnd(repmat(Lower,N,1),repmat(Upper,N,1));
        Offspring(ind) = Temp(ind);
        output1 = Offspring;
        output2 = Aux;   
    case 'parameter'
        output1 = [0,0.3]; % mutation probability 
    case 'behavior'
        output1 = {'LS','small';'GS','large'}; % small probabilities perform local search
end
if ~exist('output1','var')
    output1 = [];
end
if ~exist('output2','var')
    output2 = [];
end

```


An algorithmic component is implemented in an independent function with three main cases.
Case **execute** refers to executing the component. There are seven optional inputs:
1. Current solutions, i.e., **Parent** in line 5.
2. The problem proprieties, i.e., **Problem** in line 6.
3. The component’s inner parameters, i.e., **Para** in line 7.
4. An auxiliary structure array for saving the component’s inner parameters that are changed during
iteration (e.g., the velocity in particle swarm optimization (**PSO**)), i.e., **Aux** in line 8.
5. The algorithm’s generation counter **G**.
6. The algorithm’s inner local search iteration counter **innerG**.
7. The target problem’s input data **Data**.

The component should be implemented from line 9. The outputs of lines 21 and 22 are mandatory, in
which output1 returns solutions processed by the component, and **output2** returns the **Aux** structure
array. If the component has inner parameters that are changed during iteration, **Aux** is updated (e.g.,
update **PSO’s** velocity and save it in Aux); otherwise, **Aux** will be the same as that in line 8.

Case **parameter** defines the lower and upper bounds of the component’s inner parameter values. For
example, the mutation probability is bounded within [0, 0.3] in line 24. For components with multiple
inner parameters, each parameter’s lower and upper bounds should be saved in an independent row of
the matrix **output1**.

For search operators (components) with inner parameters controlling the search behavior, case
behavior defines how the inner parameters control the search behavior. For example, line 26 indicates that the uniform mutation with smaller mutation probabilities performs local search and that with
larger probabilities performs global search. For other operators, **output1** in case **behavior** is left empty, i.e., **output1={}**;.



