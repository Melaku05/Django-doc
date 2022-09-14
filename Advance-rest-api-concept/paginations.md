## paginations

```

`add this file to the settings.py`
```
REST_FRAMEWORK = {
   #'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination', default pagination
    'PAGE_SIZE': 10
}
```

from rest_framework.pagination import PageNumberPagination

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    
    pagination_class = PageNumberPagination

```