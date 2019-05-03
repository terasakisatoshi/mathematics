# ラグランジュ未定係数法

2 変数函数 $$f=f(x,y)=x^2-y^2$$ の $$g=g(x,y)=x^2+y^2=0$$ 条件下での条件付き極値を考える. これは $$\lambda$$ をパラメータ, $$g$$ を函数とみなしたときのラグランジュ函数

$$
\begin{align}
L=L(x,y;\lambda)
&= f(x,y)+\lambda g(x,y) \\
&= x^2+y^2+\lambda(x^2-y^2)

\end{align}
$$

の極値問題を解くことに相当する:

$$
\frac{\partial L}{\partial x}
=
\frac{\partial L}{\partial y}
=
\frac{\partial L}{\partial \lambda}
=
0
$$

$$
\begin{align}
\frac{\partial L}{\partial x}
&= 2x+2\lambda x = 2x(1+\lambda) = 0,\\
\frac{\partial L}{\partial y}
&=
2y-2\lambda y =2y(1-\lambda) = 0
\end{align}
$$

これを解くと, $$\lambda=1$$ の場合, $$(x,y)=(\pm 1,0)$$ で極大値を, $$\lambda=-1$$ の場合, $$(x,y)=(0,\pm 1)$$ で極小値をとる. 

ラグランジュ未定係数法の心は
[この記事がとても参考になります](http://www.yunabe.jp/docs/lagrange_multiplier.html)

[See](https://gist.github.com/terasakisatoshi/1efa34e74be83ee73c7ca5c9cc381c3a)

<script src="https://gist.github.com/terasakisatoshi/1efa34e74be83ee73c7ca5c9cc381c3a.js"></script>
