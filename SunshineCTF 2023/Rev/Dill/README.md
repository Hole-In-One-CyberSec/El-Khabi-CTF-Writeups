# Dill
#### Write-up author : [JustKhal](https://github.com/JustKhal)
## DESCRIPTION:
Originally this was going to be about pickles, but .pyc sounds close enough to "pickles" so I decided to make it about that instead.

## STEPS:
1. So first of all, since the is a .pyc file then we have to decompile it first to see what's really in it. I use [this online tool](https://www.toolnb.com/tools-lang-en/pyc.html) to decompile it.
```py
# uncompyle6 version 3.5.0
# Python bytecode 3.8 (3413)
# Decompiled from: Python 2.7.5 (default, Jun 20 2023, 11:36:40) 
# [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)]
# Embedded file name: dill.py
# Size of source mod 2**32: 914 bytes


class Dill:
    prefix = 'sun{'
    suffix = '}'
    o = [5, 1, 3, 4, 7, 2, 6, 0]

    def __init__(self) -> None:
        self.encrypted = 'bGVnbGxpaGVwaWNrdD8Ka2V0ZXRpZGls'

    def validate(self, value: str) -> bool:
        if not (value.startswith(Dill.prefix) and value.endswith(Dill.suffix)):
            return False
        value = value[len(Dill.prefix):-len(Dill.suffix)]
        if len(value) != 32:
            return False
        c = [value[i:i + 4] for i in range(0, len(value), 4)]
        value = ''.join([c[i] for i in Dill.o])
        if value != self.encrypted:
            return False
        else:
            return True
```

2. From that decompiler we got the real python code, as we can see we have to input a string and our input will be validated using the function validate() inside the class Dill. If after the process our string is the same as the encrypted variable then our input is the flag. So we have to reverse the process of function validate to get the flag.

```py
class Dill:
    prefix = 'sun{'
    suffix = '}'
    o = [5, 1, 3, 4, 7, 2, 6, 0]

    def __init__(self) -> None:
        self.encrypted = 'bGVnbGxpaGVwaWNrdD8Ka2V0ZXRpZGls'

    def validate(self, value: str) -> bool:
        if not (value.startswith(Dill.prefix) and value.endswith(Dill.suffix)):
            return False
        value = value[len(Dill.prefix):-len(Dill.suffix)]
        if len(value) != 32:
            return False
        c = [value[i:i + 4] for i in range(0, len(value), 4)]
        value = ''.join([c[i] for i in Dill.o])
        if value != self.encrypted:
            print("no")
            return False
        else:
            print("yeay")
            return True

x = Dill()
val = []
correct_order = [0,1,2,3,4,5,6,7]

for i in range(len(x.o)):
    correct_order[i] = x.o.index(i)

b = [x.encrypted[i:i + 4] for i in range(0, len(x.encrypted), 4)]
for i in correct_order:
    val.append(b[i])

val = ''.join(val)
val = f"sun{{{val}}}"
print(val)
x.validate(val)
```
3. So i made this simple python code and then test it using validate(). So first i made an object from Dill class with x variable. And then i prepare empty list called "val" for the final result and list called "correct_order" that contains 0 - 7 to contain the correct order of the encrypted string

```py
for i in range(len(x.o)):
    correct_order[i] = x.o.index(i)
```
4. After that we made a for loop to get the correct order of the string from the variable "o" inside the class.

```py
b = [x.encrypted[i:i + 4] for i in range(0, len(x.encrypted), 4)]
for i in correct_order:
    val.append(b[i])
```

5. Then we made a list called "b" contains the string from variable "encrypted" but split into groups of 4 characters. Then we made a for loop to append each group of 4 characters into "val" in the order from list "correct_order".

```py
val = ''.join(val)
val = f"sun{{{val}}}"
print(val)
x.validate(val)
```

6. After that, we use join() to turn the list into a single string. Then we "sun{" as the prefix and "}" as the suffix. We print it and validate it. If it's right then it will print "yeay" and if it's wrong then it will print "no"


## FLAG:

```
sun{ZGlsbGxpa2V0aGVwaWNrbGVnZXRpdD8K}
```
