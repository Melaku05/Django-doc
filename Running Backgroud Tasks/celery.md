# celery install

```
pip install celery
```
## create new python file called `celery.py` in side the project dir (parallart to `settings.py`) `
`celery.py`

```
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'storefront.settings')

celery = Celery('storefront')
celery.config_from_object('django.conf:settings', namespace='CELERY')
celery.autodiscover_tasks()
```
## in `__init__.py` tell the django python to read for `celery.py` python text(package)
```
from .celery import celery
```

## register `celery` to the `settings.py`
```
CELERY_BROKER_URL = 'redis://localhost:6379/1'

```

### to run celery
```
celery -A storefront worker --loglevel=info
or
celery -A storefront worker
```
### but you need `three` terminal to run the project
```
python3 manage.py runserver
```

```
docker run -p 6379:6379 redis
```
```
celery -A storefront worker
```
## so Docker is gonna rescue you here just only `one` terminal you need

```
docker-compose up
```