# Django model
## django relationship between table
## 1 One to one relationship
    `
    primry key =True is not allow django to have diplicated value
    id
    it is mandatory to have primary key=True in one to one relationship
    `
  
```
 class Address(models.Model):
    street = models.CharField(max_length=255)
    city = models.CharField(max_length=255)
    customer = models.OneToOneField(Customer, on_delete=models.CASCADE, primary_key=True)
```
## 2 one to many relaltionship
```
class Address(models.Model):
    street = models.CharField(max_length=255)
    city = models.CharField(max_length=255)
    customer = models.ForeignKey(
        Customer, on_delete=models.CASCADE)
```
