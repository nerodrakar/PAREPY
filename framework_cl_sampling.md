---
layout: home
parent: common_library
grand_parent: Framework
nav_order: 1
has_children: false
has_toc: false
title: sampling
---

<!--Don't delete ths script-->
<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!--Don't delete ths script-->

<h3>sampling</h3>

<br>

<p align = "justify">
    This algorithm generates a set of random numbers according to a type of distribution.
</p>

```python
random_sampling = sampling(n_samples, d, model, variables_setup)
```

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
        <td><code>n_samples</code></td>
        <td>Number of samples</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>d</code></td>
        <td>Number of dimensions</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>model</code></td>
        <td><a href="#mode">Model parameters</a></td>
        <td>Dictionary</td>
    </tr>
    <tr>
        <td><code>variables_setup</code></td>
        <td><a href="#vars">Variables parameters</a></td>
        <td>List</td>
    </tr>
</table>

Output variables
{: .label .label-yellow}

<table style = "width:100%">
   <thead>
     <tr>
       <th>Name</th>
       <th>Description</th>
       <th>Type</th>
     </tr>
   </thead>
   <tr>
       <td><code>random_sampling</code></td>
       <td>Random samples.</td>
       <td>Numpy array</td>
   </tr>
</table>

<p align = "justify" id = "mode">
    See examples of model parameters.
</p>

<h4><i>Crude Monte Carlo</i></h4>

```python
'numerical model': {'model sampling': 'mcs'}
```

<table style = "width:100%">
    <thead>
      <tr>
        <th>Name</th>
        <th>Description</th>
        <th>Type</th>
      </tr>
    </thead> 
    <tr>
        <td><code>'model sampling'</code></td>
        <td>Numerical algorithm used in sampling generator</td>
        <td>String</td>
    </tr>
</table>

<h4><i>Crude Monte Carlo - Stochastic analysis</i></h4>

```python
'numerical model': {'model sampling': 'mcs-time', 'time steps': 5}
```

<table style = "width:100%">
    <thead>
      <tr>
        <th>Name</th>
        <th>Description</th>
        <th>Type</th>
      </tr>
    </thead> 
    <tr>
        <td><code>'model sampling'</code></td>
        <td>Numerical algorithm used in sampling generator</td>
        <td>String</td>
    </tr>
    <tr>
        <td><code>'time steps'</code></td>
        <td>Number of time steps used in times series analysis</td>
        <td>Integer</td>
    </tr>
</table>


<p align = "justify" id = "vars">
    See examples of variables parameters.
</p>

<h4><i>Normal sampling</i></h4>

```python
{'type': 'normal', 'loc': 40.3, 'scale': 4.64, 'seed': None}
```

<table style = "width:100%">
    <thead>
      <tr>
        <th>Name</th>
        <th>Description</th>
        <th>Type</th>
      </tr>
    </thead> 
    <tr>
        <td><code>'loc'</code></td>
        <td>Mean</td>
        <td>Float</td>
    </tr>
    <tr>
        <td><code>'scale'</code></td>
        <td>Standard deviation</td>
        <td>Float</td>
    </tr>
    <tr>
        <td><code>'seed'</code></td>
        <td>Random seed. Use <code>None</code> for random seed</td>
        <td>Float</td>
    </tr>
</table>

<h4><i>Normal sampling in time series</i></h4>

```python
{'type': 'normal', 'loc': 40.3, 'scale': 4.64, 'stochastic variable': False, 'seed': None}
```

<table style = "width:100%">
    <thead>
      <tr>
        <th>Name</th>
        <th>Description</th>
        <th>Type</th>
      </tr>
    </thead> 
    <tr>
        <td><code>'loc'</code></td>
        <td>Mean</td>
        <td>Float</td>
    </tr>
    <tr>
        <td><code>'scale'</code></td>
        <td>Standard deviation</td>
        <td>Float</td>
    </tr>
    <tr>
      <td><code>'seed'</code></td>
      <td>Random seed. Use <code>None</code> for random seed</td>
      <td>Integer</td>
    </tr>
    <tr>
        <td><code>'stochastic variable'</code></td>
        <td>This variable represents the behavior of the random variable over time intervals. <code>False</code> represents the variable with a fixed value at each time step, and <code>True</code> represents variable behavior at each time step</td>
        <td>Boolean</td>
    </tr>
</table>

Example 1
{: .label .label-blue }

<p align = "justify">
    <i>In this example, we will use the <code>sampling</code> function to generate a set of random samples \((n=1000)\) following a Normal distribution with mean \(\mu = 3\) and standard deviation \(\sigma = 1\). Use "seed without control" in your setup.</i>
</p>

```python
from parepy_toolbox import sampling

# Dataset
model = {'model sampling': 'mcs'}
f = {'type': 'normal', 'loc': 3.00, 'scale': 1.00, 'seed': None}
varSet = [f]

# Call function
randomVariables = sampling(1000, len(varSet), model, varSet)

# Output details
print(f'random variables n={len(randomVariables)}: \n\n {randomVariables} \n\n type variable: {type(randomVariables)}')
```

```bash
random variables n=1000: 

 [[2.01162417]
 [2.68475353]
 [2.78796797]
 [2.36281564]
 [4.60781551]
 [3.59727946]
 [2.24979497]
 [2.99149908]
...
 [1.31969787]
 [2.71006801]] 

 type variable: <class 'numpy.ndarray'>
```

<p align = "center"><b>Figure 3.</b> Gumbel Distribution using Sampling function.</p>
<center><img src="assets/images/lognormal_distribution.png" width="70%"></center>
