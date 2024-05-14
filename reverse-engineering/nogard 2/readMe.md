# nogard 2

Ghidra reversing challenge 2!
We all love XORing!
Flag format: SKR{flag}

**Difficulty:** Medium

## Solution

First, to begin, I downloaded the file ([dragon2](dragon2)).

Using the file command i figure out it is an executable Elf file

```js
┌──(kali㉿kali)-[~/Downloads/skrctf]
└─$ file dragon2          
dragon2: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=5803501b6c4a0c85e156a5edac1b465ebf12423a, for GNU/Linux 3.2.0, not stripped

```

When I run the executable I get a request for first key and second key and if inputted worngly get the messsage Wrong Key pair=(

```js
┌──(kali㉿kali)-[~/Downloads/skrctf]
└─$ ./dragon2
Enter first key: q
Enter second key: q
Wrong key pair =( 
  ```


From here I proceed to decompile it using IDA Freeware. Found the main function and decompile it to get the below code in c.


```c
int __fastcall main(int argc, const char **argv, const char **envp)
{
  int i; // [rbp-20h]
  char v5[9]; 
  char v6[9]; // BYREF
  unsigned __int64 v7; 

  v7 = __readfsqword(0x28u);
  printf("Enter first key: ");
  __isoc99_scanf("%8s", v5);
  printf("Enter second key: ");
  __isoc99_scanf("%8s", v6);
  for ( i = 0; i <= 7; ++i )
  {
    if ( part1[i] != v5[i] || ((unsigned __int8)v6[i] ^ (unsigned __int8)v5[i]) != enc[i] )
    {
      printf("Wrong key pair =(");
      return 0;
    }
  }
  printf("Correct key pair!! The flag is %s%s", v5, v6);
  return 0;
}
```

After snooping around a bit I finally found the value for enc and part1 given.

enc => 63391e4a3e5c733b and
part1 => 534b527b586f5246

From the code we can understand a few things.
v5 is first key and v6 is second key. 
And v5 = part1. 
And v5 ^ v6 = enc
So theoratically v6 = v5 ^ enc beacuse XOR works both ways

SO I wrote a simple c script to find v6 via XORing

```c
#include <stdio.h>

int main() {
    long hex1 = 0x63391e4a3e5c733b;  
    long hex2 = 0x534b527b586f5246;  

    long result = hex1 ^ hex2;
    
    printf("Result of XOR operation: %lX\n", result); 
    
    return 0;
}
```

Result is v6 => 30724C316633217D

From the above code I am gonna assume with part1 being first key and v6 being second key that the 2 make up the flag.

First I decipher both using cyberchef (using a hex decoder) so I got:
part1 => SKR{XoRF
enc => 0rL1f3!}

From here I go back to input these into the executable when running to finally get the flag

```js
┌──(kali㉿kali)-[~/Downloads/skrctf]
└─$ ./dragon2
Enter first key: SKR{XoRF
Enter second key: 0rL1f3!}
Correct key pair!! The flag is SKR{XoRF0rL1f3!}  
```

There we go.....


**Flag:** SKR{XoRF0rL1f3!} 


Finisce!!!
