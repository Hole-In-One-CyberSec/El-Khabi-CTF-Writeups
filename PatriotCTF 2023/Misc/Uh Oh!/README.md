# Uh Oh!
#### Write-up author : [Severable](https://github.com/Severable)

## DESCRIPTION:
Uh Oh! While trying to add passwords to my wordlist, I accidentally added my own phone number! Can you tell me what line it's on?

https://en.wikipedia.org/wiki/North_American_Numbering_Plan#Modern_plan

Make sure the phone number follows this format: (NPA) NXX-XXXX

Format: PCTF{linenumber_phonenumonlynumbers}

## STEPS:
1. Unzip the file, you'll get a TXT file containing random words and numbers
2. Find the phone number using regular expressions in grep according to the North American Numbering Plan: (NPA) NXX-XXXX
3. Find the line number in any text editor by searching the phone number

```
grep -G '([0-9]\{3\}) [0-9]\{3\}-[0-9]\{4\}' rockyou.txt
```

## FLAG:

```
PCTF{7731484_4043037283}
```
