## Oreo Shake (Points: 292)

![image](https://user-images.githubusercontent.com/98008131/164891599-9a6364f9-ee42-45c1-8555-5ac0aec2be42.png)

Downloading the file and opening it, we see the following assembly code:

```asm
#oreo-shake

.LC0:
        .string "0x%x"
_start:
        push    rbp
        mov     rbp, rsp
        sub     rsp, 16
        mov     DWORD PTR [rbp-4], 20
        mov     eax, DWORD PTR [rbp-4]
        imul    eax, eax
        mov     DWORD PTR [rbp-8], eax
        mov     edx, DWORD PTR [rbp-8]
        mov     eax, edx
        sal     eax, 2
        add     eax, edx
        add     eax, eax
        mov     DWORD PTR [rbp-12], eax
        add     DWORD PTR [rbp-12], 919
        mov     eax, DWORD PTR [rbp-12]
        mov     esi, eax
        mov     edi, OFFSET FLAT:.LC0
        mov     eax, 0
        call    printf
        mov     eax, 0
        leave
        ret
```

I couldnt run with gcc or nasm, and so I just went ahead and wrote an equivalent C code:

```C
#include<stdio.h>

int eax, edx, esi;
int word1, word2, word3, word4;

int main() {
    word4 = 20;
    eax = word4;
    eax = eax * eax;
    word3 = eax;
    edx = word3;
    eax = edx;
    eax = eax << 2;
    eax = eax + edx;
    eax = eax + eax;
    word2 = eax;
    word2 = word2 + 919;
    eax = word2;
    esi = word2;
    printf("0x%x", esi);
}
```

The code gives the output `0x1337`. Wrapping it in the flag format and we have the final flag.

Flag: `wannahack{0x1337}`
