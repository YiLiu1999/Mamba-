# Mamba公式推导

$$
h'(t)=Ah(t)+Bx(t)
$$

$h(t)$ 表示隐状态， $x(t)$ 表示输入

控制系统理论中的原始表达式：

$$
x'(t)=Ax(t)+Bu(t)
$$

其中 $x'(t)$ 表示隐状态， $u(t)$ 是每个时间步的输入

希望找到隐状态和输入之间的关系： $x'(t)=Ax(t) \Rightarrow x'(t)-Ax(t)=Bu(t)$

高等数学中有 $(e^{x})'=e^{x}$

因此可以令：

$$
e^{-At}x'(t)-e^{-At}x(t)=e^{-At}Bu(t)
$$

令： $F(t)=e^{-At}x(t)$ ，求导后得： $F'(t)=-Ae^{-At}x(t)+e^{-At}x'(t)=e^{-At}Bu(t)$

最终希望得到： $x(t_{k+1})=Sx(t_k)$ （未来的是基于现有推到得到的）

希望最终的式子仅包含 $x(t),u(t)$ , 根据微积分定义可知： $F(t)=F(\lambda)+\int_{\lambda }^{t} F'(\tau )d \tau, \lambda \in (-\infty, +\infty)$

假设 $\lambda=0$

$$
\begin{align}
e^{-At}x(t)=x(0)+&\int_{0}^{t} e^{-At}Bu(\tau)d\tau \\
 \downarrow 对&其进行离散化\\
x(t)=e^{At}x(0)+&e^{At}\int_{0}^{t}e^{-A\tau}Bu(\tau)d\tau
\end{align}
$$

所以在 $t_{k+1},t_k$ 时：

$$
\begin{align}
x(t_{k+1}) &= e^{At_{k+1}}x(0)+e^{At_{k+1}}\int_{0}^{t_{k+1}}e^{-A\tau}Bu(\tau)d\tau \\
x(t_k) &= e^At_kx(0)+e^{At_k}\int_{0}^{t_k}e^{-A\tau}Bu(\tau)d\tau
\end{align}
$$

有

$$
\begin{align}
x(t_{k+1})&=e^A[t_k+(t_{k+1}-t_k)]x(0)+e^A[t_k+(t_{k+1}-t_k)]\int_{0}^{t_k+(t_{k+1}-t_k)}e^{-A\tau}Bu(\tau)d\tau \\
&={e^{At_k}*e^{A(t_{k+1}-t_k)}}x(0)+e^{At_k}\int_{0}^{t_{k+1}}e^{-A\tau}Bu(\tau)d\tau+e^{A(t_{k+1}-t_k)}\int_{0}^{t_{k+1}}e^{-A\tau}Bu(\tau)d\tau \\
&=e^{A(t_{k+1}-t_k)}[e^{At_k}x(0)+e^{At_k}\int_0^{t_k}e^{-A\tau}Bu(\tau)d\tau]+e^{At_{k+1}}\int_{t_k}^{t_{k+1}}e^{-\tau}Bu(\tau)d\tau\\
&=e^{A(t_{k+1}-t_k)}x(t_k)+e^{At_{k+1}}\int_{t_k}^{t_{k+1}}e^{-A\tau}Bu(\tau)d\tau\\
&=e^{A(t_{k+1}-t_k)}x(t_k)+\int_{t_k}^{t_{k+1}}e^{A(t_{k+1}-\tau)}Bu(\tau)d\tau\\
\end{align}
$$

令 $T=t_{k+1}-t_k, T \rightarrow0$

$$
\begin{align}
x(t_{k+1})&=e^{AT}x(t_k)+\int_{t_k}^{t_{k+1}}e^{A(t_{k+1}-\tau)}Bu(\tau)d\tau\\
&=e^{AT}x(t_k)+\int_{t_k}^{t_{k+1}}e^{A(t_{k+1}-\tau)}d\tau Bu(t_k)\\
&=e^{AT}x(t_k)-\frac{1}{A}e^{-A\tau}|_{t_k}^{t_{k+1}}e^{At_{k+1}}Bu(t_k) \\
&=e^{AT}x(t_k)-\frac{1}{A}(e^{-At_{k+1}}-e^{-At_{k}})e^{At_{k+1}}Bu(t_k) \\
&=e^{AT}x(t_k)+\frac{1}{A}(e^{A(t_{k+1}-t_{k})}-1)Bu(t_k) \\
&=e^{AT}x(t_k)+\frac{1}{A}(e^{AT}-1)Bu(t_k) \\
&=e^{AT}x(t_k)+B\frac{(e^{AT}-I)}{A} u(t_k)\\
视T为 \Delta \\
原式 &=e^{A\Delta}x(t_k)+\Delta B\frac{(e^{AT}-I)}{A\Delta} u(t_k)\\
\end{align}
$$

因此可令：

$$
\bar{A}&=e^{A \Delta} \\
\bar{B}&=\Delta B\frac{(e^{AT}-I)}{A\Delta}
$$
