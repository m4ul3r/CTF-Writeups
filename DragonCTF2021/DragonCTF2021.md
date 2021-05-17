---
title: "DragonCTF2021"
date: 2021-05-17
tags: ["ctf", "DragonCTF2021"]
image: ""
toc: true
---

## Web
### Simple Web
```
Time to warm up!  
[http://dctf1-chall-simple-web.westeurope.azurecontainer.io:8080](http://dctf1-chall-simple-web.westeurope.azurecontainer.io:8080/)
```

The website contained a checkbox with the text "I want the flag" and a submit button. Looked at the request with Burp Suite, there was a POST request being sent to /flag. 
[simpleweb](simpleweb.png)
Changed `flag=1&auth=0&Submit=Submit` to `flag=1&auth=1&Submit=Submit` to yield the flag.
`dctf{w3b_c4n_b3_fun_r1ght?}`

### Very secure website 
```
Some students have built their most secure website ever. Can you spot their mistake?

http://dctf1-chall-very-secure-site.westeurope.azurecontainer.io/
```
[secureWebsite](securewebsite.png)

The website gave a link to the source code:
```php
<?php
    if (isset($_GET['username']) and isset($_GET['password'])) {
        if (hash("tiger128,4", $_GET['username']) != "51c3f5f5d8a8830bc5d8b7ebcb5717df") {
            echo "Invalid username";
        }
        else if (hash("tiger128,4", $_GET['password']) == "0e132798983807237937411964085731") {
            $flag = fopen("flag.txt", "r") or die("Cannot open file");
            echo fread($flag, filesize("flag.txt"));
            fclose($flag);
        }
        else {
            echo "Try harder";
        }
    }
    else {
        echo "Invalid parameters";
    }
?>
```
Using an online hash lookup (https://md5hashing.net/hash/tiger128,4), the username has was found to be `admin`; the password was not found from this website.

PHP hash comparison has a vulnerability (https://www.darkreading.com/vulnerabilities---threats/php-hash-comparison-weakness-a-threat-to-websites-researcher-says-/d/d-id/1320353) and should be using `!==` rather than `!=`. A password was found, `5HFt8rWI`, where the hash begins with `0e` (https://github.com/spaze/hashes/blob/master/tiger128%2C4.md). 

Using the `admin` and `5HFt8rWI` gave the flag

`dctf{It's_magic._I_ain't_gotta_explain_shit.}`

### DevOps vs SecOps 
```
Automatization is amazing when it works, but it all comes at a cost... You have to be careful...

(URL not missing)
```

Flag was found on the host's github.
https://github.com/DragonSecSI/.github/blob/main/setup.py
`dctf{H3ll0_fr0m_1T_guy}`


## Crypto
### Julius' ancient script 
`I found this Ancient Roman **papyrus**. Could you decypher it for me?`

`flag.txt` was downloaded and contained encrypted flag: `rq7t{7vH_rFH_vI6_pHH1_qI67}`.
Given the hint, a Caesar cipher was used with numbers (0-9) to decode the flag. https://www.dcode.fr/caesar-cipher was used to brute force, with the rotation being +14.
`dctf{th3_d13_h4S_b33N_c4St}`

## Rev

## Pwn

## Misc
### Encrypted the flag I have
`Decrypted flag is not in exact format.`

[encryptedFlag](EncryptedTheFlagIHave.png)

The language used in this challenge sounded like "yoda-ism", so it was assumed it had to deal with Star Wars. Used an Aurebesh key to decode the flag.
`dctf{mastercodebreaker}`

### Don't let it run
`PDF documents can contain unusual objects within.`

Challenge contained `dragon.pdf`. Used `strings` on the file and found obfuscated JavaScript.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings dragon.pdf
%PDF-1.7
1 0 obj
<snip>
/S /JavaScript
/JS <766172205F3078346163393D5B2736363361435968594B272C273971776147474F272C276C6F67272C273150744366746D272C27313036387552596D7154272C27646374667B7064665F316E6A33637433647D272C273736383537376A6868736272272C2737313733343268417A4F4F51272C27373232353133504158436268272C2738333339383950514B697469272C27313434373836335256636E546F272C2731323533353356746B585547275D3B2866756E6374696F6E285F30783362316636622C5F3078316164386237297B766172205F30783536366565323D5F3078353334373B7768696C652821215B5D297B7472797B766172205F30783237353061353D7061727365496E74285F307835363665653228307831366529292B2D7061727365496E74285F307835363665653228307831366429292B7061727365496E74285F307835363665653228307831366329292B2D7061727365496E74285F307835363665653228307831373329292A2D7061727365496E74285F307835363665653228307831373129292B7061727365496E74285F307835363665653228307831373229292A2D7061727365496E74285F307835363665653228307831366129292B7061727365496E74285F307835363665653228307831366629292A7061727365496E74285F307835363665653228307831373529292B2D7061727365496E74285F307835363665653228307831373029293B6966285F30783237353061353D3D3D5F307831616438623729627265616B3B656C7365205F30783362316636625B2770757368275D285F30783362316636625B277368696674275D2829293B7D6361746368285F3078353736346134297B5F30783362316636625B2770757368275D285F30783362316636625B277368696674275D2829293B7D7D7D285F3078346163392C3078386439376629293B66756E6374696F6E205F30786128297B766172205F30783363366432303D5F3078353334373B636F6E736F6C655B5F3078336336643230283078313734295D285F307833633664323028307831366229293B7D76617220613D27626B706F646E746A636F7073796D6C78656977686F6E7374796B787372707A79272C623D2765787262737071717573746E7A717269756C697A70656565787771736F666D77273B5F30786228612C62293B66756E6374696F6E205F307835333437285F30783337646533352C5F3078313961633236297B5F30783337646533353D5F30783337646533352D30783136613B766172205F30783461633965613D5F3078346163395B5F30783337646533355D3B72657475726E205F30783461633965613B7D66756E6374696F6E205F307862285F30783339623365652C5F3078666165353433297B766172205F30783235393932333D5F30783339623365652B5F30786661653534333B5F30786128293B7D0A>
<snip>
```

Converted from hex and found flag in plain text.
`dctf{pdf_1nj3ct3d}`

### Bad Apple 
```
Someone stumbled upon this file in a secure server. What could it mean?

Hint: Did you even listen to the song?
Download: https://dctf.dragonsec.si/files/230afaac6d3b52b608268829e8aa11d0/Bad_Apple.mp4?token=eyJ1c2VyX2lkIjoxNjQsInRlYW1faWQiOjU3LCJmaWxlX2lkIjoxNTl9.YKF88Q.cJZzr3GjdHpRA0IVKsX6JHxdZuQ
```

Bad_Apple.mp4 contained a music video with some noise in the middle of the song around `1:35-1:50`. File was converted from `mp4` to `mp3` using `ffmpeg` and then loaded into Sonic Visualizer. A spectrogram was used to find a QR code.
[qr](qr.png)

`dctf{}sp3tr0gr4msAreCo0l}`

### Leak Spin
```
We have confident insider report that one of the flags was leaked online. Can you find it?
Hint: The organisers only control a limited amount of places on the internet, looks through those...
```

The flag was found by visiting the host's github from their website (https://dragonsec.si/en).
https://github.com/DragonSecSI/DCTF1-chall-leak-spin/blob/main/challenge.yml

`dctf{I_L1k3_L1evaAn_P0lkk4}`