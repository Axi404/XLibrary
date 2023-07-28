# 马尔可夫不等式

## 结论

对于任意非负随机变量 $X$，$\forall \epsilon>0$，有：

$$
P (X \geq \epsilon) \leq \frac{E (X)}{\epsilon}
$$

切比雪夫不等式 $P(|X-\mu| \geq k \sigma) \leq \frac{1}{k^{2}}(k>0)$ 是它的特例。

## 证明

根据

$$
\begin{aligned}
E (X) & =\int_{0}^{\infty} x f (x) d x \\
& \geq \int_{\epsilon}^{\infty} x f (x) d x \\
& \geq \int_{\epsilon}^{\infty} \epsilon f (x) d x \\
& =\epsilon P (X \geq \epsilon)
\end{aligned}
$$

把 $\epsilon$ 除过去，得证。离散情况一样。

# 霍夫丁不等式引理

## 结论

对于随机变量 $X$，$P (X \in[a, b])=1$，$E (X)=0$，有：

$$
E\left (e^{s X}\right) \leq e^{s^{2}(b-a)^{2} / 8}
$$

## 证明

因 $e^{s X}$ 是关于 $X$ 的凸函数，由凸函数性质：

$$
e^{s X} \leq \frac{b-X}{b-a} e^{s a}+\frac{X-a}{b-a} e^{s b}
$$

于是对 $X$ 取期望，有：

$$
\begin{aligned}
E\left (e^{s X}\right) & \leq \frac{b-E (X)}{b-a} e^{s a}+\frac{E (X)-a}{b-a} e^{s b} \\
& =\frac{b}{b-a} e^{s a}-\frac{a}{b-a} e^{s b} \\
& =\left (-\frac{a}{b-a}\right) e^{s a}\left (-\frac{b}{a}+e^{s b-s a}\right)
\end{aligned}
$$

因为 $E (X)=0$，$X \in[a, b]$，而 $a, b$ 都为 $0$ 的情况没有讨论的意义，所以有 $a<0, b>0$。令 $\theta=-\frac{a}{b-a}>0$，则上式变为：

$$
\begin{aligned}
E\left (e^{s X}\right) & \leq \theta e^{-s \theta (b-a)}\left (\frac{1}{\theta}-1+e^{s (b-a)}\right) \\
& =\left (1-\theta+\theta e^{s (b-a)}\right) e^{-s \theta (b-a)}
\end{aligned}
$$

因为：

$$
1-\theta+\theta e^{u}=\theta\left (\frac{1}{\theta}-1+e^{u}\right)=\theta\left (-\frac{a}{b}+e^{u}\right)>0
$$

所以不等式可以变为：

$$
\begin{array}{c}
E\left (e^{s X}\right) \leq e^{\ln \left (1-\theta+\theta e^{s (b-a)}\right)} e^{-s \theta (b-a)} \\
E\left (e^{s X}\right) \leq e^{\ln \left (1-\theta+\theta e^{u}\right)-\theta u}
\end{array}
$$

令 $u=s (b-a)$：

定义 $\varphi: R \rightarrow R$， $\varphi (u)=\ln \left (1-\theta+\theta e^{u}\right)-\theta u$。由 $1-\theta+\theta e^{u}=\theta\left (\frac{1}{\theta}-1+e^{u}\right)=\theta\left (-\frac{a}{b}+e^{u}\right)>0$ 可得这个函数是良定义的，也就是 $\varphi (u)$ 的 $\ln$ 并不限制 $u$ 的取值。得：

$$
E\left (e^{s X}\right) \leq e^{\varphi (u)}
$$

由泰勒中值定理，$\exists \xi \in[0, u]$ 使：

$$
\varphi (u)=\varphi (0)+u \varphi^{\prime}(0)+\frac{1}{2} u^{2} \varphi^{\prime \prime}(\xi)
$$

其中：

$$
\begin{aligned}
\varphi (0)= & 0 \\
\varphi^{\prime}(0) & =\left.\left (\frac{\theta e^{u}}{1-\theta+\theta e^{u}}-\theta\right)\right|_{u=0}=0 \\
\varphi^{\prime \prime}(\xi) & =\frac{\theta e^{\xi}\left (1-\theta+\theta e^{\xi}\right)-\theta^{2} e^{2 \xi}}{\left (1-\theta+\theta e^{\xi}\right)^{2}} \\
& =\frac{\theta e^{\xi}}{1-\theta+\theta e^{\xi}}\left (1-\frac{\theta e^{\xi}}{1-\theta+\theta e^{\xi}}\right) \\
& =t (1-t) \leq \frac{1}{4}
\end{aligned}
$$

因此有：

$$
\varphi (u) \leq 0+0+\frac{1}{2} u^{2} \times \frac{1}{4}=\frac{1}{8} s^{2}(b-a)^{2}
$$

于是：

$$
E\left (e^{s X}\right) \leq e^{s^{2}(b-a)^{2} / 8}
$$

# 霍夫丁不等式

## 结论

霍夫丁不等式适用于有界的随机变量。设有两两独立的一系列随机变量 $X_{1}, \ldots, X_{n}$。假设对所有的 $X_{i}$ 都是几乎有界（看成有界就好了）的变量，即满足：

$$
P\left (X_{i} \in\left[a_{i}, b_{i}\right]\right)=1
$$

那么这 $n$ 个随机变量的经验期望（均值）：

$$
\bar{X}=\frac{X_{1}+\cdots+X_{n}}{n}
$$

满足以下不等式：

$$
\begin{array}{c}
P (\bar{X}-E (\bar{X}) \geq t) \leq \exp \left (-\frac{2 t^{2} n^{2}}{\sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}}\right) \\
P (|\bar{X}-E (\bar{X})| \geq t) \leq 2 \exp \left (-\frac{2 t^{2} n^{2}}{\sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}}\right)
\end{array}
$$

## 证明

对于 $X_{1}, X_{2}, \ldots, X_{n}$，$n$ 个相互独立的随机变量，$P\left (X_{i} \in\left[a_{i}, b_{i}\right]\right)=1,1 \leq i \leq n$ ，令：

$$
S_{n}=\sum_{i=1}^{n} X_{i}
$$

取 $s>0, t>0$，由马尔科夫不等式得：

$$
\begin{aligned}
P\left (S_{n}-E\left (S_{n}\right) \geq t\right) & =P\left (e^{s\left (S_{n}-E\left (S_{n}\right)\right)} \geq e^{s t}\right) \\
& \leq e^{-s t} E\left (e^{s\left (S_{n}-E\left (S_{n}\right)\right)}\right) \\
& =e^{-s t} \prod_{i=1}^{n} E\left (e^{s\left (X_{i}-E\left (X_{i}\right)\right)}\right)
\end{aligned}
$$

再由引理得：

$$
\begin{aligned}
P\left (S_{n}-E\left (S_{n}\right) \geq t\right) & \leq e^{-s t} \prod_{i=1}^{n} e^{\frac{s^{2}\left (b_{i}-a_{i}\right)^{2}}{8}} \\
& =\exp \left (-s t+\frac{1}{8} s^{2} \sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}\right)
\end{aligned}
$$

到这一步，不等式中还多出了一个 $s$，因为 $\forall s>0$ ，都有以上不等式成立，因此取右边关于 $s$ 的二次函数的最小值。令：

$$
g (s)=-s t+\frac{1}{8} s^{2} \sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}
$$

求 $g^{\prime}(s)=0$ ，得：

$$
s=\frac{4 t}{\sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}}
$$

于是：

$$
P\left (S_{n}-E\left (S_{n}\right) \geq t\right) \leq \exp \left (-\frac{2 t^{2}}{\sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}}\right)
$$

变换成 $X_{i}$ 的均值 $\bar{X}$，也就是：

$$
P (\bar{X}-E (\bar{X}) \geq t) \leq \exp \left (-\frac{2 t^{2} n^{2}}{\sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}}\right)
$$

取反后依然成立：

$$
P (E (\bar{X})-\bar{X} \geq t) \leq \exp \left (-\frac{2 t^{2} n^{2}}{\sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}}\right)
$$

合到一起：

$$
P (|\bar{X}-E (\bar{X})| \geq t) \leq 2 \exp \left (-\frac{2 t^{2} n^{2}}{\sum_{i=1}^{n}\left (b_{i}-a_{i}\right)^{2}}\right)
$$

得证。

# 参考

[霍夫丁（Hoeffding）不等式证明 - 颀周](https://www.cnblogs.com/qizhou/p/12843557.html#%E9%A9%AC%E5%B0%94%E5%8F%AF%E5%A4%AB%E4%B8%8D%E7%AD%89%E5%BC%8F)