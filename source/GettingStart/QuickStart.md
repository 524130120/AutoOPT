# 1.3 Quick Start
Following the steps to use AutoOptLib:
1. Install AutoOptLib (add the repository to the Matlab path, or follow the Python installation steps in Section [1.2](./Installation.html)).
2. Implement the target optimization problem.
3. Define the space for designing algorithms.
4. Run AutoOptLib by command or GUI.
Steps 2, 3, and 4 will be detailed in Sections [2.3.1](../UserGuide/Use_AutoOptLib.html#implement-problem),
[2.3.2](../UserGuide/Use_AutoOptLib.html#define-design-space), and [2.3.3](../UserGuide/Use_AutoOptLib.html#run-autooptlib), respectively.

Below is a minimal Python example for running a small design experiment; save it as `examples/design_demo.py` and run `python examples/design_demo.py`:

```python
from autooptlib import autoopt


final_algs, alg_trace = autoopt(
    Mode="design",
    Problem="cec2013_f1",
    InstanceTrain=[10],
    InstanceTest=[10],
    AlgN=2,
    AlgFE=80,
    ProbN=20,
    ProbFE=800,
    Evaluate="exact",
    Compare="average",
    Archive=["archive_best"],
)

print("Best validation metric:", final_algs[0].ave_perform_all().min())
```
