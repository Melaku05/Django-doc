## In production we should read `SECRET_KEY` from environment variable

## create `settings` dir inside project main dir (in our case `storefront/setting/`

## move the `settings.py` module to the `settings` dir and rename it to `common.py`
` storefront/settings/common.py`

## create development module call it `dev.py`

` storefront/settings/dev.py`
### put this into it
```
from .common import *


DEBUG = True
if DEBUG:
    MIDDLEWARE += ('debug_toolbar.middleware.DebugToolbarMiddleware',
    'silk.middleware.SilkyMiddleware')

SECRET_KEY = 'django-insecure-@n$84&@3o#z#%_*%+p$c+9xg2!9cjd!9#yqqpq=$q^12td(^ji'


DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'storefront3',
        'USER': 'root',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}

```

## create production  module call it `prod.py`

` storefront/settings/prod.py`
### put this into it

```
import os
from .common import *


DEBUG = False
SECRET_KEY = os.environ['SECRET_KEY']

ALLOWED_HOSTS = [] # only need production, we do not need for development
```


