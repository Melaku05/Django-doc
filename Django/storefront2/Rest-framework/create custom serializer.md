## In API model we can create customize fields such as to calculate the task based on the given unit price for the Data(django) model


InSide the `Serializers.py` add the following file

```
from rest_framework import serializers
from .models import Product
from decimal import Decimal # to convert float to deciaml

class ProductSerializer(serializers.Serializer):
    title = serializers.CharField(max_length=255)
    price = serializers.DecimalField(max_digits=6, decimal_places=2, source='unit_price') #source='unit_price ' to customize the name of Data(django) model attribute for API model
    price_with_tax = serializers.SerializerMethodField(method_name='calculate_tax') # to calculate the tax using price value

    def calculate_tax(self, product: Product):
        return product.unit_price * Decimal(1.13)

```