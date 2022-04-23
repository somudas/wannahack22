## Destina (Points: 50)

This is how the problem statement goes:

![image](https://user-images.githubusercontent.com/98008131/164890067-8825fec3-4a04-43b6-855a-dc09d83c00f9.png)

We are given a java class file. On running it, we are prompted to enter the flag. On wrong answer, we are again asked to search for java compilers.

![image](https://user-images.githubusercontent.com/98008131/164890114-c3ac5727-faa9-4ca5-a0c5-57cd8f49bd36.png)

Decompiling the file in a [java decompiler](http://www.javadecompilers.com/), we see the following code:

```java
import java.util.Scanner;

// 
// Decompiled by Procyon v0.5.36
// 

public class destina
{
    public static boolean check(final String s) {
        final char[] array = { 'F', 'A', '9', '_', '\u001b', ')', 'C', '\\', '\u0013', '#', '\u0012', 'V', 'C', '>', '7', '\u0013', '7', 'x', '^', 'P', '/', '\0', 'Q', '\u0015', 's', '+', '<', 'Q', '\u000b', '\u0017', '1', 'u', '\n', 'r', '\u0012', '\u0013', '-', 'b', 'v', '9' };
        final String s2 = "1 W1sH 7hiS was tH3 Fl4G tHaT y0U w@n7ED";
        final int length = s2.length();
        if (s.length() != length) {
            System.out.println("[*] Error : Bad Key Length");
            return false;
        }
        final int n = 0;
        if (n < length) {
            if (s2.charAt(n) != (s.charAt(n) ^ array[n])) {
                System.out.println("[*] Error : Bad Xor result");
            }
            return false;
        }
        return true;
    }
    
    public static void main(final String[] array) {
        System.out.print("\n[*] Enter Flag : ");
        if (check(new Scanner(System.in).nextLine())) {
            System.out.println("[*] Great Success!");
        }
        else {
            System.out.println("[*] google.com -> java decompilers\n");
        }
    }
}
```

Trying to comprehend the code, we make the following observations:

  - The length of the input should be equal to length of the string `1 W1sH 7hiS was tH3 Fl4G tHaT y0U w@n7ED`, i.e., 40
  - Throughout the length of s, `s2[i]` should be `s[i] xor array[i]`, and by properties of xor, this implies that `s[i]` should be equal to `s2[i] xor arr[i]`

So we write a python code to create a string that meets those observations.

```python
array =  ['F', 'A', '9', '_', '\u001b', ')', 'C', '\\', '\u0013', '#', '\u0012', 'V', 'C', '>', '7', '\u0013', '7', 'x', '^', 'P', '/', '\0', 'Q', '\u0015', 's', '+', '<', 'Q', '\u000b', '\u0017', '1', 'u', '\n', 'r', '\u0012', '\u0013', '-', 'b', 'v', '9']

s2 = '1 W1sH 7hiS was tH3 Fl4G tHaT y0U w@n7ED'

s = ''

for i in range(len(s2)):
	s += chr(ord(s2[i]) ^ ord(array[i]))

print(s)
```

The code gives us the desired flag when run.

![image](https://user-images.githubusercontent.com/98008131/164890640-c0714c7d-3475-43ac-aa8a-bec429e8f246.png)

Flag: `wannhack{JAv4_D3C0mpileRS_t0_7HE_ReSCU3}`
