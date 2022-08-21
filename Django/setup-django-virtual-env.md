# Configration and Setup  env for django project

## Install python3 and Pip(Note:-python3 is stand for linux operationg system, use python for windows)
check python and pip install in the machine by using 

``` 
python3 --version
```

```
pip --version

```


## Create and Run Virtual Environment
create virtual environment by using the following command

``` 
python3 -m venv v_name 

```

To activate the virtual environmet use the following command on the terminal

```
source v_name/bin/activate

 ```

To deactive the virtual environment use the following command on the terminal

```
 deactivate
```


## Install  Djnago  python Django Framework
To install django in our machine we use the following command on the terminal

 ```
 pip install django==4.2
 ```

 To check the version installed django version

 ```
 django-admin ---version
 ```

 ## To create django Project

 To create Django project

 ```
 django-admin startproject project_name .
 ```

 to run the project 

 ```
 cd project_name
 ```

 
```
 python3 manage.py runserver
 ```



## Create application
```
python3 manage.py startapp AppName
```