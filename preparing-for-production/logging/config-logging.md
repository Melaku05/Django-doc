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
            'filename': 'logs/debug.log',
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