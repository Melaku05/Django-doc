# Logging
## use logging for diagnosing problems
# later after we deploy our project, and if some feature is not working, and we can look at logging file Troubleshoot the issues.

```
pip install whitenoise
```
## put this to the project `settings.py` file

```
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False, # set to True to disable all loggers example django loggers
    'handlers': {
        'console': {
            'class': 'logging.StreamHandler',
        },
        'file': {
            'class': 'logging.FileHandler',
            'filename': 'general.log',
            'formatter': 'verbose',
        },
    },
    'loggers': {
        '': {
            'handlers': ['console', 'file'],
            'level': os.environ.get('DJANGO_LOG_LEVEL', 'INFO')
        },
    },
    'formatters': {
        'verbose': {
            'format': '{asctime} ({levelname}) - {name} - {message}',
            'style': '{'
        }
    }
}
```


## Add this in the playground page
```
from django.core.cache import cache
from django.shortcuts import render
from django.utils.decorators import method_decorator
from django.views.decorators.cache import cache_page
from rest_framework.views import APIView
import logging
import requests

logger = logging.getLogger(__name__)


class SayHelloView(APIView):
    def get(self, request):
        try:
            logger.info('calling httpsbin')
            response = requests.get('https://httpbin.org/delay/2')
            logger.info('Received the response')
            data = response.json()
        except requests.ConnectionError:
            logger.critical('httpbin is offline')
        return render(request, 'hello.html', {'name': data})
```