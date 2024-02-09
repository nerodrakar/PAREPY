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
        <td><code>setup</code> keys</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td><code>'Objective function'</code></td>
        <td>Objective function.</td>
        <td>String</td>
    </tr>
    <tr>
        <td><code>'Number of samples'</code></td>
        <td>Number of samples.</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>'Dimension'</code></td>
        <td>Number of dimensions.</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>'Numerical model'</code></td>
        <td>Numerical model settings.</td>
        <td>Py dict</td>
    </tr>
    <tr>
        <td><code>'Variables settings'</code></td>
        <td>Variables settings.</td>
        <td>Py list</td>
    </tr>
    <tr>
        <td><code>'Number of state limit functions or constraints'</code></td>
        <td>Number of state limit functions or constraints.</td>
        <td>Integer</td>
    </tr>
    <tr>
        <td><code>'none_variable'</code></td>
        <td>Null dictionary.</td>
        <td>Py dict</td>
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
       <td><code>beta_lsit</code></td>
       <td>Beta list</td>
       <td>Py list</td>
   </tr>
</table>
