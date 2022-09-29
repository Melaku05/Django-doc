# [performance test(locust)](https://locust.io/)
## core use cases in this project
- Browse products
- Register, sign in , sign out
##  Install locust
```
pip install locust
```

## Implement locust 

### Create `locustfiles` dir in the root files
`locustfiles/browse_products.py`
```
import json
from unicodedata import name
from locust import HttpUser,task, between
from random import randint
class WebsiteUser(HttpUser):
    wait_time = between(1,5)
    @task(2)
    def view_products(self):
        collection_id = randint(2,6)
        self.client.get(f"/products/?collection_id={collection_id}".format(collection_id=collection_id), name="/products/")
    # viewing products
    # viewing producct details
    # adding products to cart

    @task(4)
    def view_product(self):
        product_id = randint(1,1000)
        self.client.get(
            f"/products/{product_id}/", 
            name="/products/:id/")
    @task(1)
    def add_to_cart(self):
        product_id = randint(1,1000)
        self.client.post(
            f"/carts/{self.cart_id}/items/", 
            name='/carts/items/',
            json={'product_id': product_id, 'quantity': 1})

    def on_start(self):
        response = self.client.post('/carts/')
        result = response.json()
        self.cart_id = result['id']
```
## Run performance test

```
locust -f locustfiles/browse_products.py
```
