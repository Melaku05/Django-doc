## model serializer
```
from decimal import Decimal
from rest_framework import serializers
from .models import Product, Collection

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'title', 'slug', 'description', 'price', 'inventory', 'last_update', 'collection', 'price_with_tax']
    price_with_tax = serializers.SerializerMethodField(method_name='calculate_tax')
    collection =CollectionSerializer()
    def calculate_tax(self, product: Product):
        return product.unit_price * Decimal(1.13)

```