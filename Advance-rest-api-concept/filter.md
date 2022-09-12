# filter for third party package

## [offical page site](https://django-filter.readthedocs.io/en/stable/guide/rest_framework.html)

## Method 1) step to have filter method in the views

### 1 install app
``` pip install django-filter
```
### 2 Register the app in settings.py

```
# settings.py
INSTALLED_APPS = [
    'django_filters',
]
```

### 3 import packages and implement on the views
```
from django_filters.rest_framework import DjangoFilterBackend

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    filter_backends = [DjangoFilterBackend]
    filterset_fields = ['collection_id']

```

## method 2) custom filter using generic


### 1 install app
``` pip install django-filter
```
### 2 Register the app in settings.py

```
# settings.py
INSTALLED_APPS = [
    'django_filters',
]
```

### 3 Create `filters.py` file inside the specific app

```
from django_filters.rest_framework import FilterSet
from .models import Product

class ProductFilter(FilterSet):
    class Meta:
        model = Product
        fields = {
            'collection_id': ['exact'],
            'price': ['gt', 'lt'],
        }
```

### 4 add filter method to the views 
```
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    filter_backends = [DjangoFilterBackend]
    filterset_fields = ProductFilter
```