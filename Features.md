```python
dict.setdefault(key[, default])
```
- key - ключ словаря
- default - значения
- Если указанный ключ **key** отсутствует в словаре, то данный метод вставит его в словарь **dict** со значением **default** и вернет значение **default**
- Если указанный ключ **key** есть в словаре, то
- Если значение **default** не установлено и ключ отсутствует, то метод вставит ключ в словарь со значением None, при этом никакое значение не вернется.
Данный метод никогда не вызывает исключения KeyError

```python
dictionary = {'one': 0, 'two': 20, 'three': 3, 'four': 4}
dictionary.setdefault('one')
#0

dictionary.setdefault('six', 6)
>>> dictionary
# {'one': 0, 'two': 20, 'three': 3, 'four': 4, 'six': 6}
```

## Декоратор @property

```python
class Person:

	def __init__(self, name, old):
		self.__name = name
		self.__old = old

	def get_old(self):
		return self.__old

	def set_old(self, old):
		self.__old = old

p = Person("Nikita", 21)
p.set_old(25)

print(p.get_old())
```
>output:
```shell
25
```

Когда мы работаем с приватными атрибутами, то мы должны иметь дело с геттерами и сеттерами. Если приватных переменных очень много (распространенная ситуация), то геттеров и сеттеров становится очень много и их тяжело всех помнить. Чтобы это исправить существует такая штука как **property**

```python
class Person:

	def __init__(self, name, old):
		self.__name = name
		self.__old = old
	
	def get_old(self):
		print("Here is getter")
		return self.__old
	
	def set_old(self, old):
		print("Here is setter")
		self.__old = old
	
	old = property(get_old, set_old)


p = Person("Nikita", 21)
p.old = 25
print(p.old)

```
>output
```Shell
Here is setter
Here is getter
25
```

Строку
```python
old = property(get_old, set_old)
```
можно переписать следующим образом:
```python
old = property()
old = old.setter(set_old)
old = old.getter(get_old)
```

```python
class Person:
	
	def __init__(self, name, old):
		self.__name = name
		self.__old = old
	
	@property
	def old(self):
		print("Here is getter")
		return self.__old
	
	@old.setter
	def old(self, old):
		print("Here is setter")
		self.__old = old
	
	@old.deleter
	def old(self):
		print("Here is deleter")
		del self.__old

p = Person("Nikita", 21)
p.old = 25 # Here is setter
print(p.old) # Here is getter
            # 25
del p.old # here is deleter
```
>output
```shell
Here is setter
Here is getter
25
Here is deleter
```

## Вложенные классы

```python
class Women:
	title = 'class obj for field title'
	photo = 'class obj for field photo'
	
	class Meta:
		ordering = ['id']

w = Women()
print(w.Meta.ordering)
print(Women.Meta.ordering)
```
>output
```shell
['id']
['id']
```

Это может показаться странным, что внутри класса есть ещё другой класс, но ничего особенного в этом нет. Класс **Meta** такой же полноценный как и внешний класс **Women**.

Здесь есть особенность использования такой конструкции. Если мы уж используем это, то должны придерживаться такого правила: **Внутренний класс не должен использовать никакие атрибуты внешнего класса, он должен быть полностью изолированным**.

Также важно понимать, что в примере выше, при создании экземпляра класса **Women** не создается экземпляр класса **Meta**. Но экземпляры этого класса могут быть созданы:

```python
class Women:
	title = "class obj for field title"
	photo = "class obj for field photo"
	
	def __init__(self, user: str, psw: str):
		self._user = user
		self._psw = psw
		self.meta = self.Meta(user + '@' + psw)
	
	class Meta:
		ordering = ["id"]
		
		def __init__(self, access):
			self._access = access

w = Women('root', '12345')
```
В этом примере при создании экземпляра класса Women автоматически создается экземпляр класса Meta

Вывод: вложенные классы используются исключительно для удобства программиста, также нет никакого сакрального смысла в использовании данной конструкции.
