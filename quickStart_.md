---
layout: home
nav_order: 2
has_children: true
has_toc: true
title: Quick Start
---

<!--Don't delete this script-->
<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!--Don't delete this script-->

<h1>Requirements and install</h1>

<p align="justify">To use the platform in an environment that interprets the Python language, use the following command:</p>

```python
pip install parepy-toolbox
```
<h1>Files structure</h1>

<p align="justify">Let's use the example of building a problem in PAREpy using the Jupyter Notebook. Thus, the basic file structure of the library should be as follows:</p>

```cmd
 .
 └── problem_directory
       └── of_file.py
       └── your_problem.ipynb # or your_problem.py
       └── other files
```
<p align="justify">The <code>of_file.py</code> file should contain the objective function of the problem. The <code>your_problem</code> file is the file that will contain the call to the main function and other settings necessary for the use of the algorithm.</p>

