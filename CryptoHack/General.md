# CryptoHack  
## General  
## Encoding  
### ASCII  


In this challenge we need a conversion to get the flag. It can be done using the bellow code:  

```
L=[99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
A=""
for i in range (len(L)):
	A = A + chr(L[i])
print(A)
```
This will give us the flag:  
```crypto{ASCII_pr1nt4bl3}```


### Base64

Here we have a hex encoded string, We need to decode it into bytes and then encode it into Base64.
```
import base64
base64.b64encode(bytes.fromhex("72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf"))
```

The above code will give our flag:  
`crypto/Base+64+Encoding+is+Web+Safe/"`

### Bytes and Big Integers  

Here we need to convert the integer back to bytes to read the message. 
**We got a clue like:  
Python's PyCryptodome library implements this with the methods ```Crypto.Util.number.bytes_to_long``` and ```Crypto.Util.number.long_to_bytes```**  

```
from crypto.Util.number import long_to_bytes
print(long_to_bytes(11515195063862318899931685488813747395775516287289682636499965282714637259206269))
```

This code will give us the flag:  
```crypto{3nc0d1n6_4ll_7h3_w4y_d0wn}```

### Bytes and Big Integers  

Here we need to convert the integer back to bytes to read the message. 
**We got a clue like:  
Python's PyCryptodome library implements this with the methods ```Crypto.Util.number.bytes_to_long``` and ```Crypto.Util.number.long_to_bytes```**  

```
from crypto.Util.number import long_to_bytes
print(long_to_bytes(11515195063862318899931685488813747395775516287289682636499965282714637259206269))
```

This code will give us the flag:  
```crypto{3nc0d1n6_4ll_7h3_w4y_d0wn}```

### Hex  

Here we were given a string encoded in Hexadecimal. We need to convert it back to Bytes to get the flags.  

```
str="63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d"
arr = bytearray.fromhex(str)
print(arr)
```

This will give us the flag:  
```crypto{You_will_be_working_with_hex_strings_a_lot}```

## Mathematics
### Extended GCD

Using the two primes `p = 26513, q = 32321`, find the integers u,v such that

`p * u + q * v = gcd(p,q)`


```
def ext_gcd(p,q):
    if p == 0:
        return (q, 0, 1)
    else:
        (gcd, u, v) = ext_gcd(q % p, p)
        return (gcd, v - (q // p) * u, u)

p = 26513
q = 32321

gcd, u, v = ext_gcd(p, q)
print('crypto{',end='')
print(u,end='')
print(',',end='')
print(v,end='')
print('}',end='')
```

Flag:  
`crypto{10245,-8404}`

### Greatest Common Divisor  


calculate gcd(a,b) for `a = 66528, b = 52920` and enter it below.

```
def gcd(a, b): 
    if a == 0 :
        return b 
     
    return gcd(b%a, a)
 
a = 66528
b = 52920
print(gcd(a, b))
```

Answer : `1512`

### Modular Arithmetic 1

Calculate the following integers:

`11 ≡ a mod 6`
`8146798528947 ≡ b mod 17`

The solution is the smaller of the two integers.  

```
a1=11
m1=6
a2=8146798528947
m2=17
if(a1%m1<a2%m2):
	print(a1%m1)
else:
	print(a2%m2)
```

The answer is `4`

### Modular Arithmetic 2  

Lets say we pick p = 17. Calculate `3^17 mod 17`. Now do the same but with `5^17 mod 17`.

What would you expect to get for `7^16 mod 17`? Try calculating that.

This interesting fact is known as Fermat's little theorem. We'll be needing this (and its generalisations) when we look at RSA cryptography.

Now take the prime `p = 65537`. Calculate `273246787654^65536 mod 65537`.

Did you need a calculator?

`pow(3, 17, 17)` gives `3`.     

`pow(5, 17, 17)` gives `5` similarly.  

`pow(7, 16, 17)` gives `1`.  

`pow(273246787654, 65536, 65537)` will be `1` as seen above. 

## XOR  
### Favourite byte  

Here we were given a data whch was hidden by a single byte.   
```73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d```

So we will use python code to do this:  
```
str="73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d"
arr = bytearray.fromhex(str)

for i in range(256):
	ans=""
	for x in arr:
		ans += chr(x^i)
	if("crypto" in ans):
		print(ans)
```

The code will give us the flag:  
```crypto{0x10_15_my_f4v0ur173_by7e}```

### XOR Properties  

Here they gave us some properties of XOR.  

The main idea in this challenge is that, we need to find FLAG:      
```
KEY1 = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313
KEY2 ^ KEY1 = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e
KEY2 ^ KEY3 = c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1
FLAG ^ KEY1 ^ KEY3 ^ KEY2 = 04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf
```
This can be done using **commutative property** of XOR  

The bellow code will do that:
```
import binascii
a = "a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313"
b = "37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e"
c = "c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1"
d = "04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf"

k1 = int(a, 16)
k1_k2 = int(b, 16)
k2_k3 = int(c, 16)
F_k1_k2_k3 = int(d, 16)
k2=k1_k2^k1
k3=k2_k3^k2

FLAG=hex(F_k1_k2_k3^k1^k2^k3)
print(bytes.fromhex(FLAG))
```
The final answer i.e., flag will be:  
```crypto{x0r_i5_ass0c1at1v3}```

### XOR Starter  

We need to XOR each character of `label` with 13.  

```
str="label"
a=''
for x in str:
	a+=chr(ord(x)^13)
print(a)
```

This will give us:
```aloha```

