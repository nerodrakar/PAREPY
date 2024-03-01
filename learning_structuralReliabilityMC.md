---
layout: home
grand_parent: Learning
parent: Statistical concepts
nav_order: 3
has_children: false
has_toc: false
title: Distributions
---

<!--Don't delete this script-->
<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!--Don't delete this script-->

<p align="justify">Under construction.</p>

Gaussian or Normal
{: .label .label-Blue}

<p align = "justify">
The Gaussian or Normal distribution is by far one of the most important probability distributions in literature, and it is used in many fields of engineering and science due to its simplicity and convenience. This distribution is used to model the Poisson's ratio, among other material properties, for example <a href="#ref1">[1]</a>. It is possible to say that a random variable \(X\) has a Gaussian distribution if its probability density function follows the expression.
</p>



<table style = "width:100%">
    <tr>
        <td style="width: 90%;">\[ f_{x}(x)=\frac{1}{\sqrt{2\pi}\sigma}exp\left [ - \frac{1}{2}\left ( \frac{x-\mu}{\sigma} \right ) \right ] \]</td>
        <td style="width: 10%;"><p align = "right" id = "eq1">(1)</p></td>
    </tr>
</table>

<p align = "justify">
Where the parameters of the distribution \(\mu\) and \(\sigma\) denote the mean and standard deviation of the variable \(x\), respectively, and \(x\) is identified as \(N(\mu,\sigma)\). The location (\(\mu\)) and scale (\(\sigma\)) parameters generate a family of distributions, as a presented in Figure 1.
</p>

<p align = "center"><b>Figure 1.</b> Normal Density Function.</p>
<center><img src="assets/images/Normal_Density_Function.png" width="50%"></center>
</p>

<br>


Gumbel Maximum
{: .label .label-Blue}

<br>


Gumbel Minimum
{: .label .label-Blue}

<br>


Lognormal
{: .label .label-Blue}

<br>


Uniform
{: .label .label-Blue}


<h3>Reference list</h3>

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Reference</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><p align = "center" id = "ref1">[1]</p></td>
            <td><p align = "left"><a href="https://doi.org/10.1007/978-1-84628-445-8" target="_blank" rel="noopener noreferrer">Choi, S., Canfield, R.A. & Grandhi, R.V.  (2021). https://doi.org/10.1007/978-1-84628-445-8. Springer London, 306 pgs.</a></p></td>
        </tr>
    </tbody>
</table>
