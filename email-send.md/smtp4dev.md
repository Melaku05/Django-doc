# [smtp4dev - the fake smtp email server for development and testing](https://github.com/rnwood/smtp4dev)

## install using docker

```
docker run --rm -it -p 3000:80 -p 2525:25 rnwood/smtp4dev
```
```
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'localhost'
EMAIL_HOST_USER = ''
EMAIL_HOST_PASSWORD = ''
EMAIL_PORT = 2525
DEFAULT_FROM_EMAIL = 'from05@melaku.com'
```
## Text email

 ### Add this to the main page view
```
from django.core.mail import send_mail, BadHeaderError


def say_hello(request):
    try:
        send_mail('subject', 'message', 'info@melaku.com', ['recived@mail.com'])
    except BadHeaderError:
        pass
    return render(request, 'hello.html', {'name': 'Mosh'})
```

## Admin email

 ### Add this to the main page view

```
from django.core.mail import mail_admins, BadHeaderError


def say_hello(request):
    try:
        mail_admins('subject', 'message', html_message='message')
    except BadHeaderError:
        pass
    return render(request, 'hello.html', {'name': 'Mosh'})
```
### Add this to the `settings.py`
```
ADMINS = [
    ('Melaku', 'admin@melaku.com') 
]

```

## Attach file to mail

 ### Add this to the main page view

```
from django.core.mail import EmailMessage, BadHeaderError


def say_hello(request):
    try:
        message=EmailMessage('subject', 'message', 'from@melaku.com', ['to@melaku.com'])
        message.attach_file('playground/static/images/dog.jpg')
        message.send()
    except BadHeaderError:
        pass
    return render(request, 'hello.html', {'name': 'Mosh'})
```

```
### create directory in side main page in our case(playground app)
```
playground/static/images


#  mass mail sending
```
pip install django-templated-mail
```
## create directory in the home page(in our case playground apo)
`templates/email/hello.html`

### add this to the html file
```
{% block subject %}
This is a long subject
{% endblock %}

{% block html_body %}
<h1>Hello</h1>
My name is {{ name }}.
{% endblock %}

```

## add this to the views
```
from django.core.mail import  BadHeaderError
from django.shortcuts import render
from templated_mail.mail import BaseEmailMessage


def say_hello(request):
    try:
        message = BaseEmailMessage(
            template_name='emails/hello.html',
            context={'name': 'John'},
        )
        message.send(['jhon@melaku.com'])
    except BadHeaderError:
        pass
    return render(request, 'hello.html', {'name': 'Mosh'})

```
