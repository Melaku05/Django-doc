# Pytest

## install pytest tools

```
pip install pytest #dev means developmet dependecy(we only need it for development purpose)
```

```
pip install pytest-django
```

## create `tests` folder inside the specfic application we want to test
**/tests**

## create tests/test_collections.py file in side the specfic file
### the name of the test file in pytest shoudl start with `test_ ` and also the name of the class also should start with `Test`
**/tests/test_collections.py**

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
     client = APIClient()
     response = client.post('/store/collections/', {'title':'a'}) # we gonna store client object to this address.
     # we send the request to the server, and we got response

    #Assert to check wheather the behaviour we excpect happen or not
    assert response.status_code == status.HTTP_401_UNAUTHORIZED ## boolean experession
 ```

 # pytest config
 ## create `pytest.ini` in the root directory and pu this files to there
 **pytest.ini**

[pytest]

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
## ??
 ## pytest sample 
 ```
 from django.contrib.auth.models import User
from rest_framework import status
from rest_framework.test import APIClient
import pytest


@pytest.mark.django_db
class TestCreateCollection:
  def test_if_user_is_anonymous_returns_401(self):
    client = APIClient()
    response = client.post('/collections/', {'title':'a'}) 
    assert response.status_code == status.HTTP_401_UNAUTHORIZED 
   # Authenticating the user (The client is authenticated, but the current user is not an admin)
  def test_if_user_is_not_admin_returns_403(self):
    client = APIClient()
    client.force_authenticate({})
    response = client.post('/collections/', {'title':'a'}) 
    assert response.status_code == status.HTTP_403_FORBIDDEN
  
  # The client is authenticated, the current user is admin , but the data is auto of date cenarious
  def test_if_data_is_invalid_returns_400(self):
    client = APIClient()
    client.force_authenticate(user=User(is_staff=True))
    response = client.post('/collections/', {'title':''}) 

    assert response.status_code == status.HTTP_400_BAD_REQUEST
    assert response.data['title'] is not None

  def test_if_data_is_valid_returns_201(self):
    client = APIClient()
    client.force_authenticate(user=User(is_staff=True))
    response = client.post('/collections/', {'title':'a'}) 
    
    assert response.status_code == status.HTTP_201_CREATED
    assert response.data['id'] > 0
```

# Fixtures feature in pytest
## Create `conftest.py` file inside the `tests` dir of the specfic application.
**store/tests/conftest.py**
```
from rest_framework.test import APIClient
from django.contrib.auth.models import User
import pytest

@pytest.fixture
def authenticate(api_client):
    def do_authenticate(is_staff=False):
        return api_client.force_authenticate(user=User(is_staff=is_staff))
    return do_authenticate
@pytest.fixture
def api_client():
    return APIClient()

```

**store/tests/test_collections.py**
```
from rest_framework import status
import pytest


@pytest.fixture
def create_collection(api_client):
  def do_create_collection(collection):
    return api_client.post('/collections/',collection)
  return do_create_collection
 
@pytest.mark.django_db
class TestCreateCollection:
  def test_if_user_is_anonymous_returns_401(self, create_collection):
    response = create_collection({'title':'a'}) 
    assert response.status_code == status.HTTP_401_UNAUTHORIZED 
   # Authenticating the user (The client is authenticated, but the current user is not an admin)
  def test_if_user_is_not_admin_returns_403(self, authenticate, create_collection):
    authenticate()
    response = create_collection({'title':'a'}) 
    assert response.status_code == status.HTTP_403_FORBIDDEN
  
  # The client is authenticated, the current user is admin , but the data is auto of date cenarious
  def test_if_data_is_invalid_returns_400(self, authenticate,create_collection):
    authenticate(is_staff=True)
    response = create_collection({'title':''}) 

    assert response.status_code == status.HTTP_400_BAD_REQUEST
    assert response.data['title'] is not None

  def test_if_data_is_valid_returns_201(self, authenticate, create_collection):

    authenticate(is_staff=True)
    response = create_collection({'title':'a'}) 
    
    assert response.status_code == status.HTTP_201_CREATED
    assert response.data['id'] > 0
```
# this test just for creating collection only