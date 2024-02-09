<!--Don't delete ths script-->
<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!--Don't delete ths script-->

SAMPLING
{: .label .label-green }

<p align = "justify">
This algorithm generates a set of random numbers according to a type of distribution.
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
        <td><code>n_samples</code></td>
        <td>Number of samples.</td>
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
        <td>Variables settings.</td>
        <td>Py list</td>
    </tr>
    <tr>
        <td></td>
        <td>type_dist</td>
        <td>String</td>
    </tr>
    <tr>
        <td></td>
        <td>mean_dist</td>
        <td>Float</td>
    </tr>
    <tr>
        <td></td>
        <td>stda_dist</td>
        <td>Float</td>
    </tr>
</table>

{: .note}

<p align = "justify">
The list of distributions used in <code>type_dist</code> are:
</p>
<ul>
<li></li>Normal or Gaussian = <code>"gaussian"</code> or <code>"normal"</code>;  
<li></li>Gumbel Maximum = <code>"gumbel max"</code>;  
<li></li>Gumbel Minimum = <code>"gumbel min"</code>;    
<li>Log Normal = <code>"lognormal"</code>;</li>
</ul>

Output variables
{: .label .label-yellow

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
       <td>Np array</td>
   </tr>
    <tr>
       <td><code>seeds</code></td>
       <td>Seeds used in the random sampling.</td>
       <td>Py list</td>
   </tr>
</table>

Example 1
{: .label .label-green }

<p align = "justify">In this example, we will use the SAMPLING function to generate a set of random samples following a Normal distribution. In this example, two sets of variables will be constructed with this distribution.</p>

```python
import parepy_toolbox.common_library as parepyco
import seaborn as sns
import scipy.stats as stats
import matplotlib.pyplot as plt


N_POP = 5
DEAD_LOAD = ['NORMAL', 7.64, 7.64 * 0.1, 5, None]
LIVE_LOAD = ['GUMBEL MAX', 1.43 * 0.93, 1.43 * 0.93 * 0.2, 1, None]
VARS = [DEAD_LOAD, LIVE_LOAD]


setup = {
             'number of samples': N_POP,
             'number of dimensions': len(VARS),
             'numerical model': {'model sampling': 'mcs-time', 'time analysis': 5},
             'variables settings': VARS
}

n_samples = setup['number of samples']
n_dimensions = setup['number of dimensions']
model = setup['numerical model']
variables_settings = setup['variables settings']

RESULTS = parepyco.sampling(n_samples=N_POP, d=len(VARS), model=model, variables_setup=VARS)
RESULTS
```

```cmd
[[6.83609159 1.53252329 0.        ]
 [7.54539986 1.53252329 1.        ]
 [8.04946859 1.53252329 2.        ]
 [7.06920038 1.53252329 3.        ]
 [7.75960886 1.53252329 4.        ]
 [6.43441017 1.78318922 0.        ]
 [6.33214883 1.78318922 1.        ]
 [7.49208404 1.78318922 2.        ]
 [6.29466462 1.78318922 3.        ]
 [8.15833042 1.78318922 4.        ]
 [8.49374583 1.65313961 0.        ]
 [8.01906746 1.65313961 1.        ]
 [7.32412418 1.65313961 2.        ]
 [6.66147404 1.65313961 3.        ]
 [7.08136507 1.65313961 4.        ]
 [7.40001279 2.80060108 0.        ]
 [8.74154543 2.80060108 1.        ]
 [7.86104433 2.80060108 2.        ]
 [7.01466488 2.80060108 3.        ]
 [9.28192454 2.80060108 4.        ]
 [6.90492851 1.03645123 0.        ]
 [6.78401896 1.03645123 1.        ]
 [6.70542507 1.03645123 2.        ]
 [7.11541733 1.03645123 3.        ]
 [7.30156533 1.03645123 4.        ]]
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

[Notebook example](https://mega.nz/file/31FFDIAZ#zVEB5y81VjlbIazIijpgqzTFTxLtmqJVpnA6QAF7vjA){: .btn .btn-outline }
