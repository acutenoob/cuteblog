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

# 原理

> 前方的道路，以后再来探索吧 —— 未来的我会告诉我的

26/3/12  刚刚买了《初等数论》书的 acutenoob

26/3/31  
设 $n = p_1^{\alpha_1} \dots p_m^{\alpha_m}$，则  
$$
\varphi(n) = (p_1 - 1)p_1^{\alpha_1 - 1} \dots (p_m - 1)p_m^{\alpha_m - 1}
$$

设 $p$ 是质数且 $k \ge 1$，则  
$$\varphi(p^k) = p^{k - 1}(p - 1)$$
并且模 $p^k$ 的既约剩余系可以表示为  
$$(a + bp) \bmod p^k,\quad 1 \le a \le p - 1,\; 0 \le b \le p^{k - 1} - 1$$
  
**证明**  
$$
(r,p) = \left\{
\begin{aligned}
1, &\quad p \nmid r \\
p, &\quad p \mid r
\end{aligned}
\right.
$$
$(r,p^k) = 1$ 的充要条件是 $(r,p) = 1$，所以 $\varphi(p^k)$ 等于 $1,2,\dots ,p^k$ 中不能被 $p$ 整除的数的个数。显然，这些数共有 $p^k - p^{k-1}$ 个，因为能被 $p$ 整除的数为 $p,2p,3p,\dots,p^{k-1}p$，共 $p^{k-1}$ 个。因此 $\varphi(p^k) = p^k - p^{k-1}$。证毕。

# 性质

## 定理1

设 $m = m_1 m_2$。

(i) 若 $m_2$ 的每个素因数都是 $m_1$ 的素因数（即 $m_1$ 与 $m$ 有相同的素因子集合），则  
$$ \begin{equation}\varphi(m) = m_2 \varphi(m_1) \end{equation} $$

当 $m > 1$ 时，设  
$$\begin{equation} m = p_1^{\alpha_1} p_2^{\alpha_2} \dots p_r^{\alpha_r} \end{equation}$$
则有  
$$\begin{equation} m = p_1^{\alpha_1 - 1} p_2^{\alpha_2 - 1} \dots p_r^{\alpha_r - 1} \varphi(p_1 p_2 \dots p_r) \end{equation}$$

(ii) 若 $(m_1, m_2) = 1$，则  
$$\begin{equation}\varphi(m) = \varphi(m_1) \varphi(m_2) \end{equation}$$

特别地，若 $m$ 由 (2) 给出，有  
$$\begin{equation}\varphi(m) = (p_1 - 1)p_1^{\alpha_1 - 1} \dots (p_r - 1)p_r^{\alpha_r - 1} \qquad (5) \end{equation}$$

**证明**  

由完全剩余系的一个性质可知，当 $m_1$ 与 $m$ 有相同的素因数时，令  
$$ x = x^{(1)} + m_2 x^{(2)} $$
其中 $x^{(1)}$ 遍历 $m_1$ 的既约剩余系（共 $\varphi(m_1)$ 个元素），$x^{(2)}$ 遍历 $m_2$ 的完全剩余系（共 $m_2$ 个元素），则 $x$ 遍历 $m$ 的完全剩余系。由此即证 (1)。由 (1) 可推出 (3)。

设 $m = m_1 m_2$，$(m_1, m_2) = 1$，取  
$$ x = m_2 x^{(1)} + m_1 x^{(2)} $$
则 $x$ 遍历 $m$ 的完全（既约）剩余系的充要条件是 $x^{(1)}$、$x^{(2)}$ 分别遍历 $m_1$、$m_2$ 的完全（既约）剩余系，由此得 (4)。

由 (3) 和 (4) 知  
$$ \varphi(p_1 p_2 \dots p_r) = \varphi(p_1) \varphi(p_2 \dots p_r) = (p_1 - 1) \varphi(p_2 \dots p_r) $$
反复应用可得 (5)。

## 定理2（费马小定理）

设 $(a, m) = 1$，则  
$$ a^{\varphi(m)} \equiv 1 \pmod m $$
特别地，当 $p$ 为质数时，  
$$ a^p \equiv a \pmod p $$

**证明**  

设 $r_1, r_2, \dots, r_{\varphi(m)}$ 是模 $m$ 的一组既约剩余系，则 $a r_1, a r_2, \dots, a r_{\varphi(m)}$ 也是模 $m$ 的一组既约剩余系。于是  
$$ \prod_{j=1}^{\varphi(m)} r_j \equiv \prod_{j=1}^{\varphi(m)} (a r_j) = a^{\varphi(m)} \prod_{j=1}^{\varphi(m)} r_j \pmod m $$
由于 $(r_j, m) = 1$，且当 $(c, m)=1$ 时由 $ca \equiv cb \pmod m$ 可推出 $a \equiv b \pmod m$，因此可消去 $\prod r_j$，得 $a^{\varphi(m)} \equiv 1 \pmod m$。证毕。

**推论**  
$$ a^{\varphi(m)-1} \equiv a^{-1} \pmod m $$

模幂简化公式（引用自 OI-wiki）：  
$$ a^k \equiv \begin{cases}
a^{k \bmod \varphi(m)},                &\gcd(a,m) = 1, \\[4pt]
a^k,                                   &\gcd(a,m) \ne 1,\; k < \varphi(m), \\[4pt]
a^{(k \bmod \varphi(m)) + \varphi(m)}, &\gcd(a,m) \ne 1,\; k \ge \varphi(m).
\end{cases} \pmod m $$

## 定理3

对于任意正整数 $m$，有  
$$ \sum_{d \mid m} \varphi(d) = m $$

**证明**  

由算术基本定理，设 $m = p_1^{\alpha_1} \dots p_r^{\alpha_r}$，则  
$$ \sum_{d \mid m} \varphi(d) = \sum_{e_1=0}^{\alpha_1} \dots \sum_{e_r=0}^{\alpha_r} \varphi(p_1^{e_1} \dots p_r^{e_r}) $$
利用定理1中的积性 (4) 得  
$$ \sum_{d \mid m} \varphi(d) = \sum_{e_1=0}^{\alpha_1} \dots \sum_{e_r=0}^{\alpha_r} \varphi(p_1^{e_1}) \dots \varphi(p_r^{e_r}) = \left( \sum_{e_1=0}^{\alpha_1} \varphi(p_1^{e_1}) \right) \dots \left( \sum_{e_r=0}^{\alpha_r} \varphi(p_r^{e_r}) \right) $$
而  
$$ \sum_{e=0}^{k} \varphi(p^e) = 1 + (p-1) + (p^2 - p) + \dots + (p^k - p^{k-1}) = p^k $$
因此原式等于 $p_1^{\alpha_1} \dots p_r^{\alpha_r} = m$。证毕。


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