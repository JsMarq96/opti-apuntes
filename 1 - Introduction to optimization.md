## What is optimization?
A variational aproach (?): the goal is to find a function u(x) that satisfies a series of suitable constraints.

This creteria or a constraint, are formulated thrught an energy, or cost, or objetive junction E(u). The goal is to achieve a function u(x) that either maximizes or minimizes E(u), dependeing on the problem
$$ u_0 = arg \min_u E(u) $$
This means that
$$ E(u_0) \leq E(u)\  \forall u $$
BUT that $u_0$ may not exists in the problem domain

## Image Denoising
Giben an image u, it has a noise, that we want to remove.
We need to optimize for it similarity (need to be the same iamge), and to have less noise


## Meassuring simlarity
Let $f_{i,j}$ be the values for a noisy image, and a $u_{i,j}$ be the noise-free image
$$ f_{i,j} = u_{i,j} + noise$$
How we meassure the difference between both images? $f_{i,j} - u_{i,j}$ needs to be small, but not 0, becuse then both images are the same!

How do we control that?
- $|f_{i,j} - u_{i,j}|$ is good but not diferenciable, so the gradient descent like methods fail to converge (the negative is not deribable), and the slope is all equal, so it lacks precission
- $(f_{i,j} - u_{i,j})^2$ is good, and diferentiable! Since the function is smooth, and the gradient step is different on each step, smaller when nearing the minimal

So if we use the last one, and we use it for all the pixels, we end with
$$ E(u) = \sum\sum (f_{i,j} - u_{i,j})^2 $$
But... if we use this metric
$$ \arg \min_u E(u) = \arg \min_u \sum\sum (f_{i,j} - u_{i,j})^2 $$
The result is that f = u, so that is not valid... But what if we stop at a given value $\xi$?
But i would not still give us a solution that could still be qualified as an iamge

#### Guratee that an image is denoising
In an image, the abscense is usually noise is a flat value, with differente objects art differen intensity
So we use the gradient (2D) and penalize high gradients between neighboords

$$ \triangledown u = (\delta_i u, \delta_j u)$$
$$E(u) = \sum\sum  ||(\triangledown u)_{i,j}||^2_2 $$
(Note: the notation $||u||_2$ is the normalization factor for 2 members)
But this function, maximizes to a a blank image, without any contrast
So we merge both functions
$$ E(u) = \sum\sum  ||(\triangledown u)_{i,j}||^2_2 + \lambda \sum\sum (f_{i,j} - u_{i,j})^2$$

Here the lambda is a trade-off paramtere that controlls both parts:
- A data fidelity term: $E_D(u) = \sum\sum (f_{i,j} - u_{i,j})^2$ that controls the result in order to gain a semblance of the original data
- Smoothnes or regularization termL: avoids abrupt changes


## Optical flow
Compute the motion field of teh pozels between two consecutive frames of a video sequence

If we consider a video $I : \Omega\  x \ \T \rightarrow R$ where omega is a discrete rectangular domain of each frame and T are the discrete time

The optical flow estimator is called $v: \Omega \rightarrow R^2$ and if we take a pixel x, at frame t, in teh frame t+1 the position would be $x+v(x,t)$

If we asume that the level of gray value of the moving pixel is constant over time, (cosntant brightness asumption), the optical flow constraint would be
$$ I(x,y,t) = I((x,y)+v(x,t), t+1) $$
But, in the real world is not usally true...
This problem is under-determined. That means that there are infinte solutions, becuase there is only one constraint in order to solve two variablles!
And also the illumiation changes when moving, and ther eis always noise!!

Second try, we set the minimizer as an integral, but the result has inifint minima, so it is caotic!!

Third attempt:
The gradient of v, is quite small! The same object has little diferences between eachother!, this means that the optical flow needs to be sensible

$$ \min_{(v_1,v_2)} \int_\Omega (|\triangledown v_1 (x,y)|^2 + |\triangledown v_2 (x,y)|^2) \delta x \delta y $$
TODO: Completar


# How do we solve this?
We have planteed the problem, but how do we achieve it?
- Thoes this porblem have a solution, or an optimal one?
- How do we achieve it?

### Minimizing the energy
If the energy is a smooth convex function, so we can use that to reach the minimun
We know that a solution x0 is in a mimnum (and an optimal one) if $\triangledown f(x_0) = 0$, only if the result is convex

Not always a global minimun is achibable, sometimes you can only get a local minimun (or a local optimal). :(


### Convex is da best!
If F is conex, there is a minima, and we will be able to find it!