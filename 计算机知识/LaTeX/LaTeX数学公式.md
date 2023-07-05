本文旨在教学 $\mathrm{\LaTeX}$ 的数学公式。在 Markdown 语言中，$\mathrm{\LaTeX}$ 数学公式被插入在 `$\func$` 中，而在 $\mathrm{\LaTeX}$ 其自身的语法中，也亦是如此。

下文会给出 $\mathrm{\LaTeX}$ 数学公式的效果以及对应源码。

# 声调 / 变音符号

```markdown
$\dot{a} \ddot{a} \acute{a} \grave{a}$
```

$$\dot{a} \quad \ddot{a} \quad \acute{a} \quad \grave{a}$$

```markdown
$\check{a} \breve{a} \tilde{a} \bar{a}$
```

$$\check{a} \quad \breve{a} \quad \tilde{a} \quad \bar{a}$$

```markdown
$\hat{a} \widehat{a} \vec{a}$
```

$$\hat{a} \quad \widehat{a} \quad \vec{a}$$

```markdown
$\exp_a b=a^b \exp b=e^b 10^m$
```

# 标准函数

$$\exp_a b=a^b \exp b=e^b 10^m$$

```markdown
$\sin a \cos b \tan c \sec d \csc e \cot f$
```

$$\sin a \quad \cos b \quad \tan c \quad \sec d \quad \csc e \quad \cot f$$

```markdown
$\arcsin a \arccos b \arctan c$
```

$$\arcsin a \quad \arccos b \quad \arctan c$$

```markdown
$\sinh a \cosh b \tanh c \coth d$
```

$$\sinh a \quad \cosh b \quad \tanh c \quad \coth d$$

```markdown
$\sh a \ch b \th c$
```

$$\operatorname{sh} a \quad \operatorname{ch} b \quad \operatorname{th} c$$

> 在 [[Obsidian阅读指南#什么是 Obsidian|Obsidian]] 中并未提供 `$\sh a \ch b \th c$` 的 $\mathrm{\LaTeX}$ 环境。

```markdown
$\operatorname{argsh} a \operatorname{argch} b \operatorname{argth} c$
```

> `\operatorname{}` 貌似可以将任何字符转换成标准函数的形式。

$$\operatorname{argsh} a \quad\operatorname{argch} b \quad\operatorname{argth} c$$

```markdown
$\left\vert a\right\vert \min(x,y) \max(x,y)$
```

$$\left\vert a\right\vert \quad\min(x,y) \quad\max(x,y)$$

# 界限

```markdown
$\min x \max y \inf s \sup t$
```

$$\min x \quad \max y \quad \inf s \quad \sup t$$

```markdown
$\lim u \liminf v \limsup w$
```

$$\lim u \quad \liminf v \quad \limsup w$$

```markdown
$\dim p \deg q \det m \ker\phi$
```

$$\dim p \quad \deg q \quad \det m \quad \ker\phi$$

# 映射

```markdown
$\Pr j \hom l \lVert z\rVert \arg z$
```

$$\Pr j \quad \hom l \quad \lVert z\rVert \quad \arg z$$

# 微分及导数

```markdown
$dt \mathrm{d}t \partial t \nabla\psi$
```

$$dt \quad \mathrm{d}t \quad \partial t \quad \nabla\psi$$

```markdown
$\prime \backprime f^\prime f' f'' f^{(3)} \dot{y} \ddot{y}$
```

$$\prime \quad \backprime \quad f^\prime \quad f' \quad f'' \quad f^{(3)} \quad \dot{y} \quad \ddot{y}$$

# 类字母符号及常数

```markdown
$\infty \aleph \complement \backepsilon \eth \Finv \hbar$
```

$$\infty \quad \aleph \quad \complement \quad \backepsilon \quad \eth \quad \Finv \quad \hbar$$

```markdown
$\Im \imath \jmath \Bbbk \ell \mho \wp \Re \circledS$
```

 $$\Im \quad \imath \quad \jmath \quad \Bbbk \quad \ell \quad \mho \quad \wp \quad \Re \quad \circledS$$

# 模算数

```markdown
$a\equiv1\pmod{m}$
```

$$a\equiv1\pmod{m}$$

```markdown
$a\bmod b$
```

$$a\bmod b$$ 

```markdown
$\gcd(m,n) \operatorname{lcm}(m,n)$
```

$$\gcd(m,n) \quad \operatorname{lcm}(m,n)$$

```markdown
$\mid \nmid \shortmid \nshortmid$
```

$$\mid \quad \nmid \quad \shortmid \quad \nshortmid$$

```markdown
$a\%b$
```

$$a\%b$$

> 不建议在公式中使用 `\%` 作为取模，一般仅作百分号使用）

# 根号

```markdown
$\surd \sqrt{2} \sqrt[n]{} \sqrt[n]{x}$
```

$$\surd \quad \sqrt{2} \quad \sqrt[n]{} \quad \sqrt[n]{x}$$

# 运算符

```markdown
$+ - \pm \mp \dotplus$
```

$$+ \quad - \quad \pm \quad \mp \quad \dotplus$$

```markdown
$\times \div \divideontimes / \backslash$
```

$$\times \quad \div \quad \divideontimes \quad / \quad \backslash$$

```markdown
$\cdot * \star \circ \bullet$
```

>  `*` 可以用 `\ast` 代替。

$$\cdot \quad * \quad \star \quad \circ \quad \bullet$$

```markdown
$\boxplus \boxminus \boxtimes \boxdot$
```

$$\boxplus \quad \boxminus \quad \boxtimes \quad \boxdot$$

```markdown
$\oplus \ominus \otimes \oslash \odot$
```

$$\oplus \quad \ominus \quad \otimes \quad \oslash \quad \odot$$

```markdown
$\circleddash \circledcirc \circledast$
```

$$\circleddash \quad \circledcirc \quad \circledast$$

```markdown
$\bigoplus \bigotimes \bigodot$
```

$$\bigoplus \quad \bigotimes \quad \bigodot$$

# 集合

```markdown
$\{ \} \emptyset \varnothing$
```

$$\{ \quad \} \quad \emptyset \quad \varnothing$$

```markdown
$\in \notin \not\in \ni \not\ni$
```

>  `\not` 是在下一个字符上画斜杠。

$$\in \quad \notin \quad \not\in \quad \ni \quad \not\ni$$

```markdown
$\cap \Cap \sqcap \bigcap$
```

$$\cap \quad \Cap \quad \sqcap \quad \bigcap$$

```markdown
$\cup \Cup \sqcup \bigcup \bigsqcup \uplus \biguplus$
```

$$\cup \quad \Cup \quad \sqcup \quad \bigcup \quad \bigsqcup \quad \uplus \quad \biguplus$$

```markdown
$\setminus \smallsetminus \times$
```

$$\setminus \quad \smallsetminus \quad \times$$

```markdown
$\subset \not\subset \Subset \sqsubset$
```

$$\subset \quad \not\subset \quad \Subset \quad \sqsubset$$

```markdown
$\supset \Supset \sqsupset$
```

$$\supset \quad \Supset \quad \sqsupset$$

```markdown
$\subseteq \nsubseteq \subsetneq \varsubsetneq \sqsubseteq$
```

$$\subseteq \quad \nsubseteq \quad \subsetneq \quad \varsubsetneq \quad \sqsubseteq$$

```markdown
$\supseteq \nsupseteq \supsetneq \varsupsetneq \sqsupseteq$
```

$$\supseteq \quad \nsupseteq \quad \supsetneq \quad \varsupsetneq \quad \sqsupseteq$$

```markdown
$\subseteqq \nsubseteqq \subsetneqq \varsubsetneqq$
```

$$\subseteqq \quad \nsubseteqq \quad \subsetneqq \quad \varsubsetneqq$$

```markdown
$\supseteqq \nsupseteqq \supsetneqq \varsupsetneqq$
```

$$\supseteqq \quad \nsupseteqq \quad \supsetneqq \quad \varsupsetneqq$$

### 关系符号

```markdown
$= \ne \neq \equiv \not\equiv$
```

$$= \quad \ne \quad \neq \quad \equiv \quad \not\equiv$$

```markdown
$\doteq \doteqdot \overset{\underset{def}{}}{=} :=$
```

$$\doteq \quad \doteqdot \quad \overset{\underset{def}{}}{=} \quad :=$$

```markdown
$\sim \nsim \backsim \thicksim \simeq \backsimeq \eqsim \cong \ncong$
```

$$\sim \quad \nsim \quad \backsim \quad \thicksim \quad \simeq \quad \backsimeq \quad \eqsim \quad \cong \quad \ncong$$

```markdown
$\approx \thickapprox \approxeq \asymp \propto \varpropto$
```

$$\approx \quad \thickapprox \quad \approxeq \quad \asymp \quad \propto \quad \varpropto$$

```markdown
$< \nless \ll \not\ll \lll \not\lll \lessdot$
```

$$< \quad \nless \quad \ll \quad \not\ll \quad \lll \quad \not\lll \quad \lessdot$$

```markdown
$> \ngtr \gg \not\gg \ggg \not\ggg \gtrdot$
```

$$> \quad \ngtr \quad \gg \quad \not\gg \quad \ggg \quad \not\ggg \quad \gtrdot$$

```markdown
$\le \leq \lneq \leqq \nleq \nleqq \lneqq \lvertneqq$
```

$$\le \quad \leq \quad \lneq \quad \leqq \quad \nleq \quad \nleqq \quad \lneqq \quad \lvertneqq$$

```markdown
$\ge \geq \gneq \geqq \ngeq \ngeqq \gneqq \gvertneqq$
```

$$\ge \quad \geq \quad \gneq \quad \geqq \quad \ngeq \quad \ngeqq \quad \gneqq \quad \gvertneqq$$

```markdown
$\lessgtr \lesseqgtr \lesseqqgtr \gtrless \gtreqless \gtreqqless$
```

$$\lessgtr \quad \lesseqgtr \quad \lesseqqgtr \quad \gtrless \quad \gtreqless \quad \gtreqqless$$

```markdown
$\leqslant \nleqslant \eqslantless$
```

$$\leqslant \quad \nleqslant \quad \eqslantless$$

```markdown
$\geqslant \ngeqslant \eqslantgtr$
```

$$\geqslant \quad \ngeqslant \quad \eqslantgtr$$

```markdown
$\lesssim \lnsim \lessapprox \lnapprox$
```

$$\lesssim \quad \lnsim \quad \lessapprox \quad \lnapprox$$

```markdown
$\gtrsim \gnsim \gtrapprox \gnapprox$
```

$$\gtrsim \quad \gnsim \quad \gtrapprox \quad \gnapprox$$

```markdown
$\prec \nprec \preceq \npreceq \precneqq$
```

$$\prec \quad \nprec \quad \preceq \quad \npreceq \quad \precneqq$$

```markdown
$\succ \nsucc \succeq \nsucceq \succneqq$
```

$$\succ \quad \nsucc \quad \succeq \quad \nsucceq \quad \succneqq$$

```markdown
$\preccurlyeq \curlyeqprec$
```

$$\preccurlyeq \quad \curlyeqprec$$

```markdown
$\succcurlyeq \curlyeqsucc$
```

$$\succcurlyeq \quad \curlyeqsucc$$

```markdown
$\precsim \precnsim \precapprox \precnapprox$
```

$$\precsim \quad \precnsim \quad \precapprox \quad \precnapprox$$

```markdown
$\succsim \succnsim \succapprox \succnapprox$
```

$$\succsim \quad \succnsim \quad \succapprox \quad \succnapprox$$

# 几何符号

```markdown
$\parallel \nparallel \shortparallel \nshortparallel$
```

$$\parallel \quad \nparallel \quad \shortparallel \quad \nshortparallel$$

```markdown
$\perp \angle \sphericalangle \measuredangle 45^\circ$
```

$$\perp \quad \angle \quad \sphericalangle \quad \measuredangle \quad 45^\circ$$

```markdown
$\Box \blacksquare \diamond \Diamond \lozenge \blacklozenge \bigstar$
```

$$\Box \quad \blacksquare \quad \diamond \quad \Diamond \quad \lozenge \quad \blacklozenge \quad \bigstar$$

```markdown
$\bigcirc \triangle \bigtriangleup \bigtriangledown$
```

$$\bigcirc \quad \triangle \quad \bigtriangleup \quad \bigtriangledown$$

```markdown
$\vartriangle \triangledown \triangleleft \triangleright$
```

$$\vartriangle \quad \triangledown \quad \triangleleft \quad \triangleright$$

```markdown
$\blacktriangle \blacktriangledown \blacktriangleleft \blacktriangleright$
```

$$\blacktriangle \quad \blacktriangledown \quad \blacktriangleleft \quad \blacktriangleright$$

# 逻辑符号

```markdown
$\forall \exists \nexists$
```

$$\forall \quad \exists \quad \nexists$$

```markdown
$\therefore \because \And$
```

$$\therefore \quad \because \quad \And$$

```markdown
$\lor \vee \curlyvee \bigvee$
```

$$\lor \quad \vee \quad \curlyvee \quad \bigvee$$

```markdown
$\land \wedge \curlywedge \bigwedge$
```

$$\land \quad \wedge \quad \curlywedge \quad \bigwedge$$

```markdown
$\bar{q} \bar{abc} \overline{q} \overline{abc}$
```

$$\bar{q} \quad \bar{abc} \quad \overline{q} \quad \overline{abc}$$

```markdown
$\lnot \neg \bot \top$
```

$$\lnot \quad \neg \quad \bot \quad \top$$

```markdown
$\vdash \dashv \vDash \Vdash \models$
```

$$\vdash \quad \dashv \quad \vDash \quad \Vdash \quad \models$$

```markdown
$\Vvdash \nvdash \nVdash \nvDash \nVDash$
```

$$\Vvdash \quad \nvdash \quad \nVdash \quad \nvDash \quad \nVDash$$

```markdown
$\ulcorner \urcorner \llcorner \lrcorner$
```

$$\ulcorner \quad \urcorner \quad \llcorner \quad \lrcorner$$

# 箭头

```markdown
$\Rrightarrow \Lleftarrow$
```

$$\Rrightarrow \quad \Lleftarrow$$

```markdown
$\Rightarrow \nRightarrow \Longrightarrow \implies$
```

$$\Rightarrow \quad \nRightarrow \quad \Longrightarrow \quad \implies$$

```markdown
$\Leftarrow \nLeftarrow \Longleftarrow$
```

$$\Leftarrow \quad \nLeftarrow \quad \Longleftarrow$$

```markdown
$\Leftrightarrow \nLeftrightarrow \Longleftrightarrow \iff$
```

$$\Leftrightarrow \quad \nLeftrightarrow \quad \Longleftrightarrow \quad \iff$$

```markdown
$\Uparrow \Downarrow \Updownarrow$
```

$$\Uparrow \quad \Downarrow \quad \Updownarrow$$

```markdown
$\leftarrow \rightarrow \nleftarrow \nrightarrow \leftrightarrow \nleftrightarrow \longleftarrow \longrightarrow \longleftrightarrow$
```

$$\leftarrow \quad \rightarrow \quad \nleftarrow \quad \nrightarrow \quad \leftrightarrow \quad \nleftrightarrow \quad \longleftarrow \quad \longrightarrow \quad \longleftrightarrow$$

```markdown
$\gets \to$
```

$$\gets \quad \to$$

```markdown
$\uparrow \downarrow \updownarrow \nearrow \searrow \nwarrow \swarrow$
```

$$\uparrow \quad \downarrow \quad \updownarrow \quad \nearrow \quad \searrow \quad \nwarrow \quad \swarrow$$

```markdown
$\mapsto \longmapsto$
```

$$\mapsto \quad \longmapsto$$

```markdown
$\rightharpoonup \rightharpoondown \leftharpoonup \leftharpoondown \upharpoonleft \upharpoonright \downharpoonleft \downharpoonright \leftrightharpoons \rightleftharpoons$
```

$$\rightharpoonup \quad \rightharpoondown \quad \leftharpoonup \quad \leftharpoondown \quad \upharpoonleft \quad \upharpoonright \quad \downharpoonleft \quad \downharpoonright \quad \leftrightharpoons \quad \rightleftharpoons$$

```markdown
$\curvearrowleft \circlearrowleft \Lsh \upuparrows \rightrightarrows \rightleftarrows \rightarrowtail \looparrowright$
```

$$\curvearrowleft \quad \circlearrowleft \quad \Lsh \quad \upuparrows \quad \rightrightarrows \quad \rightleftarrows \quad \rightarrowtail \quad \looparrowright$$

```markdown
$\curvearrowright \circlearrowright \Rsh \downdownarrows \leftleftarrows \leftrightarrows \leftarrowtail \looparrowleft$
```

$$\curvearrowright \quad \circlearrowright \quad \Rsh \quad \downdownarrows \quad \leftleftarrows \quad \leftrightarrows \quad \leftarrowtail \quad \looparrowleft$$

```markdown
$\hookrightarrow \hookleftarrow \multimap \leftrightsquigarrow \rightsquigarrow \twoheadrightarrow \twoheadleftarrow$
```

$$\hookrightarrow \quad \hookleftarrow \quad \multimap \quad \leftrightsquigarrow \quad \rightsquigarrow \quad \twoheadrightarrow \quad \twoheadleftarrow$$

```markdown
$\xleftarrow{left} \xrightarrow{right} \xLeftarrow{Left} \xRightarrow{Right} \xleftrightarrow{left\& right} \xLeftrightarrow{Left\& Right}$
```

$$\xleftarrow{left} \quad \xrightarrow{right} \quad \xLeftarrow{Left} \quad \xRightarrow{Right} \quad \xleftrightarrow{left\& right} \quad \xLeftrightarrow{Left\& Right}$$

# 特殊符号

```markdown
$\amalg \% \dagger \ddagger \ldots \cdots$
```

$$\amalg \quad \% \quad \dagger \quad \ddagger \quad \ldots \quad \cdots$$

```markdown
$\smile \frown \wr$
```

$$\smile \quad \frown \quad \wr$$

```markdown
$\diamondsuit \heartsuit \clubsuit \spadesuit \Game \flat \natural \sharp$
```

$$\diamondsuit \quad \heartsuit \quad \clubsuit \quad \spadesuit \quad \Game \quad \flat \quad \natural \quad \sharp$$

```markdown
$\diagup \diagdown \centerdot \ltimes \rtimes \leftthreetimes \rightthreetimes$
```

$$\diagup \quad \diagdown \quad \centerdot \quad \ltimes \quad \rtimes \quad \leftthreetimes \quad \rightthreetimes$$

```markdown
$\eqcirc \circeq \triangleq \bumpeq \Bumpeq \doteqdot \risingdotseq \fallingdotseq$
```

$$\eqcirc \quad \circeq \quad \triangleq \quad \bumpeq \quad \Bumpeq \quad \doteqdot \quad \risingdotseq \quad \fallingdotseq$$

```markdown
$\intercal \barwedge \veebar \doublebarwedge \between \pitchfork$
```

$$\intercal \quad \barwedge \quad \veebar \quad \doublebarwedge \quad \between \quad \pitchfork$$

```markdown
$\vartriangleleft \ntriangleleft \vartriangleright \ntriangleright$
```

$$\vartriangleleft \quad \ntriangleleft \quad \vartriangleright \quad \ntriangleright$$

```markdown
$\trianglelefteq \ntrianglelefteq \trianglerighteq \ntrianglerighteq$
```

$$\trianglelefteq \quad \ntrianglelefteq \quad \trianglerighteq \quad \ntrianglerighteq$$

```markdown
$\mathrm{\LaTeX}$
```

$$\mathrm{\LaTeX}$$ 

# 上标、下标及积分等

## 上标

```markdown
$a^2$
```

$$a^2$$

## 下标

```markdown
$a_2$
```

$$a_2$$

## 组合

```markdown
$a^{2+2} a_{i, j}$
```

$$a^{2+2} \quad a_{i, j}$$

## 结合上下标

```markdown
$a^2_2$
```

$$a^2_2$$

## 前置上下标

```markdown
${}^2_1\! X^3_4$
```

$${}^2_1\! X^3_4$$

## 导数

```markdown
$x' x^\prime x\prime$
```

$$x' \quad x^\prime \quad x\prime$$

## 导数点

```markdown
$\dot{x} \ddot{x}$
```

$$\dot{x} \quad \ddot{x}$$

## 向量

```markdown
$\vec{x} \overleftarrow{AB} \overrightarrow{AB} \widehat{AB}$
```

$$\vec{x} \quad \overleftarrow{AB} \quad \overrightarrow{AB} \quad \widehat{AB}$$

## 上弧

```markdown
$\overset{\frown}{AB}$
```

> 正确的语法应该是\overarc，但因为没有引入 amsmath 宏包，所以无法使用，只能用这个替代下。
$$\overset{\frown}{AB}$$

## 上划线

```markdown
$\overline{ABC}$
```

$$\overline{ABC}$$

## 下划线

```markdown
$\underline{ABC}$
```

$$\underline{ABC}$$

## 上括号

```markdown
$\overbrace{1+2+\cdots+100}$  

$\begin{matrix}5050\\\overbrace{1+2+\cdots+100}\end{matrix}$  
```

$$\overbrace{1+2+\cdots+100}$$

$$\begin{matrix}5050\\\overbrace{1+2+\cdots+100}\end{matrix}$$

## 下括号

```markdown
$\underbrace{1+2+\cdots+100}$

$\begin{matrix}\underbrace{1+2+\cdots+100}\\5050\end{matrix}$
```

$$\underbrace{1+2+\cdots+100}$$

$$\begin{matrix}\underbrace{1+2+\cdots+100}\\5050\end{matrix}$$

## 求和

```markdown
$\sum_{i=1}^na_i \sum\limits_{i=1}^na_i$
```

$$\sum_{i=1}^na_i \quad \sum\limits_{i=1}^na_i$$

## 求积

```markdown
$\prod_{i=1}^na_i \prod\limits_{i=1}^na_i$
```

$$\prod_{i=1}^na_i \quad \prod\limits_{i=1}^na_i$$

## 上积

```markdown
$\coprod_{i=1}^na_i \coprod\limits_{i=1}^na_i$
```

$$\coprod_{i=1}^na_i \quad \coprod\limits_{i=1}^na_i$$

## 极限

```markdown
$\lim_{n\to\infty}x_n \lim\limits_{n\to\infty}x_n$
```

$$\lim_{n\to\infty}x_n \quad \lim\limits_{n\to\infty}x_n$$

## 积分

```markdown
$\int_{-N}^{N}e^x\, dx$
```

$$\int_{-N}^{N}e^x\, dx$$

## 双重积分

```markdown
$\iint_M^Ndx\, dy$
```

$$\iint_M^Ndx\, dy$$

## 三重积分

```markdown
$\iiint_M^Ndx\, dy\, dz$
```

$$\iiint_M^Ndx\, dy\, dz$$

## 闭合的曲线、曲面积分

```markdown
$\oint_Cx^3\, dx+4 y^2\, dy$
```

$$\oint_Cx^3\, dx+4 y^2\, dy$$

## 交集

```markdown
$\bigcap_1^np \bigcap\limits_1^np$
```

$$\bigcap_1^np \quad \bigcap\limits_1^np$$

## 并集

```markdown
$\bigcup_1^np \bigcup\limits_1^np$
```

$$\bigcup_1^np \quad \bigcup\limits_1^np$$

# 分数、矩阵等

## 分数

```markdown
$\frac{1}{2}=0.5$
```

$$\frac{1}{2}=0.5$$

## 小型分数

```markdown
$\tfrac{1}{2}=0.5$
```

$$\tfrac{1}{2}=0.5$$

## 大型分数

```markdown
$\dfrac{1}{2}=0.5 \dfrac{1}{x+\dfrac{3}{y+\dfrac{1}{5}}}$
```

$$\dfrac{1}{2}=0.5 \quad \dfrac{1}{x+\dfrac{3}{y+\dfrac{1}{5}}}$$

## 二项式系数

```markdown
$\dbinom{n}{m}=\dbinom{n}{n-m}=C_n^m=C_n^{n-m}$
```

$$\dbinom{n}{m}=\dbinom{n}{n-m}=C_n^m=C_n^{n-m}$$

## 小型二项式系数

```markdown
$\tbinom{n}{m}=\tbinom{n}{n-m}=C_n^m=C_n^{n-m}$
```

$$\tbinom{n}{m}=\tbinom{n}{n-m}=C_n^m=C_n^{n-m}$$

```markdown
$\binom{n}{m}=\binom{n}{n-m}=C_n^m=C_n^{n-m}$
```

$$\binom{n}{m}=\binom{n}{n-m}=C_n^m=C_n^{n-m}$$

## 矩阵

```markdown
$\begin{matrix}a&b\\c&d\end{matrix}$
```

>  `&` 是使上下行对齐。

$$\begin{matrix}a&b\\c&d\end{matrix}$$

```markdown
$\begin{vmatrix}a&b\\c&d\end{vmatrix}$
```

$$\begin{vmatrix}a&b\\c&d\end{vmatrix}$$

```markdown
$\begin{Vmatrix}a&b\\c&d\end{Vmatrix}$
```

$$\begin{Vmatrix}a&b\\c&d\end{Vmatrix}$$

```markdown
$\begin{bmatrix}a&\cdots&b\\\vdots&\ddots&\vdots\\c&\cdots&d\end{bmatrix}$
```

> `\vdots` 是竖着 3 个点，`\ddots` 是斜着 3 个点。

$$\begin{bmatrix}a&\cdots&b\\\vdots&\ddots&\vdots\\c&\cdots&d\end{bmatrix}$$

```markdown
$\begin{Bmatrix}a&c\\b&d\end{Bmatrix}$
```

$$\begin{Bmatrix}a&c\\b&d\end{Bmatrix}$$

```markdown
$\begin{pmatrix}a&c\\b&d\end{pmatrix}$
```

$$\begin{pmatrix}a&c\\b&d\end{pmatrix}$$

#### 矩阵嵌套

```markdown
$\begin{vmatrix} \begin{Bmatrix}A & \\ c & d \end{Bmatrix} & x\\ \dfrac{1}{2} & \begin{matrix} 1 & 2 \\ 3 & 4 \end{matrix} \end{vmatrix}$ 
```

$$\begin{vmatrix} \begin{Bmatrix}A & \\ c & d \end{Bmatrix} & x\\ \dfrac{1}{2} & \begin{matrix} 1 & 2 \\ 3 & 4 \end{matrix} \end{vmatrix}$$

#### 条件定义 (如分段函数)

```markdown
$f (x)=\begin{cases}x-1&x\leqslant 3\\x^2+3 x-1&x>3\end{cases}$
```

$$f (x)=\begin{cases}x-1&x\leqslant 3\\x^2+3 x-1&x>3\end{cases}$$

#### 方程组

```markdown
$\begin{cases}2 x+9 y-5 z=10\\4 x+20 y+z=24\\x-\dfrac{1}{2}y+3 z=8\end{cases}$
```

$$\begin{cases}2 x+9 y-5 z=10\\4 x+20 y+z=24\\x-\dfrac{1}{2}y+3 z=8\end{cases}$$

#### 多行等式

```markdown
$\begin{aligned}f (x) & = (x + 1)^2 \\ & = x^2 + 2 x + 1\end{aligned}$

$\begin{aligned}a_1 & = 1 \\ a_2 & = 2 \\ & \dots \\ a_n & = n\end{aligned}$
```

> 原语法为 align，现在是 aligned。

$$\begin{aligned}f (x) & = (x + 1)^2 \\ & = x^2 + 2 x + 1\end{aligned}$$

$$\begin{aligned}a_1 & = 1 \\ a_2 & = 2 \\ & \dots \\ a_n & = n\end{aligned}$$

#### 数组/表格

```markdown
$\begin{array}{|c|c||c|}x&y&z\\8&2&4\\2&3&9\\10&\dfrac{3}{4}&\sqrt{3}\\a&b&c\end{array}$
```

$$\begin{array}{|c|c||c|}x&y&z\\8&2&4\\2&3&9\\10&\dfrac{3}{4}&\sqrt{3}\\a&b&c\end{array}$$

# 字体

## 希腊字母

> 部分希腊字母不支持，用英文字母代替。

```markdown
$A B\Gamma\Delta EZH\Theta$
```

$$A \quad B \quad \Gamma \quad \Delta \quad E \quad Z \quad H \quad \Theta$$

```markdown
$IK\Lambda MN\Xi O\Pi$
```

$$I \quad K \quad \Lambda \quad M \quad N \quad \Xi \quad O \quad \Pi$$

```markdown
$P\Sigma T\Upsilon\Phi X\Psi\Omega$
```

$$P \quad \Sigma \quad T \quad \Upsilon \quad \Phi \quad X \quad \Psi \quad \Omega$$

```markdown
$\alpha\beta\gamma\delta\eps ilon\zeta\eta\theta$
```

$$\alpha \quad \beta \quad \gamma \quad \delta \quad \epsilon \quad \zeta \quad \eta \quad \theta$$

```markdown
$\iota\kappa\lambda\mu\nu\xi\omicron\pi$
```

$$\iota \quad \kappa \quad \lambda \quad \mu \quad \nu \quad \xi \quad \omicron \quad \pi$$

```markdown
$\rho\sigma\tau\upsilon\phi\chi\psi\omega$
```

$$\rho \quad \sigma \quad \tau \quad \upsilon \quad \phi \quad \chi \quad \psi \quad \omega$$

```markdown
$\varepsilon\digamma\varkappa\varpi$
```

$$\varepsilon \quad \digamma \quad \varkappa \quad \varpi$$

```markdown
$\varrho\varsigma\vartheta\varphi$
```

$$\varrho \quad \varsigma \quad \vartheta \quad \varphi$$

## 希伯来符号

```markdown
$\aleph\beth\gimel\daleth$
```

$$\aleph \quad \beth \quad \gimel \quad \daleth$$

## 黑板粗体

```markdown
$\mathbb{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$
```

> 仅支持大写英文字母。

$$\mathbb{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$$

## 粗体

```markdown
$\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$
$\mathbf{abcdefghijklmnopqrstuvwxyz}$
$\mathbf{0123456789}$
```

> 支持大小写英文字母、数字和大写希腊字母。

$$\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$$

$$\mathbf{abcdefghijklmnopqrstuvwxyz}$$

$$\mathbf{0123456789}$$

## 斜体 (英文字母和小写希腊字母默认)

```markdown
$\mathit{A B\Gamma\Delta EZH\Theta}$
$\mathit{IK\Lambda MN\Xi O\Pi}$
$\mathit{P\Sigma T\Upsilon\Phi X\Psi\Omega}$
$\mathit{0123456789}$
```

$$\mathit{A B\Gamma\Delta EZH\Theta}$$

$$\mathit{IK\Lambda MN\Xi O\Pi}$$

$$\mathit{P\Sigma T\Upsilon\Phi X\Psi\Omega}$$

$$\mathit{0123456789}$$

## 罗马体

```markdown
$\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$  
$\mathrm{abcdefghijklmnopqrstuvwxyz}$  
$\mathrm{0123456789}$
```

> 支持大小写英文字母和数字。

$$\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$$

$$\mathrm{abcdefghijklmnopqrstuvwxyz}$$

$$\mathrm{0123456789}$$

## 打字机字体

```markdown
$\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$
$\mathtt{abcdefghijklmnopqrstuvwxyz}$
$\mathtt{A B\Gamma\Delta EZH\Theta}$
$\mathtt{IK\Lambda MN\Xi O\Pi}$
$\mathtt{P\Sigma T\Upsilon\Phi X\Psi\Omega}$
$\mathtt{0123456789}$
```

> 支持大小写英文字母、大写希腊字母和数字。

$$\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$$

$$\mathtt{abcdefghijklmnopqrstuvwxyz}$$

$$\mathtt{A B\Gamma\Delta EZH\Theta}$$

$$\mathtt{IK\Lambda MN\Xi O\Pi}$$

$$\mathtt{P\Sigma T\Upsilon\Phi X\Psi\Omega}$$

$$\mathtt{0123456789}$$

## 无衬线体

```markdown
$\mathsf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$  
$\mathsf{abcdefghijklmnopqrstuvwxyz}$  
$\mathsf{A B\Gamma\Delta EZH\Theta}$  
$\mathsf{IK\Lambda MN\Xi O\Pi}$  
$\mathsf{P\Sigma T\Upsilon\Phi X\Psi\Omega}$  
$\mathsf{0123456789}$
```

> 支持大小写英文字母、大写希腊字母和数字。

$$\mathsf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$$

$$\mathsf{abcdefghijklmnopqrstuvwxyz}$$

$$\mathsf{A B\Gamma\Delta EZH\Theta}$$

$$\mathsf{IK\Lambda MN\Xi O\Pi}$$

$$\mathsf{P\Sigma T\Upsilon\Phi X\Psi\Omega}$$

$$\mathsf{0123456789}$$

## 手写体/花体

```markdown
$\mathcal{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$  
$\mathcal{0123456789}$
```

> 支持大写英文字母和数字。

$$\mathcal{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$$

$$\mathcal{0123456789}$$

## $\mathfrak{Fraktur}$ 体

```markdown
$\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$  
$\mathfrak{abcdefghijklmnopqrstuvwxyz}$  
$\mathfrak{0123456789}$
```

> 支持大小写英文字母和数字。

$$\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$$

$$\mathfrak{abcdefghijklmnopqrstuvwxyz}$$

$$\mathfrak{0123456789}$$

## 小型非斜体字

```markdown
$\scriptstyle\text{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$  
$\scriptstyle\text{abcdefghijklmnopqrstuvwxyz}$  
$\scriptstyle\text{0123456789}$
```

> 支持大小写英文字母和数字，`\text` 见下一栏。

$$\scriptstyle\text{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$$

$$\scriptstyle\text{abcdefghijklmnopqrstuvwxyz}$$

$$\scriptstyle\text{0123456789}$$

## 混合字体

### 斜体字符

```markdown
$xyz$
```

$$xyz$$

### 非斜体字符

```markdown
$\text{x y z} \text{中文}$
```

> 不会忽略空格，支持大小写英文字母和数字，以及中文。

$$\text{x y z} \text{中文}$$

### 混合斜体与非斜体

```markdown
$\text{if }n\text{ is even}$
```

> 注意在 `\text` 中使用空格来显得更好看，或者可以用强制空格代替。

$$\text{if }n\text{ is even}$$

# 括号

## 普通括号

```markdown
$(\dfrac{1}{2}) (\dfrac{1}{x+\dfrac{2}{3}})$
```

> 对于较大的式子显得比较难看。

$$(\dfrac{1}{2}) (\dfrac{1}{x+\dfrac{2}{3}})$$

## 根据式子大小匹配的括号

```markdown
$\left (\dfrac{1}{2}\right) \left (\dfrac{1}{x+\dfrac{2}{3}}\right)$
```

$$\left (\dfrac{1}{2}\right) \left (\dfrac{1}{x+\dfrac{2}{3}}\right)$$

> 此功能使用 `\left` 和 `\right` 可以推广到不同的括号。

## 圆括号/小括号

```markdown
$\left (\dfrac{1}{2}\right)$
```

$$\left (\dfrac{1}{2}\right)$$

## 方括号/中括号

```markdown
$\left[\dfrac{1}{2}\right]$
```

$$\left[\dfrac{1}{2}\right]$$

## 花括号/大括号

```markdown
$\left\{\dfrac{1}{2}\right\}$
```

$$\left\{\dfrac{1}{2}\right\}$$

## 角括号

```markdown
$\left\langle\dfrac{1}{2}\right\rangle$
```

> `\langle` 可以用<，`\rangle` 可以用>。

$$\left\langle\dfrac{1}{2}\right\rangle$$

## 单竖线/绝对值

```markdown
$\left|\dfrac{1}{2}\right|$
```

$$\left|\dfrac{1}{2}\right|$$

## 双竖线

```markdown
$\left\|\dfrac{1}{2}\right\|$
```

$$\left\|\dfrac{1}{2}\right\|$$

## 向下取整

```markdown
$\left\lfloor\dfrac{1}{2}\right\rfloor$
```

$$\left\lfloor\dfrac{1}{2}\right\rfloor$$

## 向上取整

```markdown
$\left\lceil\dfrac{1}{2}\right\rceil$
```

$$\left\lceil\dfrac{1}{2}\right\rceil$$

## 斜线

```markdown
$\left/\dfrac{1}{2}\right/$
```

$$\left/\dfrac{1}{2}\right/$$

## 反斜线

```markdown
$\left\backslash\dfrac{1}{2}\right\backslash$
```

$$\left\backslash\dfrac{1}{2}\right\backslash$$

## 上下箭头

```markdown
$\left\uparrow\dfrac{1}{2}\right\uparrow$
```

$$\left\uparrow\dfrac{1}{2}\right\uparrow$$

```markdown
$\left\Downarrow\dfrac{1}{2}\right\Downarrow$
```

$$\left\Downarrow\dfrac{1}{2}\right\Downarrow$$

```markdown
$\left\updownarrow\dfrac{1}{2}\right\updownarrow$
```

$$\left\updownarrow\dfrac{1}{2}\right\updownarrow$$

因为上下箭头太多了，这里就不一一示范了。

## 混合括号

其实上述括号都可以混合使用，这里就随便列两个了。

```markdown
$\left<\dfrac{1}{2}\right/$
```

$$\left<\dfrac{1}{2}\right/$$

```markdown
$\left (\dfrac{1}{2}, 1\right]$
```

$$\left (\dfrac{1}{2}, 1\right]$$

## 单左括号

上述括号都适用，这里就随便列一个。

```markdown
$\left (\dfrac{1}{2}\right.$
```

$$\left (\dfrac{1}{2}\right.$$

## 单右括号

同上。

```markdown
$\left.\dfrac{1}{2}\right]$
```

$$\left.\dfrac{1}{2}\right]$$

## 强制括号大小

```markdown
$\Bigg (\bigg[\Big\{\big<x\big>\Big\}\bigg]\Bigg)$
```

> 即使用 `\Bigg`、`\bigg`、`\Big`、`\big` 来控制括号大小。

$$\Bigg (\bigg[\Big\{\big<x\big>\Big\}\bigg]\Bigg)$$

# 空格

一般 $\mathrm{\LaTeX}$ 能自动处理大多数空格，但必要时候需要强制控制大小。

## 紧贴

```markdown
$x\! y$
```

$$x\! y$$

宽度为 $-\frac{m}{6}$。 ​

## 无空格

```markdown
$xy$
```

$$xy$$

宽度为 $0$。

## 小空格

```markdown
$x\, y$
```

$$x\, y$$

宽度为 $\frac{m}{6}$。

## 中等空格

```markdown
$x\; y$
```

$$x\; y$$

宽度为 $\frac{2 m}{7}$。

## 大空格

```markdown
$x\ y$
```

$$x\ y$$

宽度为 $\frac{m}{3}$。

## $quad$ 空格

```markdown
$x\quad y$
```

$$x\quad y$$

宽度为 $m$。

## 两个 $quad$ 空格

```markdown
$x\qquad y$
```

$$x\qquad y$$

宽度为 $2 m$。

# 颜色

字体颜色：`${\color{色调}表达式}$ `
背景颜色：`${\color{文字色调}\colorbox{背景色调}{表达式 (可以打中文)}}$`

$${\color{Aquamarine}Aquamarine}$$

$${\color{Black}Black}$$

$${\color{Blue}Blue}$$

$${\color{BlueViolet}BlueViolet}$$

$${\color{Brown}Brown}$$

$${\color{CadetBlue}CadetBlue}$$

$${\color{CornflowerBlue}CornflowerBlue}$$

$${\color{Cyan}Cyan}$$

$${\color{DarkOrchid}DarkOrchid}$$

$${\color{ForestGreen}ForestGreen}$$

$${\color{Fuchsia}Fuchsia}$$

$${\color{Goldenrod}Goldenrod}$$

$${\color{Gold}Gold}$$

$${\color{Gray}Gray}$$

$${\color{CadetBlue}CadetBlue}$$

$${\color{Green}Green}$$

$${\color{GreenYellow}GreenYellow}$$

$${\color{Lavender}Lavender}$$

$${\color{LimeGreen}LimeGreen}$$

$${\color{Magenta}Magenta}$$

$${\color{Maroon}Maroon}$$

$${\color{Orange}Orange}$$

$${\color{OrangeRed}OrangeRed}$$

$${\color{Orchid}Orchid}$$

$${\color{Plum}Plum}$$

$${\color{Purple}Purple}$$

$${\color{Red}Red}$$

$${\color{RoyalBlue}RoyalBlue}$$

$${\color{Salmon}Salmon}$$

$${\color{SeaGreen}SeaGreen}$$

$${\color{SkyBlue}SkyBlue}$$

$${\color{SpringGreen}SpringGreen}$$

$${\color{Tan}Tan}$$

$${\color{Thistle}Thistle}$$

$${\color{Turquoise}Turquoise}$$

$${\color{Violet}Violet}$$

$${\color{White}White}$$

> 上方是白色的字

$${\color{Yellow}Yellow}$$

$${\color{YellowGreen}YellowGreen}$$

随便举个例子：

```markdown
$x=\dfrac{-b\pm\sqrt{\color{Red}b^2-4 ac}}{\color{Blue}2 a}$
```

$$x=\dfrac{-b\pm\sqrt{\color{Red}b^2-4 ac}}{\color{Blue}2 a}$$

```markdown
$\color{Blue}\colorbox{Yellow}{LaTeX 公式大全}$
```

$$\color{Blue}\colorbox{Yellow}{LaTeX 公式大全}$$

# 把数学公式框起来

```markdown
$$\boxed{\sum\limits_{i = 1}^{n} i = \dfrac{n (n - 1)}{2}}$$
```

$$\boxed{\sum\limits_{i = 1}^{n} i = \dfrac{n (n - 1)}{2}}$$

# 参考

[LaTeX 数学公式大全 - Iowa_BattleShip](https://www.luogu.com.cn/blog/IowaBattleship/latex-gong-shi-tai-quan)
[在线LaTeX公式编辑器](https://www.latexlive.com/)