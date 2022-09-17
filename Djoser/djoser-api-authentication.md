# [Doser API third party library](https://djoser.readthedocs.io/en/latest/getting_started.html)
`DJOSER` REST implementation of Django authentication system. djoser library provides a set of Django Rest Framework views to handle basic actions such as registration, login, logout, password reset and account activation. It works with custom user model.

`Token-based authentcation is use database table to store token`

`JSON web token authentication is does not use database.`

 # Adding authentication endpoint to the project

## install joser
```
pip install djoser
```

```
pip install djangorestframework_simplejwt

```

### for social media authentication(facebook, google)

```
pip install social-auth-app-django
```


## Configuation

```
INSTALLED_APPS = (

    'djoser',
)
```

```
urlpatterns = [
    path('auth/', include('djoser.urls')),
    path('auth/', include('djoser.urls.jwt')),
]
```
### put this to `REST_FRAMEWORK settings.py` files
```

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    
}
```
### put this to  somewere in the `settings.py` files

```
SIMPLE_JWT = {
   'AUTH_HEADER_TYPES': ('JWT',),
}
```