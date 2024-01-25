---
layout: home
title: sampling
nav_order: 2
grand_parent: Framework
parent: Common Library
has_children: false
---

<!--Don't delete ths script-->
<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!--Don't delete ths script-->

SAMPLING ALGORITHM
{: .label .label-green }

<p align = "justify">
This function creates the samples and evaluates the limit state functions.
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
        <td>Setup setting.</td>
        <td>Py dict</td>
    </tr>
    <tr>
        <td></td>
        <td><code>Objective function</code></td>
        <td>String</td>
    </tr>
    <tr>
        <td></td>
        <td><code>Number of samples</code></td>
        <td>Integer</td>
    </tr>
    <tr>
        <td></td>
        <td><code>Dimension</code></td>
        <td>Integer</td>
    </tr>
    <tr>
        <td></td>
        <td><code>Numerical model</code></td>
        <td>Py dict</td>
    </tr>
    <tr>
        <td></td>
        <td><code>Variables settings</code></td>
        <td>Py list</td>
    </tr>
    <tr>
        <td></td>
        <td><code>Number of state limit functions or constraints</code></td>
        <td>Integer</td>
    </tr>
    <tr>
        <td></td>
        <td><code>none_variable</code></td>
        <td>Py dict</td>
    </tr>
</table>

setup keys:
'Objective function' (str): Objective function.
'Number of samples' (int): Number of samples.
'Dimension' (int): Number of dimensions.
'Numerical model' (dict): Numerical model settings.
'Variables settings' (list): Variables settings.
'Number of state limit functions or constraints' (int):
Number of state limit functions or constraints.
'none_variable' (dict): Null dictionary.

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
