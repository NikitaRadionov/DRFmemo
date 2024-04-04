
```python
#views.py

def my_view(request, *args, **kwargs):
	pass
```

## request

Если попробовать использовать функцию **type** чтобы узнать какого типа этот объект, то можно получить следующее:
```shell
request: <class 'django.core.handlers.wsgi.WSGIRequest'>
```
Но по факту request это ни что иное как:
```shell
<class 'django.http.HttpRequest'>
```

Важные атрибуты объекта request:

```python
request.body
request.headers
request.content_type
request.method
request.GET
request.POST
request.META
```

Давайте посмотрим что они из себя представляют:

```shell
request: <class 'django.core.handlers.wsgi.WSGIRequest'>
request.body: <class 'bytes'>   
request.headers: <class 'django.http.request.HttpHeaders'>
request.content_type: <class 'str'>
request.method: <class 'str'>
request.GET: <class 'django.http.request.QueryDict'>   
request.POST: <class 'django.http.request.QueryDict'>      
request.META: <class 'dict'>
```

request.headers - HttpHeaders объект, который представляет заголовки http запроса
request.method - строка, которая содержит в себе метод, с которым пришел HTTP запрос
```css
GET, POST, ...
```
request.GET - QueryDict, который можно преобразовать в python словарь, в котором содержатся url params get http запроса.
```shell
http://localhost:8000/api/?first=value1&second=value2&third=7

{'first': ['value1'], 'second': ['value2'], 'third': ['7']}
```
request.POST - QueryDict, который можно преобразовать в python словарь, в котором содержатся

Ради интереса можно посмотреть полный список public атрибутов у объекта request:
```shell
['COOKIES', 'FILES', 'GET', 'META', 'POST', 'accepted_types', 'accepts', 'body', 'build_absolute_uri', 'close', 'content_params', 'content_type', 'csrf_processing_done', 'encoding', 'environ', 'get_full_path', 'get_full_path_info', 'get_host', 'get_port', 'get_signed_cookie', 'headers', 'is_secure', 'method', 'parse_file_upload', 'path', 'path_info', 'read', 'readline', 'readlines', 'resolver_match', 'scheme', 'session', 'upload_handlers', 'user']
```
