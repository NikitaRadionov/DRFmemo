## HttpResponse

**HttpResponse** - класс в **django.http**

```python
HttpResponse(content=b'', content_type=None,
			 status=200, reason=None,
			 charset=None, headers=None) # сигнатура метода __init__
```

## JsonResponse

**JsonResponse** - класс в **django.http**, который является наследником **HttpResponse** и предназначен для создания **JSON** ответа.

```python
JsonResponse(data, encoder=DjangoJSONEncoder,
			safe=True, json_dumps_params=None, **kwargs) # сигнатура
```
Внутри своего _____init_____ метода **JsonResponse** вызывает **json.dumps**, который преобразует объект **data** (зачастую это словарь) в строку, а затем вызывает _____init_____ метод родителя (**HttpResponse**) в который передается **data** в виде строки и указывается **content_type="application/json"**

## rest_framework.response.Response

**Response** - класс в **rest_framework.response**, который используется по причине более удобного интерфейса для возврата согласованных по содержанию ответов Web API, которые могут быть представлены в нескольких формах.

Стоит отметить, что **Response** является наследником **SimpleTemplateResponse**, а **SimpleTemplateResponse** в свою очередь является наследником **HttpResponse**. Таким образом **Reponse** является наследником **HttpResponse**.

```python
Response(data, status=None, template_name=None,
		headers=None, content_type=None) # сигнатура

```
Чем может быть **data** в этой сигнатуре ?
**data** - любой примитив Python, такой как словарь, список, строка. Поэтому прежде чем передавать, скажем, экземпляр модели, нужно его сериализовать в примитив Python.

Как правильно использовать объект Response ?

Если нам не нужна особая настройка REST framework, то для работы с объектом **Response** мы должны использовать класс **APIView**, или, если мы используем **view**, которая представляет собой функцию, которая возвращает объект **Response**, то для неё обязательно нужно использовать декоратор **@api_view** 

Такое использование гарантирует нам, что **view** сможет выполнить согласование содержимого и выбрать подходящий модель визуализации для ответа, прежде чем он будет возвращен из представления.

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(["GET"])
def api_home(request, *args, **kwargs):
	model_data = Product.objects.all().order_by("?").first()
	data = {}
	if model_data:
		data = model_to_dict(model_data, fields=['id', 'title', 'price'])
	return Response(data)

```

Важно отметить, что декоратор **@api_view** обязан принимать список из строк, которые являются названиями разрешенных http методов для данного **view**.
В примере выше мы разрешаем только **GET** http метод.

С того момента, как мы начали использовать класс **APIView** или декоратор **api_view** в нашем **view** мы будем иметь дело с объектом **rest_framework.request.Request**. Отныне объект запроса будет представлять этот класс.