## sorting/ordering filter
```
from rest_framework.filters import OrderingFilter


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    filter_backends = [OrderingFilter]
    ordering_fields = ['title', 'unit_price', 'last_update']
   
    ```