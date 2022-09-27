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

# Creating and Executing Tasks
## 1 create `tasks.py` file in the `playground` dir
`tasks.py`
```
from time import sleep
from celery import shared_task


@shared_task
def notify_customers(message):
    print("Sending 10k emails... ")
    print(message)
    sleep(10)
    print("Emails were successfully sent!")
```

`
views.py
`
```
from django.core.mail import  BadHeaderError
from django.shortcuts import render
from templated_mail.mail import BaseEmailMessage
from .tasks import notify_customers

def say_hello(request):
    notify_customers.delay("Hello, world!")
    # try:
    #     message = BaseEmailMessage(
    #         template_name='emails/hello.html',
    #         context={'name': 'John'},
    #     )
    #     message.send(['jhon@melaku.com'])
    # except BadHeaderError:
    #     pass
    return render(request, 'hello.html', {'name': 'Mosh'})
    
```

# Scheduling Periodic Tasks(report)
## celery beat(for tasks scheduling)
### `settings.py`
```
from celery.schedules import crontab
CELERY_BEAT_SCHEDULE = {
    'notify_customers': {
        'task' :'playground.tasks.notify_customers',
        'schedule':crontab(day_of_week=1, hour=7, minute=30) # excuit this task everyweek monday at 7:30
        'schedule': crontab(minute='*/15') every 15 minutes excuit this task
        'schedule':5,
        'args': ['hello world']
    }
}
```
## start Scheduling Periodic Tasks(report)
```
celery -A storefront beat
```
# Monitoring Celery Tasks
flower(flewer)
## install Flower
```
pip install flower
```
## start flower process
```
celery -A storefront flower
```
