# django-REST-exercise
Learning Django REST framework.

## Example
Here's an example Django REST Framework program that allows you to create and retrieve a list of users.

1. Make sure you have Django and Django REST Framework installed. You can do this by running the following command in your terminal:
```sh
$ pip install django djangorestframework
```

2. Create a new Django project by running:
```sh
$ django-admin startproject myproject
```

3. create a new Django app within your project:
```sh
$ cd myproject
$ python manage.py startapp myapp
```

4. Next, open the myproject/settings.py file and add 'rest_framework' to your INSTALLED_APPS list:
```python
 INSTALLED_APPS = [
    # ...
    'rest_framework',
]
```

5. Create a new file myapp/models.py and define a User model:
```python
from django.db import models

class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
```

6. Create a new file myapp/serializers.py and define a UserSerializer class:\
```python
from rest_framework import serializers
from myapp.models import User

class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['id', 'name', 'email']
```

7. Create a new file myapp/views.py and define a UserViewSet class:
```python
from rest_framework import viewsets
from myapp.models import User
from myapp.serializers import UserSerializer

class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer
```

8. Finally, update your myproject/urls.py file to include a new URL for the UserViewSet:
```python
from django.urls import include, path
from rest_framework import routers
from myapp.views import UserViewSet

router = routers.DefaultRouter()
router.register(r'users', UserViewSet)

urlpatterns = [
    path('', include(router.urls)),
]
```

9. That's it! Now you can run your Django server by running the command:
```sh
$ python manage.py runserver
```

Now you should be able to access the following endpoints:
* GET /users/ - retrieve a list of all users
* POST /users/ - create a new user
You can test this out using a tool like curl or by using a GUI tool like Postman.