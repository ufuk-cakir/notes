---
title: "Navier-Stokes Equations"
---

$$
\frac{\partial \vec{v}}{\partial t}+(\vec{v} \cdot \vec{\nabla}) \vec{v}=-\frac{1}{\rho} \vec{\nabla} p-2(\vec{\Omega} \times \vec{v})+\nu \Delta \vec{v}+\vec{g}
$$

- $\frac{\partial \vec{v}}{\partial t}$: This term represents the partial derivative of the velocity vector (\vec{v}) with respect to time (\partial t). It captures the change in velocity over time and represents the acceleration or deceleration of the fluid particles.

- $(\vec{v} \cdot \vec{\nabla}) \vec{v}$: This term corresponds to the convective or advective term. It involves the dot product (\cdot) between the velocity vector (\vec{v}) and the gradient operator (\vec{\nabla}), followed by another dot product with the velocity vector (\vec{v}). It describes the effect of the fluid's own velocity on the acceleration of neighboring fluid particles and represents the transport of momentum within the flow.

- -$\frac{1}{\rho} \vec{\nabla} p:$ This term represents the pressure gradient in the fluid. It involves the gradient operator (\vec{\nabla}) acting on the scalar pressure field (p). Dividing by the density (\rho) accounts for the influence of pressure on the acceleration of the fluid particles.

- $2(\vec{\Omega} \times \vec{v})$: This term represents the Coriolis force. It involves the cross product (\times) between the angular velocity vector (\vec{\Omega}) and the velocity vector (\vec{v}). It captures the effect of the rotation of the coordinate system on the fluid flow.

- $\nu \Delta \vec{v}$: This term represents the viscous forces in the fluid. It involves the Laplacian operator (\Delta) acting on the velocity vector (\vec{v}), and multiplying by the kinematic viscosity (\nu). It accounts for the internal friction within the fluid, causing velocity gradients and damping the flow.

- $\vec{g}$: This term represents the gravitational force acting on the fluid. It corresponds to the vector gravitational acceleration (\vec{g}) and influences the fluid flow by causing it to move in the direction opposite to the gravitational field.

Overall, this equation, known as the Navier-Stokes equation, describes the conservation of momentum in a fluid and captures the various forces and terms influencing the fluid flow.
