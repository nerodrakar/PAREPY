---
layout: home
parent: common_library
grand_parent: Framework
nav_order: 1
has_children: false
has_toc: false
title: godnesse of fit
---

<!--Don't delete ths script-->
<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!--Don't delete ths script-->

<h3>goodness_of_fit</h3>

<br>

<p align = "justify">
    Evaluates the fit of distributions to the provided data.


</p>

```python
goodness_of_fit(data, distributions='all')
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
        <td><code>data</code></td>
        <td>Data to which distributions will be fitted. It should be a list or array of numeric values.</td>
        <td>np.array or list</td>
    <tr>
        <td><code>distributions</code></td>
        <td>Distributions to be tested. If 'all', all available distributions will be tested. Otherwise, it should be a list of strings specifying the names of the distributions to test. The default is 'all'.</td>
        <td>str or list, optional</td>
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
        <td><code>dict</code></td>
        <td>A dictionary containing the top three fitted distributions. Each entry is a dictionary with the following keys:</td>
        <td>dict</td>
        <td><code></td>
    <tr>
        <td><code>rank</td>
        <td>Ranking of the top three distributions based on the fit score
        <td>str</td>
        </td>
    </tr>
        <td><code>type</td>
        <td>The name of the fitted distribution
        <td>str</td>
        </td>
    </tr>
        <td><code>params</td>
        <td>Parameters of the fitted distribution
        <td>tuple</td>
        </td>
    </tr>
</table>

Example 1
{: .label .label-blue }

<p align = "justify">
  <i>In this example, we will use the <code>sampling</code> function to generate a set of random samples \((n=30)\) following a Normal distribution with mean \(\mu = 7\) and standard deviation \(\sigma = 3\).</i>
  
  <i>The `goodness_of_fit` function is responsible for fitting different distributions to the data using the `distfit` library and returns the three distributions that best fit, based on a fit score criterion. If the `distributions` parameter is set to 'all', the function will test all available distributions; otherwise, it will test only those specified in the provided list.<i>
</p>

```python
from parepy_toolbox import sampling, godness_of_fit

model = {'model sampling': 'mcs'}
f = {'type': 'normal', 'loc': 7, 'scale': 3, 'seed': None}
varSet = [f]
size = 1000000

# Call function
r_norm = sampling(size, len(varSet), model, varSet)

r_norm_new = [item for sublista in r_norm for item in sublista]
r_norm_new = np.array(r_norm_new)

dist = distfit()
result = goodness_of_fit(r_norm_new)
print(result)
```

```bash
{'rank_1': {'type': 'beta',
  'params': (634.3092283687507,
   583.8342419491771,
   -102.15302292202938,
   209.61822809243546)},
 'rank_2': {'type': 'norm', 'params': (6.998962470093887, 2.9991521136081687)},
 'rank_3': {'type': 't',
  'params': (6792197.291882796, 6.998943769697172, 2.9991597259839553)}}
```

