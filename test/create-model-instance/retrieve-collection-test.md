# Retrieve pytest
### install

pip install model_bakery

```
from model_bakery import baker

@pytest.mark.django_db
class TestRetrieveCollection:
   def test_if_collection_exists_returns_200(self, api_client):
     
      collection = baker.make(Collection)
      response = api_client.get(f'/collections/{collection.id}/')
      
      assert response.status_code == status.HTTP_200_OK
      assert response.data == {
        'id' : collection.id,
        'title': collection.title,
        'products_count': 0
      }
```