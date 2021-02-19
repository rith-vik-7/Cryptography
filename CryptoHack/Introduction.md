# CryptoHack  
## Finding Flags  

Here the flag is provided in the description itself  

```flag = crypto{y0ur_f1rst_fl4g}```

## Great Snakes  

Here in this challenge we were provided with a python code. By compiling the code we will get our flag.  

```flag = crypto{z3n_0f_pyth0n}```

## Network Attacks  

In this challenge we were given a code and using that we need to connect to a server and buy the flag  

```
#!/usr/bin/env python3

import telnetlib
import json

HOST = "socket.cryptohack.org"
PORT = 11112

tn = telnetlib.Telnet(HOST, PORT)


def readline():
    return tn.read_until(b"\n")

def json_recv():
    line = readline()
    return json.loads(line.decode())

def json_send(hsh):
    request = json.dumps(hsh).encode()
    tn.write(request)


print(readline())
print(readline())
print(readline())
print(readline())


request = {
    "buy": "clothes"
}
json_send(request)

response = json_recv()

print(response)
```

Here it was like **"buy": "clothes"** but we need to buy the flag not clothes. So after changing it to **"buy": "flag"**, We will get our flag  

```flag = crypto{sh0pp1ng_f0r_fl4g5}```

