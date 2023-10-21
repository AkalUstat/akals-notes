Introduction to the Basic Energy Model. 
# Intro to Energy

Energy is measured in J (joules)

#### Potential Energy (U)

Energy associated with an object's position, i.e., how an object's position gives it (or takes away) from it's energy

Example: Gravitational potential $U_{g}$ depends on the object's height above the ground


#### Kinetic Energy (KE)

Energy associated with an object's motion, i.e., how much energy is in it's motion within a system.
		
#### Thermal Energy($E_{th}$)

Energy associated with the random motion of atoms within an Object

#### What is Work?

Work is the change in the energy within a system by mechanical means, e.g., pushing or pulling (a Force). If there is no displacement, there is no Work.

#### The Energy of a System

the total energy of a system is defined as $$E_{total} = KE + U + E_{th} + E_{chem} + ... $$
$$ E_{total} $$
# The Energy Principle

$$\Delta E_{sys}=W_{external}$$
#### Conservation of Energy: Energy Transformation

Systems have energy, so it is imperative to correctly define a system. This is important because energy is *conserved* within a system - transfer without loss - as long as there is no external force from the environment. 

#### Interactions with the Environment: Energy Transfer

Interactions with the environment transfer energy *into* or *out* of systems. There are two forms of this transfer
1. ==Mechanical==: pull or push forces transfer energy. Called ==Work==
	 $W>0$ when for energy added to a system
	 $W < 0$ for removed energy. 
2. ==Thermal==: energy is transferred as heat. 

The Basic Energy model is only valid as long as there is no thermal transfer of energy. 

## Work and Kinetic Energy for a Single Particle

#### Basic Equations
$KE= \frac{1}{2} mv^2$, Units $kg\> m^2/s^2$ 

$W=\Delta KE=\int_{s_{i}}^{s_{f}} F_{s} \, dx$

#### Signs of Work
Remember that work is an energy transfer. If the force is causing a speed up, then Work done is positive (and vice versa for the slow-down/negative case).

The sign of Work is not determined solely. by the direction of the force vector. The displacement $\Delta s$ also has a sign. 

$Force \rightarrow$ and $\Delta s \rightarrow$ means positive Work. $Force \leftarrow$ and $\Delta s \rightarrow$ is negative Work.

A Force perpendicular to the displacement does no work.


## Calculating Work Done

#### Dot Products: A Way of Multiplying Vectors
$$\vec A \cdot \vec B = ABcos\theta = A_{x}B_{x}  + A_{y}B_{y}$$ 
AKA ==*Scalar Product*== since this value is a Scalar.  The dot product is dependent on the orientation of the vectors. 

Work is actually also a dot product: $W = \vec F \cdot \Delta \vec r$

#### Zero Work

See skater on a wall example, chapter 9.3.4

#### Variable Force

$W=\int_{s_{i}}^{s_{f}} F_{s} \, dx$



## Restoring Forces and Springs

==Restoring Force==: a Force that restores a system to equilibrium, e.g., stretching a rubber band.
==Elastic== objects are those objects that exert restoring forces; Nearly everything that stretches, compresses, bends, flexes, or twists.

#### Springs

==*Equilibrium Length*== is the length of the spring when there is no push or pull. Restoring forces on springs are opposite to $\Delta s$ and within a certain limit, $F_{s} \propto \Delta s$ 

***Hooke's Law***: $F_{s} = -k \> \Delta s$ , where $k$ is the spring constant (Units: $\frac{N}{m}$) Hooke's Law fails when a spring is compressed/stretched too far. Only works for "ideal" springs. 

#### Work done by Springs

$W=\int_{s_{i}}^{s_{f}} F_{s} \, ds = -(\frac{1}{2} k \> (\Delta s_{f})^2 - \frac{1}{2} k (\Delta s_{i})^2)$ 


## Dissipative Forces and Thermal Energy

Atoms are constantly moving around and have kinetic energy. This movement stretches and compresses the spring-like bonds between atoms. The complete total of these atom movements and their combined $KE$ and $U$ Energies is the thermal energy of the system. 

Friction, drag, and other forces cause the macroscopic $KE$ of the system to be dissipated as thermal energy. These *dissipative forces* always increase the thermal energy of a system. 

\*Friction cannot be used to calculate work since it is the average force on the whole object. 

## Power 

***Power*** is the rate at which energy is transformed. $P = \frac{d\>E_{sys}}{d\>t}$ . The units of power are:
		1 t
	horsepower (hp) = 746 $W$
Where Watt (W) is the SI unit for power such that 1 watt = 1 $W$ = 1 $J / s$ .
$$ P = \vec F \cdot \vec v = Fv\>cos\theta$$

