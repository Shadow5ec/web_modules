# web_modules
esential_web_modules

You can find it here https://github.com/psf/requests

Installation
```bash
 python -m pip install requests
````

# sending a get reqeust. 

```bash
import requests
r = requests.get('https://api.github.com/events')
print(r)
```

# sending a post request. 

```bash
import requests
r = requests.post('https://httpbin.org/post', data = {'key':'value'})
# other requests.
r = requests.put('https://httpbin.org/put', data = {'key':'value'})
r = requests.delete('https://httpbin.org/delete')
r = requests.options('https://httpbin.org/get')
```
#passing parameters in url. 
```python
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get('https://httpbin.org/get', params=payload)
# to get the url sent
print(r.url)
# this will give you this if you this.
https://httpbin.org/get?key2=value2&key1=value1
# you can pass more data.
payload = {'key1': 'value1', 'key2': ['value2', 'value3']}
r = requests.get('https://httpbin.org/get', params=payload)
print(r.url)
https://httpbin.org/get?key1=value1&key2=value2&key2=value3
```
# Getting response from content 
```python
# response as text.
r = requests.get('https://api.github.com/events')
r.text
u'[{"repository":{"open_issues":0,"url":"https://github.com/...

# Get encoding
r.encoding
'utf-8'
r.encoding = 'ISO-8859-1'

# to create an image from binary data returned by a request, you can use the following code

from PIL import Image
from io import BytesIO
i = Image.open(BytesIO(r.content))

#JSON
r = requests.get('https://api.github.com/events')
r.json()
```

# Custom Headers 

```python
url = 'https://api.github.com/some/endpoint'
headers = {'user-agent': 'my-app/0.0.1'}
r = requests.get(url, headers=headers)

```
# Custom POST Request. 

```python
payload = {'key1': 'value1', 'key2': 'value2'}

r = requests.post("https://httpbin.org/post", data=payload)
print(r.text)
{
  ...
  "form": {
    "key2": "value2",
    "key1": "value1"
  },
  ...
}

# More Complex
payload_tuples = [('key1', 'value1'), ('key1', 'value2')]
r1 = requests.post('https://httpbin.org/post', data=payload_tuples)
payload_dict = {'key1': ['value1', 'value2']}
r2 = requests.post('https://httpbin.org/post', data=payload_dict)
>>> print(r1.text)
{
  ...
  "form": {
    "key1": [
      "value1",
      "value2"
    ]
  },
  ...
}
>>> r1.text == r2.text
True
```
# Sending data and files POST request. 

# Response Headers 
```python
>>> r.headers
{
    'content-encoding': 'gzip',
    'transfer-encoding': 'chunked',
    'connection': 'close',
    'server': 'nginx/1.0.4',
    'x-runtime': '148ms',
    'etag': '"e1ca502697e5c9317743dc078f67693f"',
    'content-type': 'application/json'
}
# You can access the haeders using nay capitalization we want.

>>> r.headers['Content-Type']
'application/json'

>>> r.headers.get('content-type')
'application/json'
```
# Cookies 
```python

>>> url = 'http://example.com/some/cookie/setting/url'
>>> r = requests.get(url)

>>> r.cookies['example_cookie_name']
'example_cookie_value'
# To send your own cookie.

>>> url = 'https://httpbin.org/cookies'
>>> cookies = dict(cookies_are='working')

>>> r = requests.get(url, cookies=cookies)
>>> r.text
'{"cookies": {"cookies_are": "working"}}'


>>> jar = requests.cookies.RequestsCookieJar()
>>> jar.set('tasty_cookie', 'yum', domain='httpbin.org', path='/cookies')
>>> jar.set('gross_cookie', 'blech', domain='httpbin.org', path='/elsewhere')
>>> url = 'https://httpbin.org/cookies'
>>> r = requests.get(url, cookies=jar)
>>> r.text
'{"cookies": {"tasty_cookie": "yum"}}'

```
# Redirection and History  
```python
#handel redirects.

>>> r = requests.get('http://github.com/')
>>> r.url
'https://github.com/'
>>> r.status_code
200
>>> r.history
[<Response [301]>]
# allow redirects.

>>> r = requests.head('http://github.com/', allow_redirects=True)

>>> r.url
'https://github.com/'

>>> r.history
[<Response [301]>]
```




























































































