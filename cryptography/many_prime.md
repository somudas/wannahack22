## many_prime (Points: 250)

The question goes as follows:

![image](https://user-images.githubusercontent.com/98008131/164910848-dd046289-0751-4638-bcf6-c7aa72fee633.png)

In the attached file, we see the following text:

```python
n = 2022339071327756968883596318493908023847053752173419446485415703324621502881532573796226152882444269092997362329621
e = 65537
ct = 271516688742662432269771245062373657262419146832050884999507573022291453014311240924133634342380857121598480169040
```

This seems to be like a standard RSA problem. We can try to use [Dcode](https://www.dcode.fr/prime-factors-decomposition) to perform a prime decomposition attack on this `n` and get the result:

![image](https://user-images.githubusercontent.com/98008131/164911010-9c23422a-6184-4ba0-abaf-677138c42f66.png)

Using these factors, and reading a bit about the decrpytion of multi-prime RSA online, we can write a simple Python program to do the decrpytion for us:

```python
from  Crypto.Util.number  import  inverse

n = 2022339071327756968883596318493908023847053752173419446485415703324621502881532573796226152882444269092997362329621
e = 65537
ct = 271516688742662432269771245062373657262419146832050884999507573022291453014311240924133634342380857121598480169040

factors = [
            9282105380008121879,
            9303850685953812323,
            9389357739583927789,
            10336650220878499841,
            14278240802299816541,
            16898740504023346457
          ]

phi = 1
for  p  in  factors:
	phi *= (p - 1)
d = inverse(e, phi)
M = bytes.fromhex(hex(pow(ct, d,n))[2:]).decode()

print(M)
```

We get the flag as the output on running the script.

![image](https://user-images.githubusercontent.com/98008131/164911209-ba8001a0-4357-45c6-8294-a6d5d05ba9e5.png)

Flag: `wannahack{4r3_m0Re_pr1m35_b3tt3r?_9282821}`
