---
layout: home
parent: Framework
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
'numerical model': {'model sampling': 'mcs-time', 'time analysis': 5}
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
        <td><code>'time analysis'</code></td>
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
        <td>float</td>
    </tr>
    <tr>
        <td><code>'seed'</code></td>
        <td>Random seed. Use <code>None</code> for random seed</td>
        <td>float</td>
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

<p align = "center"><b>Figure 1.</b> Normal Distribution using Sampling function.</p>
<center><img src="assets/images/normal_distribution.svg" width="70%"></center>

Example 2
{: .label .label-blue }

<p align = "justify">
    <i>In this example, we will use the <code>sampling</code> function to generate a set of random samples \((n=1000)\) following a Gumbel Max distribution with mean \(\mu = 3\) and standard deviation \(\sigma = 1\). Use "seed without control" in your setup.</i>
</p>

```python
from parepy_toolbox import sampling

# Dataset
model = {'model sampling': 'mcs'}
f = {'type': 'gumbel max', 'loc': 3.00, 'scale': 1.00, 'seed': None}
varSet = [f]

# Call function
randomVariables = sampling(1000, len(varSet), model, varSet)

# Output details
print(f'random variables n={len(randomVariables)}: \n\n {randomVariables} \n\n type variable: {type(randomVariables)}')
```

```bash
random variables n=1000: 

 [[2.54344536]
 [3.4132256 ]
 [2.07157173]
 [3.17322365]
 [5.08129471]
 [4.8650879 ]
 [3.12570801]
 [3.07478402]
...
 [4.24404437]
 [6.77645712]]

 type variable: <class 'numpy.ndarray'>
```

<p align = "center"><b>Figure 2.</b> Gumbel Max Distribution using Sampling function.</p>
<center><img src="assets/images/gumbelmax_distribution.svg" width="70%"></center>

Example 3
{: .label .label-blue }

<p align = "justify">
    <i>In this example, we will use the <code>sampling</code> function to generate a set of random samples \((n=1000)\) following a Gumbel Min distribution with mean \(\mu = 3\) and standard deviation \(\sigma = 1\). Use "seed without control" in your setup.</i>
</p>

```python
from parepy_toolbox import sampling

# Dataset
model = {'model sampling': 'mcs'}
f = {'type': 'gumbel min', 'loc': 3.00, 'scale': 1.00, 'seed': None}
varSet = [f]

# Call function
randomVariables = sampling(1000, len(varSet), model, varSet)

# Output details
print(f'random variables n={len(randomVariables)}: \n\n {randomVariables} \n\n type variable: {type(randomVariables)}')
```

```bash
random variables n=1000: 

 [[ 3.54288578e+00]
 [ 1.31047287e+00]
 [ 1.58150807e+00]
 [ 2.58028790e+00]
 [ 2.12311530e+00]
 [ 3.10283340e+00]
 [ 1.04313183e+00]
 [ 7.91284471e-01]
...
 [ 3.48637502e+00]
 [ 2.03970523e+00]]

 type variable: <class 'numpy.ndarray'>
```

<p align = "center"><b>Figure 3.</b> Gumbel Min Distribution using Sampling function.</p>
<center><img src="assets/images/lognormal_distribution.png" width="70%"></center>

Example 4
{: .label .label-blue }

<p align = "justify">
    <i>In this example, we will use the <code>sampling</code> function to generate a set of random samples \((n=1000)\) following a Weibull distribution with mean \(\mu = 3\) and standard deviation \(\sigma = 1\). Use "seed without control" in your setup.</i>
</p>

```python
from parepy_toolbox import sampling

# Dataset
model = {'model sampling': 'mcs'}
f = {'type': 'weibull', 'loc': 3.00, 'scale': 1.00, 'seed': None}
varSet = [f]

# Call function
randomVariables = sampling(1000, len(varSet), model, varSet)

# Output details
print(f'random variables n={len(randomVariables)}: \n\n {randomVariables} \n\n type variable: {type(randomVariables)}')
```

```bash
random variables n=1000: 

 [[ 3.54288578e+00]
 [ 1.31047287e+00]
 [ 1.58150807e+00]
 [ 2.58028790e+00]
 [ 2.12311530e+00]
 [ 3.10283340e+00]
 [ 1.04313183e+00]
 [ 7.91284471e-01]
...
 [ 3.48637502e+00]
 [ 2.03970523e+00]]

 type variable: <class 'numpy.ndarray'>
```

<p align = "center"><b>Figure 3.</b> Gumbel Min Distribution using Sampling function.</p>
<center><img src="assets/images/lognormal_distribution.png" width="70%"></center>
