# Basic Python
Quick hints:
```python
# Список из слов в строке
a = "Go Mf go".split()
>> ['Go', 'Mf', 'go']
```
### List / Список
>Набор элементов, следующих в определенном порядке.

```
bicycles = [’trek’, ‘cannondale’, ‘redline’]
print(bicycles[0])
print(bicycles[-1]) # Последний элемент массива 
```
#### Методы списка
Присоединение элемента в конец списка: 

    bicycles.append('cona') 

Добавить новый элемент в произвольную позицию списка:

    bicycles.insert(0, 'ХВЗ') 

Удаление элементов списка по индексу:

    del bicycles[0]

Удаление элементов по значению:

    # Удаляет первое вхождение
    bycecles.remove('trek') 

    # Удалить все вхождения
    while 'cat' in pets:
        pets.remove('cat')

Метод pop() удаляет элемент и возвращает его значение

    bicycles.pop() # Последний элемент по умолчанию
    bicycles.pop(1) # Можно указать индекс

##### Сортировка списка

Перманентная сортировка

    cars.sort()
    cars.sort(reverse=True) # Сортировка в обратном порядке

Временная сортировка

    sorted(cars)

Список в обратном порядке

    cars.reverse()

Определение длинны списка

    len(cars)

##### Работа с частью списка, срезы
```python
# Элементы 0, 1, 2
players[0:3]
# Элементы 1, 2 , 3
players[1:4]
# Автоматически с начала
players[:4]
# Автоматически до конца
players[2:]
# Срез конца списка (последние 3 элемента)
players[-3:]
```

##### Копирование списка

    list_b = list_a[:]

### Работа с числами

Создание числовой последовательности

    # range(start,stop,step)
    # start <= N < stop
    range(10, 0, -1)

Минимум, максимум, сумма числовой последовательности

    min(digits)
    max(digits)
    sum(digits)

~~Генераторы~~ List Comprehension 

    squares = [value**2 for value in range(11)]

### Tuples / Кортеж
>Неизменяемый список элементов (immutable)

    point = (2, 4)

### Dictionaries / Словари

```python
alien = {'color': 'green', 'points': 5}
new_points = alien['points']
alien['position'] = (1, 2)
# Удаление пар ключ-значение
del alien['points']
```
Перебор словаря
```python
for key, value in alien.items():
    ...
for key in sorted(alien.keys()):
    print(key, alien[key])

alien
# {'color': 'green', 'points': 5, 'position': (1, 2)}

alien.items()
# dict_items([('color', 'green'), ('points', 5), ('position', (1, 2))])

alien.keys()
# dict_keys(['color', 'points', 'position'])

alien.values()
# dict_values(['green', 5, (1, 2)])
```

### Functions / Функции
>Функция - именнованный блок кода, предназначенный для решения одной конкретной задачи.

```python
def greet_user(name: str = 'User'):
    """Prints simple greeting.""" # <- Строка документации
    print('Hello, ' + name + "!")
    return None

greet_user()
greet_user('Popo')
greet_user(name='Tiki')
```
#### * и **

    names = ['Boris','Anton']
```python
def greet_user(names):
    for name in names:
        print('Hello, ' + name + "!")

greet_user(names)
greet_user(['a', 'b', 'c'])
```
:duck: `greet_user(names) <==> greet_user([names[0], names[1]])`

---

```python
def greet_user(*names):
    for name in names:
        print('Hello, ' + name + "!")

greet_user(*names)
greet_user('a', 'b', 'c')
```
:duck: `greet_user(*names) <==> greet_user(names[0], names[1])`

---

```python
# **
names = {'Anton': 'Palich', 'aaaaa': 'bbbbbb'}

def greet_user(**names):
    for f_name, s_name in names.items():
        print('Hello, ' + f_name, s_name + "!")

greet_user(allhah='bah', top='sop')
greet_user(**names)
```

### Classes / Классы

```python
class Dog():
    """Simple dog model."""

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def sit(self):
        """Dog sits by command."""
        print(self.name.title() + " is now sitting.")
    def roll_over(self):
        """Dog rolls by command."""
        print(self.name.title() + " roled over!")


bobik = Dog('bobik', 7)
bobik.sit()
bobik.roll_over()

bobik.name
bobik.age
```
#### Наследование
```python
class RoboDog(Dog):
    """It's like a normal dog, but..."""
    def __init__(self, name, age, battery_size=70):
        super().__init__(name, age)
        self.battery_size = battery_size

    def describe_battery(self):
        """Shows info about battery."""
        print("This dog has a", self.battery_size, "-kWh battery.")

robik = RoboDog('robik', 1)
```

### Files / Файлы | Exceptions / Исключения

#### Открытие файла
```
with open('file_name.txt') as file_object:
    contents = file_object.read()
    print(contents)
```
Чтение по строкам
```python
filename = 'file.txt'

with open(filename) as file_object:
    for line in file_object:
        print(line)
```

Создание списка строк по содержимому файла
```python
with open(filename) as file_object:
    lines = file_object.readlines()
    for line in lines:
        print(line.rstrip())
```
#### Запись файла

```python
with open('file.txt', 'w') as file_object:
    file_object.write("I love programming.\n")
```
* r - чтение
* w - запись (затрет уже существующий)
* a - присоединение
* r+ - чтение + запись


#### Обработка исключений

```python
try:
    print(5/0)
except ZeroDivizionError:
    print("You cant divide by zero!")
```

File Not Found Error
```python
try:
    with open('file_name.txt') as file_object:
    contents = file_object.read()
except FileNotFoundError:
    print("File does not exist")
```

#### JSON

Запись
```
import json

numbers = [1, 2, 3, 8]

with open('file.json', 'w') as f_obj:
    json.dump(numbers, f_obj)
```

Чтение
```
import json

with open('file.json') as f_obj:
    numbers = json.load(numbers, f_obj)
print(numbers)
```


#### Tests / Тестирование
```python
def get_formatted_name(first, last):
    full_name = first + ' ' + last
    return full_name.title
```
```python
import unittest

class NamesTestCase(unittest.TestCase):
    def test_first_last_name(self):
        formatted_name = get_formatted_name('janis', 'joplin')
        self.assertEqual(formatted_name, 'Janis Joplin')

unittest.main()
```

| Метод    | Использование | 
|:----------|:--------------|
| assertEqual(a,b)| Проверяет, что a == b|
| assertNotEqual(a,b)|  Проверяет, что a != b |
| assertTrue(x)|  Проверяет, что значение x истинно|
| assertFalse(a,b)|  Проверяет, что значение x ложно |
| assertIn(a,b)|  Проверяет, что элемент входит в список |
| assertNotIn(a,b)|  Проверяет, что элемент не входит в список |





