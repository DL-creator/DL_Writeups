# TheBakingCase
## Task description 
TheBakingCase 
40
Misc Steganography
Difficulty: Beginner
Author: H4N5

>I hid a message for you here, see if you can find it! Take it slow, little by little, bit by bit.

>i UseD to coDE liKe A sLEEp-dEprIVed SqUirRel smasHInG keYs HOPinG BugS would dISApPear THrOugh fEAr tHeN i sPilled cOFfeE On mY LaPTop sCReameD iNTerNALly And bakeD BanaNa bREAd oUt oF PAnIc TuRNs OUT doUGh IS EasIEr tO dEbUG ThaN jaVASCrIPt Now I whIsPeR SWEEt NOtHIngs TO sOurDoUGh StARtERs aNd ThReATEN CrOissaNts IF they DoN'T rIsE My OVeN haS fEWeR CRasHEs tHAN mY oLD DEV sErvER aNd WHeN THInGS BurN i jUSt cAlL iT cARAMElIzEd FeatUReS no moRE meetInGS ThAt coUlD HAVE bEeN emailS JUst MufFInS THAt COulD HAvE BEen CupCAkes i OnCE tRIeD tO GiT PuSh MY cInnAmON rOLLs aND paNICkED WHEn I coUldn't reVErt ThEm NOw i liVe IN PeaCE uNLESs tHe yEast getS IDeas abOVe iTs StATion oR a COOkiE TrIES To sEgfAult my toOTH FILlings

## Solution - DL
The hint: "Take it slow, little by little, bit by bit." points to binary hidden in the capitalization in the text. Therefore we would need to map:
- Lowercase $\rightarrow$ 0
- Uppercase $\rightarrow$ 1
- (Ignore non-letters)
We then chunk the bits into 8-bit bytes to be able to decode it from byte to text. An example for the first 8 letters in the text:

i UseD to c $\rightarrow$ iUseDtoc $\rightarrow 01001000$ 

We can then use decoders such as cyberchef to decode the binary into text:
![[Pasted image 20251005131844.png]]
The final output:
Here is the flag brunner{I_like_Baking_More_That_Programming} easy peasy ?

### Using python
We can also apply the theory from above in a python script:
```python 
  
text = "i UseD to coDE liKe A sLEEp-dEprIVed SqUirRel smasHInG keYs HOPinG BugS would dISApPear THrOugh fEAr tHeN i sPilled cOFfeE On mY LaPTop sCReameD iNTerNALly And bakeD BanaNa bREAd oUt oF PAnIc TuRNs OUT doUGh IS EasIEr tO dEbUG ThaN jaVASCrIPt Now I whIsPeR SWEEt NOtHIngs TO sOurDoUGh StARtERs aNd ThReATEN CrOissaNts IF they DoN'T rIsE My OVeN haS fEWeR CRasHEs tHAN mY oLD DEV sErvER aNd WHeN THInGS BurN i jUSt cAlL iT cARAMElIzEd FeatUReS no moRE meetInGS ThAt coUlD HAVE bEeN emailS JUst MufFInS THAt COulD HAvE BEen CupCAkes i OnCE tRIeD tO GiT PuSh MY cInnAmON rOLLs aND paNICkED WHEn I coUldn't reVErt ThEm NOw i liVe IN PeaCE uNLESs tHe yEast getS IDeas abOVe iTs StATion oR a COOkiE TrIES To sEgfAult my toOTH FILlings"
  

bits = ''.join('1' if c.isupper() else '0' for c in text if c.isalpha())

b = bytes(int(bits[i:i+8], 2) for i in range(0, (len(bits)//8)*8, 8))
  

print(b)                   # raw bytes

print(b.decode('ascii'))   # ASCII string
```

The output will then become:
```
b'Here is the flag brunner{I_like_Baking_More_That_Programming} easy peasy ?'
Here is the flag brunner{I_like_Baking_More_That_Programming} easy peasy ?
```

[[BrunnerCTF2025 - Writeups]]  [[Writeups]] 
