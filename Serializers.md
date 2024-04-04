Сериализаторы в django rest framework позволяют преобразовывать сложные типы данных, такие как **QuerySet**, **Экземпляр модели** в примитивы Python, которые затем легко преобразовываются в **JSON**, **XML** или другие подобные штуки.

```python
from rest_framework import serializers
from rest_framework.renderers import JSONRenderer
from datetime import datetime

class Comment:
	
	def __init__(self, email, content, created=None)
		self.email = email
		self.content = content
		self.created = created or datetime.now()


class CommentSerializer(serializers.Serializer):
	email = serializers.EmailField()
	content = serializers.CharField(max_length=200)
	created = serializers.DateTimeField()

my_comment = Comment(email='leila@example.com', content='foo bar')
serializer = CommentSerializer(my_comment)

print(serializer.data)

json = JSONRenderer().render(serializer.data)

print(json)

```
>output
```shell
{'email': 'leila@example.com', 'content': 'foo bar', 'created': '2016-01-27T15:17:10.375877'}
b'{"email":"leila@example.com","content":"foo bar","created":"2016-01-27T15:17:10.375877"}'
```

В примере класс **CommentSerializer** преобразовал объект **Comment** в примитив Python - словарь, а затем с помощью **JSONRenderer().render()** мы преобразовали Python примитив (словарь) в последовательность байт, которая представляет собой **JSON** 