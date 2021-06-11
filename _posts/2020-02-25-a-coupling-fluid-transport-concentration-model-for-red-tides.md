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
and that it's the velocity. What value of velocity use? because it's the tide velocity, and this depend of time and each point of our domain, would be difficult measuring this value. However, here is when appears the Hydrodynamics: <b>the Navier-Stokes equations</b> allows to compute velocity.

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

So, the convection - diffusion equations becomes a matrix equations, that is easy to solve numerically.

<h3> Navier-stokes discretization </h3>

Notation: $u = (U, V, W)$ the velocity vector field.
We make a variable change $\displaystyle{P = \frac{p}{\rho} - g z}$, 
where $z$ is the sea depth and $g$ gravity acceleration.
We can integrate over $\omega_i$ and apply the Divergence Theorem and using similar arguments to above, but that is not enough.
Like we said at first, The Navier-Stokes equations are very complicated to solve. Still there are some issues to handle.

<h4>Additional complications of Navier-Stokes equations</h4>
  <ol>
  <li> The convective term is not linear, so in order to write a matrix equation. </li>
  <li> There is not pressure equation, we need more equations!! .</li>
  </ol>
  
  In the Finite Volume framework, the most used algorithms to solve the Navier-Stokes equations are called the Splitting methods, that consist basically in:
  <ol>
    <li> solve the equation for the velocity (fixing the pressure) </li>
    <li> write a Laplacian equation for the pressure and solve it  </li>
    <li> recorrect the velocity, computing again with the pressure obtained in the previous stage</li>
  </ol>
  
  Look for example <strong>the SIMPLE</strong> and <strong>the PIMPLE algorithms</strong>.
  Our approach it's a little different, we propose to solve only one big system instead of split the equations for pressure and velocity.
  We need to have in mind that the pressure acts like a constraint (remember <strong>the De Rham Theorem</strong> for the Stokes equation). Thus,
  
  <p>We define the pressure as follows: </p>
  <ul>
      <li> In each Finite Volume the pressure it's unknown. Here, we associate the divergence free condition. </li>
      <li> On the boundaries that there are a Dirichlet boundary condition for the velocity, there is an unknown pressure on the face of such boundary. </li>
      <li> On the boundaries that there are not a Dirichlet boundary condition for the velocity, the pressure must be given, ie, Dirichlet boundary condition for the pressure.  </li>
  </ul>
  
  In this way, we get as many equations as we want.
  
  If you want to see the results and study in more details this topics, take a look to my <a href="https://rodrigozelada.github.io/DefensaDeTesis">Master Thesis Presentation</a>.
