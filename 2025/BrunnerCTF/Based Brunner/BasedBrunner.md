# Based Brunner

## Task description 
Based Brunner
50
Misc
Difficulty: Beginner
Author: Nissen

Brunsviger is just so based, I think I could eat it in any form - from binary to decimal!

Tip: This might require a bit of programming, I would recommend looking into the int() function in Python.

## Understanding the encoding
We were given the python code that was used to encode the flag (encode.py). What it does:
- Loops bases 10 $\rightarrow$ 2
- For each base b, it replaces every current character with ord(char) written in base b, then joins tokens with spaces
- Previous spaces are not preserved as separators; they’re encoded into tokens. New spaces are inserted as separators every round
- As $b \le 10$, tokens are only digits (0-9)

## Solution - DL

Each encode step does the following:
- Take every character, turn it into its number (ord), write that number in base b and put a space in between the results 
So after a base-b pass we get: 
$$
\text{<number-in-base-b> <number-in-base-b> <number-in-base-b> } \dots
$$

To undo it we are doing the reverse for the same base:
- Split on spaces to get the tokens
- Turn each token back into a number with int(token,b)
- turn that number back into a character with chr()

This is done for bases $2 \rightarrow 10$  (the reverse order of the encoding) and we will then end up with the original flag.

Using this the following python script solve.py was made:

``` python
def decode_layers(s: str) -> str:
    for base in range(2, 11):
        s = ''.join(chr(int(tok, base)) for tok in s.split())
    return s
    
with open("based.txt", "r", encoding="utf-8") as f:
    data = f.read()
    
flag = decode_layers(data)

print(flag)
```

Running this script we get the following flag:

![[Pasted image 20251012181012.png]]
```
brunner{1s_b4s3d}