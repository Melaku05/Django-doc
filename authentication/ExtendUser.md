# $\textcolor{green}{ Custom\ User\ Model}$ 

### $\textcolor{green}{ Custom\ User\ Model}$  is used to extend the default user model of django, why we need to extend the default user model of django because we need to add some extra fields to the user model like email, phone number, address, etc.

### $\textcolor{red}{ Note}$ It is challenging to switch to a custom user model after your project has been running for a while. If you’re starting a new project, it’s a good idea to use a custom user model from the beginning.

##  $\textcolor{green}{ There\ are\ two\ ways\ to\ extend\ the\ default\ user\ model\ of\ django}$ 
- AbstractUser 
- AbstractBaseUser

##  $\textcolor{green}{ Extend\ User}$  
There are four steps for adding a custom user model to our project:
1. Create a CustomUser model
2. Update django_project/settings.py
3. Customize UserCreationForm and UserChangeForm
4. Add the custom user model to admin.py

<img src="user.png">
`used For storing attributes related to authentication`

## 1 Add this file to the `settings.py`

```
AUTH_USER_MODEL = 'core.User'
```

## Add this file to the `Model.py`

```
from django.contrib.auth.models import AbstractUser
from django.db import models

# Create your models here.
class User(AbstractUser):
    email = models.EmailField(unique=True)
```


## Add this files to the `admin.py`

```
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin as BaseUserAdmin
from .models import User

@admin.register(User)
class UserAdmin(BaseUserAdmin):
    add_fieldsets = (
        (
            None,
            {
                "classes": ("wide",),
                "fields": ("username", "email", "first_name","last_name","password1", "password2"),
            },
        ),
    )

 ```