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
        <td><code>setup</code> keys</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td><code>'Number of samples'</code></td>
        <td>Number of samples</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>'Dimension'</code></td>
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
    <tr>
        <td><code>'Number of state limit functions or constraints'</code></td>
        <td>Number of state limit functions or constraints.</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>'none_variable'</code></td>
        <td>None variable. Default is <code>None</code>. Use in objective function</td>
        <td>None, list, float, dictionary, str or any</td>
    </tr>
    <tr>
        <td><code>'Objective function'</code></td>
        <td>Objective function</td>
        <td>String</td>
    </tr>
    <tr>
        <td><code>'type process'</code></td>
        <td><a href="#vars">Architecture of algorithm</a></td>
        <td>String</td>
    </tr>
    <tr>
        <td><code>'name simulation'</code></td>
        <td>Output filename</td>
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
       <td>Results about data.</td>
       <td>Np array</td>
   </tr>
    <tr>
       <td><code>failure_prob_list</code></td>
       <td>Failure probability list</td>
       <td>Py list</td>
   </tr>
    <tr>
       <td><code>beta_list</code></td>
       <td>Beta list</td>
       <td>Py list</td>
   </tr>
</table>

Example 1
{: .label .label-yellow }

<p align = "justify">Neste exemplo, a função <code>sampling_algorithm_structural_analysis</code> será utilizada para determinar a probabilidade de falha e o índice de confiabilidade de uma viga metálica bi-apoiada, apresentada no Exemplo 5.1 da obra *Reliability of Structures*, de Andrzej S. Nowak e Kevin R. Collins. Os dados do exemplo estão disponíveis abaixo:

Variáveis aleatórias:

1. Carga distribuiída *w*: 
- Valor da carga: 0.25 k/in;
- Fator bias: 1.0
- Distribuição Normal;
- Desvio-padrão: 0.025 k/in.

2. Carga concentrada *P*:
- Valor da carga: 12.0 k;
- Fator bias: 0.85;
- Distribuição Normal;
- Desvio-padrão: 1.12 k.

3. Resistência do aço *fy*:
- Valor: 36 ksi;
- Fator bias: 1.12;
- Distribuição Normal;
- Desvio-padrão: 4.64 ksi.

Variáveis determinísticas:

1. Comprimento da viga *L*: 18 ft
2. Módulo plástico da viga *Z*: 80 in³

<p align = "center"><b>Figure 3.</b> Viga exemplo.</p>
<center><img src="assets/images/viga_ex.png" width="70%"></center>

</p>

```python
from parepy_toolbox import sampling_algorithm_structural_analysis


# Settings
f_y = ['normal', 36 * 1.12, 4.64, 1, None]
p_load = ['normal', 12 * 0.85, 1.12, 5, None]
w_load = ['normal', 0.25 * 1.0, 0.025, 5, None]
variables = [f_y, p_load, w_load]

# Função objetivo
def nowak_example(x, none_variable):
    # Time id and value
    id_analysis = int(x[-1])
    time_step = none_variable['time analysis']
    t_i = time_step[id_analysis]
    f_y = x[0]
    p_load = x[1]
    w_load = x[2]
    if t_i == 0:
        degrad = 1
    else:
        degrad = 1 - (0.2/t_i)/100
    capacity = 80*f_y*degrad
    demand = 54*p_load + 5832*w_load
    constraint = demand - capacity

    return [capacity], [demand], [constraint]


# PAREpy setup
setup = {
             'number of samples': 1000, 
             'number of dimensions': len(variables), 
             'numerical model': {'model sampling': 'mcs-time', 'time analysis': 5}, 
             'variables settings': variables, 
             'number of state limit functions or constraints': 1, 
             'none variable': {'time analysis': list(np.linspace(1, 10, num=50, endpoint=True))},
             'objective function': nowak_example,
             'type process': 'serial',
             'name simulation': 'documentation_example',
        }


results, pf, beta = sampling_algorithm_structural_analysis(setup)
```

```bash
pf: 

[[0.002, 0.002, 0.002, 0.003, 0.003]]

beta:

[[2.878161739095443,
  2.878161739095443,
  2.878161739095443,
  2.7477813854449726,
  2.7477813854449726]]
```