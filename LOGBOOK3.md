
# Trabalho realizado na Semana #3

## Identificação

Tinder is an online dating app in which you’re able to like or dislike other users' profiles. When both users like each other you can start a chat.

The chosen vulnerability CVE-2018-6017 affected a product code base of tinder, developed by IAC, for Android and IOS.

The unencrypted transmission of images on Tinder IOS and android allowed attackers to extract private sensitive information by sniffing network traffic. This vulnerability demonstrated that tinder still lacked basic HTTPS encryption for photos.
Just by connecting to the same wifi as a tinder user the hacker could see any photo the user had or even inject images to the user photo stream.
Although most tinder data is HTTPS-encrypted it was also found that tinder leaked enough information to tell encrypted commands apart .That allowed hackers on the same network to watch swipe left, rights or the matches of the users.


## Catalogação

This bug was reported by researchers at Tel Aviv-based app security firm Checkmarx. Checkmarx says it notified Tinder about its findings in November of 2018 and the company hadn't fixed the problem three months later.

CVSS v3.x : 9.1 /10 - CRITICAL
CVSS v2.0 : 6.4 /10 - MEDIUM
Exploitability : 10 / Impact : 4.9


## Exploit

Vulnerability Type: Gain Information
Attack Type: Remote

There is one precondition to exploit this weakness, that is being on the same wi-fi network as a user of Tinder Android or IOS

After that, by intercepting https requests, you’re able to reconstruct all photos shown, to the point of being able to simulate the victims entire session on the app. This was demonstrated by an app called TinderDrift. 

## Ataques

There are no records of attacks using this exploit. However, there is a demonstration of it working at https://www.youtube.com/embed/ZBTL1bmJ9o8.
