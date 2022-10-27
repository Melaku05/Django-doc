# setup static files 
## Add this to the project `settings.py`
```
STATIC_URL = 'static/'
STATIC_ROOT = 'staticfiles'
 
MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

## Add this to the root `urls.py`
```
from django.conf import settings
from django.conf.urls.static import static
from django.contrib import admin
from django.urls import path, include
import debug_toolbar

admin.site.site_header = 'Storefront Admin'
admin.site.index_title = 'Admin'
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('core.urls')),
    path('playground/', include('playground.urls')),
    path('store', include('store.urls')),
    path('auth/', include('djoser.urls')),
    path('auth/', include('djoser.urls.jwt')),
    path('__debug__/', include(debug_toolbar.urls)),
] 
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL,
                          document_root=settings.MEDIA_ROOT)
    urlpatterns += [path('silk/', include('silk.urls', namespace='silk'))]
```
## run this command to collect static fils for deployment
```
python3 manage.py collectstatic
```
# Django does not support serving static files in production time. even though we have `collectstatic` command
## to do that we have to install third party library
## [whitenoise](http://whitenoise.evans.io/en/stable/#installation)

```
pip install whitenoise
```
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware',
]
```