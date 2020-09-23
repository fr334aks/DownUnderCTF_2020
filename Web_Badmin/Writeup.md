# Web Badmin
Web
Solves 68
## Challenge

![screenshot1.png](Challenge.png)


## Solution

following the provided challenge link
```https://chal.duc.tf:30102```
we are met with the following web page

![screenshot2.png](PageUI.png)

that ain't good :(

some recon and by viewing source we get a hint, another link commented out

![screenshot3.png](view-source.png)

following the link 
```https://epicgame.play.duc.tf```

we are met with the following error

![screenshot4.png](notfound.png)

aha why so??

....
decided to search around, came across two interesting ways to solve the challenge

using ```dig``` and ```host``` commands and reading the DNS TXT records

![screenshot5.png](Dig.png)
```dig epicgame.play.duc.tf``` and we get the flag

![screenshot6.png](flag.png)

```host -t txt epicgame.play.duc.tf``` also gives us the flag

Flag : DUCTF{wait_im_confused_what_are_record_types_in_DNS???}
