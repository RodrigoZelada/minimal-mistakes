Name red tides it's a little cheating. Red tides is a phenomenon of harmful algal blooms ocurring along coastal regions, and not the sea surface coloration of red, like a lot of people believe. A best suited name it's <i>Harmful Algal Blooms (HAB)</i>.
This phenonomen has affected in Chile, particularly the Southest regions, producing economic lossing and also afecting the people's health (due to toxines of this algaes).


We can describe algal concentration using <b>the Convection-Difussion equation</b>:

$$frac{\partial c(x,t)}{\partial t}+ div(c u)- div(  D\nabla c) = F$$

with <strong>$u$</strong> sea velocity, $D$ difussion constant at sea and $F$ source term.
In the term $F$ is hidden the biological properties of algaes, like temperature, salinity, nutrients and wind direction.
Due to lack of data, we will use $F=0$.

El cálculo de la velocidad de marea se hará resolviendo numéricamente las ecuaciones de Navier-Stokes </p>
\begin{align}
\displaystyle{\frac{\partial u}{\partial t} + (u \cdot \nabla) u - \nu \Delta u}  & =    - \displaystyle{\nabla \frac{p}{\rho} + \frac{f}{\rho}} 
\textrm{ en } \; \Omega 
\label{eqn: EcuacionesNavierStokes}\\
\nabla \cdot u & =  0  \textrm{ en } \; \Omega 
\label{eqn: DivergenciaNula}
\end{align}

Navier-Stokes equations and Convection difussion equations
