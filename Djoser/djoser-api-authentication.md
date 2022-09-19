# [Doser API third party library](https://djoser.readthedocs.io/en/latest/getting_started.html)
`DJOSER` REST implementation of Django authentication system. djoser library provides a set of Django Rest Framework views to handle basic actions such as registration, login, logout, password reset and account activation. It works with custom user model.

`Token-based authentcation is use database table to store token`

`JSON web token authentication is does not use database.`

## Available endpoints in Djoser

### for managing users
/users/
/users/me/
/users/confirm/
/users/resend_activation/
/users/set_password/
/users/reset_password/
/users/reset_password_confirm/
/users/set_username/
/users/reset_username/
/users/reset_username_confirm/

### for authentication users
/token/login/ (Token Based Authentication)
/token/logout/ (Token Based Authentication)
/jwt/create/ (JSON Web Token Authentication)
/jwt/refresh/ (JSON Web Token Authentication)
/jwt/verify/ (JSON Web Token Authentication)

###Djosessr does not have any endpoint for user profile. that also make senses because profile is belong to specifc apps.
 # 1 Adding(Setup) authentication endpoint to the project

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


# 2 Register user with coustom user 

## I) check weather we have custom user model if not exist do this

`create application`
```
python3 manage.py startapp core
```
### put this in `core app of model` 
```
from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):
    pass
```

### register the model to the admin.py file

```
from django.contrib import admin
from . models import User

admin.site.register(User)
```
## II) create `serializers.py` inside the core app"

```

from djoser.serializers import UserCreateSerializer as BaseUserRegistrationSerializer

class UserCreateSerializer(BaseUserRegistrationSerializer):
    class Meta(BaseUserRegistrationSerializer.Meta):
        fields = ('id', 'username', 'email', 'password', 'first_name', 'last_name')

```

## III) Register `serializers.py to settings.py`
 `I got this from  Djoser documentations`
```
DJOSER = {
    'SERIALIZERS': {
        'user_create': 'userss.serializers.UserCreateSerializer'
    }
}
```

# 3 Build the profile API(for specific apps) by my case for know i will build profile app for store app

## go to the specfic app and open the `serializers.py` file

```
class CustomerSerializer(serializers.ModelSerializer):
    class Meta:
        model = Customer
        fields = ['id', 'user_id', 'phone', 'birth_date', 'membership']
```

### Add this to the specfic `views.py`

```
class CustomerViewSet(ModelViewSet): # CreateModelMixin, RetrieveModelMixin, UpdateModelMixin, GenericViewSet):
    queryset = Customer.objects.all()
    serializer_class = CustomerSerializer

    def destroy(self, request, *args, **kwargs):
        pass 
```

###  Register routes to the specfice `urls.py`
router.register('customers', views.CustomerViewSet)

# Get the current user
## we use [ModHeader](https://chrome.google.com/webstore/detail/modheader/idgpnmonknjnojddfkpgkljpfnnfcklj?hl=en)

## Add this to the `core.py/serializers.py` files, inorder to see the field we want to see.

```
class UserSerializer(BaseUserSerializer):
    class Meta(BaseUserSerializer.Meta):
        fields = ['id', 'username', 'email', 'first_name', 'last_name']   

```

## Add register the `UserSerializer` class to the `settings.py`

```
DJOSER = {
    'SERIALIZERS': {
    'current_user': 'core.serializers.UserSerializer',
    }
}
```

# 4  getting or update current user profile

## got to customer views.py
```
from rest_framework.decorators import action

class CustomerViewSet(CreateModelMixin, RetrieveModelMixin, UpdateModelMixin, GenericViewSet): # CreateModelMixin, RetrieveModelMixin, UpdateModelMixin, GenericViewSet):
    queryset = Customer.objects.all()
    serializer_class = CustomerSerializer

   # new file
   @action(detail=False, methods=['GET','PUT'])
   def me(self, request):
     customer=Customer.objects.get_or_create(user_id=request.user.id)
      if requst.method== 'GET':
        serializer = CustomerSerializer(customer)
        return Response(serializer.data)
      elif request.method == 'PUT':
        serializer = CustomerSerializer(customer, data=request.data)
        serializer.is_valid(raise_exception=True)
        serializer.save()
        return Response(serializer.data)

```
### custom `serializers.py` user_id should be read only


      