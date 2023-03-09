## SOLUTION 1 - CyberChef 

1. Open the VBScript file challenge002.vbs in CyberChef

![alt text](https://github.com/ATTACKnDEFEND/Deobfuscation-Challenges/blob/main/challenge002/solution/images/C2-S1-1.png)

2. Filter out junk code (comments) from the file using the Filter operation. Use the Regex pattern ^' and select the Invert condition.

![alt text](https://github.com/ATTACKnDEFEND/Deobfuscation-Challenges/blob/main/challenge002/solution/images/C2-S1-2.png)

3. Reviewing the code, we see Loki.run, where Loki is an object referencing Wscript. The command executes two functions together
ReverseAndConvert and HexToAscii on the value assigned to variable H76896O9832443280482O38423482lO4382482O4543543535345. 

To make the variable easier to understand, as there are purposely long similar names used to annoy analysts, we use the Find / Replace operation in CyberChef 
to improve readability.

Find: H76896O9832443280482O38423482lO4382482O4543543535345
Replace: HAMMER

![alt text](https://github.com/ATTACKnDEFEND/Deobfuscation-Challenges/blob/main/challenge002/solution/images/C2-S1-3.png)

The value of the variable HAMMER is: 226578652e636c616320737365636f72502d74726174532220646e616d6d6f432d206578652e6c6c6568737265776f70

Review the code and locate the object Loki.run. The command executes two functions - ReverseAndConvert and HexToAscii - on the value assigned to the variable H76896O9832443280482O38423482lO4382482O4543543535345. 
To make the variable more readable, we can use the Find/Replace operation in CyberChef.

Find: H76896O9832443280482O38423482lO4382482O4543543535345
Replace: HAMMER

It is now easier to locate the value of the new variable: 226578652e636c616320737365636f72502d74726174532220646e616d6d6f432d206578652e6c6c6568737265776f70.

4. Convert from Hex to ASCII and reverse the strings

Copy the variable HAMMER to a new input tab, and apply the "From Hex" and "Reverse" operations.

The obfuscated VBScript executes a PowerShell command.

![alt text](https://github.com/ATTACKnDEFEND/Deobfuscation-Challenges/blob/main/challenge002/solution/images/C2-S1-4.png)

## COMING NEXT - SOLUTION 2 - FlameVM using Python and code execution

#### References or additional resources:

Deobfuscation of VBScript-based Malware: https://dspace.cvut.cz/bitstream/handle/10467/94915/F8-BP-2021-Havranek-Matej-thesis.pdf?sequence=-1&isAllowed=y




