---
layout: default
title: Publications
---

<div id="pub-container">

<!-- GEODE -->
<div class="pub-main">
<p><a href="http://ericyewang.github.io">Ye Wang</a>, <a href="http://sites.carloalberto.org/canale/">Antonio Canale</a>, <a href="https://stat.duke.edu/~dunson/">David Dunson</a>. Scalable geometric density estimation. 
Accepted to <i>AISTAT 2016</i>.</p>
<p><i><font color="#ff9900">Accepted for a full oral presentation (<6.5%).</font></i></p>
<p>[pdf]&nbsp;&nbsp;&nbsp; [Online Document]&nbsp;&nbsp;&nbsp; [Code]</p>

<div class="pub-sub">
<p><b>Abstract</b></p>
<p>It is standard to assume a low-dimensional structure in estimating a high-dimensional density. However, popular methods, such as probabilistic principal component analysis, scale poorly computationally. We introduce a novel empirical Bayes method that we term geometric density estimation (GEODE) and show that, with mild assumptions, the subspace spanned by the principal axes of the data is the MAP linear subspace under the proposed model. With these axes pre-computed using fast singular value decomposition, GEODE easily scales to high dimensional problems while providing uncertainty characterization. The model is also capable of imputing missing data and learning the true intrinsic dimension. Finally, we generalize GEODE by mixing it across a dyadic clustering tree. Both simulation studies and real world data applications show superior performance of GEODE in terms of robustness and computational efficiency.</p>
</div>
</div>

<!-- electroGP -->
<div class="pub-main">
<p><a href="http://ericyewang.github.io">Ye Wang</a>, <a href="https://stat.duke.edu/~dunson/">David Dunson</a>. (2015) Probabilistic curve learning: Coulomb repulsion and the electrostatic Gaussian process. 
In <i>NIPS</i>, volume 28, pages 1729-1737, 2015.</p>
<p>[<a href="https://papers.nips.cc/paper/5794-probabilistic-curve-learning-coulomb-repulsion-and-the-electrostatic-gaussian-process.pdf">pdf</a>]&nbsp;&nbsp;&nbsp; [Online Document]&nbsp;&nbsp;&nbsp; [Code]</p>

<div class="pub-sub">
<p><b>Abstract</b></p>
<p>Learning of low dimensional structure in multidimensional data is a canonical problem in machine learning. One common approach is to suppose that the observed data are close to a lower-dimensional smooth manifold. There are a rich variety of manifold learning methods available, which allow mapping of data points to the manifold. However, there is a clear lack of probabilistic methods that allow learning of the manifold along with the generative distribution of the observed data. The best attempt is the Gaussian process latent variable model (GP-LVM), but identifiability issues lead to poor performance. We solve these issues by proposing a novel Coulomb repulsive process (Corp) for locations of points on the manifold, inspired by physical models of electrostatic interactions among particles. Combining this process with a GP prior for the mapping function yields a novel electrostatic GP (electroGP) process. Focusing on the simple case of a one-dimensional manifold, we develop efficient inference algorithms, and illustrate substantially improved performance in a variety of experiments including filling in missing frames in video.</p>
</div>
</div>

</div>
