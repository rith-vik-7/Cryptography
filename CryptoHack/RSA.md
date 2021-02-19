# CryptoHack  
## RSA  
### RSA Starter 1

Find the solution to `101^17 mod 22663`  

```
>>> pow(101, 17, 22663)
19906
```

### RSA Starter 2  

"Encrypt" the number `12` using the exponent `e = 65537` and the primes `p = 17 and q = 23`. What number do you get as the ciphertext?

`a = 12^e mod N`  

`N = p * q`

```
>>> pow(12, 65537, 17*23)
301
```

### RSA Starter 3

Given `N = p*q` and two primes:

`p = 857504083339712752489993810777`

`q = 1029224947942998075080348647219`

What is the `totient` of N?


`φ(n) = (p − 1)(q − 1)`

```
>>> p = 857504083339712752489993810777
>>> q = 1029224947942998075080348647219
>>> (p-1)*(q-1)
882564595536224140639625987657529300394956519977044270821168
```

### RSA Starter 4

Given the two primes:

`p = 857504083339712752489993810777`

`q = 1029224947942998075080348647219`

and the exponent:

`e = 65537`

What is the private key `d`?  

```
>>> from Crypto.PublicKey import RSA
>>> from Crypto.Util.number import *
>>> p = 857504083339712752489993810777
>>> q = 1029224947942998075080348647219
>>> e = 65537
>>> n = p*q
>>> phin = (p-1)*(q-1)
>>> d = inverse(e,phin)
>>> print(d)
121832886702415731577073962957377780195510499965398469843281
```

### RSA Starter 5  

I've encrypted a secret number for your eyes only using your public key parameters:

`N = 882564595536224140639625987659416029426239230804614613279163`

`e = 65537`

Use the private key that you found for these parameters in the previous challenge to decrypt this ciphertext:

`c = 77578995801157823671636298847186723593814843845525223303932`

```
>>> N = 882564595536224140639625987659416029426239230804614613279163
>>> e = 65537
>>> c = 77578995801157823671636298847186723593814843845525223303932
>>> pow(c,d,n)
13371337
```
