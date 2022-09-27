# Pytest

## install pytest tools

```
pip install --dev pytest #dev means developmet dependecy(we only need it for development purpose)
```

```
pip install --dev pytest-django
```

## create `tests` folder inside the specfic application we want to test

## create tests/test_collections.py file in side the specfic file
### the name of the test file in pytest shoudl start with `test_ ` and also the name of the class also should start with `Test`


## Every test have three part
### AAA (Arrange, Act, Assert)
Arrange:- prepare the system on the test, create the object,put the database on the inital state.
Act:-kick up the behaviour we want test.in this case send the request to the server

```
from rest_framework import status
from rest_framework.test import APIClient
from pytest


@pytest.mark.django_db
class TestCreateCollection:
  def test_if_user_is_anonymous_returns_401(self):
     # we create client object
     # Act
     client = APIClinet()
     response = client.post('/store/collections/', {'title':'a'}) # we gonna store client object to this address.
     # we send the request to the server, and we got response

    #Assert to check wheather the behaviour we excpect happen or not
    assert response.status_code == status.HTTP_401_UNAUTHORIZED ## boolean experession
 ```

 # pytest config
 ## create `pytest.ini` in the root directory and pu this files to there

 DJANGO_SETTINGS_MODULE=storefront.settings

 # run pytest
 ```
 pytest or ptw(python test watch)
 ```
 ```
 pytest store/tests/test_collections.py::TestCreateCollection::test_if_user_is_anonymous_returns_401
 ```
 ```
 pytest -k anonymous
 ```
 ### to skip the test 
 ```
 @pytest.mark.skip
```
 ## continous testing
 ```
 pip install --dev pytest-watch
 # then run the test
```
## Running and Debugging tests in VSCode



