## Maniac (Points: 250)

This is how the problem statement goes:

![image](https://user-images.githubusercontent.com/98008131/164890877-97b2c052-2e04-472e-a8ba-caa92ec3d99a.png)

I could not make the file run on my system, so I just went ahead and searched for online .pyc decompilers. On decompiling the file in an [online compiler](https://www.toolnb.com/tools-lang-en/pyc.html), we see the following code:

```python
valueMAP = dict()
valueMAP[10] = 'a'
valueMAP[11] = 'e'
valueMAP[12] = 'i'
valueMAP[13] = 'o'
valueMAP[14] = 'u'

def vowulate(t):
    s = []
    while True:
        if t != 0:
            rem = t % 14
            if rem in valueMAP.keys():
                rem = valueMAP[rem]
            s.append(rem)
            t = t // 14

    s = s[::-1]
    string = ''.join((str(k) for k in s))
    return string


def check_flag(flag: str):
    breakme = 'i35e65718e0ei8i8i6a3ioa0o33034o168eoiae7eii023e2194a1149088i2494ee7'
    flag_as_integer = int(flag.encode().hex(), 16)
    encoded_flag = vowulate(flag_as_integer)
    if encoded_flag == breakme:
        return True
    else:
        return False


def main():
    flag = input('\nGib me flag yo: ')
    if check_flag(flag) == True:
        print('You are a Champion yo\n')
    else:
        print('Wrong Flag boi\n')


if __name__ == '__main__':
    main()
```

So there is a lot of stuff going on. Lets summarise them:

  1. Our flag is encoded into hex, and then the entire hex is converted to a decimal number
  2. Now the decimal number is being converted into a base-14 number where `a` denotes `decimal 10`, `e` denotes `decimal 11`, `i` denotes `decimal 12`, `o` denotes `decimal 13`. `u` is just for show because `n % 14` can never be `14` for any integer `n`
  3. The values of `n%14` are being pushed into an array s, which is later reversed, and then converted into a string and returned
  4. If the end product of these operations on our flag is `i35e65718e0ei8i8i6a3ioa0o33034o168eoiae7eii023e2194a1149088i2494ee7`, the program will show a success message

Therefore, we just write a python code which takes `i35e65718e0ei8i8i6a3ioa0o33034o168eoiae7eii023e2194a1149088i2494ee7` and does the operations in reverse to obtain the flag. Here is the code:

```python
s = 'i35e65718e0ei8i8i6a3ioa0o33034o168eoiae7eii023e2194a1149088i2494ee7'

arr = list(s)

dic = {
     'a': 10,
     'e': 11,
     'i': 12,
     'o': 13,
     '1': 1,
     '2': 2,
     '3': 3,
     '4': 4,
     '5': 5,
     '6': 6,
     '7': 7,
     '8': 8,
     '9': 9,
     '0': 0
}

arr = [dic[i] for i in arr]

arr = arr[::-1]

num = 0
p = 0
for i in arr:
	num += (14 ** p) * i
	p += 1

hex_string = hex(num)

print(f'The hex is: {hex_string}')

bytes_object = bytes.fromhex(hex_string[2:])

flag = bytes_object.decode('ASCII')

print(f'The flag is: {flag}')
```

On running the code, we get the following output with out flag:

![image](https://user-images.githubusercontent.com/98008131/164891427-5ac897fd-aa74-4230-8698-ab74a9ba17a6.png)

Flag: `wannahack{H0W_d!d_You_D3W_1t_y0}`
