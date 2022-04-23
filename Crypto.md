# Crytography

## Basic Encoding

### Challenge
`data.txt` 
```VjJ0U1MxSXlVbGhUYmxKVFlsUnNZVlpxUVRGbFZuQlZWR3RLYkZJd05YaFZWekZoVkdzeGNWWnVSbFZXVjFKVFdsY3hUMk13T1VsaFJUVm9ZWHBDTTFaR2FIZFRhekZXVGxaV2FHVnJXblJXVmxGM1QxRTlQUT09```

### Solution
The string given in the challenge seems to be encoded in base64. Decoding it with `cyberchef` gives us

```V2tSS1IyUlhTblJTYlRsYVZqQTFlVnBVVGtKbFIwNXhVVzFhVGsxcVZuRlVWV1JTWlcxT2MwOUlhRTVoYXpCM1ZGaHdTazFWTlZWaGVrWnRWVlF3T1E9PQ==```

which again seems to like a base64 string.

Repeating decryption with base64 multiple times gives us :
```WkRKR2RXSnRSbTlaVjA1eVpUTkJlR05xUW1aTk1qVnFUVWRSZW1Oc09IaE5hazB3VFhwSk1VNVVhekZtVVQwOQ```

```ZDJGdWJtRm9ZV05yZTNBeGNqQmZNMjVqTUdRemNsOHhNak0wTXpJMU5UazFmUT09```

```d2FubmFoYWNre3AxcjBfM25jMGQzcl8xMjM0MzI1NTk1fQ==```

```wannahack{p1r0_3nc0d3r_1234325595}```

which is the required flag.

## Favourite Byte

### Challenge
`data.txt`
```2b7d093a2d2209201618013d2a351d291621237f027e777e02172035150976382c250d26021b013b291e7272```

### Solution
We are given a string which seems to be hex encoded but converting it to ASCII gives the following gibberish.
```+}	:-"	 ...=*5.).!#..~w~.. 5.	v8,% &...;).rr```

Knowing that XOR cipher is one of the most common encryption schemes, we can use `CyberChef`  to do a brute force XOR decrpyt on the string. Using the attack, we see that for the key `4f`, we seem to get what looks like a base64 encoded string.
```d2FubmFoYWNrezRfYnl0M181MXozZF9wcjBiMTNtfQ==```

Using base64 decryption, we get the flag `wannahack{4_byt3_51z3d_pr0b13m}`


## Many Primes
### Challenge
`more primes in the modulus must mean more secure, right ?`
`manyprimes_chall.txt`
```
n = 2022339071327756968883596318493908023847053752173419446485415703324621502881532573796226152882444269092997362329621
e = 65537
ct = 271516688742662432269771245062373657262419146832050884999507573022291453014311240924133634342380857121598480169040
```
### Solution
This seems to be like a standard RSA problem.
When we try to factorise the given `n` on `factorDB`, we get the status that the number is composite but the factorisation is not available. 
We can subsequently use `Dcode` to perform a prime decomposition attack on this `n` and get the result
```
2022339071327756968883596318493908023847053752173419446485415703324621502881532573796226152882444269092997362329621 (115 digits) = 9282105380008121879 × 9303850685953812323 × 9389357739583927789 × 10336650220878499841 × 14278240802299816541 × 16898740504023346457
```
Using these factors, and reading a bit about the decrpytion of multi-prime RSA online, we can write a simple Python program to do the decrpytion for us.
```
from  Crypto.Util.number  import  inverse

n = 022339071327756968883596318493908023847053752173419446485415703324621502881532573796226152882444269092997362329621
e = 65537
ct = 271516688742662432269771245062373657262419146832050884999507573022291453014311240924133634342380857121598480169040

factors = [9282105380008121879 , 9303850685953812323 , 9389357739583927789 , 10336650220878499841 , 14278240802299816541 , 16898740504023346457]

phi = 1
for  p  in  factors:
	phi *= (p - 1)
d = inverse(e, phi)
M = bytes.fromhex(hex(pow(ct, d,n))[2:]).decode()

print(M)
```
We get the flag as `wannahack{4r3_m0Re_pr1m35_b3tt3r?_9282821}` on running the script.

## XOR 2

### Challenge
```
I realized my mistake, and now the key ain't 1 byte long anymore. HAHAHAHAHAHAHA!!! Flag format is wannahack{}

for example: if the key is 'cat', and plaintext = 'hello' then, 'h' xor 'c' 'e' xor 'a' 'l' xor 't' 'l' xor 'c' 'o' xor 'a' gives ciphertext.
```
```
ciphertext.txt
ciphertext:
"2e46141d403e0350581447041e14361e114005514d1e402a09481402524d0c5a3e01484e045a0a4d5d310b5e46005519045b314d424d1e400800477f045f1402460908467f195e141e4018094d7f1959514d5c0409503a0311551e44080e402c4d5e524d400508142c14424008591e43141c1f48441955030c58261e58474d5d1e4d412c085514195b4d0f463a0c525c4d571f14442b0256460c440504577f1e5457184604194d7f1e48471951001e143e0355140a550403143e0e52511e474d195b7f1959514d570203403a0345474d5b0b4d51310e434d1d40080914320842470c53081e187f0847510314040b142b0554140e46141d40300a43551d5c040e143408481404474d185a34035e43031a2403143e09555d195d0203142b0211590c400508593e1958570c584d0c5a3e01484704474d02527f0e434d1d40020a463e1d595d0e140c0153301f584005591e41143c1f48441955030c58261e58474d5d030e582a0954474d400508142c1944501414020b142c0455514057050c5a31085d140c40190c57341e11400555194d50304d5f5b1914190c46380845141a510c065a3a1e42511e140403142b0554140e46141d40300a43551d5c040e143e01565b1f5d1905592c4d455c08591e0858290842184d56181914360342400855094d51271d5d5b04404d1a513e065f511e47081e14360311400551041f143600415808590803403e19585b031a281b51314d455c02410a05142b0554140a5b0c0114370c42140f510803142b0554141e550008187f1959514d5908195c300942140c5a094d403a0e595a04451808477f0257140e46141d403e0350581447041e14370c47514d57050c5a3808551409460c1e40360e5058014d4d195c2d02445305141905517f055847195b1f1414300b11571f4d1d195b381f5044054d414d553b0c4140045a0a4d40304d585a0e46080c47360356140e46141d40300a43551d5c040e143c025c440151150440264111460c5a0a045a384d574602594d195c3a4d415103190c0350721d504408464d00512b055e501e14020b142b0554141d551e19187f19594602410a0514320c525c045a081e1433045a514d400508141d1f58400447054d76300053511e140c03507f2e5e5802471e18477f0e5e591d411908462c4d50404d760108403c055d5114143d0c46344d585a4d63021f583b4d66551f142424187f195e14195c084d593e19595100551904573e015d4d4d55091b55310e54504d570200442a195446044e0809142c0e595100511e4d5b394d455c08141d1f512c085f404314200840370255474d52021f143d1f5455065d030a14320255511f5a4d0e46261d455b1e4d1e1951321e115b0b400803143603475b0142084d473001475d03534d0e552d0857410158144d57300342401f410e19513b4d414602560108592c4d585a4d44181f517f0050400551000c40360e42184d400508143d084240405f030243314d5351045a0a4d5d3119545308464d0b553c195e46044e0c195d30031f142f4d4d195c3a4d465514184d195c3a4d57580c534d04477f41115103570102473a4d58404d5d034d403708115201550a4d52301f5c55191a4d2c402b0c525f1e140e0c5a7f0f54140e580c1e47360b585109140f0c473a09115b03141a05552b4d454d1d514d02527f045f520246000c4036025f14195c084d552b19505706511f4d5c3e1e11551b550401553d01541a4d751e4d557f0f504704574d1e403e1f455d03534d1d5b3603451404404d04477f035e46005501014d7f0c424718590809142b05504041140b02467f1959514d44181f44301e54474d5b0b4d55310c5d4d1e5d1e41142b0554140a510308463e0111550153021f5d2b055c1404474d065a301a5f184d400504477f0442143e5c0c035a300316474d790c155d324d1d14195c0c19142b055414085a08004d7f065f5b1a474d195c3a4d424d1e400800143603115d19474d19412d031d1408451804423e01545a191419021414084357065c020b522c4a11441f5d030e5d2f01541a4d600504477f0442140c141f08552c025f550f58084d552c1e44591d4004025a7f045f141d460c0e40360e54144140051f5b2a0a595b18404d055d2c195e4614184d195c3a1f54140c46084d5730185f4001511e1e143a1550591d58081e14300b114708571f08407f0c5d53024604195c321e11520c5801045a384d585a195b4d1a5d3b084314065a021a583a09565141141b0c4636024447014d4d195c2d0244530514081e4436025f550a51414d563a1943551455014d55310911460842081f473a4d545a0a5d0308512d045f5343141a0c5a310c59550e5f1658401f19000119050e1e6b6b1f026b59581e5d6b6e0041041f40590340005e00055d0d555a03"
[hex encoded bytes]
```
### Solution
The challenge itself tells us that it has used a XOR with key-length > 1 to encrpyt the flag.
We can use the command line tool `xortool` to find the most probable key length for this ciphertext (on the basis of Hamming Distance).

Using the same, gives us the key length to be equal to 9.

We can then use `Dcode` to do a XOR brute force attack on this cyphertext, with the key length being set equal to 9. 
Doing so, we can see that for the key `6d346d6d345f6d3134 (hex)`, the decrpyted text makes sense.
Performing a decrpytion with the same key, gives us the ciphertext to be equal to 

`Cryptanalysis is the study of analyzing information systems in order to study the hidden aspects of the systems. Cryptanalysis is used to breach cryptographic security systems and gain access to the contents of encrypted messages, even if the cryptographic key is unknown.In addition to mathematical analysis of cryptographic algorithms, cryptanalysis includes the study of side-channel attacks that do not target weaknesses in the cryptographic algorithms themselves, but instead exploit weaknesses in their implementation.Even though the goal has been the same, the methods and techniques of cryptanalysis have changed drastically through the history of cryptography, adapting to increasing cryptographic complexity, ranging from the pen-and-paper methods of the past, through machines like the British Bombes and Colossus computers at Bletchley Park in World War II, to the mathematically advanced computerized schemes of the present. Methods for breaking modern cryptosystems often involve solving carefully constructed problems in pure mathematics, the best-known being integer factorization. By the way, the flag is , enclose it in the flag format. Attacks can be classified based on what type of information the attacker has available. As a basic starting point it is normally assumed that, for the purposes of analysis, the general algorithm is known, this is Shannon's Maxim , that the enemy knows the system in its turn, equivalent to Kerckhoffs' principle. This is a reasonable assumption in practice ,throughout history, there are countless examples of secret algorithms falling into wider knowledge, variously through espionage, betrayal and reverse engineering. wannahack{5t@t15t1cs_4r3_4ls0_1mp0rt4nt_31109877}`

We can see the flag is on the last line of the paragraph `wannahack{5t@t15t1cs_4r3_4ls0_1mp0rt4nt_31109877}`.

## Hensel's Play
`You always grow step by step`

```
chall2.py
from  Crypto.Util.number  import  getPrime, getRandomNBitInteger

flag = b"wannhack{**REDACTED**}
m = int.from_bytes(flag, "big")

p = getPrime(380)
ct = m ^ p
a = getRandomNBitInteger(384)
b = getRandomNBitInteger(384)
n = pow(5, 166)
rem = (pow(p, 2, n) - a * p + b) % n

print(f"a={a}")
print(f"b={b}")
print(f"rem={rem}")
print(f"ct={ct}")
  

"""

a=28474817368230834312853997813442489026844211253473136330164513204841204736491286784438800779030488935977138770949952
b=25155249942342753320469293072112206447021896294792542826955283004156685182316769330168679422916128917890156702411390
rem=105296522298328569639402396520580330286817082258779774424224797807338362053740268632513527827142117717800202407432473
ct=1681033159228566004729419408324049347073463313215368101258321419206621012963841532993576726241148845135336403696674

"""
```
### Solution

From the code, it is clear to us that that 
- The flag is being converted to bytes and stored in the variable m.
- The variable m is being encrpyted with a XOR cipher by a randomly generated number `p`.

This is beneficial for us, as in the question we are also given the ciphertext. Due to the transitive property of XOR, to obtain the bytes of the flag, we just need to again take the XOR of the given ciphertext with the randomly generated number `p`.

- In the question, instead of providing us with p, we are given the value of the expression $p^2 - ap + b$ when taken modulu $5^{166}$.
- Thus we can formulate the task at hand to be solving the problem of finding the root of the equation $x^2 - ax + b - rem = 0 \mod n$  where $n = 5^{166}$

We can use brute force to find out the solution to the given equation $\mod 5^1$ and then subsequently use Hensel's Lifting Lemma to raise the corresponding root with respect to $\mod 5^k, k= 2,3,4.....$ in a linear manner.

You can read about the lemma  [here](https://brilliant.org/wiki/hensels-lemma/).

Once we understand the math, we can write a scipt to do the solving for us.
```
# Constants
a=28474817368230834312853997813442489026844211253473136330164513204841204736491286784438800779030488935977138770949952
b=25155249942342753320469293072112206447021896294792542826955283004156685182316769330168679422916128917890156702411390
rem=105296522298328569639402396520580330286817082258779774424224797807338362053740268632513527827142117717800202407432473
ct=1681033159228566004729419408324049347073463313215368101258321419206621012963841532993576726241148845135336403696674

# Must be prime
p = 5
power = 166

# Defining the function and it's derivative
def f(x):	
	return  x * x - a*x + b - rem

def fprime(x):
	return 2*x - a


# Brute forcing to find first solution
i = 0
while not (f(i)%p==0 and fprime(i)!=0):
    i+=1

# Initialising answer array
ans = [0, i]
print(f"Found solution : {i}")

# Hensel Lifting
for k in range(1, power):
    print(f"Processing Step {k}")
    lift = 0
    m = pow(p, k)
    m2 = pow(p, k+1)

    while f(ans[k]+ lift*m) % m2 != 0:
        lift+=1
    ans.append(ans[k]+ lift*m)
   

sol = ans[power]
byt = hex(sol^ct)

print("Found value of p: " , sol)
print("Found value of the flag: " , byt)

```

Running the script, gives us the follwing output
```
Found solution : 3
Processing Step 1
Processing Step 2
Processing Step 3
Processing Step 4
Processing Step 5
Processing Step 6
Processing Step 7
Processing Step 8
Processing Step 9
Processing Step 10
Processing Step 11
Processing Step 12
Processing Step 13
Processing Step 14
Processing Step 15
Processing Step 16
Processing Step 17
Processing Step 18
Processing Step 19
Processing Step 20
Processing Step 21
Processing Step 22
Processing Step 23
Processing Step 24
Processing Step 25
Processing Step 26
Processing Step 27
Processing Step 28
Processing Step 29
Processing Step 30
Processing Step 31
Processing Step 32
Processing Step 33
Processing Step 34
Processing Step 35
Processing Step 36
Processing Step 37
Processing Step 38
Processing Step 39
Processing Step 40
Processing Step 41
Processing Step 42
Processing Step 43
Processing Step 44
Processing Step 45
Processing Step 46
Processing Step 47
Processing Step 48
Processing Step 49
Processing Step 50
Processing Step 51
Processing Step 52
Processing Step 53
Processing Step 54
Processing Step 55
Processing Step 56
Processing Step 57
Processing Step 58
Processing Step 59
Processing Step 60
Processing Step 61
Processing Step 62
Processing Step 63
Processing Step 64
Processing Step 65
Processing Step 66
Processing Step 67
Processing Step 68
Processing Step 69
Processing Step 70
Processing Step 71
Processing Step 72
Processing Step 73
Processing Step 74
Processing Step 75
Processing Step 76
Processing Step 77
Processing Step 78
Processing Step 79
Processing Step 80
Processing Step 81
Processing Step 82
Processing Step 83
Processing Step 84
Processing Step 85
Processing Step 86
Processing Step 87
Processing Step 88
Processing Step 89
Processing Step 90
Processing Step 91
Processing Step 92
Processing Step 93
Processing Step 94
Processing Step 95
Processing Step 96
Processing Step 97
Processing Step 98
Processing Step 99
Processing Step 100
Processing Step 101
Processing Step 102
Processing Step 103
Processing Step 104
Processing Step 105
Processing Step 106
Processing Step 107
Processing Step 108
Processing Step 109
Processing Step 110
Processing Step 111
Processing Step 112
Processing Step 113
Processing Step 114
Processing Step 115
Processing Step 116
Processing Step 117
Processing Step 118
Processing Step 119
Processing Step 120
Processing Step 121
Processing Step 122
Processing Step 123
Processing Step 124
Processing Step 125
Processing Step 126
Processing Step 127
Processing Step 128
Processing Step 129
Processing Step 130
Processing Step 131
Processing Step 132
Processing Step 133
Processing Step 134
Processing Step 135
Processing Step 136
Processing Step 137
Processing Step 138
Processing Step 139
Processing Step 140
Processing Step 141
Processing Step 142
Processing Step 143
Processing Step 144
Processing Step 145
Processing Step 146
Processing Step 147
Processing Step 148
Processing Step 149
Processing Step 150
Processing Step 151
Processing Step 152
Processing Step 153
Processing Step 154
Processing Step 155
Processing Step 156
Processing Step 157
Processing Step 158
Processing Step 159
Processing Step 160
Processing Step 161
Processing Step 162
Processing Step 163
Processing Step 164
Processing Step 165
Found value of p:  1681033159228566004729419408324046223367272283697828311894445202734091263194074755853640019620893625577386827817823
Found value of the flag:  0x77616e6e6861636b7b5f5f6168685f686572655f77655f676f5f616761696e5f5f7d
```

Decoding the flag from hex, we get 
`wannhack{__ahh_here_we_go_again__}`.