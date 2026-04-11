---
title: 最大公因数 gcd
date: 2026-03-04 20:01:18
tags: [模板,数论]
---

# 实现

```cpp
long long _gcd(long long a,long long b)
{
    if(b == 0) return a;
    return _gcd(b,a%b);
}
```

# 原理

$gcd(a,b) = gcd(b,a\%b)$
