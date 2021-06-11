<h1> Introduction </h1>

Name red tides it's a little cheating. Red tides is a phenomenon of harmful algal blooms ocurring along coastal regions, and not the sea surface coloration of red, like a lot of people believe. A best suited name it's <i>Harmful Algal Blooms (HAB)</i>.
This phenonomen has affected in Chile, particularly the Southest regions, producing economic lossing and also afecting the people's health (due to toxines of this algaes).

<h1> Mathematical Model </h1>

We can describe algal concentration using <b>the Convection-Difussion equation</b>:

$$\frac{\partial c(x,t)}{\partial t}  + div(c u)- div(  D\nabla c) = F$$

with <strong>$u$</strong> tides velocity, $D$ difussion constant at sea and $F$ source term.
In the term $F$ is hidden the biological properties of algaes, like temperature, salinity, nutrients and wind direction.
Due to lack of data, we will use $F=0$.

Great, we have an equation to compute concentration. We are ready...NO, that formulation hides a great difficulty, even harder than convection-diffusion equation,
and that it's the velocity. What value of velocity use? because it's the tide velocity, and this depend of time and each point of our domain, would be difficult measuring this value. However, here is when appear the Hydrodynamic of our model: <b>the Navier-Stokes equations</b> allows to compute velocity.

$$\begin{align}
\displaystyle{\frac{\partial u}{\partial t} + (u \cdot \nabla) u - \nu \Delta u}  & =    - \displaystyle{\nabla \frac{p}{\rho} + \frac{f}{\rho}} 
\textrm{ on} \; \Omega 
\label{eqn: EcuacionesNavierStokes}\\
\nabla \cdot u & =  0  \textrm{ on } \; \Omega 
\label{eqn: DivergenciaNula}
\end{align}$$

where
<ul>
    <li> $f$ force per volume unit. </li>
    <li> $\nu$ fluid kinematic viscosity. </li>
    <li> $\rho$ fluid density. </li>
</ul> 

At first sight, the equations look similar, but the Navier-Stokes equations are 3D, while the convection-diffusion equation es 1D. 
The velocity it's a vector field, while concentration it's a scalar field.

<h1> Finite Volume Method </h1>

<h3> Convection-difussion discretization </h3>

Let be $\omega_i \subset \Omega$ finite volume, with $i \in \{1, \ldots, N\}$ and
$N$ the number of Finite Volumnes, ie,  
$\displaystyle{\Omega = \bigcup_{i=1} ^{N} \omega_i}$. 
Let be $\omega_i$ a finite volume,  with boundary 
$\displaystyle{\partial \omega_i = \bigcup_{j: \Gamma_{j} \text{ es cara de } \omega_i}  \Gamma_{j}}$. 
Integrating over $\omega_i$,

<ul>
    <li> Evolution term: </li>
    <p>$$\begin{array}{ccl}
    \displaystyle{\int_{\omega_i} \frac{\partial c}{\partial t} d\omega} 
    & \approx & \displaystyle{\frac{\left|\omega_i\right|}{\Delta t} (c_i ^k - c_i ^{k-1})}
    \end{array}$$ </p>
    <li> Convective term: </li> 
     <p>$$\displaystyle{\int_{\omega_i}div(c u) d\omega \approx \sum_{\substack{j : \Gamma_{j}  \omega_i 's \text{ face } \\
     \Gamma_j \text{ intern face } \\
     (u^k \cdot n)(\Gamma_{j}) < 0}} (c_{j} ^k -c_i ^k) (u^k \cdot n) (\Gamma_{j}) \left|\Gamma_{j}\right| } $$ </p>
     <li> Diffusive term:</li>
     <p> $$ \begin{array}{ccll}
\displaystyle{ \int_{\omega_i} \Delta U d\omega} 
& \approx & \displaystyle{\sum_{\substack{j : \Gamma_{j} \omega_i 's \text{ face } \\  
       \Gamma_j \text{ intern face } }} D\frac{(c_{j} ^k - c_i ^k)}{d_c (\omega_i, \omega_{j})} \left|\Gamma_{j}\right| + 
       \sum_{\substack{j : \Gamma_{j} \omega_i 's \text{ face } \\  
       \Gamma_j \text{ boundary face } }} D\frac{(c_{\Gamma_j} ^k - c_i ^k)}{d_c (\omega_i, \Gamma_{j})} \left|\Gamma_{j}\right|} \\
\end{array} $$ </p>
</ul>

<h3> Navier-stokes discretization </h3>

Notation: $u = (U, V, W)$ the velocity vector field.
We make a variable change $\displaystyle{P = \frac{p}{\rho} - g z}$, 
where $z$ is the sea depth and $g$ gravity acceleration.
We can integrate over $\omega_i$ and apply the Divergence Theorem and using similar arguments to above, but that is not enough.
Like we said at first, The Navier-Stokes equations are very complicated to solve. Still there are some issues to handle

<h4>Complicaciones adicionales Navier-Stokes</h4>
                                  <ol>
                                  <li> El término convectivo es no lineal, luego para escribir el sistema matricial se realizan iteraciones tipo punto fijo. </li>
                                  <li> Faltan ecuaciones. No hay ecuación para la presión.</li>
                                  </ol>
                                  <p>La presión se define como: </p>
                                  <ul>
                                      <li> En cada volumen la presión es incógnita. Acá tienen asociadas la condición de divergencia nula. </li>
                                      <li> En los bordes en que hay condición de borde Dirichlet para la velocidad, hay una presión incógnita en las caras de dicho borde. </li>
                                      <li> En los bordes en que NO hay condición de borde Dirichlet para la velocidad, la presión debe ser dato. </li>
                                  </ul>
                                  <p>Así se consiguen tantas ecuaciones como incógnitas.</p>
						   </section>

						   <section>
						       <h4>Sistema matricial de Navier-Stokes</h4>
                               <p>Para una cierta etapa temporal $k \in \mathbb{N}$ fija y para cada $\ell \in \mathbb{N}$, el sistema de ecuaciones se escribe en forma matricial a continuación
                              \begin{equation*}
                              \begin{bmatrix}
                              A_{UU} & 0_{N\times N} & 0_{N \times N} & A_{UP} \\
                              0_{N \times N} & A_{VV} & 0_{N \times N} & A_{VP} \\
                              0_{N \times N} & 0_{N \times N} & A_{WW} & A_{WP} \\
                              A^T_{UP} & A^T_{VP} & A^T_{WP} & 0_{M \times N}
                              \end{bmatrix}
                              \begin{pmatrix}
                              U^{k,\ell} \\
                              V^{k,\ell} \\
                              W^{k,\ell} \\
                              P^{k,\ell}
                              \end{pmatrix}
                              = 
                              \begin{pmatrix}
                              b_{U} \\
                              b_{V} \\
                              b_{W} \\
                              b_{P} \\
                              \end{pmatrix}
                              \end{equation*} 
                              \[\begin{array}{cccl} 
                                   \text{donde } & U^{k,\ell} & = & (U_1 ^{k,\ell},\ldots, U_N ^{k,\ell}) \\
                                   & V^{k,\ell} & = & (V_1 ^{k,\ell},\ldots, V_N ^{k,\ell}) \\ 
                                   & W^{k,\ell} & = & (W_1 ^{k,\ell},\ldots, W_N ^{k,\ell}) \\
                                   & P^{k,\ell} & = & (P_1 ^{k,\ell},\ldots, P_N ^{k,\ell}, P_{N+1} ^{k,\ell} \ldots P_{M} ^{k,\ell}) \\
                              \end{array}\]  </p>

<h3> Convection-diffusion discrezitation </h3>
