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

<h1><code>of_file.py</code></h1>

<p align="justify">
In this section, we will describe the of_file file and its characteristics. The of_file file should contain a def function that takes the following data as input.</p> 

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
        <td><code>X</code></td>
        <td>Sampling</td>
        <td>Py list</td>
    </tr>
    <tr>
        <td><code>NULL_DIC</code></td>
        <td>Empty variable to use in your objective function</td>
        <td>Empty variable</td>
    </tr>  
</table>

Output variables
{: .label .label-yellow }

<p align="justify">
In structural problems <code>MY_FUNCTION</code> returns Capacity, Demand and State Limit Funciton.</p> 

<table style = "width:100%">
    <thead>
      <tr>
        <th>Name</th>
        <th>Description</th>
        <th>Type</th>
      </tr>
    </thead>
    <tr>
        <td><code>R</code></td>
        <td>Capacity dataset</td>
        <td>Py list</td>
    </tr>
    <tr>
        <td><code>S</code></td>
        <td>Demand dataset</td>
        <td>Py list</td>
    </tr>
    <tr>
        <td><code>G</code></td>
        <td>State Limit Function dataset</td>
        <td>Py list</td>
    </tr>
</table>

```python
def MY_FUNCTION(X, NULL_DIC):

    # Statement of the random variables in the numerical model
    LOAD = X[0]
    BENDING_RESISTANCE = X[1]

    # Statement of the deterministic variables in the numerical model
    L = 5    
    # or using NULL_DIC variable (L = NULL_DIC['LENGHT (m)'])

    # Internal load
    M_S = LOAD * L / 4

    # State Limite Function
    G_M = M_S - BENDING_RESISTANCE

    # Outputs 
    R = [BENDING_RESISTANCE]
    S = [M_S]
    G = [G_M]
    
    return R, S, G

# other way

def BENDING(LOAD, L):
    return LOAD * L / 4


def MY_FUNCTION(X, NULL_DIC):

    # Statement of the random variables in the numerical model
    LOAD = X[0]
    BENDING_RESISTANCE = X[1]

    # Statement of the deterministic variables in the numerical model
    L = 5    
    # or using NULL_DIC variable (L = NULL_DIC['LENGHT (m)'])

    # Internal load
    M_S = BENDING(LOAD, L)

    # State Limite Function
    G_M = M_S - BENDING_RESISTANCE

    # Outputs 
    R = [BENDING_RESISTANCE]
    S = [M_S]
    G = [G_M]

    return R, S, G
```

{: .important }
> It is also important to note that any libraries used in this function should be imported in the file header.

{: .warning }
> The construction of the limit state function must preserve the format $G = D - C$, where $G$ is limit state function, $D$ is demand in the mathematical problem and $C$ is capacity in the mathematical problem.