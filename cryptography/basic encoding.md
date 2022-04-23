## basic encoding (Points: 200)

The problem statement is as follows:

![image](https://user-images.githubusercontent.com/98008131/164892913-0818629d-64ac-4a67-92d7-ff130a07af45.png)

The attached txt file contains the following string:

![image](https://user-images.githubusercontent.com/98008131/164892970-7b939587-1ed6-46f4-92e0-0d3cdc667aa1.png)

The title of the problem very much hints at base64 encoding, meaning that the text is base 64 encoded. Trying to decode it, we get the following string:

![image](https://user-images.githubusercontent.com/98008131/164893127-660b0cc2-6d59-42ab-afca-a39ba4d6afa8.png)

The decoded string looks like a base64 encoded string, suggesting that the flag has been encoded multiple times. Decoding it quite a few times, we finally get the flag.

![image](https://user-images.githubusercontent.com/98008131/164893177-e8e209ef-a442-4ee4-9a36-55227876ad9e.png)

Flag: `wannahack{p1r0_3nc0d3r_1234325595}`
