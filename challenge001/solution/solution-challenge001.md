### Solution - CHALLENGE001

1. To make analysis slightly safer from any accidental execution first we rename the file from challenge001.cmd to challenge001.cmd.txt

2. Opening in a text editor, we notice a large block of ASCII characters as well as the Windows system command certutil, which supports that these characters are most likely encoded in Base64.

```
start /MIN cmd %ComSpec% /V/D/c "s^eT IITV=%APPDATA%\%RANDOM%.^j^S&&echo dmFyIENTYUo9IlciKyJzQyIrIlIiOw0KdmFyIERTYUo9ImlQIisidC4iOw0KdmFyIEVTYUo9IlNoIisiRWwiKyJsIjsNCnZhciBGU2FKPSJoIisiVCIrIlQiOw0KdmFyIEdTYUo9InAiKyJzOi8iKyIvIjsNCnZhciBzaGVsbCA9IG5ldyBBY3RpdmVYT2JqZWN0KENTYUorRFNhSitFU2FKKTsNCnNoZWxsLnJ1bihGU2FKICsgR1NhSiArICJhdHRhY2tuZGVmZW5kLmNvbSIpOw== >!IITV!&&cErtUtil -f -dEco^de !IITV! !IITV!&& w^s^c^r^ipt !IITV!"
```

While certutil is used to manage certificates, the tool can be abused by attackers in quite a few ways including downloading files, and also encoding and decoding files in Base64[^1]. This technique to use native system tools is referred to as Living off the Land. See reference section for more details.

3. The initial cmd file utilises windows environment variables, as well as setting a new variable to an encoded Base64 file. I've added a few additional windows environment variables which were not included in the original sample such as the %RANDOM% environment variable when creating the file.

4. The initial cmd also heavily uses an obfuscation technique of uninterpreted escape characters[^2], in this case ^. While a simple technique, it can be highly effective. I've added the direct use of WScript and also utilised the same obfuscation technique to this command. See reference section for more details.

5. Decode the Base64. Example, using online tool Base64 Guru [^3].

Copy and paste the Base64 to Base64* window, then select Decode Base64. 

Select download which saves the file to text.txt

![alt text](https://github.com/ATTACKnDEFEND/Deobfuscation-Challenges/blob/main/challenge001/solution/image1.png)

6. Reviewing text:txt, the file is JavaScript referenced by the original cmd file:

```
var CSaJ="W"+"sC"+"R";
var DSaJ="iP"+"t.";
var ESaJ="Sh"+"El"+"l";
var FSaJ="h"+"T"+"T";
var GSaJ="p"+"s:/"+"/";
var shell = new ActiveXObject(CSaJ+DSaJ+ESaJ);
shell.run(FSaJ + GSaJ + "attackndefend.com");
```

The first type of obfuscation is called string concatenation, where parts of a string are separated and combined using a concatenation operator, such as the "+" symbol in this example.

The second type of obfuscation is called variable substitution, where commands or strings are broken up and assigned to variables to make them less recognizable to human readers.

7. Script execution

The script opens the url, https://attackndefend.com

#### F00TN0TES

[^1]: https://redcanary.com/threat-detection-report/techniques/obfuscated-files-information/

[^2]: certutil | LOLBAS (lolbas-project.github.io) : https://lolbas-project.github.io/lolbas/Binaries/Certutil/

[^3]: Obfuscated Files or Information, Technique T1027 - Enterprise | MITRE ATT&CK® : https://attack.mitre.org/techniques/T1027/

[^4]: Base64 to File | Base64 Decode | Base64 Converter | Base64 : https://base64.guru/converter/decode

