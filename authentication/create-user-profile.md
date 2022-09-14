# Create user profile

`To define user profile  we create profile model in our case it is customer,
in the profile model we add one to one relationship to the user model

## add this file to the custom model
```
user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
```