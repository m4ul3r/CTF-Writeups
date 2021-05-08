# These Ladies Paved Your Way
```
Per womenintech.co.uk, these 10 women paved your way as technologists. One of them holds more than 100 issued patents and is known for writing understandable textbooks about network security protocols. What other secrets does she hold?
```

The challenge contained a zip file with 10 pictures of historical women in tech. Searching each Wikipeda page for who hold patents, Radia Perlman was the person of interest. 

Using strings on the jpg file returned two interesting strings.
```bash
┌──(kali㉿kali)-[~/Downloads/images]
└─$ strings radia_perlman.jpg | head -n 10
JFIF
^Photoshop 3.0
8BIM
U3Bhbm5pbmdUcmVlVmlnCg==
VpwtPBS{r0m5 0W t4x3IB5}
;CREATOR: gd-jpeg v1.0 (using IJG JPEG v62), quality = 80
 , #&')*)
-0-(0%()(
((((((((((((((((((((((((((((((((((((((((((((((((((
$3br
```

`U3Bhbm5pbmdUcmVlVmlnCg==` is a base64 encoded string. `VpwtPBS{r0m5 0W t4x3IB5}` is the flag format.
```bash
┌──(kali㉿kali)-[~/Downloads/images]
└─$ echo "U3Bhbm5pbmdUcmVlVmlnCg==" | base64 -d
SpanningTreeVig
```

Using a Vigenere Decode on CyberChef was able to yield the flag.
`DawgCTF{l0t5 0F p4t3NT5}`