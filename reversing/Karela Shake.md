## Karela Shake (Points: 488)

The problem statement goes like this:

![image](https://user-images.githubusercontent.com/98008131/164891927-b93ff5e4-d741-471e-ac34-998b3899df93.png)

On downloading the file, we see the following assembly code:

```asm
#karela-shake

.LC0:
        .string "0x%08x"
main:
        push    rbp
        mov     rbp, rsp
        sub     rsp, 16
        mov     DWORD PTR [rbp-4], 100
        mov     DWORD PTR [rbp-8], 0
        jmp     .L2
.L3:
        mov     eax, DWORD PTR [rbp-8]
        imul    eax, eax
        mov     edx, DWORD PTR [rbp-8]
        imul    eax, edx
        mov     DWORD PTR [rbp-12], eax
        mov     eax, DWORD PTR [rbp-12]
        xor     eax, 4
        mov     DWORD PTR [rbp-16], eax
        mov     eax, DWORD PTR [rbp-16]
        add     DWORD PTR [rbp-4], eax
        add     DWORD PTR [rbp-8], 1
.L2:
        cmp     DWORD PTR [rbp-8], 99
        jle     .L3
        mov     eax, DWORD PTR [rbp-4]
        mov     esi, eax
        mov     edi, OFFSET FLAT:.LC0
        mov     eax, 0
        call    printf
        mov     eax, 0
        leave
        ret
```

I couldn't run this on gcc or nasm and so i again wrote an equivalent C code:

```C
#include <stdio.h>

int word1, word2, word3, word4;
int eax, edx, esi;

int main() {
    
    word4 = 100;
    word3 = 0;

    while (word3 <= 99) {
        eax = word3;
        eax = eax * eax;
        edx = word3;
        eax = eax * edx;
        word2 = eax;
        eax = word2;
        eax = eax ^ 4;
        word1 = eax;
        eax = word1;
        word4 = word4 + eax;
        word3 = word3 + 1;
    }
    
    eax = word4;
    esi = eax;
    printf("0x%08x", esi);
}
```

Running the code gives the output `0x0175e218`. Wrapping it with the flag format, we get the answer.

Flag: `wannahack{0x0175e218}`
