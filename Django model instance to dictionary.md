```python
#views.py

from django.forms.models import model_to_dict

from django.http import JsonResponse
from products.models import Product

def api_home(request, *args, *kwargs):
	model_data = Product.objects.all().order_by("?").first()
	data = {}
	if model_data:
		data = model_to_dict(model_data, fields=['id', 'title'])
	return JsonResponse(data)

```
Пусть у нас есть в models.py модель ==Product==, у которой есть поля **title**, **content**, **price** и само собой **id**. Мы хотим преобразовать instance of Product в словарь. Для этого можно пользоваться функцией **model_to_dict**

```python
def model_to_dict(instance, fields=None, exclude=None) # сигнатура
```
В нашем примере мы передаем экземпляр Product в model_to_dict, а также мы указываем в аргументе fields какие поля этой записи мы хотим видеть в словаре. Если аргумент fields не указан, то в словаре будут все поля данной записи.
Таким образом в data может лежать что-то вроде этого:
```shell
{'id': 1, 'title': 'Hello world'}
```
Важно подчеркнуть что model_to_dict принимает экземпляр Product, а не QuerySet
Также можно исключить поля, которые мы не хотим видеть в нашем словаре
```python
data = model_to_dict(model_data, exclude=["id", "content"])
```
В таком случае в data может лежать что-то вроде этого:
```shell
{'title': 'Hello world', 'price': '0.00'}
```

**_Зачем это нужно ?_**
Если вы не знакомы с этой функцией, то можете написать что-то вроде этого:

```python
def api_home(request, *args, **kwargs):
    model_data = Product.objects.all().order_by("?").first()
    
    data = {}
    if model_data:
        data['id'] = model_data.id
        data['title'] = model_data.title
        data['content'] = model_data.content
        data['price'] = model_data.price

    return JsonResponse(data)
```
Мы создали словарь и вручную его стали заполнять. Если вы как и я начинающий разработчик, то, написав так в своём тестовом задании, вы продемонстрируете своё _незнание_ базовых функций.

Если что-то до вас уже было реализовано, то используйте это !