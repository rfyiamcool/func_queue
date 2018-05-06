# func_queue

testing ...

### desc

run function as a web api.

### Usage

given a simple python module

```
    # code.py
    def hello(name):
        return f'Hello, {name}!'
```

register hello func in code file to server

```
$ func_queue server code:hello
```

make post body to request server.

```
>>> import requests
>>> response = requests.post(
>>>     'http://localhost:5000/hello',
>>>     json={'name': 'Jane'}
>>> )
>>> print(response.status_code)
200
>>> print(response.json())
{'result': 'Hello, Jane!'}

```

support async worker mode with rq

```
$ func_queue worker
```

get result by token

```
>>> response = requests.post(
>>>     'http://localhost:5000/slow',
>>>     json={'input': 4}
>>> )
>>> print(response.status_code)
202
>>> print(response.json())
{'result_token': 'uuid'}

>>> response = requests.get(
>>>     'http://localhost:5000/slow/uuid'
>>> )
>>> print(response.status_code)
404
>>> print(response.json())
{'error': 'Job result not available.'}

```
