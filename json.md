## Json
```python
import json
```

Здесь внимание приковано к двум методам:
> **dumps**
> **loads**

### dumps
Принимает на вход python объект и возвращает строку, которая представляет собой Json.

```python
sample_dict = {
	"name": "Nikita",
	"age": 21,
	"achievs": [
		"some1",
		"some2"
	],
	"value": 21.2,
}

json_string = json.dumps(sample_dict, indent="  ") # ident для красивого отступа
print(json_string)
print(type(json_string))
```
>output:
```json
{
  "name": "Nikita",
  "age": 21,
  "achievs": [
    "some1",
    "some2"
  ],
  "value": 21.2
}
<class 'str'>
```
### loads
Может принимать на вход str, bytes, bytearray, которые содержат JSON документ, а отдает python объект
```python
sample_dict = {
    "name": "Michael",
    "age": 42,
    32: "hello"
}

json_string = json.dumps(sample_dict, indent="  ") # ident для красивого отступа

myByteArray = bytearray(json_string, 'utf-8')
myBytes = bytes(json_string, 'utf-8')

res1 = json.loads(myByteArray)
res2 = json.loads(myBytes)
res3 = json.loads(json_string)

print(res1)
print(type(res1))
```
>output

```shell
{'name': 'Michael', 'age': 42, '32': 'hello'}
<class 'dict'>
```
