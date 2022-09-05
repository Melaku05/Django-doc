## serializers
serializer Converts a model instance to a dictionary

## create serializers
create  `serializers.py` inside specific application
```
from rest_framework import serializers

class ProductSerializer(serializers.Serializer):
    name = serializers.CharField(max_length=100)
    description = serializers.CharField(max_length=100)
    price = serializers.DecimalField(max_digits=10, decimal_places=2)
    quantity = serializers.IntegerField()
    tags = serializers.CharField(max_length=100)
  ```
## put it inside the setting.py 
  ```
  # To change the django rest default value of intger filed string to int
REST_FRAMEWORK = {
   'COERCE_DECIMAL_TO_STRING': False,
}
  ```
  ## views.py inside the app views file(API views)

  ```
from django.shortcuts import get_object_or_404
from rest_framework import status
from django.http import HttpResponse
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Product
from .serializers import ProductSerializer

# Create your views here.
@api_view()
def product_list(request):
    queryset =Product.objects.all() # returns queryset
    serializer = ProductSerializer(queryset, many=True)
    return Response(serializer.data)

@api_view()
def product_detail(request, id):
        product = get_object_or_404(Product, pk=id) #checking the id is valid or not and respond with 404 if not
        serializer = ProductSerializer(product)
        return Response(serializer.data)
  
  ```