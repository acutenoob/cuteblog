---
title: 欧拉函数
date: 2026-03-12 10:47:30
tags: [模板, unsolve, 数论]
---

> 欧拉函数（Euler's totient function），即 $\varphi(n)$，表示的是小于等于 $n$ 且与 $n$ 互质的数的个数。

# 实现

## 在线

```cpp
int euler(int n)
{
    int res = n;
    for(int i = 2; i * i <= n; i++)
    {
        if(n % i == 0)
        {
            res = res / i * (i - 1);
            while(n % i == 0)
                n /= i;
        }
    }
    if(n > 1)
        res = res / n * (n - 1);
    return res;
}
```

## 离线

```cpp
const int mxi = 50000;
int phi[mxi + 1];
bool np[mxi + 1];
vector<int> pm;
void init()
{
    for(int i = 2;i <= mxi;i++)
    {
        if(!np)
            pm.push(i),phi[i] = i - 1;
        for(int j = 0;j < np.size() && i * np[j] <= mxi;j++)
        {
            if(i % pm[j] == 0)
            {
                phi[i * pm[j]] = phi[i] * pm[j];
                break;
            }
            phi[i * pm[j]] = phi[i] * (pm[j] - 1);
        }
    }
}
```

# 原理

> 前方的道路，以后再来探索吧 未来的我会告诉我的

26/3/12 刚刚买了《初等数论》书的 acutenoob

26/3/31  
设 $n = p_1^{\alpha_1} \dots p_m^{\alpha_m}$，则  
$$
\varphi(n) = (p_1 - 1)p_1^{\alpha_1 - 1} \dots (p_m - 1)p_m^{\alpha_m - 1}
 $$

设 p 是质数 且 $k \ge 1 $ 则 
$$\varphi(p^k) = p^{k - 1}(p - 1)$$
并且模 p 的既约同余类是 $(a + bp) \mod p^k,0 \le a \le p - 1,0 \le b \le p^{k - 1} - 1$  
    
**证明** 
$$(r,p) = \left\{
\begin{aligned}
1, p \nmid r \\
p, p \mid r
\end{aligned}
\right.
$$
$(r,p^k) = 1$ 的充要条件是 $ (r,p) = 1 $ 所以 $\varphi(x) $ 等于 $1,2,\dots ,p ^ k$ 中不能被 p 整除的数个数 显然 这些数个数为 $p ^ {k - 1},\ (p,2p,3p...p^{k - 1}p) $ 所以 $\varphi(x) = p^k - p^{k - 1}$ 及证

# 性质

## 定理1
设 $m = m_1m_2$

(i)若 m 和 $ m_1$有共同的素因数 则
    $$\begin{equation}\varphi(m) = m_2\varphi(m_1) \end{equation}$$ 
当 m > 1 时
    $$\begin{equation} m = p_1^{\alpha_1}p_2^{\alpha_2}\dots p_r^{\alpha_r} \end{equation}$$
则
    $$\begin{equation}m = p_1^{\alpha_1 - 1}p_2^{\alpha_2 - 1}\dots p_r^{\alpha_r - 1}\varphi(p_1p_2\dots p_ r)\end{equation}$$
(ii) 若 $(m_1,m_2) = 0$
则
    $$\begin{equation}\varphi(m) = \varphi(m_1)\varphi(m_2)\end{equation}$$ 

特别地 若 m 由 (2) 给出 有
    $$\begin{equation}\varphi(m) = (p_1 - 1)p_1^{\alpha_1 - 1} \dots (p_r - 1)p_r^{\alpha_r - 1}(5)\end{equation}$$


**证明**

由 完全剩余系的一个性质可知 $m_1$ 与 m 有相同的素因数时 
    $$ x = x^{(1)} + m_2x^{(2)} $$
$ x^{(1)} $遍历 $m_1$ 的既约剩余系 $ x^{(2)} $遍历 $m_2$ 的完全剩余系 则 x 遍历 m 的完全剩余系 $x^{(1)}$ 的 既约剩余系 有 $\varphi(m_1) $个元素  $x^{(2)}$  的完全剩余系 有 $m_2$ 个元素 及证（1） 由 (1) 可推得(3)

设 $m = m_1m_2,(m_1,m_2) = 1$
$$ x = m_2x^{(1)} + m_1x^{(2)} $$
则 x 遍历 m 的完全(既约)剩余系的充要条件是 $ x^{(1)} , x^{(2)} $ 分别遍历 $m_1,m_2$的完全(既约)剩余系  推得 (4)

由(3) (4) 知 $\varphi(p_1p_2\dots p_ r) = \varphi(p_1)\varphi(p_2\dots p_ r) = (p_1 - 1)\varphi(p_2\dots p_ r) $ 可知 (5)

## 定理2 费马小定理

设 (a,m) = 1
$$a^{\varphi(m)}\equiv 1 \pmod m$$
特别地 p 为质数时
$$a ^ p \equiv p \pmod m$$

**证明**

设 $r_1,\dots r_{\varphi(a)} $ 为 a 的一组既约同余系有 则 $ar_1,\dots ar_{\varphi(a)}$ 也是 a的一组既约同余系

有 
$$\prod_{j = 1}^{\varphi(m)}r_j \equiv \prod_{j = 1}^{\varphi(m)}(ar_j) = a^{\varphi(m)}\prod_{j = 1}^{\varphi(m)}r_j \pmod m$$
当 (c,m) = 1 时 $ca \equiv cb \pmod m $ 可知 $a \equiv b \pmod m$
由定义知 $(r_j,m) = 1 (1 \le j \le \varphi(m)$
及证

**推论** 
$$a ^ {\varphi(m) - 1} \equiv a^{-1} \pmod m$$

$$
a^k \equiv \begin{cases}
a^{k \bmod \varphi(m)},                &\gcd(a,m) =  1,                   \\
a^k,                                   &\gcd(a,m)\ne 1, k <   \varphi(m), \\
a^{(k \bmod \varphi(m)) + \varphi(m)}, &\gcd(a,m)\ne 1, k \ge \varphi(m).
\end{cases} \pmod m
$$
引用自oiwiki https://github.com/OI-wiki/OI-wiki/blob/master/docs/math/number-theory/fermat.md
## 定理3
对于任意 m

$$\sum_{d \mid m}\varphi(d) = m$$

**证明**

由算术基本定理得

$$\sum_{d \mid m}\varphi(d) = \sum_{e_1}^{\alpha_1}\dots\sum_{e_r}^{\alpha_r}\varphi(p_1^{e_1}\dots p_r^{e_r})$$
利用(4)得到 
$$\sum_{d \mid m}\varphi(d) = \sum_{e_1}^{\alpha_1}\dots\sum_{e_r}^{\alpha_r}\varphi(p_1^{e_1})\dots \varphi(p_r^{e_r})$$
$$\sum_{d \mid m}\varphi(d) = \left( \sum_{e_1}^{\alpha_1}\varphi(p_1^{e_1}\right)\dots  \left(\sum_{e_r}^{\alpha_r}\varphi(p_r^{e_r})\right)$$
$$ 1 + (p - 1) + (p^2 - p) + \dots + (p^k - p^{k - 1}) = p^k $$

及证

## 个人原型

### 在线
```cpp
int euler(int n)
{
    int res = n;
    for(int i = 2;i * i <= n;i++)
    {
        if(n % i != 0)
            continue;
        res = res / i * (i - 1); 
        while(n % i == 0)
            n /= i;
    }
    if(n > 1)
        res = res / n * (n - 1);
    return res;
}
```

### 离线

```cpp
const int mxn = 100000;
vector<bool> np(mxn + 1);
vector<int> pm;
vector<int> phi(mxn + 1);

void init()
{
    for(int i = 2; i <= mxn; i++)
    {
        if(!np[i])
            pm.push_back(i), phi[i] = i - 1;
        for(int j = 0; j < pm.size() && 1ll * i * pm[j] <= mxn; j++)
        {
            np[i * pm[j]] = 1;
            if(i % pm[j] == 0)
            {
                phi[i * pm[j]] = phi[i] * pm[j]; // 此时能被整除，乘 pm[j]
                break;
            }
            phi[i * pm[j]] = phi[i] * (pm[j] - 1); // 此时 i 不能被 pm[j] 整除，乘 pm[j] - 1
        }
    }
}
```
# 小知识 RSA 加密

设 n = pq ,其中 p,q 是一对很大的质数

设 $\alpha \beta \equiv 1 \pmod {\varphi(n)}$

令 $B \equiv A^\alpha \pmod n$

对于任意整数 k 有 
$$ k^{\alpha \beta} \equiv k \pmod n$$

那么我们可以发送 B 

利用 $ B^\beta \equiv A^{\alpha \beta } \equiv A  \pmod n$ 及可解密 