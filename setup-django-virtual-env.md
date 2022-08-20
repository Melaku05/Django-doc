# Configration and Setup  env for django project

## Install python3 and Pip
check python and pip install in the machine by using 

`python3 --version`

`pip --version`


## Create and Run Virtual Environment
create virtual environment by using the following command

`python3 -m venv v_name`

To activate the virtual environmet use the following command on the terminal

`source v_name/bin/activate`

To deactive the virtual environment use the following command on the terminal

`deactivate`


## Install and Create Djnago project 
To install django in our machine we use the following command on the terminal

 `pip install django==4.2`

 To check the version installed django version

 `django-admin ---version`

 `django-admin startproject project_name .`

 to run the project 
 
 `cd project_name`

` python3 manage.py runserver`


## Create application
`python3 manage.py startapp AppName`