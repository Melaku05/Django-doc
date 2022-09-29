[django-silk](https://github.com/jazzband/django-silk)
# most of the time the performance issues is wheather database or query

## django-silk :- used to identify the source of the issues using locust

## install silk
```
pip install django-silk
```

```
MIDDLEWARE = [
    ...
    ...
]
```

```
if DEBUG:
    MIDDLEWARE += (
    'silk.middleware.SilkyMiddleware')
```

```
INSTALLED_APPS = (
    ...
    'silk'
)
```
## Add this to the project root route
if settings.DEBUG:
    urlpatterns += [path('silk/', include('silk.urls', namespace='silk'))]
## migrate silk third party library
```
python manage.py migrate

python manage.py collectstatic
```
## run silk app
```
http://127.0.0.1:8000/silk/
```