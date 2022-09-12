## paginations

```
from rest_framework.pagination import PageNumberPagination

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    
    pagination_class = PageNumberPagination

    ```