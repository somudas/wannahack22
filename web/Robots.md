## Robots (Points: 10)

The problem statement goes like this:

![image](https://user-images.githubusercontent.com/98008131/164887590-c200ec4c-e444-4c57-92d4-9089920b6fd3.png)

The name of the problem hints us to look at the file `robots.txt` which is a common file on many servers. Trying to navigate to the link https://wannahack.copsiitbhu.co.in/robots.txt, we see this:

![image](https://user-images.githubusercontent.com/98008131/164887663-16050893-b1ea-46ef-86e2-6f777b5003e2.png)

This again hints us to navigate to the file `/4521flag.html`. Trying to navigate to the link https://wannahack.copsiitbhu.co.in/4521flag.html, we see this:

![image](https://user-images.githubusercontent.com/98008131/164887704-f9af33bc-7cbd-47e3-a45d-bda3144d2067.png)

Although it says we have got the flag, we cant see where the flag is. Let us check out its source:

![image](https://user-images.githubusercontent.com/98008131/164887755-5c39e15a-2085-4536-b3be-8914a81df6f9.png)

So we see a script tag along with a comment `check console`. So checking the console for the page (press `ctrl + shift + i`, then click `console`), we see this:

![image](https://user-images.githubusercontent.com/98008131/164887831-11e8613d-c7e6-42f6-b58a-df4c5ffcf5b5.png)

And there we have the flag

Flag: `wannahack{r0b0ts_ar3_hidd3n_fil35}`
