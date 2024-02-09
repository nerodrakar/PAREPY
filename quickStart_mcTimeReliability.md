---
layout: home
parent: Quick Start
nav_order: 1
has_children: false
has_toc: false
title: Monte Carlo and Structural Time Reliability
---

<!--Don't delete this script-->
<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!--Don't delete this script-->

<h1>Steel beam and progressive damage</h1>

<p align="justify">
A simply supported timber beam of length 5 \(m\) is loaded with a central load Q having mean \(\mu_Q =\) 3 \(kN\) and with a coefficient of variation (COV) of 0.33 (Normal distribuition). The bending strength of similar beams has been found to have a mean strength \(\mu_R =\) 10 \(kN.m\) with a coefficient of variation (COV) of 0.15 (Normal distribuition). It is desired to evaluate the probability of failure.
</p> 

of_file
{: .label .label-green }

```python
def nowak_example(x, none_variable):
    """Objective function for the Nowak example (tutorial).
    """
    # Time id and value
    id_analysis = int(x[-1])
    time_step = none_variable['time analysis']
    t_i = time_step[id_analysis]

    # Random variables
    f_y = x[0]
    p_load = x[1]
    w_load = x[2]
    if t_i == 0:
        degrad = 1
    else:
        degrad = 1 - (0.2/t_i)/100

    # Capacity and demand
    capacity = 80*f_y*degrad
    demand = 54*p_load + 5832*w_load

    # State limit function
    constraint = demand - capacity

    return [capacity], [demand], [constraint]
```

your_problem
{: .label .label-green }
```python
# Libraries
import pandas as pd
pd.set_option('display.max_columns', None)
import numpy as np

from parepy_toolbox import sampling_algorithm_structural_analysis
from obj_function import nowak_example

# Variables, setup and run
# Settings
f_y = ['normal', 40.3, 4.64, 1, None]
p_load = ['normal', 10.2, 1.12, 1, None]
w_load = ['normal', 0.25, 0.025, 10, None]
variables = [f_y, p_load, w_load]

# PAREpy setup
setup = {
             'number of samples': 5, 
             'number of dimensions': len(variables), 
             'numerical model': {'model sampling': 'mcs-time', 'time analysis': 10}, 
             'variables settings': variables, 
             'number of state limit functions or constraints': 1, 
             'none variable': {'time analysis': list(np.linspace(1, 50, num=10, endpoint=True))},
             'objective function': nowak_example,
             'type process': 'serial',
             'name simulation': 'nowak_example',
        }

# Call algorithm
results, pf, beta = sampling_algorithm_structural_analysis(setup)
```

```bash
PARE^py Report: 

- Output file name: nowak_example_MCS-TIME_20240207-204929.txt
- Processing time (s): 0.1849977970123291
```

<p align="justify">
See more details in <a href="https://www.w3schools.com" target="_blank"><b>sampling_algorithm_structural_analysis</b></a>.
</p> 