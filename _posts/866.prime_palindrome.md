[To Index](/index.md)
---
# 866.回文素数

>求出大于或等于 N 的最小回文素数。
回顾一下，如果一个数大于 1，且其因数只有 1 和它自身，那么这个数是素数。
例如，2，3，5，7，11 以及 13 是素数。
回顾一下，如果一个数从左往右读与从右往左读是一样的，那么这个数是回文数。
例如，12321 是回文数。

方法，先定义两个函数，一个求回文，一个判断素数。
难点在于超时问题，当n大于11，且n的位数为偶数时，n不可能为回文素数，因此为了缩减时间，将偶数位回文数加一个数量级。

```
class Solution {
public:
    int primePalindrome(int N) {
        if(N<=2)
            return 2;
        if(N%2 ==0 )
            N++;
        while(true)
        {
            if(N > 11 && (int)log10(N)%2)
                N = pow(10,(int)log10(N)+1)+1;
            if(reverse(N) == N &&  palin(N) )
                return N;
            N +=2;
        }
        return -1;

    }
private:
    int reverse(int n)
    {
        int tmp=0;
        while(n)
        {
            tmp = 10*tmp + n%10;
            n /=10;
        }
        return tmp;
    }
    int palin(int n)
    {
        int tmp=sqrt(n);
        for (int i=2; i<=tmp;i++)
            if(n%i==0)
                return 0;
        return 1;
    }
};
```
