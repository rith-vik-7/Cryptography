# Cryptopals  
## Set1
### Challenge1 - Convert hex to base64  

We need to convert hex string to base64 now  

```
str = "49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d"
ans = str.decode("hex").encode("base64")
print(ans)
```

This code will give us the required answer:  
```SSdtIGtpbGxpbmcgeW91ciBicmFpbiBsaWtlIGEgcG9pc29ub3VzIG11c2hyb29t```

### Challenge 2  

We were given three strings
```
1c0111001f010100061a024b53535009181c
```
... after hex decoding, and when XOR'd against:  
```
686974207468652062756c6c277320657965
```
... should produce:  
```
746865206b696420646f6e277420706c6179
```

This can be done using the following python script:
```
str1 = "1c0111001f010100061a024b53535009181c"
a = int(str1, 16)
str2 = "686974207468652062756c6c277320657965"
b = int(str2, 16)
c = a ^ b 
print(hex(c))
```

### Challenge 5  

Here we were given a string and a key
```
Burning 'em, if you ain't quick and nimble
I go crazy when I hear a cymbal
```
key = "ICE", using repeating-key XOR, We need to produce 
```
0b3637272a2b2e63622c2e69692a23693a2a3c6324202d623d63343c2a26226324272765272
a282b2f20430a652e2c652a3124333a653e2b2027630c692b20283165286326302e27282f
```

This can be done using the program:

```
import binascii

str="Burning 'em, if you ain't quick and nimbleI go crazy when I hear a cymbal"

x = bytes(str.encode())
key="ICE"

flag=""
for i in range (len(x)):
	flag = flag + key[i%len(key)]

res=""
for i in range (len(x)):
	res+=chr(x[i]^ord(fla[i]))

print(binascii.hexlify(res.encode()).decode())
```
