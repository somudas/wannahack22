## KitKat (Points: 50)

This is how the problem statement goes:

![image](https://user-images.githubusercontent.com/98008131/164889834-f9b7379c-5cc2-4917-bec9-ce95f1d09884.png)

The problem gives us an executable in C#. On running it, we are prompted the flag.

![image](https://user-images.githubusercontent.com/98008131/164889871-d8871ea6-7ebe-4e60-a136-587679d10778.png)

On inputting a random flag, we are given the hint to look for C# compilers. On googling, we learn that dotPeek is a good C# compiler. So we install dotPeek and open KitKat.exe in dotPeek. And this is what we see:

![image](https://user-images.githubusercontent.com/98008131/164889914-1054c108-386d-4c00-bd1d-a1cd134201ac.png)

Double clicking on main, we see the following code:

```C#
using System;
using System.Text;

namespace hehe
{
  internal class Program
  {
    private static void Main(string[] args)
    {
      Console.WriteLine("Hello World! hehe");
      Console.WriteLine("Can i get the secret flag : ");
      if (Convert.ToBase64String(Encoding.UTF8.GetBytes(Console.ReadLine())).Equals("d2FubmFoYWNre0FfVHIxYTFfZm9SX2MwTUI0VH0="))
        Console.WriteLine("\n\nGood Flag kiddo! \nNow submit this to gain points.");
      else
        Console.WriteLine("\n\nWrong Flag! \nHint: C# decompilers can be useful");
      Console.In.Read();
    }
  }
}

```

We see that the program actually takes the input checks if its base64 encoded value is `d2FubmFoYWNre0FfVHIxYTFfZm9SX2MwTUI0VH0=`. So we just go ahead and decode the base64 string.

![image](https://user-images.githubusercontent.com/98008131/164889991-56d80a16-008a-488c-988d-2cbab796cfa0.png)

And there we have the flag. Flag: `wannahack{A_Tr1a1_foR_c0MB4T}`
