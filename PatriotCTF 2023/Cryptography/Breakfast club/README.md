
# Breakfast club
#### Write-up author : [JustKhal](https://github.com/JustKhal)

## DESCRIPTION:
As the sysadmin for your college, you're responsible for overseeing the security of all the clubs. One of the on campus orginizations is a breakfast club with their own personal website that the leader insured you was "unhackable". He was so sure of this, that he sent you an example of how hashes are stored in the database, something about "changing the hash type multiple times for each password" or something like that. Can you crack the password and prove him wrong?

## STEPS:
1. Decode each encoded string with its algorithm with this Python script i made
```py
from Crypto.Hash import SHA, SHA1, MD2, MD4, MD5, SHA224, SHA256, SHA384, SHA512, SHA3_224, SHA3_256, SHA3_384, SHA3_512, TupleHash128, TupleHash256, BLAKE2s, BLAKE2b
from pwn import *

target = ['511993d3c99719e38a6779073019dacd7178ddb9',
'32096c2e0eff33d844ee6d675407ace18289357d',
'ae8033c09e7cf93b230414cd919da992',
'189bb272d916eea5b99b2a572ad93e9a',
'f95b70fdc3088560732a5ac135644506',
'7e27c59a202f5e2b2b3b5458300140ef7aa7edc3a97a605b788546a1',
 'c3641f8544d7c02f3580b07c0f9887f0c6a27ff5ab1d4a3e29caf197cfc299ae',
 '1861ebe932dc65c5f04d33f6972b13acc8b1e572344016bf3cc950f60bfad6fdc0e32f0318e8bba57cf756eac0a49fce',
 '9032fb94055d4d14e42185bdff59642b98fe6073f68f29d394620c4e698a86fb2e51351ca6997e6a164aae0b871cf789fbc6e0d863733d05903b4eb11be58d9c',
 'd22e03747b83667e3e84c78e9fb49f7c9376334b9cb337addbdf3ff9',
 'd14a329a1924592faf2d4ba6dc727d59af6afae983a0c208bf980237b63a5a6a',
 '3bd4e7dcad9d3c02adfa7aa5388727d346278a9a7b007f497b48a4fa2a12b9545c820df150854a8f8c494275bd6fd941',
 '2d44da53f305ab94b6365837b9803627ab098c41a6013694f9b468bccb9c13e95b3900365eb58924de7158a54467e984efcfdabdbcc9af9a940d49c51455b04c',
 'aed477850ed48df54054e9d3e7b8cae7e1764d949adb68fe4f24802ec464cb6c334ef97cc0453471fac5faf0118265bc9388062ccb704d5ac4010489bee201da',
 'a130e4df9144790d9c8824f90f4c1220a3eb5aa0cb296ab1f4f41f23f3ed0800f2ac3fad4f235a4ee601a8ca8bf0be394e06e53e2f789a6272f1bc54c4901d0c',
 '5abf6b1a79dee98ea32a98195c61a667c29a3674e79c82e43f0d19b0efa4b6f7',
 '7ae26253cfd42a3a090c44023c234ec63d0ffe63f8ad40b7913f3f646503b7a7cb8ac571d42a311ef71508344de72f30b57e5c100b402130060ebc947e07a59b']

hash_alg = [SHA,
SHA1,
MD2,
MD4,
MD5,
SHA224,
SHA256,
SHA384,
SHA512,
SHA3_224,
SHA3_256,
SHA3_384,
SHA3_512,
TupleHash128,
TupleHash256,
BLAKE2s,
BLAKE2b,]

decoded_flag = []

hash_str = string.ascii_lowercase + string.ascii_uppercase + string.digits + string.punctuation
for i in range(len(hash_alg)):
    for j in range(len(hash_str)):
        decoded_hash = hash_alg[i].new()
        decoded_hash.update(hash_str[j].encode())
        if target[i] == decoded_hash.hexdigest():
            print("THIS IS THE ONE = ", hash_str[j])
            decoded_flag.append(hash_str[j])
            break
decoded_flag = "".join(decoded_flag)
print(decoded_flag)
```

## FLAG:

```
PCTF{H@5H_8R0WNS}
```



