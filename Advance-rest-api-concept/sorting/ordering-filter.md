## sorting/ordering filter
```
from rest_framework.filters import OrderingFilter


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
   
    pagination_class = PageNumberPagination
    ```