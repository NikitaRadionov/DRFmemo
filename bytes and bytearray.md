## bytes

**==bytes==** - builtins класс
```python
bytes([source[, encoding[, errors]]]) # сигнатура
```
source может быть 
- str 
- int
- iterable 
Если передаётся int, то объект bytes представляет собой 5 байтов, заполненных нулями. То есть мы инициализируем байтовый объект нулями.
Если передаётся iterable object, то он может содержать только целые числа в диапазоне [0, 255].
```python
string = "I love Python"
myInt = 5
myList = [1, 2, 3, 4]
myRange = range(1, 5)

myBytes1 = bytes(string, "utf-8")
myBytes2 = bytes(myInt)
myBytes3 = bytes(myList)
myBytes4 = bytes(myRange)

print(myBytes1)
print(myBytes2)
print(myBytes3)
print(myBytes4)

print(type(myBytes1))
```
>output:
```shell
b'I love Python'
b'\x00\x00\x00\x00\x00'
b'\x01\x02\x03\x04'
b'\x01\x02\x03\x04'
<class 'bytes'>
```

По объекту типа bytes можно итерироваться, а также обращаться к элементам по индексу:
```python
string = "Love"
myBytes = bytes(string, "utf-8")

for byte in myBytes:
    print(byte)

print(type(myBytes[0]))
```
>output:
```shell
76
111
118
101
<class 'int'>
```
Мы итерируемся по каждому байту - элементу коллекции bytes -, который представляет собой целое число.
Важно, что объект bytes является неизменяемым (unmutable), поэтому изменить значение какого-либо элемента коллекции или саму коллекцию не получится.

## bytearray

**==bytearray==** - builtins класс
```python
bytearray([source[, encoding[, errors]]]) # сигнатура
```
bytearray также представляет собой итерируемую коллекцию байтов.
Принимаемые аргументы и базовое использование в точности такое же как и у bytes. 
Разница между bytearray и bytes заключается в том, что bytearray является изменяемым объектом.

```python
myByteArray = bytearray(3)

print(myByteArray)

myByteArray.append(12)
myByteArray[0] = 1
myByteArray.pop(1)

print(myByteArray)
```
>output
```shell
bytearray(b'\x00\x00\x00')
bytearray(b'\x01\x00\x0c')
```
## Срезы для bytes и bytearray
Также представляет интерес операция среза
```python
myBytes = bytes('abcd', encoding='utf-8')
myByteArray = bytearray('abcd', encoding='utf-8')

print(myBytes[2:], type(myBytes[2:]))
print(myByteArray[2:], type(myByteArray[2:]))
```
>output
```shell
b'cd' <class 'bytes'>
bytearray(b'cd') <class 'bytearray'>
```
