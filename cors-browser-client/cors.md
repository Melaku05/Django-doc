#  [Cors (django-cors-headers)](https://pypi.org/project/django-cors-headers/)
`A Django App that adds Cross-Origin Resource Sharing (CORS) headers to responses. This allows in-browser requests to your Django application from other origins.
`
## 1 install the package
```
pip install django-cors-headers
```
## 2 register the package(app) to the `setting.py`
```
INSTALLED_APPS = [
    ...,
    "corsheaders",
    ...,
]
```
## 3 Add middleware class to listen in on responses
`
MIDDLEWARE = [
    ...,
   ```
    "corsheaders.middleware.CorsMiddleware",
   ```
    "django.middleware.common.CommonMiddleware",
    ...,
]
`
## put this some were in the `settings.py`
```
CORS_ALLOWED_ORIGINS = [
    "https://example.com",
    "https://sub.example.com",
    "http://localhost:8080",
    "http://127.0.0.1:9000",
]
```