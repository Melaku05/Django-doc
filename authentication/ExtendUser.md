# Extend User

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