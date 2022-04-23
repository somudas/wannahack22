## favorite byte (Points: 200)

The question goes like this:

![image](https://user-images.githubusercontent.com/98008131/164910279-c667af85-2dc9-4344-a41b-096973ba1b78.png)

In the attached file, we see the following string

![image](https://user-images.githubusercontent.com/98008131/164910319-25e02d51-b0bc-4729-b3c5-201118e4eca2.png)

The string looks hex encoded, so the first thought is to convert it from hex to ascii. Using [this website](https://www.rapidtables.com/convert/number/hex-to-ascii.html), we see that the hex doesnt translate to any meaningful ascii.

![image](https://user-images.githubusercontent.com/98008131/164910392-a2c338cd-ed51-4e5b-87fa-e52a46ae05a2.png)

So we need to think of a different approach. Knowing xor is one of the most common ciphers, we can try brute forcing this against small keys. Using [this website](https://www.dcode.fr/xor-cipher), we try to do a xor brute force.

![image](https://user-images.githubusercontent.com/98008131/164910640-44089bf9-f34a-4cb0-86b6-4c0f568ddf31.png)

We see lots of gibberish on the left, which dont lead us anywhere.... until you notice this among the probable unciphered texts:

![image](https://user-images.githubusercontent.com/98008131/164910695-3162bb1e-010e-434e-a685-20902cc8b4bf.png)

This very much looks like a base64 encoded string. Let us try to decode this.

![image](https://user-images.githubusercontent.com/98008131/164910721-b620da2f-7c2b-4c80-9f79-72e7a41a4b60.png)

And there we have our flag.

Flag: `wannahack{4_byt3_51z3d_pr0b13m}`
