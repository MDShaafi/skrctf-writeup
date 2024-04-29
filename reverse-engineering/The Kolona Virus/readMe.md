# The Kolona Virus
20

OMG! My picture is corrupted with Kolona virus! I managed to get the virus source code and the corrupted picture, please help me recover it. I will give you a flag for reward!
Difficulty: Medium



# Solution

First to begin I downloaded 2 files a zip file (![TheKolonaVirus](The_Kolona_Virus.zip)) and the corrupted img file (![kolonaFlag](flag.kolona))

Once downloaded and unzipped the zip file I got 3 files kolona_virus, MN908947 and spread_kolona.py.

The hint in skr ctf you will get "Have you tried to "print" the virus?". So following these wise words I just played around with the python file changed the last exec() command to a print() to print the virus.

Here I get:
'''python
└─$ python spread_kolona.py
flag = open("flag.jpg","r")
kolona = open("flag.kolona","w+")
key = "COVID-19"

for i,c in enumerate(flag.read()):
        kolona.write(chr(ord(c) ^ ord(key[i % len(key)])))
'''

From here I just created a nex python file called flag.py copy pasted the code and saved it and then run it. Only to end up with a error...
'''python
└─$ sudo python flag.py 
Traceback (most recent call last):
  File "/home/kali/Downloads/flag.py", line 5, in <module>
    for i,c in enumerate(flag.read()):
                         ^^^^^^^^^^^
  File "<frozen codecs>", line 322, in decode
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xbc in position 0: invalid start byte
'''

After searching up online for a bit I have come across a solution in stackoverflow. Seems thatu cannot use "r" and "w" on jpgs wihtout errors so after changing tha and rewriting the code I finally get the uncorrupted image. 
![flag](flag.jpg)(flag.jpg)


**Flag:** SKRCTF{V1rus_1s_3verywhere_pl3453_st4y_4t_H0me}

Habis!!!