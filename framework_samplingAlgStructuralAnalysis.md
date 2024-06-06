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

<h4><i><p align = "justify" id = "results">Results in PAREpy Framework</p></i></h4>


Example 1
{: .label .label-blue }

<p align = "justify">Consider the simply supported beam shown in the Figure xx. The beam is subjected to a concentrated live load \(\left(P\right)\) and a uniformly distributed dead load \(\left(w\right)\). The loads are random variables. Assume that \(P\), \(w\) and the yield stress \(\left(f_y\right)\), are random quantities; the lenght \(L=18\;ft\) and plastic section modulus \(Z=80\;in³\) are assumed to be precisely known (deterministic) <a href="#ref1">[1]</a>. Using Crude Monte Carlo method determine the value of \(\beta\) index. Use serial architecture and 500.000 samples to solve this example.</p>

<table style = "width:100%">
   <thead>
     <tr>
       <th>Name</th>
       <th>Mean</th>
       <th>Standard Deviation</th>
     </tr>
   </thead>
   <tr>
       <td>Yield stress \(\left(f_y\right)\)</td>
       <td>40.3 \(ksi\)</td>
       <td>4.64 \(ksi\)</td>
   </tr>
   <tr>
       <td>Concentrated live load \(\left(P\right)\)</td>
       <td>10.2 \(kip\)</td>
       <td>1.12 \(kip\)</td>
   </tr>
   <tr>
       <td>Uniformly distributed dead load \(\left(w\right)\)</td>
       <td>0.25 \(kip/in\)</td>
       <td>0.025 \(kip/in\)</td>
   </tr>
</table>

<p align = "center"><b>Table 1.</b> Random variables.</p>

```python
from parepy_toolbox import sampling_algorithm_structural_analysis

# Dataset
f = {'type': 'normal', 'loc': 40.3, 'scale': 4.64, 'seed': None}
p = {'type': 'normal', 'loc': 10.2, 'scale': 1.12, 'seed': None}
w = {'type': 'normal', 'loc': 0.25, 'scale': 0.025, 'seed': None}
vars = [f, p, w]

# PAREpy setup
setup = {
             'number of samples': 500000, 
             'number of dimensions': len(vars), 
             'numerical model': {'model sampling': 'mcs'}, 
             'variables settings': vars, 
             'number of state limit functions or constraints': 1, 
             'none variable': None,
             'objective function': nowak_example,
             'type process': 'serial',
             'name simulation': 'nowak_example',
        }

# Call algorithm
results, pf, beta = sampling_algorithm_structural_analysis(setup)

# Output details
print('Beta index: ', beta[0][0])
```

```bash
Beta index:  3.0123892463595308
```

{: .warning }
> As a result, the first id in the list indicates the id of the state limit function. The second id in the results indicates the outcome of the reliability process. In stochastic analysis, the list is formed by sequence results in each time step. See the second example following.

Example 2
{: .label .label-blue }

<p align = "justify">Consider the simply supported beam shown in the Figure xx. The beam is subjected to a concentrated live load \(\left(P\right)\) and a uniformly distributed dead load \(\left(w\right)\). The loads are random variables. Assume that \(P\), \(w\) and the yield stress \(\left(f_y\right)\), are random quantities; the lenght \(L=18\;ft\) and plastic section modulus \(Z=80\;in³\) are assumed to be precisely known (deterministic) <a href="#ref1">[1]</a>. Using Crude Monte Carlo method determine the value of \(\beta\) index. Use serial architecture and 500.000 samples to solve this example.</p>

<table style = "width:100%">
   <thead>
     <tr>
       <th>Name</th>
       <th>Mean</th>
       <th>Standard Deviation</th>
     </tr>
   </thead>
   <tr>
       <td>Yield stress \(\left(f_y\right)\)</td>
       <td>40.3 \(ksi\)</td>
       <td>4.64 \(ksi\)</td>
   </tr>
   <tr>
       <td>Concentrated live load \(\left(P\right)\)</td>
       <td>10.2 \(kip\)</td>
       <td>1.12 \(kip\)</td>
   </tr>
   <tr>
       <td>Uniformly distributed dead load \(\left(w\right)\)</td>
       <td>0.25 \(kip/in\)</td>
       <td>0.025 \(kip/in\)</td>
   </tr>
</table>

<p align = "center"><b>Table 1.</b> Random variables.</p>

```python
from parepy_toolbox import sampling_algorithm_structural_analysis

# Dataset
f = {'type': 'normal', 'loc': 40.3, 'scale': 4.64, 'seed': None}
p = {'type': 'normal', 'loc': 10.2, 'scale': 1.12, 'seed': None}
w = {'type': 'normal', 'loc': 0.25, 'scale': 0.025, 'seed': None}
vars = [f, p, w]

# PAREpy setup
setup = {
             'number of samples': 500000, 
             'number of dimensions': len(vars), 
             'numerical model': {'model sampling': 'mcs'}, 
             'variables settings': vars, 
             'number of state limit functions or constraints': 1, 
             'none variable': None,
             'objective function': nowak_example,
             'type process': 'serial',
             'name simulation': 'nowak_example',
        }

# Call algorithm
results, pf, beta = sampling_algorithm_structural_analysis(setup)

# Output details
print('Beta index: ', beta[0][0])
```

```bash
Beta index:  3.0123892463595308
```

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



