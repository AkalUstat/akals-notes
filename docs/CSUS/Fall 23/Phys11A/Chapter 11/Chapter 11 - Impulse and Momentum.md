# 1. Momentum and Impulse: An Introduction

## Momentum

When objects collide, they are not like particles; they deform. When they collide, the object is more like an *elastic object* that compresses (storing elastic potential energy) and then expanding and rebounding into the opposite direction (transforming that PE into KE). 

This change can be modeled using Newton's Second Law: $m \vec a = m \frac{d \vec v}{dt} = \vec F(t)$. Further extrapolating this, we get the equation of ***momentum***:
$$
\vec p = m \vec v \tag{11.1}
$$
in units of kg m/s.

```ad-note
title: Sign of P

The momentum is parallel to the velocity vector and has the same sign as velocity.
```

Newton's Second Law is actually, originally written in terms of momentum, i.e., $\vec F = \frac{d \vec p}{dt}$. 

## Impulse

Impulse is the change in momentum, or the time integral of the force:
$$
\vec J = \int_{t_{i}}^{t_{f}} \ \vec F(t) \, dt = \Delta \vec p \tag{11.2}
$$
In words, this is the ***moment principle***, or the idea that an impulse delivered to an object causes a change in momentum. 
$$
\vec p_{f} = \vec p_{i} + \vec J
$$

## Energy and Impulse

The energy principle, covered in [[Chapter 9 Reading Notes]], is as follows:
$$
\Delta K = W = \int_{x_{i}}^{x_{f}} \ F_{x} \, dx $$

Note that this equation is very similar to the equation for the moment principle. The only difference is that this is integrated with respect to position, rather than time.

It is important to note that a Force does not do only one or the other: it provides both an impulse and work. You will use either equation depending on the question. 

## Conservation of Momentum

In an isolated system (no interaction or external force from the environment), the total momentum is conserved, i.e.,
$$
\vec P_{f} = \vec P_{i} \tag{11.3}
$$
or in other words,
$$
(p_{fx})_{1} + (p_{fx})_{2} + ... = (p_{ix})_{1} + (p_{ix})_{2} + ... 
$$

```ad-warning
title: Choose the Right System

Momentum is only conserved in an isolated system. This means that you must be careful in choosing the right system.
```

# 2. Collisions

## Inelastic Collisions

An ***inelastic collision*** occurs when two objects collide, stick together, and then move with a common final velocity. In this collision, total momentum is conserved, but mechanical energy is not (since some KE is transformed into thermal energy).

## Elastic Collisions

An ***elastic collision*** occurs when two objects collide, and then perfectly bounce off each other (all energy is conserved). Total momentum and mechanical energy is conserved. 
![[Pasted image 20230502160741.png]]

## Reference Frames

See Textbook Chapter 11.3.3

# 3. Explosions

An explosion is the *opposite* of a collision. The particles of a system move apart from each other after a brief, intense interaction. The explosive forces that cause this explosion are internal forces, an if the system is properly isolated, then total momentum will be conserved. 

# 4. Momentum in 2D

Momentum can be expanded into 2D with $x$- and $y$- components. As shown in Equation 11.3 in [[#2. Collisions]]. 

# 5. Rocket Propulsion

$F_{thrust} = v_{ex}R$ 

Don't worry too much about this. 