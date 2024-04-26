# Mamba公式推导

$$
h'(t)=Ah(t)+Bx(t)
$$

h(t)表示隐状态，x(t)表示输入

控制系统理论中的原始表达式：

$$
x'(t)=Ax(t)+Bu(t)
$$

其中 $x'(t)$ 表示隐状态， $u(t)$ 是每个时间步的输入

希望找到隐状态和输入之间的关系：

$$x'(t)=Ax(t) \Rightarrow x'(t)-Ax(t)=Bu(t)$$


高等数学中有 $(e^{x})'=e^{x}$ ,因此可以令：

$$
e^{-At}x'(t)-e^{-At}x(t)=e^{-At}Bu(t)
$$

令： $F(t)=e^{-At}x(t)$ ，求导后得：

$$F'(t)=-Ae^{-At}x(t)+e^{-At}x'(t)=e^{-At}Bu(t)$$


最终希望得到： $x(t_{k+1})=Sx(t_k)$ （未来的是基于现有推到得到的）

希望最终的式子仅包含 $x(t),u(t)$ 

根据微积分定义可知：

$$F(t)=F(\lambda)+\int_{\lambda }^{t} F'(\tau )d \tau, \lambda \in (-\infty, +\infty)$$


假设 $\lambda=0$ :

$$
e^{-At}x(t)=x(0)+\int_{0}^{t} e^{-At}Bu(\tau)d\tau \\
\downarrow 对其进行离散化 \\
x(t)=e^{At}x(0)+e^{At}\int_{0}^{t}e^{-A\tau}Bu(\tau)d\tau
$$

所以在 $t_{k+1},t_k$ 时：
$$
x(t_{k+1})=e^{At_{k+1}}x(0)+e^{At_{k+1}}\int_{0}^{t_{k+1}}e^{-A\tau}Bu(\tau)d\tau
$$

