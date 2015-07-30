---
layout: default
title: Code
---

<div id="pub-container">

<!-- lrpd -->
<div class="pub-main">
<h3>R Package: lrpd</h3>
<p>A small R package providing efficient matrix inversion and determinant calculation for low-rank positive definite (lrpd) matrices. 
A matrix $$\boldsymbol{M}$$ is low-rank positive definite if $$\boldsymbol{M}=\boldsymbol{N}+\boldsymbol{L}\boldsymbol{S}\boldsymbol{L}^{T}$$ 
is true, where $$\boldsymbol{N}$$ is a positive diagonal matrix and $$\boldsymbol{S}$$ is a positive definite matrix with a smaller dimension. 
The package also provdes efficient density calculation and random sampler for multivariate Gaussians with such low-rank covariances.</p>
<p>[<a href="http://arxiv.org/pdf/1506.03768v1.pdf">Github Repository</a>]&nbsp;&nbsp;&nbsp; [Online Document]&nbsp;&nbsp;&nbsp;</p>

<div class="pub-sub">
<p><b>Abstract</b></p>
<p>Learning of low dimensional structure in multidimensional data is a canonical problem in machine learning. One common approach is to suppose that the observed data are close to a lower-dimensional smooth manifold. There are a rich variety of manifold learning methods available, which allow mapping of data points to the manifold. However, there is a clear lack of probabilistic methods that allow learning of the manifold along with the generative distribution of the observed data. The best attempt is the Gaussian process latent variable model (GP-LVM), but identifiability issues lead to poor performance. We solve these issues by proposing a novel Coulomb repulsive process (Corp) for locations of points on the manifold, inspired by physical models of electrostatic interactions among particles. Combining this process with a GP prior for the mapping function yields a novel electrostatic GP (electroGP) process. Focusing on the simple case of a one-dimensional manifold, we develop efficient inference algorithms, and illustrate substantially improved performance in a variety of experiments including filling in missing frames in video.</p>
</div>
</div>

<!-- A new one below -->

</div>

</div>
