# whataxor
#### Write-up author : [JustKhal](https://github.com/JustKhal)
## DESCRIPTION:
Now you actually need to figure what the binary is doing...... maybe try a tool like https://dogbolt.org/ It shows you the output of several tools that try to extract a representation similar to what the original code might have looked like..... which is a lot nicer than reading bytes.

## STEPS:
1. First we open the whataxor file using [dogbolt](https://dogbolt.org/)
```
uint64_t xor_transform(void* arg1, char arg2)
{
    int32_t var_c = 0;
    uint64_t rax_8;
    while (true)
    {
        rax_8 = *(arg1 + var_c);
        if (rax_8 == 0)
        {
            break;
        }
        *(arg1 + var_c) = (*(arg1 + var_c) ^ arg2);
        var_c = (var_c + 1);
    }
    return rax_8;
}

int32_t main(int32_t argc, char** argv, char** envp)
{
    void* fsbase;
    int64_t rax = *(fsbase + 0x28);
    printf("Enter your password: ");
    void var_78;
    __isoc99_scanf("%99s", &var_78);
    xor_transform(&var_78, 0xaa);
    char var_c8 = 0xc9;
    char var_c7 = 0xd9;
    char var_c6 = 0xcb;
    char var_c5 = 0xdd;
    char var_c4 = 0xc9;
    char var_c3 = 0xde;
    char var_c2 = 0xcc;
    char var_c1 = 0xd1;
    char var_c0 = 0x9a;
    char var_bf = 0xc4;
    char var_be = 0xcf;
    char var_bd = 0xf5;
    char var_bc = 0xd9;
    char var_bb = 0xc2;
    char var_ba = 0xcf;
    char var_b9 = 0xcf;
    char var_b8 = 0xfa;
    char var_b7 = 0xf5;
    char var_b6 = 0x9b;
    char var_b5 = 0xdd;
    char var_b4 = 0xc5;
    char var_b3 = 0xf5;
    char var_b2 = 0xd9;
    char var_b1 = 0xc2;
    char var_b0 = 0xcf;
    char var_af = 0xfd;
    char var_ae = 0xda;
    char var_ad = 0xf5;
    char var_ac = 0x98;
    char var_ab = 0xc2;
    char var_aa = 0xd8;
    char var_a9 = 0xcf;
    char var_a8 = 0xcf;
    char var_a7 = 0xf5;
    char var_a6 = 0x9f;
    char var_a5 = 0xc2;
    char var_a4 = 0xcf;
    char var_a3 = 0xcf;
    char var_a2 = 0xc1;
    char var_a1 = 0xd9;
    char var_a0 = 0xf5;
    char var_9f = 0xf5;
    char var_9e = 0xf5;
    char var_9d = 0xf5;
    char var_9c = 0xf5;
    char var_9b = 0xd0;
    char var_9a = 0xf5;
    char var_99 = 0xf5;
    char var_98 = 0xf5;
    char var_97 = 0xd0;
    char var_96 = 0xd0;
    char var_95 = 0xd0;
    char var_94 = 0xf5;
    char var_93 = 0xf5;
    char var_92 = 0xf5;
    char var_91 = 0xf5;
    char var_90 = 0xf5;
    char var_8f = 0xd0;
    char var_8e = 0xd0;
    char var_8d = 0xd0;
    char var_8c = 0xd0;
    char var_8b = 0xd0;
    char var_8a = 0xd0;
    char var_89 = 0xf5;
    char var_88 = 0xf5;
    char var_87 = 0xf5;
    char var_86 = 0xf5;
    char var_85 = 0xd2;
    char var_84 = 0xc5;
    char var_83 = 0xd8;
    char var_82 = 0xd7;
    if (strcmp(&var_78, &var_c8) != 0)
    {
        puts("Access denied.");
    }
    else
    {
        puts("Correct!");
    }
    if (rax == *(fsbase + 0x28))
    {
        return 0;
    }
    __stack_chk_fail();
    /* no return */
}
```

2. From that we can see our input will be transform using xor with the function "xor_transform" where each character of our input will be xor with 0xaa and then will be compared with the combination of characters. So with that we can just transform each of the character in that code so we can get the password/flag

3. I made a simple python script to get it
```py
arr= [0xc9, 0xd9, 0xcb, 0xdd, 0xc9, 0xde, 0xcc, 0xd1, 0x9a, 0xc4, 0xcf, 0xf5, 0xd9, 0xc2, 0xcf, 0xcf, 0xfa, 0xf5, 0x9b, 0xdd, 0xc5, 0xf5, 0xd9, 0xc2, 0xcf, 0xfd, 0xda, 0xf5, 0x98, 0xc2, 0xd8, 0xcf, 0xcf, 0xf5, 0x9f, 0xc2, 0xcf, 0xcf, 0xc1, 0xd9, 0xf5, 0xf5, 0xf5, 0xf5, 0xf5, 0xd0, 0xf5, 0xf5, 0xf5, 0xd0, 0xd0, 0xd0, 0xf5, 0xf5, 0xf5, 0xf5, 0xf5, 0xd0, 0xd0, 0xd0, 0xd0, 0xd0, 0xd0, 0xf5, 0xf5, 0xf5, 0xf5, 0xd2, 0xc5, 0xd8, 0xd7]

passwd = []
for i in range(len(arr)):
    passwd.append(chr(arr[i]^0xaa))

print("".join(passwd))
```

## FLAG:

```
csawctf{0ne_sheeP_1wo_sheWp_2hree_5heeks_____z___zzz_____zzzzzz____xor}
```
