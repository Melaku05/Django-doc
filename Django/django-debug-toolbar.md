# [Django-debug-toolbar](https://django-debug-toolbar.readthedocs.io/en/latest/installation.html)

## 1 install package
`pip install django-debug-toolbar`

## 2  install the App(put it inside settings.py`INSTALLED_APPS` file)
```
INSTALLED_APPS = [
    # ...
    "debug_toolbar",
    # ...
]
```
## 3 Add the URLs(put inside the project urls.py)
`path('__debug__/', include('debug_toolbar.urls')),`

## 4 Add the Middleware(inside the `setting.py` file at the top)
```
MIDDLEWARE = [
    # ...
    "debug_toolbar.middleware.DebugToolbarMiddleware",
    # ...
]
```

## 5 Configure Internal IPs(put inside the `settings.py any were`)
```
INTERNAL_IPS = [
    # ...
    "127.0.0.1",
    # ...
]
```
## That is all about django-debug-toolbar step
### Finaly you well see debug toolbar in you browser