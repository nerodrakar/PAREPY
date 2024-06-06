---
layout: home
parent: Framework
nav_order: 2
has_children: false
has_toc: false
title: sampling_algorithm_structural_analysis
---

<!--Don't delete ths script-->
<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!--Don't delete ths script-->

<h3>sampling_algorithm_structural_analysis</h3>
<br>
```python
df_results, pf, beta = sampling_algorithm_structural_analysis(setup)
```

<p align = "justify">
    This function creates the samples and evaluates the limit state functions in structural reliability problems.
</p>

Input variables
{: .label .label-yellow }

<table style = "width:100%">
    <thead>
      <tr>
        <th>Name</th>
        <th>Description</th>
        <th>Type</th>
      </tr>
    </thead>
    <tr>
        <td><code>setup</code></td>
        <td>algorithms settings</td>
        <td>Dictionary</td>
    </tr>
    <tr>
        <td><code>'number of samples'</code></td>
        <td>Number of samples (key in setup dictionary)</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>'dimension'</code></td>
        <td>Number of dimensions (key in setup dictionary)</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>'numerical model'</code></td>
        <td><a href="https://wmpjrufg.github.io/PAREPY/framework_cl_sampling.html#mode" target="_blank" rel="noopener noreferrer">Model parameters</a> (key in setup dictionary)</td>
        <td>Dictionary</td>
    </tr>
    <tr>
        <td><code>'variables settings'</code></td>
        <td><a href="https://wmpjrufg.github.io/PAREPY/framework_cl_sampling.html#vars" target="_blank" rel="noopener noreferrer">Variables parameters</a> (key in setup dictionary)</td>
        <td>List</td>
    </tr>
    <tr>
        <td><code>'number of state limit functions or constraints'</code></td>
        <td>Number of state limit functions or constraints (key in setup dictionary)</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>'none_variable'</code></td>
        <td>None variable. Default is None. User can use this variable in objective function (key in setup dictionary)</td>
        <td>None, list, float, dictionary, str or any</td>
    </tr>
    <tr>
        <td><code>'objective function'</code></td>
        <td>Objective function. The Parepy user defined this function (key in setup dictionary)</td>
        <td>Python function [def]</td>
    </tr>
    <tr>
        <td><code>'type process'</code></td>
        <td><a href="#arch">Type process</a>. Options: 'auto', 'parallel' or 'serial' (key in setup dictionary)</td>
        <td>String</td>
    </tr>
    <tr>
        <td><code>'name simulation'</code></td>
        <td>Output filename (key in setup dictionary)</td>
        <td>String</td>
    </tr>
</table>

Output variables
{: .label .label-yellow }

<table style = "width:100%">
   <thead>
     <tr>
       <th>Name</th>
       <th>Description</th>
       <th>Type</th>
     </tr>
   </thead>
   <tr>
       <td><code>results_about_data</code></td>
       <td><a href="#results">Results about reliability analysis</a></td>
       <td>Dataframe</td>
   </tr>
    <tr>
       <td><code>failure_prob_list</code></td>
       <td><a href="#results">Failure probability list</a></td>
       <td>List</td>
   </tr>
    <tr>
       <td><code>beta_list</code></td>
       <td><a href="#results">Beta list</a></td>
       <td>List</td>
   </tr>
</table>

<h3>Architecture of algorithm</h3>

<p align = "justify" id = "arch">
    See examples of Architecture of algorithm.
</p>

<h4><i>Serial process</i></h4>

<p align = "justify" id = "arch">
Serial architecture processing is attending to and processing one item at a time.
</p>

```python
'type process': 'serial'
```

<h4><i>Parallel process</i></h4>

<p align = "justify" id = "arch">
Parallel achitecture processing is the act of attending to and processing all items simultaneously.
</p>

```python
'type process': 'parallel'
```

<h4><i>Automatic process</i></h4>

<p align = "justify" id = "arch">
The algorithm runs ten times the objective function and chooses the achitecture to spend the minimum amount of time.
</p>

```python
'type process': 'auto'
```

Example 1
{: .label .label-blue }

<p align="justify">
Consider the simply supported beam show in example 5.1 Nowak and Collins <a href="#ref1">[1]</a>. The beam is subjected to a concentrated live load \(p\) and a uniformly distributed dead load \(w\). The loads are random variables. Assume \(\boldsymbol{P}, \boldsymbol{W}\) and the yield stress, \(\boldsymbol{F_y}\), are random quantities; the length \(l\) and the plastic setion modulus \(z\) are assumed to be precisely know (deterministic). The distribution parameters for \(\boldsymbol{P}, \boldsymbol{W}\) and \(\boldsymbol{F_y}\) are given bellow:<br><br>
<table style = "width:100%">
    <tr>
        <th style="width: 25%;">Variable</th>
        <th style="width: 25%;">Distribution</th>
        <th style="width: 25%;">Mean</th>
        <th style="width: 25%;">coefficient of variation (COV)</th>
    </tr>
    <tr>
        <td style="width: 25%;">Live load (\(\boldsymbol{F_y}\))</td>
        <td style="width: 25%;">Normal</td>
        <td style="width: 25%;">40.3</td>
        <td style="width: 25%;">0.115</td>
    </tr>
    <tr>
        <td style="width: 25%;">Live load (\(\boldsymbol{P}\))</td>
        <td style="width: 25%;">Gumbel max.</td>
        <td style="width: 25%;">10.2</td>
        <td style="width: 25%;">0.110</td>
    </tr>
    <tr>
        <td style="width: 25%;">Dead load (\(\boldsymbol{W}\))</td>
        <td style="width: 25%;">Log-normal</td>
        <td style="width: 25%;">0.25</td>
        <td style="width: 25%;">0.100</td>
    </tr>
</table>

The limit state function for beam bending can be expressed as:

<table style = "width:100%">
    <tr>
        <td style="width: 90%;">\[ \boldsymbol{R} = 80 \cdot \boldsymbol{F_y} \]</td>
        <td style="width: 10%;"><p align = "right" id = "eq1">(1)</p></td>
    </tr>
    <tr>
        <td style="width: 90%;">\[ \boldsymbol{S} = 54 \cdot \boldsymbol{P} + 5832 \cdot \boldsymbol{W} \]</td>
        <td style="width: 10%;"><p align = "right" id = "eq2">(2)</p></td>
    </tr>
    <tr>
        <td style="width: 90%;">\[ \boldsymbol{G} = \boldsymbol{S} - \boldsymbol{R} \begin{cases}
\leq 0 & \text{safe}\\ 
> 0 & \text{failure}
\end{cases} \]</td>
        <td style="width: 10%;"><p align = "right" id = "eq3">(3)</p></td>
    </tr>
</table>


</p> 
<h3><code>of_file.py</code></h3>

```python
def nowak_collins_example(x, none_variable):
    """Objective function for the Nowak example (tutorial).
    """

    # Random variables
    f_y = x[0]
    p_load = x[1]
    w_load = x[2]
    capacity = 80*f_y
    demand = 54*p_load + 5832*w_load

    # State limit function
    constraint = demand - capacity

    return [capacity], [demand], [constraint]
```

<h3><code>your_problem.ipynb</code></h3>

```python
# Libraries
import pandas as pd
pd.set_option('display.max_columns', None)
import numpy as np

from parepy_toolbox import sampling_algorithm_structural_analysis
from obj_function import nowak_collins_example

# Dataset
f = {'type': 'normal', 'loc': 40.3, 'scale': 4.64, 'seed': None}
p = {'type': 'gumbel max', 'loc': 10.2, 'scale': 1.12, 'seed': None}
w = {'type': 'lognormal', 'loc': 0.25, 'scale': 0.025, 'seed': None}
var = [f, p, w]

# PAREpy setup
setup = {
             'number of samples': 10000, 
             'number of dimensions': len(var), 
             'numerical model': {'model sampling': 'mcs'}, 
             'variables settings': var, 
             'number of state limit functions or constraints': 1, 
             'none variable': None,
             'objective function': nowak_collins_example,
             'type process': 'auto',
             'name simulation': 'nowak_collins_example',
        }

# Call algorithm
results, pf, beta = sampling_algorithm_structural_analysis(setup)
```

```bash
PARE^py Report: 

- Output file name: nowak_example_MCS_20240505-135418.txt
- Processing time (s): 7.355956315994263  (serial kernel)
```

<h4><i><p align = "justify" id = "results">Results in PAREpy framework</p></i></h4>

<p align = "justify">
To access results in structural reliability, you need to print <code>pf</code>, <code>beta</code>, and <code>results</code> variables.
<code>results</code> contain all samples about simulation. Just print this variable in the command window. See the content in Figure 1.
</p>

```python
# jupyter notebook file
results
```

```bash
# python file
prints(results)
```

<p align = "center"><b>Figure 1.</b> <code>results</code> content.</p>
<center><img src="assets/images/results_dataframe.png" width="80%"></center>

<p align = "justify">
<code>beta</code> and <code>pf</code> are list variables that contain respective values about reliability index and failure probability. Samples contains just one state limit function. Therefore, the <code>beta</code> and <code>pf</code> lists contain just one value.
</p>

```python
print(pf)
```

```bash
[[0.0022]]
```

<p align = "justify">
Use the command below to see results about the \(g_0\) state limit function.
</p>

```python
pf[0][0]
```

```bash
0.0022
```

{: .note }
> Apply the same process in the ```beta``` variable and obtain your results.

<h3>Reference list</h3>

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Reference</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><p align = "center" id = "ref1">[1]</p></td>
            <td><p align = "left"><a href="https://www.amazon.com.br/Reliability-Structures-Second-Andrzej-Nowak/dp/0415675758" target="_blank" rel="noopener noreferrer">Andrzej S. Nowak e Kevin R. Collins (2012). Reliability of Structures, Second Edition. CRC Press.</a></p></td>
        </tr>
    </tbody>
</table>



