Interferometry it's a Astronomic Resolution technique that uses many antennas together, which produces better precision and allow to analyze data in radar wavelength.
The resolution doesn't depend on antennas diameter, inded it depends of separation: while antennas further between them, greater it's the interferometer resolution, so images are more detailed. <b>ALMA</b> (<strong>Atacama Large Milimiter Array</strong>) it's a revolutionary interferometer, due to his 66 antennes between 6 and 12 meters.
We will review briefly the <b>Maximimum Entropy Method</b> (<strong>MEM</strong>) and also study the relationship between spectrum and frequency.
This is based on 
<ul>
  <li><i>Cárcamo, M. (2014). Reconstrucción de imágenes de interferometría mediante algoritmos iterativos paralelos en múltiples GPU. Universidad de Santiago
    de Chile </i> </li>
  <li><i>GPUVMEM: Maximum Entropy Method (MEM) GPU algorithm for radio astronomical image synthesis by Miguel Cárcamo, Nicolás Muñoz, Fernando Rannou, Pablo Román, Simón Casassus, Axel Osses and Victor Moral</i> </li>
    <li><i>High resolution interferometry in ALMA by Simon Casassus, Pablo Roman, Axel Osses and Jorge Silva</i>. </li>
</ul>

<h1> Problem statement </h1>

Let be $V$ a visibility vector of dimension $k$, and $I$ the image vector that we can reconstruct of dimension $k$. The main idea is using the fact that visibilities are known and how we want to get the best possible image, we write the problem as an optimization problem:
The image maximum a posteriori (MAP) it's the following:

$$\hat{I}_{MAP} = argmax_{I} \mathbb{P}(I|V)$$

From Bayes formula, we have that 
$$\mathbb{P}(I|V) = \frac{\mathbb{P}(V|I)\mathbb{P}(I)}{\mathbb{P}(V)}$$
and how we are maximizing with respect to I, the optimization problem is equivalent to

$$\hat{I}_{MAP} = argmax_{I} \mathbb{P}(V|I)\mathbb{P}(I)$$

Using that logarithm is a strictly increasing function

$$\hat{I}_{MAP} = argmax_{I} log(\mathbb{P}(V|I)) + log(\mathbb{P}(I))$$

Let be $V^O$ a visibility vector observed on Fourier plane, then we define the noise as 
$$r_k = V_k - V_k ^O$$ 
that follows a normal distribution with null mean and variance $\sigma_k$.
Assuming that are random variables, we have that
$$\mathbb{P}(V|I) = \prod_{k=1} ^n exp(\frac{-(V_k - V_k ^O)^2}{2\sigma_k ^2})$$

MEM algorithm assumes that the image follows a distribution $$\prod_{k=1} ^n (\frac{I_k}{M})^{-I_k}$$
with $M$ the minimum value that can take a pixel.

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/ALMA.jpg" alt="hi" class="inline"/>

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/todas.png" alt="hi" class="inline"/>

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/M%3D05M0.png" alt="hi" class="inline"/>
