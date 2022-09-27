# upload image

## serve the application
### to upload image from users
  - create `media` directory in the root folder
  - register or tell the django seeting about this directory

  ### in the settings
  ```
  MEDIA_URL = '/media/'
  MEDIA_ROOT = BASE_DIR / 'media'

### in root urls.py

```
from django.conf import settings
from django.conf.urls.static import static


urlpatterns = [
    ...
] 
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL,
                          document_root=settings.MEDIA_ROOT)

```
### install pillow
```
pip install pillow

```

## create model for the specific app(in our case it is for store app)
```
class ProductImage(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='images')
    image = models.ImageField(upload_to='store/images')

```
## create serializer for images
```
class ProductImageSerializer(serializers.ModelSerializer):
    def create(self, validated_data):
        porduct_id = self.context['product_id']
        return ProductImage.objects.create(product_id=porduct_id, **validated_data)

    class Meta:
        model = ProductImage
        fields = ['id','image']
  ```

## register the routes 
```
products_router.register('images', views.ProductImageViewSet, basename='product-images')# because of override of get_queryset on the viewset

```