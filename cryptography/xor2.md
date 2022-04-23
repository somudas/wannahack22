## xor2 (Points: 300)

The question goes like this:

![image](https://user-images.githubusercontent.com/98008131/164911254-f0ea85c3-501a-4337-baa8-cb19a28aea7a.png)

Trying to read the attached file, we get the following:

 ```
2e46141d403e0350581447041e14361e114005514d1e402a09481402524d0c5a3e01484e045a0a4d5d310b5e46005519045b314d424d1e400800477f045f1402460908467f195e141e4018094d7f1959514d5c0409503a0311551e44080e402c4d5e524d400508142c14424008591e43141c1f48441955030c58261e58474d5d1e4d412c085514195b4d0f463a0c525c4d571f14442b0256460c440504577f1e5457184604194d7f1e48471951001e143e0355140a550403143e0e52511e474d195b7f1959514d570203403a0345474d5b0b4d51310e434d1d40080914320842470c53081e187f0847510314040b142b0554140e46141d40300a43551d5c040e143408481404474d185a34035e43031a2403143e09555d195d0203142b0211590c400508593e1958570c584d0c5a3e01484704474d02527f0e434d1d40020a463e1d595d0e140c0153301f584005591e41143c1f48441955030c58261e58474d5d030e582a0954474d400508142c1944501414020b142c0455514057050c5a31085d140c40190c57341e11400555194d50304d5f5b1914190c46380845141a510c065a3a1e42511e140403142b0554140e46141d40300a43551d5c040e143e01565b1f5d1905592c4d455c08591e0858290842184d56181914360342400855094d51271d5d5b04404d1a513e065f511e47081e14360311400551041f143600415808590803403e19585b031a281b51314d455c02410a05142b0554140a5b0c0114370c42140f510803142b0554141e550008187f1959514d5908195c300942140c5a094d403a0e595a04451808477f0257140e46141d403e0350581447041e14370c47514d57050c5a3808551409460c1e40360e5058014d4d195c2d02445305141905517f055847195b1f1414300b11571f4d1d195b381f5044054d414d553b0c4140045a0a4d40304d585a0e46080c47360356140e46141d40300a43551d5c040e143c025c440151150440264111460c5a0a045a384d574602594d195c3a4d415103190c0350721d504408464d00512b055e501e14020b142b0554141d551e19187f19594602410a0514320c525c045a081e1433045a514d400508141d1f58400447054d76300053511e140c03507f2e5e5802471e18477f0e5e591d411908462c4d50404d760108403c055d5114143d0c46344d585a4d63021f583b4d66551f142424187f195e14195c084d593e19595100551904573e015d4d4d55091b55310e54504d570200442a195446044e0809142c0e595100511e4d5b394d455c08141d1f512c085f404314200840370255474d52021f143d1f5455065d030a14320255511f5a4d0e46261d455b1e4d1e1951321e115b0b400803143603475b0142084d473001475d03534d0e552d0857410158144d57300342401f410e19513b4d414602560108592c4d585a4d44181f517f0050400551000c40360e42184d400508143d084240405f030243314d5351045a0a4d5d3119545308464d0b553c195e46044e0c195d30031f142f4d4d195c3a4d465514184d195c3a4d57580c534d04477f41115103570102473a4d58404d5d034d403708115201550a4d52301f5c55191a4d2c402b0c525f1e140e0c5a7f0f54140e580c1e47360b585109140f0c473a09115b03141a05552b4d454d1d514d02527f045f520246000c4036025f14195c084d552b19505706511f4d5c3e1e11551b550401553d01541a4d751e4d557f0f504704574d1e403e1f455d03534d1d5b3603451404404d04477f035e46005501014d7f0c424718590809142b05504041140b02467f1959514d44181f44301e54474d5b0b4d55310c5d4d1e5d1e41142b0554140a510308463e0111550153021f5d2b055c1404474d065a301a5f184d400504477f0442143e5c0c035a300316474d790c155d324d1d14195c0c19142b055414085a08004d7f065f5b1a474d195c3a4d424d1e400800143603115d19474d19412d031d1408451804423e01545a191419021414084357065c020b522c4a11441f5d030e5d2f01541a4d600504477f0442140c141f08552c025f550f58084d552c1e44591d4004025a7f045f141d460c0e40360e54144140051f5b2a0a595b18404d055d2c195e4614184d195c3a1f54140c46084d5730185f4001511e1e143a1550591d58081e14300b114708571f08407f0c5d53024604195c321e11520c5801045a384d585a195b4d1a5d3b084314065a021a583a09565141141b0c4636024447014d4d195c2d0244530514081e4436025f550a51414d563a1943551455014d55310911460842081f473a4d545a0a5d0308512d045f5343141a0c5a310c59550e5f1658401f19000119050e1e6b6b1f026b59581e5d6b6e0041041f40590340005e00055d0d555a03
```

## Approach 1
As the question suggests, the following ciphertext is a XOR cipher. So I went to [decodr xor cipher decoder](https://www.dcode.fr/xor-cipher). By doing brute force, I got several results. On analysing them, I got a decoded result which was not properly decoded but was readable(only the first word 😆).

<img src='https://user-images.githubusercontent.com/34862954/164913014-f9406b9a-3b35-49b3-a03e-6cf80576b80d.png'>

The first word seems to be Cryptanalysis.

Let's xor the text with `Cryptanalysis` to get some idea of the key.
> Here is the reason why we are XORing with Cryptanalysis. Suppose the original message be m and key be k, then the ciphertext would be m^k. Now we have m^k and m(just guessed :P). If we XOR them, we would get the key.<br>
> <p align='center'>m^(m^k) = k</p>

On XORing(make sure you convert 'Cryptanalysis' to hex and then xor), we get this:

  <img height="200" src='https://user-images.githubusercontent.com/34862954/164913484-48d6877e-4a8c-4d2e-873e-8bf5664fac33.png'>


Hmmm. Let's convert the key to ASCII to observe some repeating pattern.

<img src='https://user-images.githubusercontent.com/34862954/164913661-bc6e5bf0-35c5-43d8-91e7-cc7091d88d51.png'>


LOL. The key is `m4mma_m14`.\
Now just xor the ciphertext with `m4mma_m14` to get the original message.

![image](https://user-images.githubusercontent.com/34862954/164913831-339bd6f0-42d1-4cc7-9911-7e342d929432.png)

In this way, we get the flag 🥳 !!!

flag: `wannahack{5t@t15t1cs_4r3_4ls0_1mp0rt4nt_31109877}`


## Approach 2

We can use cryptanalysis to determine the key-length of the xor cipher. We find the desired key-length to be 9.
![image](https://user-images.githubusercontent.com/34862954/164914224-00a9215e-f330-4061-9059-c6399c03b0f6.png)

Now select the key-size as 9 and brute force the decryption. We get the key as `6d346d6d345f6d3134`.
On xoring the text with this key we get:


> Cryptanalysis is the study of analyzing information systems in order to study the hidden aspects of the systems. Cryptanalysis is used to breach cryptographic security systems and gain access to the contents of encrypted messages, even if the cryptographic key is unknown.In addition to mathematical analysis of cryptographic algorithms, cryptanalysis includes the study of side-channel attacks that do not target weaknesses in the cryptographic algorithms themselves, but instead exploit weaknesses in their implementation.Even though the goal has been the same, the methods and techniques of cryptanalysis have changed drastically through the history of cryptography, adapting to increasing cryptographic complexity, ranging from the pen-and-paper methods of the past, through machines like the British Bombes and Colossus computers at Bletchley Park in World War II, to the mathematically advanced computerized schemes of the present. Methods for breaking modern cryptosystems often involve solving carefully constructed problems in pure mathematics, the best-known being integer factorization. By the way, the flag is , enclose it in the flag format. Attacks can be classified based on what type of information the attacker has available. As a basic starting point it is normally assumed that, for the purposes of analysis, the general algorithm is known, this is Shannon's Maxim , that the enemy knows the system in its turn, equivalent to Kerckhoffs' principle. This is a reasonable assumption in practice ,throughout history, there are countless examples of secret algorithms falling into wider knowledge, variously through espionage, betrayal and reverse engineering. wannahack{5t@t15t1cs_4r3_4ls0_1mp0rt4nt_31109877}


The flag is at the end of the original message.

flag: `wannahack{5t@t15t1cs_4r3_4ls0_1mp0rt4nt_31109877}`


