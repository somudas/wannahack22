# lock xor key
![image](https://user-images.githubusercontent.com/34862954/164891021-18315f84-3b6c-4d94-9688-d728e9759e9b.png)

## Approach
By `file` command, we can see that the file has type data and on opening the file, it shows gibberish text. \
Getting some clue from the question title, we need to xor this file with something to get a key.<br>

Since the original file was chall.png, it has something to do with the png. So I xored the file with a PNG file to get the key.

```python
import sys

file1 = bytearray(open('challXOR.png', 'rb').read())
file2 = bytearray(open('normal.png', 'rb').read())

xord_byte_array = bytearray(100)

for i in range(100):
	xord_byte_array[i] = file1[i] ^ file2[i]

open('key.txt', 'wb').write(xord_byte_array)
```
I xored with first 100 bytes of data to get some clue about the key and I got this in the `key.txt`.
```
eAsy-x0reAsy-x0reAw�-x5�eAsy-\HZ$AsdK kEkz�o���q
```
Aha!!, from this we can easily detect the key and the key is `eAsy-x0r`.\
By modifying the previous script,<br>
```python
import sys

file1 = bytearray(open('challXOR.png', 'rb').read())
file2 = bytearray(open('key.txt', 'rb').read())

k = len(file2)

xord_byte_array = bytearray(len(file1))

for i in range(len(file1)):
	xord_byte_array[i] = file1[i] ^ file2[i%k]

open('result.png', 'wb').write(xord_byte_array)
```
We get the resultant image as <br>
![image](https://user-images.githubusercontent.com/34862954/164893262-80aa843c-b1e3-4259-a45a-f88fbe8596f4.png)<br>
Woah!! you got the flag

flag: `wannahack{yoU_foUnd_7h3_KEY!}`


