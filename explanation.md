# Explanation 

`src =` https://www.hassamali.com/posts/understanding-n--n---1 

## How It Works
Let’s break down the process:

- When you subtract 1 from a number (n - 1), all bits after the rightmost 1 are inverted, and that rightmost 1 becomes 0
- When you AND (&) this result with the original number, it effectively removes that rightmost 1 For example, let’s take the number 52:

```
n     = 52 = 110100
n - 1 = 51 = 110011
n & (n-1)  = 110000 = 48
```

`src =` https://stackoverflow.com/questions/4678333/n-n-1-what-does-this-expression-do 

It's figuring out if n is either zero or an exact power of two. 
It works because a power of two is represented in binary as 1000...000, a one-bit followed by zero or more zero-bits. 
If you subtract one from that, you'll end up with a binary representation 111...111 (as many one-bits as there were trailing zero-bits in the original).
Then, when you AND those together, you get zero, such as with:
```
  1000 0000 0000 0000
&  111 1111 1111 1111
  ==== ==== ==== ====
= 0000 0000 0000 0000
```
Any non-power-of-two input value (other than zero) will not give you zero when you perform that operation.
For example, let's try all the 4-bit combinations:
```
     <----- binary ---->
 n      n    n-1   n&(n-1)
--   ----   ----   -------
 0   0000   1111    0000 *
 1   0001   0000    0000 *
 2   0010   0001    0000 *
 3   0011   0010    0010
 4   0100   0011    0000 *
 5   0101   0100    0100
 6   0110   0101    0100
 7   0111   0110    0110
 8   1000   0111    0000 *
 9   1001   1000    1000
10   1010   1001    1000
11   1011   1010    1010
12   1100   1011    1000
13   1101   1100    1100
14   1110   1101    1100
15   1111   1110    1110
```

You can see that only 0 and the powers of two (1, 2, 4 and 8) result in a 0000 bit pattern, all others are non-zero (zero and non-zero are treated in C as false and true respectively when evaluated in a conditional manner).
