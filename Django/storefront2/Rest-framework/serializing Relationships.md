## Serializer Relationships
### 1 put this inside serializers.py
```

from rest_framework import serializers
from .models import Product, Collection

class ProductSerializer(serializers.Serializer):
    title = serializers.CharField(max_length=255)
    collection =serializers.StringRelatedField()

```
### 2 put this inside views.py specifc app

```
def product_list(request):
    queryset =Product.objects.select_related('collection').all() # returns queryset (fix the queryset problem)
     #queryset =Product.objects.all() # returns queryset but we crash our system around 1000 queryset pre request
    serializer = ProductSerializer(queryset, many=True)
    return Response(serializer.data)

```

# Scond way of serializer relations is netested object

### 1 put this inside serializers.py
```
from decimal import Decimal
from rest_framework import serializers
from .models import Product, Collection

class CollectionSerializer(serializers.Serializer):
      id =serializers.IntegerField(read_only=True)
      title = serializers.CharField()

class ProductSerializer(serializers.Serializer):
    title = serializers.CharField(max_length=255)
    price = serializers.DecimalField(max_digits=6, decimal_places=2, source='unit_price')
    price_with_tax = serializers.SerializerMethodField(method_name='calculate_tax')
    collection =CollectionSerializer()
    def calculate_tax(self, product: Product):
        return product.unit_price * Decimal(1.13)


```

### 2 put this inside views.py specifc app

```
def product_list(request):
    queryset =Product.objects.select_related('collection').all() # returns queryset (fix the queryset problem)
     #queryset =Product.objects.all() # returns queryset but we crash our system around 1000 queryset pre request
    serializer = ProductSerializer(queryset, many=True)
    return Response(serializer.data)

```

# Third way of serializer relations is netested object

### 1 put this inside serializers.py
```
from decimal import Decimal
from rest_framework import serializers
from .models import Product, Collection

class ProductSerializer(serializers.ModelSerializer):
    title = serializers.CharField(max_length=255)
    collection =serializers.HyperlinkedRelatedField(
        queryset=Collection.objects.all(),
        view_name='collection-detail',
    )
```