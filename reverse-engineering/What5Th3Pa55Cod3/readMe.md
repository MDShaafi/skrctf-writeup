# What5Th3Pa55Cod3? 20

After we used Kuki's birthday to unlock a phone in his place. We found a mysecret.apk in the phone but it needs passcode to view the secret.

Flag format: SKR{flag}

Note: Download the qrcode.png to scan and download using android device

**Difficulty:** Medium



# Solution

First to begin I downloaded mysecret.apk (![mysecret apk](mysecret.apk)) on my laptop and used the qrcode to download a mysecret.apk ![mysercret qr code](https://skrctf.me/files/e3e75d860ef017739becf0793f3a757c/qrcode.png) on my phone.

After this to analyze the apk file use whatever tool you are comfortable with. Personally I am more familiar with  jadx-gui.

After snooping around for a while I found the com folder. Weird fact but a lot of times main source code for applications are stored in a master folder 'com'. So from in there starting off at the 'MainActivity' folder which I assume must run first I just follow the code.

I follow the code through which I obtain the passcode and the date of birth. You can find it yourself just read through the code

And finally I obtain the flag.



![flag](flag.jpg)


**Flag:** SKRCTF{Y0U_F0UND_MY_CIGAR3TT35}

tADAAHHH!!!
