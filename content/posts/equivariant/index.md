---
title: "A Guide to Equivariance Theory for Chemists"
date: 2026-06-19T14:03:50+08:00
draft: true
categories: ["AI"]
tags: ["AI", "chemistry", "equivariant", "GDL"]
---

## Introduction

Suppose we want to simulate the motion of atoms in a molecule or a material. In principle, the forces on the nuclei come from quantum mechanics. In practice, this is hard because the full electron-nuclear Schrodinger equation is far too expensive to solve at every molecular dynamics step.

The usual starting point is the Born-Oppenheimer approximation. Since nuclei are much heavier and move much more slowly than electrons, we treat the nuclear positions as fixed while solving the electronic problem. Let

$$
\mathbf R = (\mathbf r_1,\ldots,\mathbf r_N)
$$

denote a nuclear configuration, together with atomic species

$$
\mathbf Z = (Z_1,\ldots,Z_N).
$$

(In most of the following discussion, $\mathbf Z$ is treated as fixed or carried as an atom-type label, so we sometimes only write $\mathbf R$ for brevity.)

For a fixed $\mathbf R$, we solve an electronic Schrodinger equation

$$
\hat H_{\rm e}(\mathbf R)\psi_{\mathbf R}
= E(\mathbf R)\psi_{Z, \mathbf R}.
$$

The ground-state energy $E(\mathbf R)$ is then interpreted as the potential energy of that nuclear configuration. As $\mathbf R$ varies, these values form a potential energy surface (PES). The nuclear forces are the negative gradients of this surface:

$$
\mathbf F_i(\mathbf R) = -\nabla_{\mathbf r_i} E(\mathbf R).
$$

Once we know the forces, the nuclei can be evolved by Newton's equations. This is the basic loop behind ab initio molecular dynamics.

The bottleneck is that solving the electronic structure problem repeatedly is computationally expensive. Machine-learned interatomic potentials try to learn the map

$$
(\mathbf Z,\mathbf R)\longmapsto E(\mathbf R),
\qquad
\mathbf F_i(\mathbf R)=-\nabla_{\mathbf r_i}E(\mathbf R)
$$

from reference calculations such as DFT or higher-level quantum chemistry. But this map is not an arbitrary function of a coordinate vector. Atomic systems are labeled point clouds with symmetries:

- translating the whole system should not change the energy;
- rotating or reflecting the whole system should not change the energy;
- permuting identical atoms should not change the energy;
- forces should rotate or reflect together with the molecule.

This is the natural entrance point for geometric deep learning. Instead of asking a neural network to rediscover these constraints from data, we build them into the architecture. NequIP is a particularly clean example: it learns an invariant total energy while allowing hidden features and forces to be equivariant under $E(3)$, the group of translations, rotations, and reflections in three-dimensional space.

## Equivariance Theory

A group is a set of transformations that can be composed. In molecular modeling, the relevant examples include translations, rotations, reflections, and permutations of identical atoms. A group action tells us how a group element acts on a space. If $G$ acts on an input space $\mathcal A$ by $\alpha_g$ and on an output space $\mathcal B$ by $\beta_g$, a map

$$
\Phi:\mathcal A\to\mathcal B
$$

is equivariant if

$$
\Phi(\alpha_g a)=\beta_g\Phi(a),
\qquad g\in G.
$$

In words: transforming the input and then applying the model gives the same result as applying the model and then transforming the output. If the output action $\beta_g$ is the identity action, then equivariance becomes invariance:

$$
\Phi(\alpha_g a)=\Phi(a).
$$

Energy is invariant under rotations and translations. Force is not invariant: if we rotate a molecule, the force vectors rotate too. So force is equivariant.

For vector spaces, group actions are often represented by matrices. If

$$
\alpha_g=\rho_{\rm in}(g),
\qquad
\beta_g=\rho_{\rm out}(g),
$$

then equivariance becomes

$$
\Phi(\rho_{\rm in}(g)f)
=\rho_{\rm out}(g)\Phi(f).
$$

This equation is the basic design constraint for an equivariant neural network.

### Set Up the Stage

- **stage**: the geometric space on which data live;
- **role**: how features attached to that space transform.

For example, an edge direction between two atoms is not just a generic vector of numbers. After separating a relative displacement into radius and direction,

$$
\mathbf r_{ij}=r_{ij}\hat{\mathbf r}_{ij},
\qquad
\hat{\mathbf r}_{ij}\in S^2,
$$

the angular variable lives on the sphere $S^2$. This matters because the natural basis for functions on the sphere is given by spherical harmonics $Y_{\ell m}$, which transform predictably under rotations.

The geometric language for this is that many spaces of interest are homogeneous spaces. A space $X$ is homogeneous under $G$ if $G$ acts transitively on it: any point can be moved to any other point by some group element. Fix a reference point $x_0\in X$ and define its stabilizer

$$
H=\operatorname{Stab}(x_0)
=\{h\in G:h\cdot x_0=x_0\}.
$$

Then

$$
X\simeq G/H,
\qquad
gH\mapsto g\cdot x_0.
$$

Examples:

- $\mathbb R^3\simeq E(3)/O(3)$ by choosing the origin;
- $S^2\simeq SO(3)/SO(2)$ by choosing the north pole;
- with reflections included, $S^2\simeq O(3)/O(2)$.

A scalar field on $X$ can be treated as an ordinary function $X\to\mathbb R$. But vector or tensor features are not just numbers attached to points: their components depend on a choice of local frame. The stabilizer $H$ records the freedom in choosing that frame. A representation $\tau$ of $H$ specifies how the feature coordinates change when the frame is changed. This is why we need to introduce associated bundles next.

On a homogeneous space $X\simeq G/H$, feature types are described by how they transform under the stabilizer $H$. Let

$$
\tau:H\to \mathrm{GL}(V_\tau)
$$

be a representation of $H$. It defines the associated vector bundle

$$
E_\tau=G\times_H V_\tau\longrightarrow G/H,
\qquad
(g,v)\sim(gh,\tau(h^{-1})v).
$$

A feature field is a section

$$
s\in\Gamma(E_\tau).
$$

Equivalently, it can be represented by a function

$$
\tilde s:G\to V_\tau
$$

satisfying the constraint

$$
\tilde s(gh)=\tau(h^{-1})\tilde s(g),
\qquad h\in H.
$$

The intuition is simple. The coset $gH$ is the actual point in the base space, while $g$ is a choice of representative, or a choice of local frame. Replacing $g$ by $gh$ should not change the underlying geometric object. It only changes the frame used to describe that object. Therefore the coordinate vector in the fiber must transform in the opposite way, by $\tau(h^{-1})$.

This is the same idea as changing coordinates in ordinary vector calculus: the geometric vector stays fixed, while its coordinate representation changes with the frame. The associated-bundle notation is a compact way to keep track of this dependence on local frames.

For many practical equivariant neural networks, including NequIP, we often work in a global laboratory frame and store features as blocks that transform under irreducible representations. But the bundle viewpoint explains why "a feature vector at a point" is not always just a plain function $X\to V$. The feature has a type, and the type tells us how its components are allowed to mix under symmetry transformations.

### Layer-Wise Equivariance Implies Global Equivariance

If each layer is equivariant, and if the input and output actions match between adjacent layers, then the whole network is equivariant.

```text
 A0  --Phi1-->  A1  --Phi2-->  A2
 |              |              |
 a_g^(0)        a_g^(1)        a_g^(2)
 |              |              |
 v              v              v
 A0  --Phi1-->  A1  --Phi2-->  A2
```

In the finite-dimensional representation case:

$$
\Phi_2(\Phi_1(\rho_0(g)x))
=\Phi_2(\rho_1(g)\Phi_1(x))
=\rho_2(g)\Phi_2(\Phi_1(x)).
$$

This viewpoint explains familiar architectures. CNNs are translation-equivariant on grids. RNNs are designed around temporal translation of sequence position. A Transformer without positional encoding is permutation-equivariant with respect to token order. NequIP applies the same idea to atomistic systems, where the relevant group is $E(3)$ together with atom permutations.

This gives a practical engineering rule to design an equivariant network: stacking up equivariant layers. So the next two subsections explain how to design an equivariant layer.

### Linear Equivariant Maps

A linear layer between feature fields can be written as an integral kernel:

$$
(Ls)(x)=\int_X K(x,y)s(y)\,dy,
\qquad
K(x,y)\in
\operatorname{Hom}\bigl((E_{\rm in})_y,(E_{\rm out})_x\bigr).
$$

If $L$ is equivariant, the kernel cannot be arbitrary. It must satisfy a covariance constraint:

$$
K(ux,uy)(u\cdot v)
=u\cdot\bigl(K(x,y)v\bigr).
$$

One way to see this is to compare the two routes in the equivariance square. Put a feature value $v$ at $y$. If we first transform by $u$, the value becomes $u\cdot v$ at $uy$, and the kernel sends it to $K(ux,uy)(u\cdot v)$. If instead we first apply the kernel and then transform the output, we get $u\cdot(K(x,y)v)$. Equivariance requires these to agree for every $u,x,y,v$.

If the kernel is lifted to the group, a representative

$$
\kappa:G\to\operatorname{Hom}(V_{\rm in},V_{\rm out})
$$

satisfies stabilizer constraints of the form

$$
\kappa(h_{\rm out}a h_{\rm in}) =
\tau_{\rm out}(h_{\rm out})\,
\kappa(a)\,
\tau_{\rm in}(h_{\rm in}).
$$

This is the mathematical reason equivariant convolution kernels have fewer degrees of freedom than generic kernels. The geometry constrains which learnable parameters are allowed.

There is another important consequence. If a finite-dimensional representation decomposes into irreducible blocks,

$$
V_{\rm in}
=\bigoplus_\lambda
\left(\mathbb R^{c_\lambda^{\rm in}}\otimes V_\lambda\right),
\qquad
V_{\rm out}
=\bigoplus_\lambda
\left(\mathbb R^{c_\lambda^{\rm out}}\otimes V_\lambda\right),
$$


then Schur-type arguments imply:

- non-isomorphic irreps cannot be mixed by a linear equivariant map;
- copies of the same irrep may mix through ordinary channel matrices.

So an equivariant linear layer is not free to mix every component with every other component. It may mix channels, but only within compatible representation types.

### Tensor Products (Bilinear Equivariant Maps)

Linear equivariant maps alone are not enough to build expressive networks. We also need ways to combine typed features.

The tensor product is the natural operation. If $v$ transforms under $\rho_1$ and $w$ transforms under $\rho_2$, then $v\otimes w$ transforms under the product representation

$$
(\rho_1\otimes\rho_2)(g)
=\rho_1(g)\otimes\rho_2(g).
$$

For $SO(3)$, tensor products decompose into irreducible output types:

$$
V_{\ell_1}\otimes V_{\ell_2}
\simeq
\bigoplus_{\ell=|\ell_1-\ell_2|}^{\ell_1+\ell_2}V_\ell.
$$

The projection onto each output $\ell$ is implemented by Clebsch-Gordan coefficients:

$$
\left[
h^{(\ell_1)}\otimes_\ell y^{(\ell_2)}
\right]_m = \sum_{m_1,m_2}
C^{\ell m}_{\ell_1m_1,\ell_2m_2}
h^{(\ell_1)}_{m_1}
y^{(\ell_2)}_{m_2}.
$$

These Clebsch-Gordan projections are intertwiners: they commute with the group action. That is why the tensor-product path preserves equivariance.

For $O(3)$, parity also follows a selection rule:

$$
p_{\rm out}=p_1p_2.
$$

This is the representation-theoretic version of familiar vector calculus facts. Vector times vector can produce a scalar-like dot product, a vector-like cross product, and a rank-2 symmetric traceless part. In irrep language,

$$
V_1\otimes V_1\simeq V_0\oplus V_1\oplus V_2.
$$

This is also why we should not simply concatenate all components and feed them through a generic MLP. A generic MLP has no reason to respect the $m$-component structure inside an irrep and will usually break equivariance. Tensor-product paths only produce representation-theoretically allowed output types.

### Nonlinearities

Standard pointwise nonlinearities are safe on invariant scalar channels:

$$
h^{(0,+)}\mapsto \sigma(h^{(0,+)}).
$$

They are not generally safe on vector or higher-order channels. For example, take a vector feature $v$ and the inversion operation $v\mapsto -v$. Componentwise ReLU would require

$$
\operatorname{ReLU}(-v)=-\operatorname{ReLU}(v),
$$

which is false in general. Therefore a componentwise activation applied to a vector feature breaks equivariance.

Common equivariant alternatives include:

- **gates**, where invariant scalars scale non-scalar irreps:

  $$
  h^{(\ell,p)}\mapsto \gamma(s)h^{(\ell,p)};
  $$

- **norm nonlinearities**, where a non-scalar feature is scaled by a function of an invariant norm;
- **tensor-product nonlinearities**, which build polynomial equivariant features through tensor products.

NequIP uses gated equivariant nonlinearities in its interaction blocks. The gate is an invariant scalar, so it commutes with the transformation of the non-scalar block it scales.

## Application: NequIP as an E(3)-Equivariant Potential

NequIP, introduced in *E(3)-Equivariant Graph Neural Networks for Data-Efficient and Accurate Interatomic Potentials*, is a graph neural network for learning interatomic potentials from ab initio reference data.

Its input is an atomic structure:

$$
\{(Z_i,\mathbf r_i)\}_{i=1}^N.
$$

Its output is an invariant total energy:

$$
\hat E=\sum_i \hat E_i,
$$

and forces are obtained by automatic differentiation:

$$
\hat{\mathbf F}_i=-\nabla_{\mathbf r_i}\hat E.
$$

This last choice is important. Since the force is the gradient of a scalar energy, the predicted force field is conservative by construction. Since the energy is invariant under $E(3)$, the resulting forces are equivariant.

The paper's key architectural difference from older invariant GNN potentials is that NequIP does not restrict hidden features to scalars. Each atom carries scalar, vector, and higher-order tensor features, organized as $O(3)$ irreps. The model can therefore pass angular information through the network without destroying the symmetry.

### The NequIP Pipeline

NequIP can be understood as the following sequence:

```text
{Z_i, r_i}
  -> relative displacements r_ij
  -> radial bases B_n(r_ij), cutoff f_cut(r_ij), spherical harmonics Y_lm(rhat_ij)
  -> tensor-product message passing
  -> gated equivariant updates
  -> scalar readout from 0+ channels
  -> sum of atomic energies
  -> forces by energy gradients
```

Each step has a symmetry role.

#### 1. Atomic embedding

Atomic numbers are embedded into initial scalar features:

$$
h_i^{(0,+)}\in \mathbb R^C.
$$

These are $\ell=0$, even-parity features. They are invariant under rotations and reflections, which is appropriate because an element type does not rotate.

#### 2. Edge geometry

Edges are built from local neighborhoods, usually by connecting atoms within a cutoff radius $r_c$. Instead of using absolute positions, NequIP uses relative displacements:

$$
\mathbf r_{ij}=\mathbf r_j-\mathbf r_i.
$$

This removes dependence on global translation. The displacement is separated into radius and direction:

$$
r_{ij}=|\mathbf r_{ij}|,
\qquad
\hat{\mathbf r}_{ij}=\frac{\mathbf r_{ij}}{r_{ij}}.
$$

The radial part is expanded in a basis such as Bessel functions, with a smooth cutoff envelope:

$$
B_n(r_{ij})f_{\rm cut}(r_{ij}).
$$

The angular part is expanded in spherical harmonics:

$$
Y_{\ell m}(\hat{\mathbf r}_{ij}).
$$

A typical edge basis has the form

$$
\phi_{ij}^{(\ell mn)} =
f_{\rm cut}(r_{ij})B_n(r_{ij})Y_{\ell m}(\hat{\mathbf r}_{ij}).
$$

The radial network produces scalar weights depending only on $r_{ij}$. The spherical harmonics carry the angular irrep type.

#### 3. Equivariant message passing

Node features are decomposed into irrep blocks:

$$
h_i=\bigoplus_{\ell,p}h_i^{(\ell,p)}.
$$

A schematic message from atom $j$ to atom $i$ is

$$
m_{ij} = \operatorname{TP}\left(h_j,\phi(\mathbf r_{ij})\right),
$$

where $\operatorname{TP}$ denotes the Clebsch-Gordan tensor-product coupling.

More explicitly, one message path has the form

$$
m_{ij}^{(\ell,p)} = \sum_{\ell_1,p_1,\ell_2,p_2}
w_{\ell_1p_1,\ell_2p_2\to\ell p}(r_{ij})
\left[
h_j^{(\ell_1,p_1)}
\otimes_\ell
Y_{\ell_2}^{(p_2)}(\hat{\mathbf r}_{ij})
\right].
$$

The scalar radial weight $w(r_{ij})$ is invariant. The node feature has type $(\ell_1,p_1)$. The spherical harmonic has angular type $\ell_2$ and parity $p_2$. The Clebsch-Gordan projection produces an output type $(\ell,p)$ only when the selection rules allow it:

$$
|\ell_1-\ell_2|\le \ell\le \ell_1+\ell_2,
\qquad
p=p_1p_2.
$$

This is the heart of NequIP's equivariance.

#### 4. Aggregation and update

Messages are summed over neighbors:

$$
m_i^{(\ell,p)}=\sum_{j\in\mathcal N(i)}m_{ij}^{(\ell,p)}.
$$

The sum is insensitive to the order in which neighbors are listed, so it respects permutation symmetry. Since all terms in the sum have the same irrep type, aggregation preserves the feature type.

The node state is then updated using equivariant linear self-interactions, equivariant convolutions, residual connections, and gated nonlinearities. A typical schematic update is

$$
h_i^{(t+1)} = \operatorname{Gate}
\left(
L_{\rm self}h_i^{(t)}
+L_{\rm msg}m_i^{(t)}
\right).
$$

Linear maps mix only compatible irrep channels. Gates use scalar channels to modulate non-scalar channels. Therefore the update remains equivariant.

#### 5. Scalar readout

At the end, NequIP reads atomic energies from invariant scalar channels, usually the even $\ell=0$ channels:

$$
\hat E_i = \operatorname{Readout}
\left(h_i^{(0,+)}\right).
$$

Then it sums atomic contributions:

$$
\hat E=\sum_i \hat E_i.
$$

The readout is rotationally and reflection invariant because it uses scalar channels. The atom sum is permutation invariant. Therefore the final energy is invariant.

Finally,

$$
\hat{\mathbf F}_i(\mathbf R)
=-\nabla_{\mathbf r_i}\hat E(\mathbf R).
$$

If a transformed structure has coordinates $g\cdot\mathbf R$, with rotational/reflection part $Q$, then energy invariance implies

$$
\hat E(g\cdot\mathbf R)=\hat E(\mathbf R),
$$

and the forces transform as

$$
\hat{\mathbf F}_i(g\cdot\mathbf R)
=Q\hat{\mathbf F}_i(\mathbf R).
$$

Thus conservative equivariant forces are obtained from an invariant differentiable energy.

### Why This Helps Data Efficiency

The NequIP paper reports state-of-the-art accuracy across small molecules, water and ice, reactions on surfaces, amorphous solids, and lithium superionic conductors. The most interesting point is not just accuracy, but data efficiency.

The model was shown to perform well with fewer than 1,000, and in some cases as little as 100, reference ab initio calculations. In learning-curve experiments, the authors compared equivariant NequIP models with an invariant $\ell=0$ version. The equivariant models learned faster as more data became available, while the invariant version behaved more like conventional scalar GNN potentials. This supports the paper's central claim: the improvement is tied to the use of equivariant tensor features and equivariant convolutions, not merely to parameter count.

From the viewpoint of chemistry, this is plausible. Molecular energies depend strongly on geometry: bond angles, orientations, local coordination, and higher-order spatial correlations. A scalar invariant model can represent these effects, but it must encode angular information indirectly through invariant summaries. NequIP keeps angular information alive as typed geometric features and only collapses to invariants at the energy readout. That gives the model a representation closer to the structure of the physical problem.

## Takeaways

Molecules and materials should not be treated as ordinary coordinate vectors. They are geometric objects with symmetry. Energies are invariant. Forces are equivariant. Hidden features can be equivariant too, and this is often more expressive than forcing every intermediate representation to be invariant.

The main ideas are:

- equivariance means "transforming before the model equals transforming after the model";
- homogeneous spaces explain where geometric variables live, such as directions on $S^2$;
- irreducible representations describe the allowed feature types;
- equivariant linear maps are constrained intertwiners;
- tensor products and Clebsch-Gordan coefficients are the natural way to combine angular features;
- ordinary nonlinearities must be replaced or controlled by gates, norms, or tensor products;

The result is a symmetry-first architecture for machine-learned potential energy surfaces. It does not merely fit the PES as a black-box function. It builds the geometry of atomistic physics into the function class.

## Appendix: Associated Bundles on Right Cosets

The discussion above used the left-coset convention $G/H$. In that setting the projection $G\to G/H$ has a right action of $H$:

$$
g\mapsto gh,
\qquad h\in H,
$$

and the associated bundle is defined by

$$
G\times_H V=(G\times V)/\sim,
\qquad
(g,v)\sim(gh,\rho(h^{-1})v).
$$

The inverse appears because changing the representative $g\mapsto gh$ changes the local frame, while the coordinate vector in the fiber must change in the opposite way.

For a right-coset space $H\backslash G$, the side of the stabilizer action is reversed. Let $P=G$ and let $H$ act on $P$ from the left:

$$
p\mapsto hp.
$$

Given a representation $\rho:H\to\mathrm{GL}(V)$, the associated bundle over $H\backslash G$ is

$$
P\times_H V=(P\times V)/\sim,
\qquad
(p,v)\sim(hp,\rho(h)v).
$$

Equivalently, a section can be represented by a function $F:P\to V$ satisfying

$$
F(hp)=\rho(h)F(p),
\qquad h\in H.
$$

So in the right-coset convention the fiber coordinate transforms covariantly by $\rho(h)$, not contravariantly by $\rho(h^{-1})$. The difference is purely a matter of which side the stabilizer acts on.

One way to remember the convention is to think about rigid motions. Take $G=SE(3)$ and $H=SO(3)$. If a local frame $O'$ is obtained by first translating and then rotating around the original origin $O$, then a rotation around $O$ also induces the opposite change when described from the moving frame $O'$. In the left-coset convention this opposite frame change is written explicitly as an inverse on the fiber coordinate. In the right-coset convention, however, the stabilizer already acts from the other side, so this reversal is absorbed by the left action on $P$. The two sign reversals cancel, and the quotient relation becomes

$$
(p,v)\sim(hp,\rho(h)v).
$$

The main warning is that both conventions are valid, but the inverse moves depending on whether the principal $H$-action is written on the right or on the left. Mixing these conventions is a common source of sign and inverse errors.


## References

- Simon Batzner et al., [*E(3)-Equivariant Graph Neural Networks for Data-Efficient and Accurate Interatomic Potentials*](https://arxiv.org/abs/2101.03164), Nature Communications, 2022.
- Michael M. Bronstein, Joan Bruna, Taco Cohen, and Petar Velickovic, *Geometric Deep Learning: Grids, Groups, Graphs, Geodesics, and Gauges*, 2021.
- Taco Cohen, Mario Geiger, and Maurice Weiler, *A General Theory of Equivariant CNNs on Homogeneous Spaces*, NeurIPS, 2019.
- Nathaniel Thomas et al., *Tensor Field Networks: Rotation- and Translation-Equivariant Neural Networks for 3D Point Clouds*, 2018.
