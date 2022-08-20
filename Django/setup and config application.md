# Setup and config Application in Django project
## 1.Register the apps in  `settings.py` py files

`app_name.apps.App_nameConfig`


## 2. Create URL inside the application(urls.py)

`from django.url import path
 from . import views`

`urlpatterns =[<br>
    path(' /', views.index)<br>
]`

## 3. Add the path of the apps URL in Django(project) URL

`from django.urls import path, include
path("/", include('app_name.urls'))`

## 4 Create the application view

`def index(request):
  return render(request, 'index.html')

## 5 Create templates

1  create `templates` dir in the main dir or specific app

2 put it in the `setting.py     TEMPLATES = [ {'DIRS' :['templates'],` 
 
3 create `index.html` file inside templates dir

4. write html file inside of index.html file you want to display in the screen

5 run the application using `python3 manage.py runserver`