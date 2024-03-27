---
title: "Correlation Function and Power Spectrum"
categories: 'Cosmology'
---

这是一篇对2pcf及功率谱的简要介绍。由于学术书面语言需要，下文使用英语。/

Here is a short introduction of 2pcf and power spectrum. The following would be written in English.

# Correlation function

## 2PCF

* $ dN_{ab}=\langle n_an_b\rangle $ : the number of pairs in volumes $dV_a$ and $dV_b$ seperated by $r_{ab}$ .

  Def 2pcf (2 point correlation function $\xi(r_{ab})$ , $\rho_0=N/V$ is the average numerical density.

$$
dN_{ab}=\langle n_an_b \rangle=\rho_0^2 dV_a dV_b [1+\xi(r_{ab})]\\
\xi(r_{ab})=\dfrac{dN_{ab}}{\rho_0^2 dV_a dV_b}-1=\langle \delta(r_a)\delta(r_b)\rangle,\ \delta(r_a)=n_a/(\rho_0dV_a)-1
$$

​	Obviously, $\langle \delta(r_a) \rangle=0$.

* $\langle \rangle$ , average, may have 2 meanings.
  * taking many relizations of the distribution, all of them produced in the same IC (initial condition), selecting in each realization that $dV_a,dV_b$ at the same locations an then aceraging the pair number $n_an_b$ --- ensemble average.
  * take pairs at different spots within the same realization seperated by the same $r_{ab}$.

* If we take the average as the sample average, then $\delta(\mathbf r)=\frac 1V\int\delta(\mathbf y)\delta (\mathbf{y+r})dV_y$.

* In practice, we often choose $dV_a$ s.t. $\rho_0 d V_a=1$. Then we have the follows:

$$
dN_b=\rho_0dV_b[1+\xi(r_b)]\\
\xi(r)=\dfrac{dN(r)}{\rho_0dV}-1=\dfrac{\langle\rho_c\rangle}{\rho_0}-1
$$

* i.e. evaluates the correlation function as the average number of particles at distant $r$ from any given particle, divided by the expected number of particles at the same distance in a uniform distribution, minus 1. 

  In a finite volume with $N=\rho_0V$ particles, $\int \xi(r)dV=0$ apparently.

* If $\xi(r)$ positive, there are more particles than in a uniform distribution, i.e. the distribution is positively clustered. 

* Usually only consider its dependence on the modulus $r$. So the volume $V$ is chosen as a **shell** around each particle. Then $\rho_c$ is the number density inside a shell of thickness $dr$ at distance $r$ from every particle.  Just requires the estimation of the density in every shell.

  * One could generalize the Def by introducing anisotropic CF as # of pairs in V separated by vec. $\mathbf r$.

*  The simplest way to measure $\xi$ is to compare the real catalog to an artificial random catalog with exactly the same boundaries and the same selection function.
  $$
  \xi=\dfrac{n_R DD}{n_D DR}-1
  $$
  $n_R,n_D$ is the number density of galaxies in the data and random catalogs. $DD$ means the number of galaxies at distance r counted by an observer centered on a real galaxy (data $D$). $DR$ is the number of galaxies at the same distance but in the random catalog centered on a real galaxy. Actually we are estimating $\xi$ by counting galaxies with MC method.

  * "random catalog" $R$ has the identical three dimensional coverage as the data - including the same sky coverage and smoothed redshift distribution - but is populated with randomly-distribution points.

* An estimator with smaller err by Hamilton 1993:
  $$
  \xi=\dfrac{DD\ RR}{(DR)^2}-1
  $$
  
* A most commonly-used estimator is from Landy & Szalay (1993) with smaller errors:
  $$
  \xi=\dfrac 1 {RR}[DD(\dfrac{n_R}{n_D})^2-2DR\dfrac{n_R}{n_D}+RR]
  $$
  It's less sensitive to the size of random catalog and handles edge corrections well.

## nPCF

* 1pcf --- average number density $\rho_0$ ; 2pcf -- $\xi(r)$

* 3pcf: $\zeta_{abc}(r_a,r_b,r_c)=\langle\delta(r_a)\delta(r_b)\delta(r_c)\rangle=\dfrac{n_an_bn_c}{\rho_0^3dV_adV_bdV_c}-\xi_{ab}-\xi_{ac}-\xi_{ac}-1$

  Then $\langle n_an_bn_c\rangle=\rho_0^3dV_adV_bdV_c (\xi_{ab}+\xi_{ac}+\xi_{ac}+\zeta_{abc}+1)$

  When $\zeta_{abc}=0$, a field is Gaussian, then the 2pcf or the power spectrum completely describes the statistical properties of the field.

## Power spectrum

**Power spectrum is the FT of 2pcf:**
$$
P(\mathbf k)=V|\delta_{\mathbf k}|^2=\frac 1V\int \delta(\mathbf x)\delta(\mathbf y)e^{-i\mathbf{k\cdot (x-y)}}dV_xdV_y=\int\xi(\mathbf r)e^{-i\mathbf {k\cdot r}}dV
$$
Wavelengths in different modes are uncorrelated if the field is statistically homogeneous.





#### Updating...