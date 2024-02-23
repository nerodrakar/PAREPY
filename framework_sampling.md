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
        <td>Model settings</td>
        <td>Py dict</td>
    </tr>
    <tr>
        <td><code>variables_setup</code></td>
        <td>Variables settings</td>
        <td>Py list</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[0]</code> \(=\) Type of distribution</td>
        <td>String</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[1]</code> \(=\) loc of the distribution</td>
        <td>Float</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[2]</code> \(=\) scale of the distribution</td>
        <td>Float</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[3]</code> \(=\) Seeds used in the random sampling</td>
        <td>Integer or None</td>
    </tr>
</table>

<p align = "justify">
When it is necessary to generate a sample for time series, use the input presented below.
</p>

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
        <td>Model settings</td>
        <td>Py dict</td>
    </tr>
    <tr>
        <td><code>variables_setup</code></td>
        <td>Variables settings</td>
        <td>Py list</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[0]</code> \(=\) Type of distribution</td>
        <td>String</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[1]</code> \(=\) loc of the distribution</td>
        <td>Float</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[2]</code> \(=\) scale of the distribution</td>
        <td>Float</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[3]</code> \(=\) Number of time steps in temporal analysis</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td></td>
        <td>index <code>[4]</code> \(=\) Seeds used in the random sampling</td>
        <td>Integer or None</td>
    </tr>
</table>

<p align = "justify">
    The list of distributions used in <code>type_dist</code> are:
</p>

<ul>
    <li>Normal or Gaussian = <code>"gaussian"</code> or <code>"normal"</code>;</li>  
    <li>Gumbel Maximum = <code>"gumbel max"</code>; </li> 
    <li>Gumbel Minimum = <code>"gumbel min"</code>;</li>    
    <li>Log Normal = <code>"lognormal"</code>;</li>
    <li>Weibull = <code>"weibull"</code>;</li>
</ul>

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

Example 1
{: .label .label-blue }

<p align = "justify">
    <i>In this example, we will use the <code>sampling</code> function to generate a set of random samples \((n=10)\) following a Normal distribution with mean \(\mu = 3\) and standard deviation \(\sigma = 1\). Use "seed without control" in your setup.</i>
</p>

```python
from parepy_toolbox import sampling

# Dataset
x = ['normal', 3, 1, None]
vars_set = [x]
model = {'model sampling': 'mcs'}

# Call function
random_set = sampling(n_samples=10, d=len(vars_set), model=model, variables_setup=vars_set)

# Output details
print('random variables: \n\n', random_set)
```

```bash
random variables: 

[[4.83211826]
[2.54537651]
[2.98509002]
[3.92658834]
[4.94070085]
[4.66545679]
[3.69488262]
[3.0909251 ]
[4.10526687]
[4.2336168 ]]
```

Example 2
{: .label .label-blue }

<p align = "justify">
    <i>In this example, we will use the <code>sampling</code> function to generate a set of random samples \(n=10)\ following a Normal distribution with mean (\mu = 3\) and standard deviation\(\sigma = 1\). Use "seed without control" in your setup.</i>
</p>

```python
from parepy_toolbox import sampling

# Dataset
x = ['normal', 3, 1, None]
vars_set = [x]
model = {'model sampling': 'mcs'}

# Call function
random_set = sampling(n_samples=10, d=len(vars_set), model=model, variables_setup=vars_set)

# Output details
print('random variables: \n\n', random_set)
```

```bash
random variables: 

[[4.83211826]
[2.54537651]
[2.98509002]
[3.92658834]
[4.94070085]
[4.66545679]
[3.69488262]
[3.0909251 ]
[4.10526687]
[4.2336168 ]]
```

<p align = "center"><b>Figure 1.</b> Normal distribution using Sampling function.</p>
<center><img src="assets/images/normal_distribution.png" width="70%"></center>

Example 2
{: .label .label-yellow }

<p align = "justify">In this example, we will explore the SAMPLING function to generate random samples following the Gumbel Maximum (Gumbel Max) distribution. The Gumbel Max distribution is commonly used to model extreme value events, making it useful in various fields such as engineering and finance. We will set the number of samples to 1000 and the dimension to 1. Using the "MCS" (Monte Carlo Sampling) sampling model, we will configure a variable with the Gumbel Max distribution, specifying the location and scale parameters. Through this example, we will demonstrate how the SAMPLING function facilitates the generation of random samples that follow different distributions.</p>

```python
pip install PARE-TOOLBOX
from PARE_TOOLBOX import *
import numpy as np
import pandas as pd

kwargs = {
    'N_POP': 1000,
    'D': 1,
    'MODEL': 'MCS',
    'VARS': [
        ('GUMBEL MAX', 0, 1),
    ]
}

random, random_state = SAMPLING(**kwargs)
random_sampling = random.flatten()

# Data
DF =  pd.DataFrame({'col1': random_sampling})
COLUMN = 'col1'

# Chart config
CHART_CONFIG = {
              'NAME': f"{COLUMN}_Histogram",
              'EXTENSION': 'svg',
              'WIDTH': 0.20,
              'HEIGHT': 0.10,
              'X AXIS LABEL': '$x_{i}$ variable',
              'X AXIS SIZE': 15.5,
              'Y AXIS LABEL': 'Frequency',
              'Y AXIS SIZE': 15.5,
              'AXISES COLOR': '#000000',
              'LABELS SIZE': 15.5,
              'LABELS COLOR': '#000000',
              'CHART COLOR': '#2219F0',
              'BINS': 20,
              'DPI': 600,
             }

# Data statement
DATA = {
         'DATASET': DF,
         'COLUMN': COLUMN
       }

# Call function
HISTOGRAM_CHART(DATASET = DATA, PLOT_SETUP = CHART_CONFIG)
```

<p align = "center"><b>Figure 2.</b> Gumbel Distribution using Sampling function.</p>
<center><img src="assets/images/gumbelmax_distribution.png" width="70%"></center>

Example 3
{: .label .label-yellow }

<p align = "justify">In this new example, we will delve into the SAMPLING function once again, this time generating random samples that adhere to the Gumbel Minimum (Gumbel Min) distribution. The Gumbel Min distribution is commonly employed to model extreme minimum values, making it suitable for applications such as analyzing rare events in engineering and environmental sciences. With the number of samples set at 1000 and the dimension at 1, we will utilize the "MCS" (Monte Carlo Sampling) sampling model. By configuring a variable with the Gumbel Min distribution, specifying the location and scale parameters, we will demonstrate how the SAMPLING function facilitates the creation of random samples that align with distinct distributions.</p>

```python
pip install PARE-TOOLBOX
from PARE_TOOLBOX import *
import numpy as np
import pandas as pd

kwargs = {
    'N_POP': 1000,
    'D': 1,
    'MODEL': 'MCS',
    'VARS': [
        ('GUMBEL MIN', 0, 1),
    ]
}

random, random_state = SAMPLING(**kwargs)
random_sampling = random.flatten()

# Data
DF =  pd.DataFrame({'col1': random_sampling})
COLUMN = 'col1'

# Chart config
CHART_CONFIG = {
              'NAME': f"{COLUMN}_Histogram",
              'EXTENSION': 'svg',
              'WIDTH': 0.20,
              'HEIGHT': 0.10,
              'X AXIS LABEL': '$x_{i}$ variable',
              'X AXIS SIZE': 15.5,
              'Y AXIS LABEL': 'Frequency',
              'Y AXIS SIZE': 15.5,
              'AXISES COLOR': '#000000',
              'LABELS SIZE': 15.5,
              'LABELS COLOR': '#000000',
              'CHART COLOR': '#2219F0',
              'BINS': 20,
              'DPI': 600,
             }

# Data statement
DATA = {
         'DATASET': DF,
         'COLUMN': COLUMN
       }

# Call function
HISTOGRAM_CHART(DATASET = DATA, PLOT_SETUP = CHART_CONFIG)
```

<p align = "center"><b>Figure 3.</b> Gumbel Distribution using Sampling function.</p>
<center><img src="assets/images/gumbelmin_distribution.png" width="70%"></center>

Example 4

In this new example, we will utilize the SAMPLING function once again to generate a set of random samples following a Lognormal distribution. The Lognormal distribution is frequently employed to model data with positive skewness and non-symmetrical distribution. We will set the number of samples to 2000 and the dimension to 1. Employing the "MCS" (Monte Carlo Sampling) sampling model, we will configure a variable with a Lognormal distribution, specifying the shape and location parameters. Through this example, we aim to illustrate how the SAMPLING function can be applied to generate random samples adhering to diverse distributions.

```python
pip install PARE-TOOLBOX
from PARE_TOOLBOX import *
import numpy as np
import pandas as pd

kwargs = {
    'N_POP': 2000,
    'D': 1,
    'MODEL': 'MCS',
    'VARS': [
        ('LOGNORMAL', 0.5, 1),
    ]
}

random, random_state = SAMPLING(**kwargs)
random_sampling = random.flatten()

# Data
DF =  pd.DataFrame({'col1': random_sampling})
COLUMN = 'col1'

# Chart config
CHART_CONFIG = {
              'NAME': f"{COLUMN}_Histogram",
              'EXTENSION': 'svg',
              'WIDTH': 0.20,
              'HEIGHT': 0.10,
              'X AXIS LABEL': '$x_{i}$ variable',
              'X AXIS SIZE': 15.5,
              'Y AXIS LABEL': 'Frequency',
              'Y AXIS SIZE': 15.5,
              'AXISES COLOR': '#000000',
              'LABELS SIZE': 15.5,
              'LABELS COLOR': '#000000',
              'CHART COLOR': '#2219F0',
              'BINS': 20,
              'DPI': 600,
             }

# Data statement
DATA = {
         'DATASET': DF,
         'COLUMN': COLUMN
       }

# Call function
HISTOGRAM_CHART(DATASET = DATA, PLOT_SETUP = CHART_CONFIG)
```

<p align = "center"><b>Figure 3.</b> Gumbel Distribution using Sampling function.</p>
<center><img src="assets/images/lognormal_distribution.png" width="70%"></center>

Example 5
{: .label .label-yellow }

<p align = "justify">In the context of Monte Carlo Sampling (MCS), now the task involves simultaneously generating samples for two variables: one following a normal distribution and the other a maximum Gumbel distribution. Employing the <code>sampling</code> function, the first variable, characterized by a normal distribution, is assigned parameters such as mean (e.g., 10) and standard deviation (e.g., 2). Simultaneously, for the second variable, governed by a Gumbel maximum distribution, the sampling function utilizes assigned parameters like mean (e.g., 5) and standard deviation (e.g., 2). </p>


```python
from parepy_toolbox import sampling


# Dataset
x = ['normal', 10, 2, None]
y = ['gumbel max', 5, 2, None]
vars_set = [x, y]
model = {'model sampling': 'mcs'}

# Call function
random_set = sampling(n_samples=10, d=len(vars_set), model=model, variables_setup=vars_set)

# Output details
print('random variables: \n\n', random_set)
```

```bash
random variables: 

array([[12.61920647,  2.57530007],
       [ 8.38910484,  4.19627003],
       [ 6.27031516,  2.55536836],
       [11.54718689,  3.8906196 ],
       [12.69990336,  4.48205009],
       [ 8.05295889,  8.05021698],
       [11.11945454,  4.50465106],
       [ 7.24139933,  4.04727455],
       [12.0154908 , 13.5154254 ],
       [11.17992241, 16.81078212]])
```

Example 6
{: .label .label-yellow }

<p align = "justify">Until now, the <code>sampling</code> function has been employed for generating samples without associating this process with, for instance, a specific time period. Now, we have enhanced the use of the sampling function to generate random samples, taking into account the type of distribution, mean, standard deviation, and user-defined steps. These steps are analogous to time intervals, related, for example, to stochastic processes, where new samples need to be generated.

In this specific example, the sampling function will be applied to generate three sets of samples, each following distinct parameters:

1. Samples 'x': Normal distribution, with mean 10, standard deviation 2, and 5 steps.
2. Samples 'y': Gumbel Maximum distribution, with mean 5, standard deviation 2, and 5 steps.
3. Samples 'z': Gumbel Minimum distribution, with mean 3, standard deviation 0.5, and 1 step. 

The analysis will now be conducted using the 'MCS-TIME' method </p>


```python
from parepy_toolbox import sampling


# Dataset
x = ['normal', 10, 2, 5, None]
y = ['gumbel max', 5, 2, 5, None]
z = ['gumbel min', 3, 0.5, 1, None]

vars_set = [x, y, z]
model = {'model sampling': 'mcs-time', 'time analysis': 5}

# Call function
random_set = sampling(n_samples=5, d=len(vars_set), model=model, variables_setup=vars_set)

# Output details
print('random variables: \n\n', random_set)
```

```bash
random variables: 

array([[ 6.3880708 ,  4.67208194,  2.3664532 ,  0.        ],
       [11.11336784, 11.84393812,  2.3664532 ,  1.        ],
       [ 8.95049021,  5.54912367,  2.3664532 ,  2.        ],
       [ 9.57084618,  6.66237138,  2.3664532 ,  3.        ],
       [ 9.16265906,  9.6933928 ,  2.3664532 ,  4.        ],
       [ 8.15910868,  8.8211972 ,  3.48796738,  0.        ],
       [13.98462245,  8.38819017,  3.48796738,  1.        ],
       [11.37540875,  4.14407044,  3.48796738,  2.        ],
       [10.68082533, 11.03124821,  3.48796738,  3.        ],
       [ 9.81149609,  4.63868841,  3.48796738,  4.        ],
       [ 8.45515701,  4.24838893,  2.15139355,  0.        ],
       [12.77140955,  3.43951671,  2.15139355,  1.        ],
       [ 9.9179501 ,  6.19567215,  2.15139355,  2.        ],
       [ 8.97246367,  4.5366788 ,  2.15139355,  3.        ],
       [ 9.09446587, 16.28240539,  2.15139355,  4.        ],
       [12.46682074,  5.03827731,  1.77753615,  0.        ],
       [ 8.83439838,  7.08445333,  1.77753615,  1.        ],
       [ 8.57059665,  5.29338317,  1.77753615,  2.        ],
       [ 9.00762842,  5.35360043,  1.77753615,  3.        ],
       [ 9.69885338,  6.90526775,  1.77753615,  4.        ],
       [ 9.13338015,  6.59422425,  1.97167767,  0.        ],
       [12.33064682,  5.84164455,  1.97167767,  1.        ],
       [ 8.95874604,  8.07210378,  1.97167767,  2.        ],
       [ 9.30655686,  5.03772817,  1.97167767,  3.        ],
       [10.34505715,  4.39656306,  1.97167767,  4.        ]])
```

<p align = "justify">
Note that for a 5-year analysis, as shown in the example above, variables 'x' and 'y', which have 5 steps, had 5 different values for each set of 5 years, according to the parameters of their distributions. However, variable 'z', defined for only 1 step, had the same values for all steps in each set of 5 years.</p>




[Notebook example](https://mega.nz/file/31FFDIAZ#zVEB5y81VjlbIazIijpgqzTFTxLtmqJVpnA6QAF7vjA){: .btn .btn-outline }
