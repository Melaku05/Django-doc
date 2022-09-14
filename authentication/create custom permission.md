# Create custom permissions

## Add this to the order model

```
class Meta:
        permissions = [
            ('cancel_order', 'can cancel order')
        ]
```