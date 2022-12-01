## Функции и приёмы

1. [Транспонирование матрицы](#транспонирование-матрицы)
2. [Сортировка словаря по ключу/значению](#сортировка-словаря-по-ключузначению)
3. [Вывод итерируемого объекта без цикла](#вывод-итерируемого-объекта-без-цикла)
4. [Преобразование цвета из RGB в HEX формат](#преобразование-цвета-из-rgb-в-hex-формат)
5. [Измерение быстродействия других функций](#измерение-быстродействия-других-функций)
6. [Конвертация арабских цифр в римские и наоборот](#конвертация-арабских-цифр-в-римские-и-наоборот)

### Транспонирование матрицы
```python
def transposed_matrix(matrix: list) -> list:
    return list(zip(*matrix))


print(transposed_matrix([[1, 2, 3], [4, 5, 6], [7, 8, 9]]))
# [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
```

____

### Сортировка словаря по ключу/значению
```python
# по ключу
print(dict(sorted({3: 'three', 1: 'one', 2: 'two'}.items())))
# {1: 'one', 2: 'two', 3: 'three'}

# или
print(dict(sorted({3: 'three', 1: 'one', 2: 'two'}.items(), key=lambda x: x[0])))
# {1: 'one', 2: 'two', 3: 'three'}

# по значению
print(dict(sorted({3: 'c', 1: 'a', 2: 'b'}.items(), key=lambda x: x[1])))
# {1: 'a', 2: 'b', 3: 'c'}
```

____

### Вывод итерируемого объекта без цикла
```python
# список
[print(digit) for digit in ['one', 'two', 'three']]
# one
# two
# three

# словарь
[print(f'{digit}: {string}') for digit, string in {1: 'one', 2: 'two', 3: 'three'}.items()]
# 1: one
# 2: two
# 3: three
```

____

### Преобразование цвета из RGB в HEX формат
```python
def rgb(r, g, b):
    """Функция для преобразования цвета из RGB в HEX формат"""
    check = lambda x: 0 if x < 0 else 255 if x > 255 else x
    return ('{:02x}' * 3).format(check(r), check(g), check(b)).upper()


print(rgb(255, 255, 255))
# FFFFFF
```

____

### Измерение быстродействия других функций
```python
import time

def time_of_function(func):
    """Функция для измерения быстродействия других функций"""
    start_time = time.time()
    result = func()
    execution_time = round(time.time() - start_time, 1)
    print(f'Время выполнения функции {func.__name__}: {execution_time} с.')
    return result


def sleep_one_sec():
    time.sleep(1)


time_of_function(sleep_one_sec)
# Время выполнения функции sleep_one_sec: 1.0 с.
```

____

### Конвертация арабских цифр в римские и наоборот
```python
class RomanNumerals:
    """Класс-конвертор арабских цифр в римские и наоборот"""
    d = {'M': 1000, 'CM': 900, 'D': 500, 'CD': 400, 'C': 100, 'XC': 90,
         'L': 50, 'XL': 40, 'X': 10, 'IX': 9, 'V': 5, 'IV': 4, 'I': 1}

    @classmethod
    def to_roman(cls, val):
        if val > 3999:
            return 'The maximum number that can be written in Roman numerals is 3999'
        elif val < 1:
            return 'The minimum number that can be written in Roman numerals is 1'
        d, res = {arabic: roman for roman, arabic in cls.d.items()}, ''
        while val > 0:
            for d_val in d:
                if d_val <= val:
                    res += d[d_val]
                    val -= d_val
                    break
        return res

    @classmethod
    def from_roman(cls, roman_num):
        d, res = cls.d, 0
        roman_num = list(roman_num)
        while roman_num:
            num = roman_num.pop(0)
            if not roman_num:
                res += d[num]
            else:
                if d[num] >= d[roman_num[0]]:
                    res += d[num]
                else:
                    res += d[roman_num.pop(0)] - d[num]
        return res


print(RomanNumerals.to_roman(2008))
# MMVIII
print(RomanNumerals.from_roman('MMVIII'))
# 2008
```
