# validate file

## validate the images size or files size

### create `validators.py` file in the specfic app
```
from django.core.exceptions import ValidationError

def validate_file_size(file):
    max_size_kb = 10

    if file.size >max_size_kb*1024:
        raise ValidationError(f'Files cannot be larger than {max_size_kb}Kb!')

```
### add this validations to the model  specfic 
```
from .validators import validate_file_size
 
class ProductImage(models.Model):
    ...
    image = models.ImageField(upload_to='store/images', validators=[validate_file_size])
```
## for file validating
### use ```FileField``` instade `Imagefield`

### import this package in the specfic model
```from django.core.validators import FileExtensionValidator

class ProductImage(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='images')
    image = models.ImageField(upload_to='store/images', validators=[FileExtensionValidator(allowed_extensions=['pdf'])])
```
### we do not need this one for `ImageField` because it was done by `pillow` under hook


