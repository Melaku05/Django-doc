# GUID(Globaly Unique Identifier)guwet
Use to prevent the hacker from using the id of the user carts. long to 32 character

`we don't need GUID for authorized users`

```
# in models.py
from uuid import uuid4
 
 #in specfice model class we want to override the default django id(integer)

 id = models.UUIDField(primary_key=True, default=uuid4)
  #It is a passing reference, not just a calling function.

  
  # in views.py

id = serializers.UUIDField(read_only=True)
 # we dont want to send object to the server, we want to send to the server only empty object.

 ```