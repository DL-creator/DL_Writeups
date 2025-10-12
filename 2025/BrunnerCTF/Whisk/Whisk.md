# Whisk
## Task description 
Whisk
40
Crypto
Difficulty: Beginner
Author: rvsms

>Someone tried sabotaging our operation by "whisking” away the secret ingredient for the perfect brunsviger. All that's left on the workbench is this sticky note full of pastry-themed symbols and random letters.

>Can you help us recover the secret ingredient?

(The ciphertext is inside the zip file)
## Solution - DL
In this challenge we are working with a simple substitution cipher on letters/symbols only (digits and punctuation are unchanged). This means same ciphertext $\Rightarrow$ same plaintext. As the flag has the format: brunner{...}, the {} in the ciphertext from whisk.txt indicates where the flag body appears. 

Therefore we know the characters before { must correspond to brunner. Meaning:

$$\text{OZ🥖SS🥐Z\{$\dots$\} $\rightarrow$ brunner\{$\dots$\}}$$
Therefore we have the following fixed decryptions:

| Cipher | Plaintext |
|:------:|:---------:|
|   O    |     b     |
|   Z    |     r     |
|   🥖   |     u     |
|   S    |     n     |
|   🥐   |     e     |

We can therefore insert the symbols we do know into the ciphertext and replace all other characters with underscores (the symbol | represents a space):
```
_ _e | _e_re_ | _n_re_ _en_ | _ _ | _ _ _ _ _ _ | _ _ _e. | _ _ | b _ _ e | _ | _er_e_ _
brun_ _ _ _er, | _e_ _ | bu_ _er | _ _ _ _ | br_ _n | _u_ _r, | _ _ur | _ _ | _ _er | _ _e | _ _r_
_ _u_ _, | _n_ | _e_ | _ _e | _ _ru_ | _ee_ | _n_ _ | e_er_ | _ _rner. |_ _ _ _e, | _ _ _ _e,
_n_ | re_e_ber: | _ _ _r_n_ | _ _ _ _r_ | _ _ _ | _ _ | _ _n_ _ _ _r_.

brunner{n0_ _0r3_ _u_ _ _ _ _1_ _3r}
```

Now we need lock english anchors (e.g., and, remember, butter, brown sugar)  and propagate the new letters globally. Doing so resolves the text naturally and yields the final flag:

```
brunner{n0_m0r3_lumpy_c1ph3r}
```