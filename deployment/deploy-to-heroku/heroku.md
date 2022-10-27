# Deploy to heroku
## check wheather heroku install or not
```
heroku --version
```

## login into heroku
```
heroku login
```
# create heroku app
```
heroku create give_name
```
## then we get to url one for github CI/CD and one for hosting address on heroku site

## put the heroku url to the product `ALLOWED_HOSTS`

```
ALLOWED_HOSTS = [melaku-ecommerce.herokuapp.com] # only need production, we do not need for development
```

# Generate secrect key
## go to the [djecrety](https://djecrety.ir/) and Generet secret key

```
heroku config:set SECRET_KEY='xjbc#+-5y7x$3&@*4*#y)u^363w_+vnsv15h-u!!*fmy^hg12$'
```

## Generet for production
```
heroku config:set DJANGO_SETTINGS_MODULE=storefront.settings.ecommerce
```

# creating a procfile
## creating special file to tell heroku how to start our application

## Add new file in the root folder `Procfile` (process file)
`Procfile`
```
release: python manage.py migrate
web: gunicorn storefront.wsgi
worker: celery -A storefront worker

```