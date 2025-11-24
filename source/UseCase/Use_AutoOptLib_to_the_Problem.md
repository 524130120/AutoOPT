# 4.2 Use AutoOptLib to the Problem

AutoOptLib is used according to the three steps detailed in Sections [2.3.1](../UserGuide/Use_AutoOptLib.html#implement-problem),
[2.3.2](../UserGuide/Use_AutoOptLib.html#step-2-define-design-space), and [2.3.3](../UserGuide/Use_AutoOptLib.html#step-3-run-autooptlib), respectively:
<br>

1.Implement problem: The target problem is implemented according to the template prob template.m.
In particular, in line 35, get_sum_rate is the user’s method for calculating solutions’ objective
values (constraint violations have been involved in the objective values).

```matlab
 1: switch varargin{end}
 2:     case 'construct' % define problem properties
 3:         Problem  = varargin{1};
 4:         instance = varargin{2};       
 5: 
 6:         orgData  = load('Beanforming.mat','Data');
 7:         Data = orgData.Data((instance));
 8:         for i = 1:length(instance)
 9:             D = size(Data(i).G,1);
10:             phases_cnt = 2^Data(i).b-1;
11:             lower = zeros(1,D); % 1*D, lower bound of the D-dimension decision space
12:             upper = repmat(phases_cnt,1,D); % 1*D, upper bound of the D-dimension decision space
13:             Problem(i).type = {'discrete','static','certain'};
14:             Problem(i).bound = [lower;upper];
15:         end
16:         
17:         output1 = Problem;
18:         output2 = Data;
19: 
20:     case 'repair' % repair solutions
21:         Decs = varargin{2};
22:         output1 = Decs;
23:     
24:     case 'evaluate' % evaluate solution's fitness
25:         Data = varargin{1}; % load problem data
26:         m    = varargin{2}; % load the current solution(s)
27:         
28:         b     = Data.b;
29:         PT    = Data.PT;
30:         G     = Data.G;
31:         Hd    = Data.Hd;
32:         Hr    = Data.Hr;
33:         omega = Data.omega;
34:       
35:         sR = get_sum_rate(m,b,Hd, Hr,G,PT,omega); % calculate objective value
36:         sR = sR'; % N*1
37: 
38:         output1 = sR; % matrix for saving objective function values
39: end
40: 
41: if ~exist('output2','var')
42:     output2 = [];
43: end
44: if ~exist('output3','var')
45:     output3 = [];
46: end
47: end
```
<br>

2.Define design space: AutoOptLib’s default design space (with all components for discrete problems,
as shown in [Figure 1](../UserGuide/auto_alg_design.html#Fig1) and [Listing 1](../UserGuide/Use_AutoOptLib.html#listing1), respectively) is utilized.

3.Run AutoOptLib: AutoOptLib is executed by the command `AutoOpt(‘Mode’, ‘design’, ‘Problem’,
‘beamforming’, ‘InstanceTrain’, [1:5], ‘InstanceTest’, [6:10], ‘Metric’, ‘quality’)`,
where 10 problem instances with different numbers of RIS elements are considered; five of the
instances are chosen as training instances; another five are for test; solution quality is set as the
design objective (metric); other settings are kept default.
<br>
<br>
<br>


<style>
	th,td{
    border: 1px solid #999;
    text-align: center;
    padding: 20px 0;
}

table{
    width: 100%;
    border-collapse: collapse;
    font-size: 12px;
}
</style>
