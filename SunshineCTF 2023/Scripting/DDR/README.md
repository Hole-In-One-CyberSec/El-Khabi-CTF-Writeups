# DDR
#### Write-up author : [JustKhal](https://github.com/JustKhal)
## DESCRIPTION:
All the cool robots are playing Digital Dance Robots, a new rythmn game that... has absolutely no sound! Robots are just that good at these games... until they crash because they can't count to 256. Can you beat the high score and earn a prize?

nc chal.2023.sunshinectf.games 23200

## STEPS:
1. So like its title, we are playing DDR (Dance Dance Revolution) but it's really fast, so have to make our own script to able to get the flag. 
```py
from pwn import *
import itertools

def play():
    host = "chal.2023.sunshinectf.games"
    port = 23200
    r = remote(host, port)
    r.recvuntil("   -- Press ENTER To Start --   ")
    r.recvline()
    r.sendline("")
    r.recvline()
    for i in range(257):
        print(f"Round {i+1}")
        inp = ""
        comb = []
        seq = r.recvline().decode()

        for j in range(len(seq)):
            if seq[j] == "⇧":
                comb.append("w")
            elif seq[j] == "⇨":
                comb.append("d")
            elif seq[j] == "⇩":
                comb.append("s")
            elif seq[j] == "⇦":
                comb.append("a")
            else:
                print(seq[j])

        inp = "".join(comb)
        r.sendline(inp)

play()
```

2. From the chall description, we have to beat it until round 255, but just in case i set my script to loop until 256. 

3. Each round the script takes the sequence of arrows and then decode it since it was in bytes not string.

4. Then it loops for the length of the sequence, then it compares each character aka arrow in this case.
    - If it's "⇧" then it adds "w" to the list called "comb" (combination).
    - If it's "⇨" then it adds "d" to the list called "comb" (combination).
    - If it's "⇩" then it adds "s" to the list called "comb" (combination).
    - If it's "⇦" then it adds "a" to the list called "comb" (combination).

5. After the loop for the comparison ends, it turns the list into a single string using join() after that it sends it. If it's right then the game continues, if not it ends.



## FLAG:

```
sun{d0_r0b0t5_kn0w_h0w_t0_d4nc3}
```