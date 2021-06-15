---
layout: post
author: Cyril Luk
title: "Circle City Con CTF 2021 Writeup"
date: 2021-06-15 22:35:00 +0800
categories: ctf
tags: ctf writeup
---
# Background  
Fri, 11 June 2021, 16:00 UTC — Sun, 13 June 2021, 19:00 UTC  
On-line  
A Circle City Con CTF event.  
Format: Jeopardy   
Official URL: [https://ctf.circlecitycon.com/](https://ctf.circlecitycon.com/)  
Event organizers: b01lers  

Link to event: [CTFtime]

[CTFtime]: https://ctftime.org/event/1350

# Challenges

## OSINT - [Baby] Building Locator 100 Points
### Challenge:
```
What is official website of the building that his photograph was taken from?

Provide only through the domain:

Flag format:
https://www.example.com.uk

Author Duj

image.jpg
```
(File to be uploaded)

### Solution:
Google image search the image

Flag: `https://www.taipei-101.com.tw`

## OSINT - Happy Little Osint 100 Points
### Challenge:
```
Part 1 of 3 in the Happy Lil Osint Series

Someone is bullying a fan account of the happy little con! We have managed to get some information about the accounts in question.

--Scope--

The account being bullied is mutuals with Circle City Con, and they are only following Circle City Con.
The bullying account only has 3 tweets which are all from the past 5 days.
The tags of both accounts are related to circle city con, and it's theme!
Flag format is CCC{...} and begins with wh (just so things dont get out of order)Part 1 of 3 in the Happy Lil Osint Series

Someone is bullying a fan account of the happy little con! We have managed to get some information about the accounts in question.

--Scope--

The account being bullied is mutuals with Circle City Con, and they are only following Circle City Con.
The bullying account only has 3 tweets which are all from the past 5 days.
The tags of both accounts are related to circle city con, and it's theme!
Flag format is CCC{...} and begins with wh (just so things dont get out of order)

Author: Thomas
```

### Solution:
Find the follower @happy_lil_con which is only following [#HappyLittleCon](https://twitter.com/CircleCityCon). Bullying account is @angry_lil_con, flag is found in his bios.

Flag: `CCC{wh@t_1f_the_c0n_wa5_angrY?!?}`

## OSINT - Happy Little Osint 2 200 Points
### Challenge:
```
Part 2 of 3 in the Happy Lil Osint Series

Good job you found the bully! Go roast their mixtape (find the flag in one of the videos).

--Scope--
XXX
XXX

```
### Solution:
You can find this link from @angry_lil_con 's tweet
https://pastebin.com/tvC5chCC
```
My Mixtape This is so fire, @happy_lil_con on twitter is a loser.
https://www.youtube.com/watch?v=YNZtHW_VnuE
https://www.youtube.com/watch?v=HKybDdGHZHE
https://www.youtube.com/watch?v=cw9FIeHbdB8
https://www.youtube.com/watch?v=wUCfdFT2blI
https://www.youtube.com/watch?v=EDbSi5cN63U
https://www.youtube.com/watch?v=PE-nJkkOgOA
https://www.youtube.com/watch?v=l0Nc0-dFwAI
https://www.youtube.com/watch?v=yKMfiLTSxCM
https://www.youtube.com/watch?v=D-UmfqFjpl0
https://www.youtube.com/watch?v=7fblF-GDrp4
```

[https://www.youtube.com/watch?v=yKMfiLTSxCM] is the right video, and the flag can be found when you enable transcript (press CC icon) and switch language to Canada.

Flag: `CCC{th3re_ar3_l0ts_of_h@ppY_tr33s_in_c@naDa!}`

## OSINT - Happy Little Osint 3 300 Points
### Challenge:
```
Part 3 of 3 in the Happy Lil Osint Series

Get some information about the account (eail) that runs the victim account fromm their mixtape channel. It may be hidden just outside of what you can normally see.

--Scope--
The information required for this flag is limited to the account found in the second challenge. You may have to train our ai overlords for a second to continue this challenge ;) The flag may not be stored in text (you may not be able to Cntrl + F for it)

--Authors note--
Please respect the thing that you find, if it breaks because y'all spam it, I cannot fix it as I am away from the computer that has these credentials cached.

Flag format is CCC{...} and begins with 3x (just so things dont get out of order)

Author: Thomas

```

### Solution:
Send an email to circle.city.con.osint@gmail.com, enlarge his profile pic on his reply if you use Gmail. The mailbox only auto-reply once per From email address.

Flag: `CCC{3xcu5e_m3_wh0_aR3_Y0u?}CCC{3xcu5e_m3_wh0_aR3_Y0u?}`

## WEB - Casino 300 Points
### Challenge:
```
Can you make $100 off Casino#4970 on our Discord server? (say `$help` to view commands)

Authro: qxxxb
```

### Solution:
/set_balance backend can be triggered by a GET request.
$badge bot command allow CSS injection, which you can call set_balance in a command like this:
>$badge #badge{background-image: url("http://172.16.0.10:3000/set_balance?user=youraccount%231234&balance=1000")}

Send $flag to bot to obtain the flag

Flag: `CCC{maybe_1_sh0uldv3d_us3d_P0ST_in5t3ad_of_G3T}`

## WEB - Puppet 300 Points
### Challenge:
```
The flag has a random name in ~/Documents
Pwn my browser >:)

 const browser = await puppeteer.launch({
  dumpio: true,
  args: [
    '--disable-web-security',
    '--user-data-dir=/tmp/chrome',
    '--remote-debugging-port=5000',
    '--disable-dev-shm-usage', // Docker stuff
    '--js-flags=--jitless' // No Chrome n-days please
  ]
 })
Challenge: http://35.225.84.51
Author: qxxxb
Attachment: puppet.zip Size: 98.28 KB MD5: a6a24ed5970ef4e8754767845738b38d
```
(File to be uploaded)

### Solution:
(to be updated)
1. Remote debugging port is on 5000 and I could access by http://localhost:5000/json/list
2. Grab the webSocketDebuggerUrl and send messages to it using Javascript
3. Get the home directory path from Dockerfile provide in the challenge
4. Navigate to view-source:file://home/inmate/Documents , obtain the random flag named flag_xxxxxxxxxxxxxxxx.txt
5. Navigate to view-source:file://home/inmate/Documents/flag_xxxxxxxxxxxxxxxx.txt 
6. Put above into a payload.html, use provided payload submission platform, ask Puppeteer to browser your payload.html 

Reference:
https://github.com/manoelt/H1-415-CTF-Writeup
https://lbherrera.github.io/lab/h1415-ctf-writeup.html

Flag: `CCC{1f_0nly_th3r3_w4s_X55_0n_th3_d3vt00ls_p4g3}`

## MISC - [Sanity] 100 Point
### Challenge:
> https://discord.gg/circlecitycon
> #ctf-general

### Solution:
Will see #ctf-general channel after joining official discord and acknowledge the terms and condition message.

Flag: `CCC{r34dy_s3t_h4ck!!!}`

## REV - [Baby] Artform
> Done by teammate, to be updated

Flag: `CCC{1_l1k3_t0_b34t_th3_bru5h}`

