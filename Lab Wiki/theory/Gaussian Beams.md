# Math
Laser beam radius $w$ depends on position along the direction of propagation $z$ as
$$
\begin{equation}
w(z) = w_0\sqrt{ 1+\frac{(z-z_0)^2\lambda^2}{\pi^2w_0^4} } = w_0\sqrt{ 1+(z-z_0)^2/R^2 }
\end{equation}
$$
where $w_0$ is the beam waist located at $z_0$, and $R$ is the **Rayleigh range** ($R = \pi w_0^2/\lambda$) of the light of wavelength $\lambda$. The intensity profile for the beam is

$I(r, z) = \frac{2P_0}{\pi w^2(z)}e^{-2r^2/w^2(z)}$

where $P_0 = \int I(r,z)r drd\theta$.

# Beam Waist Measurement

Often when working with lasers we need to know where the beam waist is so that we may pinhole the beam (to clean the mode). Other times we need the waist at a specific spot (such as the center of our trap), which we achieve with knowledge of the beam shape $w(z)$, a system of two lenses, and the Gaussian Beam simulator. To find $w(z)$ for our laser in the lab we need a set of position and radius points to fit our equation for $w(z)$. To get these sample points of $w(z)$ we can use a camera. If we do not have a camera we use a razor in what is called the knife-edge technique.

In the knife-edge technique we mount a razor on a translation stage and take power data as we translate the razor to block more of the light. We then fit this using our equation for intensity $I(z)$, where we integrate over one dimension to find the power blocked as a function of the razor position
$$
\begin{align*}

P(x) &= P_{Total}-P_{covered}\\

&=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} I(x,y)dxdy - \int_{-\infty}^{\infty} \int_{-\infty}^x I(x,y)dxdy \\

&= \int_{-\infty}^{\infty} \int_{x}^{\infty} I(x,y)dxdy\\

&= \frac{2P_0}{\pi w^2} \int_{-\infty}^{\infty} \int_{x}^{\infty} e^{-2(x^2+y^2)/w^2} dxdy\\

&= \frac{P_0}{w} \sqrt{ \frac{2}{\pi} } \int_x^{\infty} e^{-2x^2/w^2} dx \\

&= \frac{P_0}{w} \sqrt{ \frac{2}{\pi} } \left\{\int_0^{\infty} e^{-2x^2/w^2} dx - \int_0^{x} e^{-2x^2/w^2(z)} dx \right\}\\

&= \frac{P_0}{w} \sqrt{ \frac{2}{\pi} } \left\{\frac{1}{2}\sqrt{\frac{\pi}{2}}w - \frac{w}{\sqrt{2}}\int_0^{x\sqrt{2}/w} e^{-u^2} du \right\}
\end{align*}
$$

$P(x) = \frac{P_0}{2} \left\{1 -erf\left(\frac{x\sqrt{2}}{w}\right) \right\}$

We may now fit the power data obtained from the knife edge experiment to equation directly above to find $w$. This can be done numerically with python, using scipy.special.erf and scipy.optimize.cuve_fit. Keep units in mind as translation data will likely be in thousandths of an inch rather than micro meters as desired for beam radius.