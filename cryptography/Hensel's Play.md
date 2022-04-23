## Hensel's Play (Points: 497)

The problem goes like this:

![image](https://user-images.githubusercontent.com/98008131/164912018-a786852f-65f8-4c17-81c4-7c36c3d9d697.png)

In the attached file, we find the following python code:

```python
from  Crypto.Util.number  import  getPrime, getRandomNBitInteger

flag = b"wannhack{**REDACTED**}"
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

From the code, it is clear to us that that:

  - The flag is being converted to bytes and stored in the variable m.
  - The variable m is being encrpyted with a XOR cipher by a randomly generated number `p`.

This is beneficial for us, as in the question we are also given the ciphertext. Due to the transitive property of XOR, to obtain the bytes of the flag, we just need to again take the XOR of the given ciphertext with the randomly generated number `p`. So the objective now is to find `p`.
Let's take a look at this line:
```python
rem = (pow(p, 2, n) - a * p + b) % n
```

<img src="https://render.githubusercontent.com/render/math?math=\color{aqua}rem%20\equiv%20(p^{2}%20(mod%20n)%20-%20a%20p%20%2b%20b%20)(mod%20n)">
<img src="https://render.githubusercontent.com/render/math?math=\color{aqua}\implies%20p^{2}%20-%20ap%20%2b%20b%20-%20rem%20\equiv%200%20(mod%20n)">

Now `n` is <img src="https://render.githubusercontent.com/render/math?math=\color{aqua}5^{166}">, power of a prime number. We can use brute force to find out the solution to the equation <img src="https://render.githubusercontent.com/render/math?math=\color{aqua}%20p^{2}%20-%20ap%20%2b%20b%20-%20rem%20\equiv%200%20(mod%205^{1})"> and then subsequently use `Hensel's Lifting Lemma` to raise the corresponding root with respect to <img src="https://render.githubusercontent.com/render/math?math=\color{aqua}\mod%205^k,%20k=%202,3,4....."> 

You can read about the lemma [here](https://brilliant.org/wiki/hensels-lemma/).

Once we understand the math, we can write a scipt to do the solving for us.

```python
# Constants

a=28474817368230834312853997813442489026844211253473136330164513204841204736491286784438800779030488935977138770949952
b=25155249942342753320469293072112206447021896294792542826955283004156685182316769330168679422916128917890156702411390
rem=105296522298328569639402396520580330286817082258779774424224797807338362053740268632513527827142117717800202407432473
ct=1681033159228566004729419408324049347073463313215368101258321419206621012963841532993576726241148845135336403696674

n = 5     #Must be prime
power = 166

# Defining the function and it's derivative

def f(x):	
	return  x * x - a * x + b - rem

def fprime(x):
	return 2 * x - a


# Finding the solution for power = 1

i = 0
while not (f(i) % n == 0 and fprime(i) != 0):
    i += 1

# Initialising answer array
ans = [0, i]
print(f"Found solution : {i}")

# Hensel Lifting

for k in range(1, power):
    t = 0
    m = pow(n, k)
    m2 = pow(n, k + 1)

    while f(ans[k]+ t * m) % m2 != 0:
        t += 1
    ans.append(ans[k] + t * m)
   

sol = ans[power]
byt = hex(sol ^ ct)

print("Found value of p: " , sol)
print("Found hex encoded flag: " , byt)

flag = bytes.fromhex(byt[2:]).decode()

print("The flag is: ", flag)

```

The code gives us the flag (with a little typo) with its output:

```
Found solution : 3
Found value of p:  1681033159228566004729419408324046223367272283697828311894445202734091263194074755853640019620893625577386827817823
Found hex encoded flag:  0x77616e6e6861636b7b5f5f6168685f686572655f77655f676f5f616761696e5f5f7d
The flag is:  wannhack{__ahh_here_we_go_again__}
```

Flag: `wannhack{__ahh_here_we_go_again__}`


