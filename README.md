## Deducing the explicit mapping function of SVM

**王淳 2017301470026**

School of Mathematics and Statistics, Wu Han University

---

**RBF Kernel:**                            $K\left(\mathbf{x}_{1}, \mathbf{x}_{2}\right)=\exp \left(-\frac{\left\|\mathbf{x}_{1}-\mathbf{x}_{2}\right\|^{2}}{2 \sigma^{2}}\right)$

**Goal:**     
$$
\begin{align}
\begin{array}{c}
Find\quad \mathbf{\Phi}(\mathbf{·})\\

s.t.\quad \mathbf{\Phi}(\mathbf{y})^{T} \mathbf{\Phi}(\mathbf{x})=K(\mathbf{x}, \mathbf{y})=\exp \left(-\frac{\left\|\mathbf{x}-\mathbf{y}\right\|^{2}}{2 \sigma^{2}}\right)
\end{array}
\end{align}
$$

---

$$
\begin{align}
K\left(\mathbf{x}, \mathbf{y}\right)&=\exp \left(-\frac{\left\|\mathbf{x}-\mathbf{y}\right\|^{2}}{2 \sigma^{2}}\right)\\

&=\exp \left(-\frac{1}{2 \sigma^{2}}(\mathbf{x}-\mathbf{y})^{T}(\mathbf{x}-\mathbf{y})\right)\\

&=\exp \left(-\frac{1}{2 \sigma^{2}}\left(\mathbf{x}^{T} \mathbf{x}+\mathbf{y}^{T} \mathbf{y}-2 \mathbf{y}^{T} \mathbf{x}\right)\right)\\

&=\exp \left(-\frac{1}{2 \sigma^{2}}\left(\|\mathbf{x}\|^{2}+\|\mathbf{y}\|^{2}\right)\right) \cdot \exp \left(\frac{1}{\sigma^{2}} \mathbf{y}^{T} \mathbf{x}\right)\\

&=C(\mathbf{x})C(\mathbf{y}) \cdot \exp \left(\frac{1}{\sigma^{2}} \mathbf{y}^{T} \mathbf{x}\right)\\

&=C(\mathbf{x})C(\mathbf{y}) \cdot \sum_{i=0}^{\infty} \frac{\left(\frac{1}{\sigma^{2}} \mathbf{y}^{T} \mathbf{x}\right)^{i}}{i !}\qquad (Taylor)\\

&=\sum_{i=0}^{\infty} \frac{C(\mathbf{x})C(\mathbf{y})}{\sigma^{2 i} i !}\left(\mathbf{y}^{T} \mathbf{x}\right)^{i}\\

&=\sum_{i=0}^{\infty} \frac{C(\mathbf{x})C(\mathbf{y})}{\sigma^{2 i} i !}\left(\sum_{j=1}^{m} x_{j} y_{j}\right)^{i}
\end{align}
$$

Where:

- $\mathrm{C(\mathbf{x})}=\exp \left(\frac{\|\mathbf{x}\|^{2}}{-2 \sigma^{2}}\right),\quad \mathrm{C(\mathbf{y})}=\exp \left(\frac{\|\mathbf{y}\|^{2}}{-2 \sigma^{2}}\right)$

---
**Now, if we can find:        $\phi_i(·)$**
$$
s.t.\quad \mathbf{\phi}_{i}(\mathbf{y})^{T} \mathbf{\phi}_{i}(\mathbf{x})=\left(\mathbf{y}^{T} \mathbf{x}\right)^{i}=\left(\sum_{j=1}^{m} x_{j} y_{j}\right)^{i}
$$
**Then we can get:**
$$
\begin{align}
\frac{C(\mathbf{x})C(\mathbf{y})}{\sigma^{2 i} i !}\left(\mathbf{y}^{T} \mathbf{x}\right)^{i}&=\frac{C(\mathbf{y})}{\sigma^{i} \sqrt{i !}} \mathbf{\phi}_{i}(\mathbf{y})^{T} \frac{C(\mathbf{x})}{\sigma^{i} \sqrt{i !}} \mathbf{\phi}_{i}(\mathbf{x})\\

&=a_{i}(\mathbf{y}) \mathbf{\phi}_{i}(\mathbf{y})^{T} a_{i}(\mathbf{x}) \mathbf{\phi}_{i}(\mathbf{x})
\end{align}
$$

Where:
- $a_{i}(\mathbf{x})=\frac{C(\mathbf{x})}{\sigma^{i} \sqrt{i !}}, \quad a_{i}(\mathbf{y})=\frac{C(\mathbf{y})}{\sigma^{i} \sqrt{i !}}$

---
**Meanwhile, $\phi_i(·)$ Happens to be the mapping function of the Polynomial Kernel:**
$$
\mathbf{\phi}_{d}(\mathbf{y})^{T} \mathbf{\phi}_{d}(\mathbf{x})=K_{d}(\mathbf{x}, \mathbf{y})=\left(\mathbf{y}^{T} \mathbf{x}\right)^{d}=\left(\sum_{j=1}^{m} x_{j} y_{j}\right)^{d}
$$

---

**Th:**    (Multinomial Theorem)
$$
\left(x_{1}+x_2+\cdots+x_{m}\right)^{n}=\sum_{|\alpha|=n}\left(\begin{array}{l}n \\ \alpha\end{array}\right) \mathbf{x}^{\alpha}, \quad \alpha=\left(\alpha_{1}, \alpha_{2}, \cdots, \alpha_{m}\right)
$$

where:

- $|\alpha|=\sum_{k=1}^{m} \alpha_{k}$
- $\mathbf{x}^{\alpha}=x_{1}^{\alpha_{1}} x_{2}^{\alpha_{2}} \cdots x_{m}^{\alpha_{m}}$
- $\left(\begin{array}{l}n \\ \alpha\end{array}\right)=\left(\begin{array}{c}n \\ \alpha_{1}, \alpha_{2}, \cdots, \alpha_{m}\end{array}\right)=\frac{n !}{\alpha_{1} ! \alpha_{2} ! \cdots \alpha_{m} !}$

**Example:**
$$
\begin{equation*}
\begin{aligned}
(x_1+x_2)^2&=\left(\begin{array}{c}2 \\ 2,0\end{array}\right)x_1^2x_2^0 + \left(\begin{array}{c}2 \\ 1,1\end{array}\right)x_1^1x_2^1 + \left(\begin{array}{c}2 \\ 0,2\end{array}\right)x_1^0x_2^2\\
&= x_1^2 + 2x_1x_2 + x_2^2
\end{aligned}
\end{equation*}
$$

---

According to Multinomial Theorem:

$$
\begin{align}
K_{d}\left(\mathbf{x}, \mathbf{y}\right)&=\left(\sum_{i=1}^{n} x_{i} y_{i}\right)^{d}\\

&=\sum_{|\alpha|=d}\left(\begin{array}{l}d \\ \alpha\end{array}\right){(x_{1}y_{1})}^{\alpha_{1}} {(x_{2}y_{2})}^{\alpha_{2}} \cdots {(x_{m}y_{m})}^{\alpha_{m}}\\

&=\sum_{|\alpha|=d}\left(\begin{array}{l}d \\ \alpha\end{array}\right)x_{1}^{\alpha_{1}} x_{2}^{\alpha_{2}} \cdots x_{m}^{\alpha_{m}}y_{1}^{\alpha_{1}} y_{2}^{\alpha_{2}} \cdots y_{m}^{\alpha_{m}}\\

&=\sum_{|\alpha|=d}\left(\begin{array}{l}d \\ \alpha\end{array}\right) \mathbf{x}^{\alpha} \mathbf{y}^{\alpha}\\

&=\sum_{|\alpha|=d} \sqrt{\left(\begin{array}{l}d \\ \alpha\end{array}\right)} \mathbf{x}^{\alpha} \sqrt{\left(\begin{array}{l}d \\ \alpha\end{array}\right)} \mathbf{y}^{\alpha}\\

&=\left[\sqrt{\left(\begin{array}{l}d \\ \alpha\end{array}\right)} \mathbf{y}^{\alpha}\right]^{T}\left[\sqrt{\left(\begin{array}{l}d \\ \alpha\end{array}\right)} \mathbf{x}^{\alpha}\right], \forall|\alpha|=d \\

&=\mathbf{\phi}_{d}(\mathbf{y})^{T} \mathbf{\phi}_{d}(\mathbf{x}) \\
\end{align}
$$

$$
\therefore \quad \mathbf{\phi}_{d}(\mathbf{x})=\left[\sqrt{\left(\begin{array}{c}
d \\
\alpha_{1}, \alpha_{2}, \cdots, \alpha_{n}
\end{array}\right)} x_{1}^{\alpha_{1}} x_{2}^{\alpha_{2}} \cdots x_{m}^{\alpha_{m}}\right], \forall \sum_{k=1}^{m} \alpha_{k}=d
$$
---
**Example:**

- $for \quad \mathbf{x} \in \mathbf{R}^2,\quad d=2$ :

$$
\mathbf{\phi}_{2}\left(\mathbf{x}\right)=\mathbf{\phi}_{2}\left(\left[\begin{array}{c} x_{1}\\ x_{2}\end{array}\right]\right)=\left[\begin{array}{c} x_{1}^{2}\\ \sqrt{2} x_{1} x_{2}\\  x_{2}^{2}\\ \end{array}\right]
$$
- $for \quad \mathbf{x} \in \mathbf{R}^2,\quad d=3$ :
$$
\mathbf{\phi}_{3}\left(\mathbf{x}\right)=\mathbf{\phi}_{3}\left(\left[\begin{array}{c} x_{1}\\ x_{2}\end{array}\right]\right)

=\left[ \begin{array}{c}x_{1}^{3}\\ \sqrt{3} x_{1}^{2} x_{2}\\ \sqrt{3} x_{1} x_{2}^2\\  x_{2}^{3} \end{array}\right]
$$

---

**Then for the RBF kernel:**
$$
\begin{align}
K(\mathbf{x}, \mathbf{y})&=\sum_{i=0}^{\infty} \frac{C(\mathbf{x})C(\mathbf{y})}{\sigma^{2 i} i !}\left(\mathbf{y}^{T} \mathbf{x}\right)^{i}\\

&=\sum_{i=0}^{\infty} a_{i}(\mathbf{y}) \mathbf{\phi}_{i}(\mathbf{y})^{T} a_{i}(\mathbf{x}) \mathbf{\phi}_{i}(\mathbf{x})\\

&=\mathbf{\Phi}(\mathbf{y})^{T} \mathbf{\Phi}(\mathbf{x})\\
\end{align}
$$

$$
\therefore \quad \mathbf{\Phi}(\mathbf{x})=\left[\begin{array}{c} a_{0}(\mathbf{x}) \mathbf{\phi}_{0}(\mathbf{x})\\ a_{1}(\mathbf{x}) \mathbf{\phi}_{1}(\mathbf{x})\\ a_{2}(\mathbf{x}) \mathbf{\phi}_{2}(\mathbf{x})\\ \vdots \end{array}\right]
$$

Where:

- $a_{i}(\mathbf{x})=\frac{C(\mathbf{x})}{\sigma^{i} \sqrt{i !}}=\frac{\exp \left(\frac{\|\mathbf{x}\|^{2}}{-2 \sigma^{2}}\right)}{\sigma^{i} \sqrt{i !}}$
- $\mathbf{\phi}_{i}(\mathbf{x})=\left[\sqrt{\left(\begin{array}{c}
  i \\
  \alpha_{1}, \alpha_{2}, \cdots, \alpha_{n}
  \end{array}\right)} x_{1}^{\alpha_{1}} x_{2}^{\alpha_{2}} \cdots x_{m}^{\alpha_{m}}\right], \forall \sum_{k=1}^{m} \alpha_{k}=i$

---

