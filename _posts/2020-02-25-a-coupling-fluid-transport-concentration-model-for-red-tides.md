Name red tides it's a little cheating. Red tides is a phenomenon of harmful algal blooms ocurring along coastal regions, and not the sea surface coloration of red, like a lot of people believe. A best suited name it's <i>Harmful Algal Blooms (HAB)</i>.
This phenonomen has affected in Chile, particularly the Southest regions, producing economic lossing and also afecting the people's health (due to toxines of this algaes).


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

