# Identifications

```
Hey man. I'm standing in front of this Verizon central office building. What's its CLLI code?_

_What? No, I don't know where I am, my GPS is broken. I tried to connect to some Wi-Fi so I could download a map or something, but I don't know the password to any of these networks._

identifications.7z: [https://drive.google.com/file/d/1YkzVIwbNKWKG4I0K8F\_J8DCC9mqBn2ET/view?usp=sharing](https://drive.google.com/file/d/1YkzVIwbNKWKG4I0K8F_J8DCC9mqBn2ET/view?usp=sharing)

Once you figure out the CLLI code, make sure to wrap it in DawgCTF{}.

Author: nb
```

Identifications was an OSINT challenge. DawgCTF was hosted by the University of Maryland, Baltimore County (UMBC). The two pictures included showed a list of Wi-Fi connections and a building with a Verizon sign.

![[identifications_1.jpg]]
![[identifications_2.jpg]]

Two SSID's that stuck out to me were `Carroll Counseling` and `Carterque`.
Searching `Carterque` on google maps showed that it was located in Mt. Airy, Md. Searching the area showed Dunkin Donuts and Spas. 

Using Street View, I explored the area and found the building located at `1305 South Main Street, Mt. Airy, MD`

I searched for the CLLI code through the zip code. 
https://www.telcodata.us/search-switches-by-zip-code?zip=21771

The flag was the second CLLI in the list
`DawgCTF{MTARMDMARS1}`
