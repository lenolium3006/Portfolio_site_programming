
# Лабораторные работы

## **Two sum**

###  **Описание программы**

Данная программа решает популярную задачу Two Sum.
Необходимо найти два числа в списке, сумма которых равна заданному значению `target`, и вернуть их индексы.

Программа реализована на языке Python с использованием класса `Solution` и метода `twoSum`.

###  **Что реализовано**

* Создан класс `Solution`.
* Реализован метод `twoSum`.
* Используется перебор элементов списка с помощью двух циклов.
* Выполняется проверка суммы двух чисел.
* При нахождении подходящей пары программа возвращает индексы элементов.
* Добавлен пример запуска программы.

###  **Код программы**

```python
class Solution:
    def twoSum(self, nums, target):
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):  
                if nums[i] + nums[j] == target:
                    return [i, j]

solution = Solution()

print(solution.twoSum([2, 7, 11, 15], 9))
```
### **Объяснение работы программы**

1. Программа получает список чисел `nums`.
2. Задается число `target`.
3. С помощью двух вложенных циклов перебираются все возможные пары чисел.
4. Если сумма двух элементов равна `target`, программа возвращает их индексы.
5. Результат выводится на экран.

### **Входные данные**

```python
nums = [2, 7, 11, 15]
target = 9
```
### **Вывод программы**

```python
[0, 1]
```
### **Результат работы**

Программа успешно находит два элемента массива, сумма которых равна заданному числу.
В данном примере числа `2` и `7` дают сумму `9`, поэтому выводятся их индексы — `[0, 1]`.


---
## Вычисление деления

### **Описание программы**

Данная программа реализует работу с делением чисел и настройкой точности вычислений через конфигурационный файл.

В программе:

* создана функция `calculate` для деления двух чисел;
* реализована возможность задания точности вычислений `epsilon`;
* создана функция `load_params` для чтения параметров из файла `settings.ini`;
* написаны тесты для проверки корректной работы функций.


### **Что реализовано**

* Деление целых и дробных чисел.
* Проверка диапазона значения `epsilon`.
* Обработка ошибки деления на ноль.
* Загрузка параметров из конфигурационного файла.
* Проверка корректности формата числа.
* Набор тестов для автоматической проверки программы.

### **Основной код программы**

```python 
import configparser


def calculate(a, b, epsilon=0.0001):
    if not (10**-9 < epsilon < 10**-1):
        raise ValueError("epsilon вне допустимого диапазона")

    if b == 0:
        raise ZeroDivisionError("Деление на ноль невозможно")

    result = a / b

    return round(result, len(str(epsilon).split(".")[1]))


def load_params():
    config = configparser.ConfigParser()

    if not config.read("settings.ini"):
        raise FileNotFoundError("Файл settings.ini не найден")

    try:
        epsilon = float(config["SETTINGS"]["epsilon"])
    except ValueError:
        raise ValueError("Неверный формат epsilon")

    if not (10**-9 < epsilon < 10**-1):
        raise ValueError("epsilon вне допустимого диапазона")

    return epsilon


epsilon = load_params()

result = calculate(1, 2, epsilon)

print(result)
```

### **Конфигурационный файл settings.ini**

```ini 
[SETTINGS]
epsilon = 0.001
```

### **Тесты программы**

```python 
import unittest


class TestCalculate(unittest.TestCase):

    def test_half(self):
        self.assertEqual(calculate(1, 2, 0.1), 0.5)

    def test_thousand(self):
        self.assertEqual(calculate(1, 1000, 0.001), 0.001)

    def test_zero_division(self):
        with self.assertRaises(ZeroDivisionError):
            calculate(1, 0)

    def test_epsilon_range(self):
        with self.assertRaises(ValueError):
            calculate(1, 2, 1)

    def test_wrong_format(self):
        with self.assertRaises(ValueError):
            config = configparser.ConfigParser()
            config.read_dict({
                "SETTINGS": {
                    "epsilon": "abc"
                }
            })

            float(config["SETTINGS"]["epsilon"])


if __name__ == "__main__":
    unittest.main()
```

### **Объяснение работы программы**

1. Функция `calculate` принимает два числа и значение точности.
2. Проверяется корректность `epsilon`.
3. Выполняется деление первого числа на второе.
4. Результат округляется до нужной точности.
5. Функция `load_params` считывает значение `epsilon` из файла `settings.ini`.
6. Тесты автоматически проверяют работу программы и обработку ошибок.


### **Пример входных данных**

```python 
a = 1
b = 2
epsilon = 0.1
```

### **Вывод программы**

```python 
0.5
```

### **Результат работы**

Программа успешно выполняет деление чисел с заданной точностью, загружает параметры из конфигурационного файла и корректно обрабатывает возможные ошибки.

--- 
## Бинарное дерево

### **Описание программы**

Данная программа реализует рекурсивное построение бинарного дерева на языке Python.

Каждый узел дерева содержит не более двух потомков:
- левого;
- правого.

Дерево строится на основе:
- высоты дерева (`height`);
- значения корня (`root`);
- формул вычисления потомков.

В качестве структуры хранения используется словарь Python (`dict`).

### **Что реализовано**

- Рекурсивная функция `gen_bin_tree`
- Генерация бинарного дерева заданной высоты
- Использование пользовательских параметров
- Формирование дерева в виде словаря
- Документация по стандарту PEP-257
- Аннотации типов (`typing`)
- Набор тестов с использованием `unittest`


### **Код программы**

```python
import unittest
from typing import Dict, List

TreeType = Dict[str, List]


def gen_bin_tree(
    height: int = 4,
    root: int = 3
) -> TreeType:
    """
    Рекурсивно генерирует бинарное дерево.

    Параметры
    ----------
    height : int
        Высота дерева.

    root : int
        Значение корневого узла.

    Возвращает
    ----------
    TreeType
        Бинарное дерево в виде словаря.

    Формулы потомков
    ----------------
    left_leaf = root + 2
    right_leaf = root * 3
    """

    if height == 0:
        return {str(root): []}

    left_leaf = root + 2
    right_leaf = root * 3

    left_subtree = gen_bin_tree(height - 1, left_leaf)
    right_subtree = gen_bin_tree(height - 1, right_leaf)

    return {
        str(root): [
            left_subtree,
            right_subtree
        ]
    }


tree = gen_bin_tree()

print(tree)
```


### **Пример результата работы программы**

```python
{
    '3': [
        {
            '5': [
                {'7': []},
                {'15': []}
            ]
        },
        {
            '9': [
                {'11': []},
                {'27': []}
            ]
        }
    ]
}
```

### **Тесты программы**

```python
class TestGenBinTree(unittest.TestCase):

    def test_height_1(self):
        expected = {
            '3': [
                {'5': []},
                {'9': []}
            ]
        }

        result = gen_bin_tree(1, 3)

        self.assertEqual(result, expected)

    def test_height_2(self):
        expected = {
            '3': [
                {
                    '5': [
                        {'7': []},
                        {'15': []}
                    ]
                },
                {
                    '9': [
                        {'11': []},
                        {'27': []}
                    ]
                }
            ]
        }

        result = gen_bin_tree(2, 3)

        self.assertEqual(result, expected)

    def test_leaf_node(self):
        expected = {'3': []}

        result = gen_bin_tree(0, 3)

        self.assertEqual(result, expected)


if __name__ == "__main__":
    unittest.main()
```

---

### **Объяснение работы программы**

1. Пользователь задает высоту дерева и значение корня.
2. Функция рекурсивно создает левый и правый узел.
3. Для каждого потомка повторяется процесс генерации.
4. Когда высота становится равной нулю, создается лист дерева.
5. Итоговая структура возвращается в виде словаря.


### **Входные данные**

```python
height = 2
root = 3
```

### **Вывод программы**

```python
{
    '3': [
        {
            '5': [
                {'7': []},
                {'15': []}
            ]
        },
        {
            '9': [
                {'11': []},
                {'27': []}
            ]
        }
    ]
}
```

### **Результат работы**

Программа успешно генерирует бинарное дерево заданной высоты с использованием рекурсии.
Также реализовано тестирование программы и документирование кода по стандарту PEP-257.

---
## Итератор, генератор. Cопрограмма


###  **Описание программы**

Данная программа реализует работу с рядом Фибоначчи с использованием:

* генераторов;
* сопрограмм (корутин);
* пользовательских итераторов.

Программа позволяет:

* генерировать список чисел Фибоначчи;
* получать элементы ряда по запросу;
* фильтровать элементы списка, оставляя только числа Фибоначчи;
* выполнять автоматическое тестирование программы.

### **Что реализовано**

* Генератор элементов ряда Фибоначчи.
* Сопрограмма `my_genn`.
* Декоратор для автоматического запуска корутины.
* Итератор `FibonacchiLst`.
* Проверка принадлежности числа ряду Фибоначчи.
* Набор тестов с использованием `pytest` и `unittest`.

### **Файл gen_fib.py**

```python 
import functools


def fib_elem_gen():
    """
    Генератор элементов ряда Фибоначчи.
    """

    a = 0
    b = 1

    while True:
        yield a
        a, b = b, a + b


def my_genn():
    """
    Сопрограмма для генерации списка чисел Фибоначчи.
    """

    while True:
        number_of_fib_elem = yield

        fib_list = []

        a = 0
        b = 1

        for _ in range(number_of_fib_elem):
            fib_list.append(a)
            a, b = b, a + b

        yield fib_list


def fib_coroutine(g):
    """
    Декоратор для автоматического запуска сопрограммы.
    """

    @functools.wraps(g)
    def inner(*args, **kwargs):
        gen = g(*args, **kwargs)
        gen.send(None)
        return gen

    return inner


my_genn = fib_coroutine(my_genn)

gen = my_genn()

print(gen.send(5))
```

### **Файл fib_iterator.py**

```python 
class FibonacchiLst:
    """
    Итератор, возвращающий числа Фибоначчи из списка.
    """

    def __init__(self, instance):
        self.instance = instance
        self.idx = 0

    def __iter__(self):
        return self

    def is_fibonacci(self, number):
        """
        Проверка принадлежности числа ряду Фибоначчи.
        """

        a = 0
        b = 1

        while a <= number:
            if a == number:
                return True

            a, b = b, a + b

        return False

    def __next__(self):

        while True:
            try:
                res = self.instance[self.idx]

            except IndexError:
                raise StopIteration

            self.idx += 1

            if self.is_fibonacci(res):
                return res
```

### **Файл test_fib.py**

```python 
from gen_fib import my_genn


def test_fib_1():
    gen = my_genn()

    assert gen.send(3) == [0, 1, 1]


def test_fib_2():
    gen = my_genn()

    assert gen.send(5) == [0, 1, 1, 2, 3]


def test_fib_3():
    gen = my_genn()

    assert gen.send(1) == [0]


def test_fib_4():
    gen = my_genn()

    assert gen.send(0) == []


def test_fib_5():
    gen = my_genn()

    assert gen.send(8) == [0, 1, 1, 2, 3, 5, 8, 13]
```

### **Файл test_fib_it.py**

```python 
import unittest

from fib_iterator import FibonacchiLst


class TestFibIterator(unittest.TestCase):

    def test_normal(self):
        result = list(FibonacchiLst(
            [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1]
        ))

        self.assertEqual(result, [0, 1, 2, 3, 5, 8, 1])

    def test_corner_0(self):
        result = list(FibonacchiLst([]))

        self.assertEqual(result, [])

    def test_corner_1(self):
        result = list(FibonacchiLst([0]))

        self.assertEqual(result, [0])

    def test_corner_2(self):
        result = list(FibonacchiLst([0, 1]))

        self.assertEqual(result, [0, 1])

    def test_corner_3(self):
        result = list(FibonacchiLst([1, 1]))

        self.assertEqual(result, [1, 1])


if __name__ == "__main__":
    unittest.main()
```

### **Объяснение работы программы**

1. Генератор `fib_elem_gen` создает последовательность чисел Фибоначчи.
2. Сопрограмма `my_genn` получает число `n` и возвращает первые `n` элементов ряда.
3. Декоратор автоматически активирует корутину.
4. Итератор `FibonacchiLst` перебирает список и возвращает только числа Фибоначчи.
5. Тесты проверяют корректность работы программы и обработку крайних случаев.


### **Пример входных данных**

```python 
gen.send(5)
```

### **Вывод программы**

```python 
[0, 1, 1, 2, 3]
```

### **Результат работы**

Программа успешно реализует генерацию чисел Фибоначчи с помощью генераторов, сопрограмм и итераторов.
Также реализовано автоматическое тестирование всех основных сценариев работы программы.

---

## Паттерны проектирования


### **Описание программы**

Данная программа реализует получение курсов валют с помощью API Центрального Банка РФ и использование шаблона проектирования Decorator (Декоратор).

Базовый компонент получает данные о валютах в формате JSON, а декораторы позволяют:

* преобразовывать данные в YAML;
* преобразовывать данные в CSV;
* сохранять результаты в файлы соответствующих форматов.

Программа разработана с использованием:

* интерфейсов `ABC`;
* аннотаций типов;
* документации PEP-257;
* тестирования `unittest`.

### **Что реализовано**

* Шаблон проектирования Decorator.
* Абстрактный интерфейс через `ABC`.
* Получение валют с API ЦБ РФ.
* Конкретный компонент для JSON.
* Декоратор YAML.
* Декоратор CSV.
* Сохранение данных в файлы.
* Набор тестов.
* Аннотации типов и документация.

### **Код программы main.py**

```python 
from abc import ABC, abstractmethod
from typing import Dict, Any
import requests
import yaml
import csv


class Component(ABC):
    """
    Базовый интерфейс компонента.
    """

    @abstractmethod
    def operation(self) -> Any:
        """
        Метод получения данных.
        """
        pass

    @abstractmethod
    def save_to_file(self, filename: str) -> None:
        """
        Метод сохранения данных в файл.
        """
        pass


class ConcreteComponent(Component):
    """
    Базовый компонент, возвращающий JSON.
    """

    def __init__(self):

        self.url = "https://www.cbr-xml-daily.ru/daily_json.js"

    def operation(self) -> Dict:
        """
        Получение JSON с API ЦБ РФ.
        """

        response = requests.get(self.url)

        return response.json()

    def save_to_file(self, filename: str) -> None:
        """
        Сохранение JSON в файл.
        """

        data = self.operation()

        with open(filename, "w", encoding="utf-8") as file:
            file.write(str(data))


class Decorator(Component):
    """
    Базовый класс декоратора.
    """

    def __init__(self, component: Component):

        self._component = component

    def operation(self) -> Any:

        return self._component.operation()

    def save_to_file(self, filename: str) -> None:

        self._component.save_to_file(filename)


class YamlDecorator(Decorator):
    """
    Декоратор YAML.
    """

    def operation(self) -> str:
        """
        Преобразование данных в YAML.
        """

        data = self._component.operation()

        return yaml.dump(
            data,
            allow_unicode=True
        )

    def save_to_file(self, filename: str) -> None:
        """
        Сохранение YAML в файл.
        """

        data = self.operation()

        with open(filename, "w", encoding="utf-8") as file:
            file.write(data)


class CsvDecorator(Decorator):
    """
    Декоратор CSV.
    """

    def operation(self) -> list:
        """
        Преобразование данных в CSV формат.
        """

        data = self._component.operation()

        currencies = []

        for key, value in data["Valute"].items():

            currencies.append([
                key,
                value["Name"],
                value["Value"]
            ])

        return currencies

    def save_to_file(self, filename: str) -> None:
        """
        Сохранение CSV в файл.
        """

        data = self.operation()

        with open(
            filename,
            "w",
            newline="",
            encoding="utf-8"
        ) as file:

            writer = csv.writer(file)

            writer.writerow([
                "Code",
                "Name",
                "Value"
            ])

            writer.writerows(data)


def client_code(component: Component) -> None:
    """
    Клиентский код.
    """

    result = component.operation()

    print(result)


if __name__ == "__main__":

    simple = ConcreteComponent()

    print("JSON:")
    client_code(simple)

    yaml_component = YamlDecorator(simple)

    print("\nYAML:")
    client_code(yaml_component)

    csv_component = CsvDecorator(simple)

    print("\nCSV:")
    client_code(csv_component)

    yaml_component.save_to_file("currencies.yaml")

    csv_component.save_to_file("currencies.csv")
```


### **Тесты программы test_main.py**

```python 
import unittest

from main import (
    ConcreteComponent,
    YamlDecorator,
    CsvDecorator
)


class TestCurrencies(unittest.TestCase):

    def test_json_response(self):

        component = ConcreteComponent()

        result = component.operation()

        self.assertIn("Valute", result)

    def test_json_type(self):

        component = ConcreteComponent()

        result = component.operation()

        self.assertIsInstance(result, dict)

    def test_yaml_response(self):

        component = YamlDecorator(
            ConcreteComponent()
        )

        result = component.operation()

        self.assertIsInstance(result, str)

    def test_yaml_contains_currency(self):

        component = YamlDecorator(
            ConcreteComponent()
        )

        result = component.operation()

        self.assertIn("USD", result)

    def test_csv_response(self):

        component = CsvDecorator(
            ConcreteComponent()
        )

        result = component.operation()

        self.assertIsInstance(result, list)

    def test_csv_contains_data(self):

        component = CsvDecorator(
            ConcreteComponent()
        )

        result = component.operation()

        self.assertTrue(len(result) > 0)


if __name__ == "__main__":
    unittest.main()
```

### **Объяснение работы программы**

1. Базовый компонент получает JSON-данные с API ЦБ РФ.
2. Декоратор YAML преобразует данные в YAML-формат.
3. Декоратор CSV преобразует данные в CSV-формат.
4. Каждый декоратор может сохранить данные в файл.
5. Тесты проверяют корректность работы всех компонентов.


### **Пример входных данных**

```python 
https://www.cbr-xml-daily.ru/daily_json.js
```

### **Пример вывода программы**

```python 
[
    ['USD', 'Доллар США', 89.12],
    ['EUR', 'Евро', 97.45]
]
```

### **Результат работы**

Программа успешно реализует шаблон проектирования «Декоратор» для работы с валютами, преобразует данные в YAML и CSV форматы, а также сохраняет результаты в файлы.


---
## Задание на использование шаблона "Одиночка"

### **Описание программы**

Данная программа реализует получение курсов валют с сайта Центрального Банка РФ в объектно-ориентированном стиле.

В программе используется шаблон проектирования Singleton (Одиночка), реализованный через метакласс. Это позволяет создать только один объект класса во время работы программы.

Программа:

* получает курсы валют по ID;
* сохраняет значения валют;
* ограничивает частоту запросов;
* визуализирует данные в виде графика;
* поддерживает тестирование работы методов.

### **Что реализовано**

* Шаблон проектирования Singleton через метакласс.
* Получение XML-данных с сайта ЦБ РФ.
* Парсинг XML-файла.
* Работа с валютами по ID.
* Хранение дробной и целой части отдельно.
* Ограничение частоты запросов.
* Геттеры и сеттеры.
* Визуализация валют в графике.
* Сохранение графика в файл `currencies.jpg`.
* Набор тестов с использованием `unittest`.


### **Код программы main.py**

```python 
import requests
import time
from xml.etree import ElementTree as ET
import matplotlib.pyplot as plt


class SingletonMeta(type):
    """
    Метакласс Singleton.
    """

    _instance = None

    def __call__(cls, *args, **kwargs):

        if cls._instance is None:
            cls._instance = super().__call__(*args, **kwargs)

        return cls._instance


class CurrenciesLst(metaclass=SingletonMeta):
    """
    Класс для работы с валютами.
    """

    def __init__(self, delay=1):

        self.__cur_lst = []
        self.__delay = delay
        self.__last_request_time = 0

    def __del__(self):
        """
        Деструктор класса.
        """

        self.__cur_lst.clear()

    def get_currencies(self, currencies_ids_lst: list) -> list:
        """
        Получение курсов валют.
        """

        current_time = time.time()

        if current_time - self.__last_request_time < self.__delay:
            raise Exception("Слишком частые запросы")

        self.__last_request_time = current_time

        response = requests.get(
            'http://www.cbr.ru/scripts/XML_daily.asp'
        )

        root = ET.fromstring(response.content)

        result = []

        for valute in root.findall("Valute"):

            valute_id = valute.get('ID')

            if valute_id in currencies_ids_lst:

                name = valute.find('Name').text
                value = valute.find('Value').text
                char_code = valute.find('CharCode').text
                nominal = valute.find('Nominal').text

                integer_part, fractional_part = value.split(',')

                result.append({
                    char_code: (
                        name,
                        (integer_part, fractional_part),
                        nominal
                    )
                })

        for currency_id in currencies_ids_lst:

            found = False

            for item in result:
                if currency_id in str(item):
                    found = True

            if not found:
                result.append({currency_id: None})

        self.__cur_lst = result

        return result

    def get_cur_lst(self):
        """
        Геттер списка валют.
        """

        return self.__cur_lst

    def set_delay(self, delay):
        """
        Сеттер задержки запросов.
        """

        self.__delay = delay

    def visualize_currencies(self):
        """
        Построение графика валют.
        """

        currencies = []
        values = []

        for item in self.__cur_lst:

            for key, value in item.items():

                if value is not None:

                    currencies.append(key)

                    integer_part = value[1][0]
                    fractional_part = value[1][1]

                    full_value = float(
                        integer_part + "." + fractional_part
                    )

                    values.append(full_value)

        plt.bar(currencies, values)

        plt.title("Курсы валют")

        plt.savefig("currencies.jpg")

        plt.show()


if __name__ == '__main__':

    currencies = CurrenciesLst()

    result = currencies.get_currencies(
        ['R01035', 'R01335', 'R01700J']
    )

    print(result)

    currencies.visualize_currencies()
```


### **Тесты программы test_currency.py**

```python 
import unittest

from main import CurrenciesLst


class TestCurrencies(unittest.TestCase):

    def test_wrong_id(self):

        currencies = CurrenciesLst()

        result = currencies.get_currencies(['R9999'])

        self.assertEqual(result, [{'R9999': None}])

    def test_gbp_currency(self):

        currencies = CurrenciesLst()

        result = currencies.get_currencies(['R01035'])

        currency = result[0]['GBP'][0]

        self.assertEqual(
            currency,
            'Фунт стерлингов Соединенного королевства'
        )

    def test_currency_value_range(self):

        currencies = CurrenciesLst()

        result = currencies.get_currencies(['R01035'])

        integer_part = int(result[0]['GBP'][1][0])

        self.assertTrue(0 <= integer_part <= 999)


if __name__ == '__main__':
    unittest.main()
```

### **Объяснение работы программы**

1. Создается Singleton-объект класса `CurrenciesLst`.
2. Выполняется запрос к сайту ЦБ РФ.
3. XML-файл обрабатывается и извлекаются нужные валюты.
4. Значения валют разделяются на целую и дробную часть.
5. Результат сохраняется в список.
6. При повторном запросе раньше заданного времени вызывается ошибка.
7. Метод `visualize_currencies` строит график курсов валют.


### **Пример входных данных**

```python 
['R01035', 'R01335', 'R01700J']
```

### **Вывод программы**

```python 
    {
        'GBP': (
            'Фунт стерлингов Соединенного королевства',
            ('113', '2069'),
            '1'
        )
    },

    {
        'KZT': (
            'Казахстанских тенге',
            ('19', '8264'),
            '100'
        )
    },

    {
        'TRY': (
            'Турецких лир',
            ('33', '1224'),
            '10'
        )
    }
]
```

### **Результат работы**

Программа успешно получает и обрабатывает курсы валют с сайта ЦБ РФ, реализует шаблон Singleton, ограничивает частоту запросов и строит график изменения валют.

--- 