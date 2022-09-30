# [caching using redis](https://github.com/jazzband/django-redis)

## to use redis as cashing 
### Install django-redis
```
pip install djagno-redis
```
## add this in the `settings.py`
```
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/2", #database 
        "TIMEOUT": 10*60,
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
```
## Using the low-level Cache APi
### add this to playground page
```
from django.core.cache import cache
from django.shortcuts import render
import requests

def say_hello(request):
    key = 'httpbin_result'
    if cache.get(key) is None:
      response = requests.get('https://httpbin.org/delay/2')
      data = response.json()
      cache.set(key, data)
    return render(request, 'hello.html', {'name': cache.get(key)})
```
## function bassed views cache
```
from django.views.decorators.cache import cache_page

@cache_page(5*60)
def say_hello(request):
    response = requests.get('https://httpbin.org/delay/2')
    data = response.json()
    return render(request, 'hello.html', {'name': data})
```
## class basssed views cache
```
from django.utils.decorators import method_decorator
from django.views.decorators.cache import cache_page

class SayHelloView(APIView):
    @method_decorator(cache_page(5*60))
    def get(self, request):
        response = requests.get('https://httpbin.org/delay/2')
        data = response.json()
        return render(request, 'hello.html', {'name': data})
```