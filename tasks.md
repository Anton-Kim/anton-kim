## Задачи с решениями

1. [Ближайший ноль](#ближайший-ноль)
2. [Стек - Max](#стек---max)
3. [Стек - MaxEffective](#стек---maxeffective)
4. [Скобочная последовательность](#скобочная-последовательность)
5. [Списочная очередь](#списочная-очередь)
6. [Дек](#дек)
7. [Калькулятор](#калькулятор)
8. [Комбинации](#комбинации)
9. [Подпоследовательность](#подпоследовательность)
10. [Гардероб](#гардероб)
11. [Большое число](#большое-число)
12. [Пузырек](#пузырек)
13. [Клумбы](#клумбы)
14. [Поиск в сломанном массиве](#поиск-в-сломанном-массиве)
15. [Эффективная быстрая сортировка](#эффективная-быстрая-сортировка)

### Ближайший ноль
Тимофей ищет место, чтобы построить себе дом. Улица, на которой он хочет жить, имеет длину n, то есть состоит из n одинаковых идущих подряд участков. Каждый участок либо пустой, либо на нём уже построен дом.
Общительный Тимофей не хочет жить далеко от других людей на этой улице. Поэтому ему важно для каждого участка знать расстояние до ближайшего пустого участка. Если участок пустой, эта величина будет равна нулю — расстояние до самого себя.
Помогите Тимофею посчитать искомые расстояния. Для этого у вас есть карта улицы. Дома в городе Тимофея нумеровались в том порядке, в котором строились, поэтому их номера на карте никак не упорядочены. Пустые участки обозначены нулями.

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке дана длина улицы —– n (1 ≤ n ≤ 106). В следующей строке записаны n целых неотрицательных чисел — номера домов и обозначения пустых участков на карте (нули). Гарантируется, что в последовательности есть хотя бы один ноль. Номера домов (положительные числа) уникальны и не превосходят 10\*\*9.

**Формат вывода:** Для каждого из участков выведите расстояние до ближайшего нуля. Числа выводите в одну строку, разделяя их пробелами.
```python
def data():
    n = input()
    areas = ['1' if elem != '0' else '0' for elem in input().split()]
    return areas


def find_furthest_zeros(elems, side):
    """Функция нахождения индексов крайних нулей в списке строчных цифр"""
    lst_str = ''.join(elems)  # rindex не работает на списке
    return lst_str.index('0') if side == 'l' else lst_str.rindex('0')


def distances_from_zero(elems, left_zero, right_zero):
    """Функция для определения расстояния от элемента в списке до ближайшего
    нуля"""
    for i in range(left_zero, len(elems)):
        elems[i] = '0' if elems[i] == '0' else int(elems[i - 1]) + 1
    for i in range(right_zero, left_zero, -1):
        elems[i] = '0' if elems[i] == '0' else min(
            elems[i], int(elems[i + 1]) + 1
        )
    for i in range(left_zero, -1, -1):
        elems[i] = '0' if elems[i] == '0' else int(elems[i + 1]) + 1
    return elems


def main():
    areas = data()
    left_zero = find_furthest_zeros(areas, 'l')
    right_zero = find_furthest_zeros(areas, 'r')
    areas = distances_from_zero(areas, left_zero, right_zero)
    print(*areas)


if __name__ == "__main__":
    main()
```
</details>

____

### Стек - Max
Нужно реализовать класс StackMax, который поддерживает операцию определения максимума среди всех элементов в стеке. Класс должен поддерживать операции push(x), где x – целое число, pop() и get_max().

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке записано одно число n — количество команд, которое не превосходит 10000. В следующих n строках идут команды. Команды могут быть следующих видов:
- push(x) — добавить число x в стек;
- pop() — удалить число с вершины стека;
- get_max() — напечатать максимальное число в стеке;
Если стек пуст, при вызове команды get_max() нужно напечатать «None», для команды pop() — «error».

**Формат вывода:** Для каждой команды get_max() напечатайте результат её выполнения. Если стек пустой, для команды get_max() напечатайте «None». Если происходит удаление из пустого стека — напечатайте «error».
```python
class StackMax:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if len(self.items):
            return self.items.pop()
        else:
            print('error')

    def get_max(self):
        if len(self.items):
            print(max(self.items))
        else:
            print('None')


n = int(input())
stack = StackMax()

for _ in range(n):
    s = input().split()
    if s[0] == 'push':
        stack.push(int(s[1]))
    elif s[0] == 'pop':
        stack.pop()
    elif s[0] == 'get_max':
        stack.get_max()
```
</details>

____

### Стек - MaxEffective
Реализуйте класс StackMaxEffective, поддерживающий операцию определения максимума среди элементов в стеке. Сложность операции должна быть O(1). Для пустого стека операция должна возвращать None. При этом push(x) и pop() также должны выполняться за константное время.

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке записано одно число — количество команд, оно не превосходит 100000. Далее идут команды по одной в строке. Команды могут быть следующих видов:

- push(x) — добавить число x в стек;
- pop() — удалить число с вершины стека;
- get_max() — напечатать максимальное число в стеке;
Если стек пуст, при вызове команды get_max нужно напечатать «None», для команды pop — «error».

**Формат вывода:** Для каждой команды get_max() напечатайте результат её выполнения. Если стек пустой, для команды get_max() напечатайте «None». Если происходит удаление из пустого стека — напечатайте «error».
```python
class StackMaxEffective:
    def __init__(self):
        self.items = []

    def push(self, item):
        if self.items:
            new_max = max(item, self.items[-1])
        else:
            new_max = item
        self.items.append(new_max)

    def pop(self):
        if self.items:
            return self.items.pop()
        else:
            print('error')

    def get_max(self):
        if self.items:
            print(self.items[-1])
        else:
            print('None')


n = int(input())
stack = StackMaxEffective()

for _ in range(n):
    s = input().split()
    if s[0] == 'push':
        stack.push(int(s[1]))
    else:
        d = {'pop': stack.pop, 'get_max': stack.get_max}
        d[s[0]]()
```
</details>

____

### Скобочная последовательность
Вот какую задачу Тимофей предложил на собеседовании одному из кандидатов. Если вы с ней ещё не сталкивались, то наверняка столкнётесь –— она довольно популярная.
Дана скобочная последовательность. Нужно определить, правильная ли она.
Будем придерживаться такого определения:

- пустая строка —– правильная скобочная последовательность;
- правильная скобочная последовательность, взятая в скобки одного типа, –— правильная скобочная последовательность;
- правильная скобочная последовательность с приписанной слева или справа правильной скобочной последовательностью —– тоже правильная.

На вход подаётся последовательность из скобок трёх видов: [], (), {}.
Напишите функцию is_correct_bracket_seq, которая принимает на вход скобочную последовательность и возвращает True, если последовательность правильная, а иначе False.

<details>
<summary>Решение</summary>

**Формат ввода:** На вход подаётся одна строка, содержащая скобочную последовательность. Скобки записаны подряд, без пробелов.

**Формат вывода:** Выведите «True» или «False».
```python
def is_correct_bracket_seq(seq):
    if not seq:
        return True
    while '()' in seq or '[]' in seq or '{}' in seq:
        if '()' in seq:
            seq = seq.replace('()', '')
        elif '[]' in seq:
            seq = seq.replace('[]', '')
        elif '{}' in seq:
            seq = seq.replace('{}', '')
    return not seq


print(is_correct_bracket_seq(input()))
```
</details>

____

### Списочная очередь
Любимый вариант очереди Тимофея — очередь, написанная с использованием связного списка. Помогите ему с реализацией. Очередь должна поддерживать выполнение трёх команд:

- get() — вывести элемент, находящийся в голове очереди, и удалить его. Если очередь пуста, то вывести «error».
- put(x) — добавить число x в очередь
- size() — вывести текущий размер очереди

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке записано количество команд n — целое число, не превосходящее 1000. В каждой из следующих n строк записаны команды по одной строке.

**Формат вывода:** Выведите ответ на каждый запрос по одному в строке.
```python
class ListQueue:
    class Node:
        def __init__(self, value=None, next_item=None):
            self.value = value
            self.next_item = next_item

        def __str__(self):
            return self.value

    def __init__(self):
        self.head = self.Node()
        self.tail = self.Node()
        self.size = 0

    def get(self):
        if self.size == 0:
            return 'error'
        x = self.head
        if self.size == 1:
            self.head = self.Node()
            self.tail = self.Node()
            self.size -= 1
            return x
        if self.size == 2:
            x = self.head
            self.head = self.tail
            self.size -= 1
            return x
        x = self.head
        self.head = self.tail.next_item.next_item  # self.head.next_item
        self.tail.next_item = self.head
        self.size -= 1
        return x

    def put(self, x):
        if self.size == 0:
            self.head = self.Node(value=x)
            self.tail = self.head
        else:
            self.tail.next_item = self.Node(value=x)
            self.tail.next_item.next_item = self.head
            self.tail = self.tail.next_item
        self.size += 1


n = int(input())
s = ListQueue()
res = []
for _ in range(n):
    com = input().split()
    if len(com) == 2:
        s.put(com[1])
    if com[0] == 'get':
        print(s.get())
    if com[0] == 'size':
        print(s.size)
```
</details>

____

### Дек
Гоша реализовал структуру данных Дек, максимальный размер которого определяется заданным числом. Методы push_back(x), push_front(x), pop_back(), pop_front() работали корректно. Но, если в деке было много элементов, программа работала очень долго. Дело в том, что не все операции выполнялись за O(1). Помогите Гоше! Напишите эффективную реализацию.

**Внимание: при реализации используйте кольцевой буфер.**

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке записано количество команд n — целое число, не превосходящее 100000. Во второй строке записано число m — максимальный размер дека. Он не превосходит 50000. В следующих n строках записана одна из команд:

- push_back(value) – добавить элемент в конец дека. Если в деке уже находится максимальное число элементов, вывести «error».
- push_front(value) – добавить элемент в начало дека. Если в деке уже находится максимальное число элементов, вывести «error».
- pop_front() – вывести первый элемент дека и удалить его. Если дек был пуст, то вывести «error».
- pop_back() – вывести последний элемент дека и удалить его. Если дек был пуст, то вывести «error».

Value — целое число, по модулю не превосходящее 1000.

**Формат вывода:** Выведите результат выполнения каждой команды на отдельной строке. Для успешных запросов push_back(x) и push_front(x) ничего выводить не надо.
```python
class MyDeque:
    """Класс структуры данных Дек"""

    def __init__(self, max_size):
        self._queue = [None] * max_size
        self._max_value = max_size
        self._head = 0
        self._tail = 0
        self._size = 0

    def no_overflow(self):
        """Проверка на переполненность дека"""
        return self._size < self._max_value

    def push_front(self, value):
        """Добавить элемент в начало дека"""
        if self._size == 0:
            self._queue[self._head] = value
            self._size += 1
        elif self.no_overflow():
            self._head = (self._head + 1) % self._max_value
            self._queue[self._head] = value
            self._size += 1
        else:
            raise OverflowError

    def push_back(self, value):
        """Добавить элемент в конец дека"""
        if self._size == 0:
            self._queue[self._tail] = value
            self._size += 1
        elif self.no_overflow():
            self._tail = (self._tail - 1) % self._max_value
            self._queue[self._tail] = value
            self._size += 1
        else:
            raise OverflowError

    def pop_front(self):
        """Вывести первый элемент дека и удалить его"""
        if self._size == 1:
            x = self._queue[self._head]
            self._queue[self._head] = None
            self._size -= 1
            return x
        elif self._size > 1:
            x = self._queue[self._head]
            self._queue[self._head] = None
            self._head = (self._head - 1) % self._max_value
            self._size -= 1
            return x
        else:
            raise IndexError

    def pop_back(self):
        """Вывести последний элемент дека и удалить его"""
        if self._size == 1:
            x = self._queue[self._tail]
            self._queue[self._tail] = None
            self._size -= 1
            return x
        elif self._size > 1:
            x = self._queue[self._tail]
            self._queue[self._tail] = None
            self._tail = (self._tail + 1) % self._max_value
            self._size -= 1
            return x
        else:
            raise IndexError


def data():
    """Функция для получения начальных данных"""
    n, m = int(input()), int(input())
    d = MyDeque(m)
    return n, d


def command_handler(cnt, handler):
    """Функция для обработки входящих команд"""
    for _ in range(cnt):
        command = input().split()
        if len(command) > 1:
            if command[0] == 'push_front':
                try:
                    handler.push_front(command[1])
                except OverflowError:
                    print('error')
            elif command[0] == 'push_back':
                try:
                    handler.push_back(command[1])
                except OverflowError:
                    print('error')
        else:
            if command[0] == 'pop_front':
                try:
                    print(handler.pop_front())
                except IndexError:
                    print('error')
            elif command[0] == 'pop_back':
                try:
                    print(handler.pop_back())
                except IndexError:
                    print('error')


def main():
    commands_count, deque = data()
    command_handler(commands_count, deque)


if __name__ == "__main__":
    main()
```
</details>

____

### Калькулятор
Задание связано с обратной польской нотацией. Она используется для парсинга арифметических выражений. Еще её иногда называют постфиксной нотацией.
В постфиксной нотации операнды расположены перед знаками операций.

Пример 1:

3 4 + означает 3 + 4 и равно 7

Пример 2:

12 5 / Так как деление целочисленное, то в результате получим 2.

Пример 3:

10 2 4 * - означает 10 - 2 * 4 и равно 2

Разберём последний пример подробнее:

Знак * стоит сразу после чисел 2 и 4, значит к ним нужно применить операцию, которую этот знак обозначает, то есть перемножить эти два числа. В результате получим 8.

После этого выражение приобретёт вид:

10 8 - Операцию «минус» нужно применить к двум идущим перед ней числам, то есть 10 и 8. В итоге получаем 2.

Рассмотрим алгоритм более подробно. Для его реализации будем использовать стек.

Для вычисления значения выражения, записанного в обратной польской нотации, нужно считывать выражение слева направо и придерживаться следующих шагов:

1. Обработка входного символа:
    - Если на вход подан операнд, он помещается на вершину стека.
    - Если на вход подан знак операции, то эта операция выполняется над требуемым количеством значений, взятых из стека в порядке добавления. Результат выполненной операции помещается на вершину стека.
2. Если входной набор символов обработан не полностью, перейти к шагу 1.
3. После полной обработки входного набора символов результат вычисления выражения находится в вершине стека. Если в стеке осталось несколько чисел, то надо вывести только верхний элемент.

**Замечание про отрицательные числа и деление:** в этой задаче под делением понимается математическое целочисленное деление. Это значит, что округление всегда происходит вниз. А именно: если a / b = c, то b ⋅ c — это наибольшее число, которое не превосходит a и одновременно делится без остатка на b.

Например, -1 / 3 = -1. Будьте осторожны: в C++, Java и Go, например, деление чисел работает иначе.

В текущей задаче гарантируется, что деления на отрицательное число нет.

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке записано количество команд n — целое число, не превосходящее 100000. Во второй строке записано число m — максимальный размер дека. Он не превосходит 50000. В следующих n строках записана одна из команд:

- push_back(value) – добавить элемент в конец дека. Если в деке уже находится максимальное число элементов, вывести «error».
- push_front(value) – добавить элемент в начало дека. Если в деке уже находится максимальное число элементов, вывести «error».
- pop_front() – вывести первый элемент дека и удалить его. Если дек был пуст, то вывести «error».
- pop_back() – вывести последний элемент дека и удалить его. Если дек был пуст, то вывести «error».

Value — целое число, по модулю не превосходящее 1000.

**Формат вывода:** Выведите результат выполнения каждой команды на отдельной строке. Для успешных запросов push_back(x) и push_front(x) ничего выводить не надо.
```python
class MyDeque:
    """Класс структуры данных Дек"""

    def __init__(self, max_size):
        self._queue = [None] * max_size
        self._max_value = max_size
        self._head = 0
        self._tail = 0
        self._size = 0

    def no_overflow(self):
        """Проверка на переполненность дека"""
        return self._size < self._max_value

    def push_front(self, value):
        """Добавить элемент в начало дека"""
        if self._size == 0:
            self._queue[self._head] = value
            self._size += 1
        elif self.no_overflow():
            self._head = (self._head + 1) % self._max_value
            self._queue[self._head] = value
            self._size += 1
        else:
            raise OverflowError

    def push_back(self, value):
        """Добавить элемент в конец дека"""
        if self._size == 0:
            self._queue[self._tail] = value
            self._size += 1
        elif self.no_overflow():
            self._tail = (self._tail - 1) % self._max_value
            self._queue[self._tail] = value
            self._size += 1
        else:
            raise OverflowError

    def pop_front(self):
        """Вывести первый элемент дека и удалить его"""
        if self._size == 1:
            x = self._queue[self._head]
            self._queue[self._head] = None
            self._size -= 1
            return x
        elif self._size > 1:
            x = self._queue[self._head]
            self._queue[self._head] = None
            self._head = (self._head - 1) % self._max_value
            self._size -= 1
            return x
        else:
            raise IndexError

    def pop_back(self):
        """Вывести последний элемент дека и удалить его"""
        if self._size == 1:
            x = self._queue[self._tail]
            self._queue[self._tail] = None
            self._size -= 1
            return x
        elif self._size > 1:
            x = self._queue[self._tail]
            self._queue[self._tail] = None
            self._tail = (self._tail + 1) % self._max_value
            self._size -= 1
            return x
        else:
            raise IndexError


def data():
    """Функция для получения начальных данных"""
    n, m = int(input()), int(input())
    d = MyDeque(m)
    return n, d


def command_handler(cnt, handler):
    """Функция для обработки входящих команд"""
    for _ in range(cnt):
        command = input().split()
        if len(command) > 1:
            if command[0] == 'push_front':
                try:
                    handler.push_front(command[1])
                except OverflowError:
                    print('error')
            elif command[0] == 'push_back':
                try:
                    handler.push_back(command[1])
                except OverflowError:
                    print('error')
        else:
            if command[0] == 'pop_front':
                try:
                    print(handler.pop_front())
                except IndexError:
                    print('error')
            elif command[0] == 'pop_back':
                try:
                    print(handler.pop_back())
                except IndexError:
                    print('error')


def main():
    commands_count, deque = data()
    command_handler(commands_count, deque)


if __name__ == "__main__":
    main()
```
</details>

____

### Комбинации
На клавиатуре старых мобильных телефонов каждой цифре соответствовало несколько букв. Примерно так:

2:'abc', 3:'def', 4:'ghi', 5:'jkl', 6:'mno', 7:'pqrs', 8:'tuv', 9:'wxyz'

Вам известно в каком порядке были нажаты кнопки телефона, без учета повторов. Напечатайте все комбинации букв, которые можно набрать такой последовательностью нажатий.

<details>
<summary>Решение</summary>

**Формат ввода:** На вход подается строка, состоящая из цифр 2-9 включительно. Длина строки не превосходит 10 символов.

**Формат вывода:** Выведите все возможные комбинации букв через пробел.
```python
d = {'2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl', '6': 'mno', '7': 'pqrs',
     '8': 'tuv', '9': 'wxyz'}


def two_digs(data):
    res = []
    for dig_1 in d[data[-2]]:
        for dig_2 in d[data[-1]]:
            res.append(dig_1 + dig_2)
    return res


def tel_rec(digits):
    if len(digits) == 1:
        print(*digits[0])
    elif len(digits) == 2:
        print(*two_digs(digits))
    else:
        res = two_digs(digits)
        digits = digits[:-2]
        while digits != '':
            res = [x + y for x in d[digits[-1]] for y in res]
            digits = digits[:-1]
        print(*res)


tel_rec(input())
```
</details>

____

### Подпоследовательность
Гоша любит играть в игру «Подпоследовательность»: даны 2 строки, и нужно понять, является ли первая из них подпоследовательностью второй. Когда строки достаточно длинные, очень трудно получить ответ на этот вопрос, просто посмотрев на них. Помогите Гоше написать функцию, которая решает эту задачу.

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке записана строка s.

Во второй —- строка t.

Обе строки состоят из маленьких латинских букв, длины строк не превосходят 150000. Строки не могут быть пустыми.

**Формат вывода:** Выведите True, если s является подпоследовательностью t, иначе —– False.
```python
s, t = input(), input()


def check_substring(sub, text):
    flag = True
    ind = 0
    for char in sub:
        ind = text.find(char, ind)
        if ind == -1:
            flag = False
            break
        else:
            ind += 1
    return flag


print(check_substring(s, t))
```
</details>

____

### Гардероб
Рита решила оставить у себя одежду только трёх цветов: розового, жёлтого и малинового. После того как вещи других расцветок были убраны, Рита захотела отсортировать свой новый гардероб по цветам. Сначала должны идти вещи розового цвета, потом —– жёлтого, и в конце —– малинового. Помогите Рите справиться с этой задачей.

Примечание: попробуйте решить задачу за один проход по массиву!

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке задано количество предметов в гардеробе: n –— оно не превосходит 1000000. Во второй строке даётся массив, в котором указан цвет для каждого предмета. Розовый цвет обозначен 0, жёлтый —– 1, малиновый –— 2.

**Формат вывода:** Нужно вывести в строку через пробел цвета предметов в правильном порядке.
```python
def counting_sort(array, k=3):
    counted_values = [0] * k
    new_array = []
    for value in array:
        counted_values[value] += 1
    for i in range(k):
        new_array += ([i] * counted_values[i])
    return new_array


n, colors = int(input()), list(map(int, input().split()))
print(*counting_sort(colors))
```
</details>

____

### Большое число
Вечером ребята решили поиграть в игру «Большое число».
Даны числа. Нужно определить, какое самое большое число можно из них составить.

<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке записано n — количество чисел. Оно не превосходит 100.
Во второй строке через пробел записаны n неотрицательных чисел, каждое из которых не превосходит 1000.

**Формат вывода:** Нужно вывести самое большое число, которое можно составить из данных чисел.
```python
n = int(input())
source_array = input().split()


def bubble_sort(num, seq):
    for i in range(num - 1):
        for j in range(0, num - i - 1):
            var1 = seq[j] + seq[j + 1]
            var2 = seq[j + 1] + seq[j]
            if var1 < var2:
                seq[j], seq[j + 1] = seq[j + 1], seq[j]

    print(''.join(seq))


bubble_sort(n, source_array)
```
</details>

____

### Пузырек
Чтобы выбрать самый лучший алгоритм для решения задачи, Гоша продолжил изучать разные сортировки. На очереди сортировка пузырьком — https://ru.wikipedia.org/wiki/Сортировка_пузырьком

Её алгоритм следующий (сортируем по неубыванию):

1. На каждой итерации проходим по массиву, поочередно сравнивая пары соседних элементов. Если элемент на позиции i больше элемента на позиции i + 1, меняем их местами. После первой итерации самый большой элемент всплывёт в конце массива.
2. Проходим по массиву, выполняя указанные действия до тех пор, пока на очередной итерации не окажется, что обмены больше не нужны, то есть массив уже отсортирован.
3. После не более чем n – 1 итераций выполнение алгоритма заканчивается, так как на каждой итерации хотя бы один элемент оказывается на правильной позиции.

Помогите Гоше написать код алгоритма.
<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке на вход подаётся натуральное число n — длина массива, 2 ≤ n ≤ 1000.
Во второй строке через пробел записано n целых чисел.
Каждое из чисел по модулю не превосходит 1000.

Обратите внимание, что считывать нужно только 2 строки: значение n и входной массив.

**Формат вывода:** После каждого прохода по массиву, на котором какие-то элементы меняются местами, выводите его промежуточное состояние.
Таким образом, если сортировка завершена за k меняющих массив итераций, то надо вывести k строк по n чисел в каждой — элементы массива после каждой из итераций.
Если массив был изначально отсортирован, то просто выведите его.
```python
n = input()
digits = list(map(int, input().split()))


def bubble_sort(seq):
    first_temp_seq = seq[:]
    stop = len(seq) - 1
    while stop > 0:
        counter = 0
        temp_seq = seq[:]
        while counter < stop:
            if seq[counter] > seq[counter + 1]:
                seq[counter], seq[counter + 1] = seq[counter + 1], seq[counter]
            counter += 1
        if first_temp_seq == seq:
            print(*seq)
            break
        elif temp_seq != seq:
            print(*seq)
        stop -= 1
    return seq


bubble_sort(digits)
```
</details>

____

### Клумбы
Алла захотела, чтобы у неё под окном были узкие клумбы с тюльпанам. На схеме земельного участка клумбы обозначаются просто горизонтальными отрезками, лежащими на одной прямой. Для ландшафтных работ было нанято n садовников. Каждый из них обрабатывал какой-то отрезок на схеме. Процесс был организован не очень хорошо, иногда один и тот же отрезок или его часть могли быть обработаны сразу несколькими садовниками. Таким образом, отрезки, обрабатываемые двумя разными садовниками, сливаются в один. Непрерывный обработанный отрезок затем станет клумбой. Нужно определить границы будущих клумб.

Рассмотрим примеры.

**Пример 1:**
Два одинаковых отрезка [7, 8] и [7, 8] сливаются в один, но потом их накрывает отрезок [6, 10]. Таким образом, имеем две клумбы с координатами [2,3] и [6,10].

**Пример 2**
Отрезки [2,3], [3, 4] и [3,4] сольются в один отрезок [2,4]. Отрезок [5,6] ни с кем не объединяется, добавляем его в ответ.
<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке задано количество садовников n. Число садовников не превосходит 100 000.

В следующих n строках через пробел записаны координаты клумб в формате: start end, где start —– координата начала, end —– координата конца. Оба числа целые, неотрицательные и не превосходят 107. start строго меньше, чем end.

Обратите внимание, что считывать нужно только 2 строки: значение n и входной массив.

**Формат вывода:** Нужно вывести координаты каждой из получившихся клумб в отдельных строках. Данные должны выводится в отсортированном порядке —– сначала клумбы с меньшими координатами, затем —– с бОльшими.
```python
gards = []
for _ in range(int(input())):
    gard = [int(x) for x in input().split()]
    gards.append(gard)

gards = sorted(gards)
res = [gards[0]]

for gard in gards[1:]:
    if res[-1][0] <= gard[0] <= res[-1][1] <= gard[1]:
        res[-1][1] = gard[1]
    elif gard[0] > res[-1][1]:
        res.append(gard)

for gard in res:
    print(*gard)
```
</details>

____

### Поиск в сломанном массиве
Алла ошиблась при копировании из одной структуры данных в другую. Она хранила массив чисел в кольцевом буфере. Массив был отсортирован по возрастанию, и в нём можно было найти элемент за логарифмическое время. Алла скопировала данные из кольцевого буфера в обычный массив, но сдвинула данные исходной отсортированной последовательности. Теперь массив не является отсортированным. Тем не менее, нужно обеспечить возможность находить в нем элемент за O(logn).
Можно предполагать, что в массиве только уникальные элементы.
<details>
<summary>Решение</summary>

**Формат ввода:** Функция принимает массив натуральных чисел и искомое число k. Длина массива не превосходит 10000
. Элементы массива и число k не превосходят по значению 10000.
В примерах:

В первой строке записано число n — длина массива.

Во второй строке записано положительное число k — искомый элемент. 

Далее в строку через пробел записано n натуральных чисел – элементы массива.

**Формат вывода:** Функция должна вернуть индекс элемента, равного k, если такой есть в массиве (нумерация с нуля). Если элемент не найден, функция должна вернуть −1. Изменять массив нельзя.

Для отсечения неэффективных решений ваша функция будет запускаться от 100000 до 1000000 раз.
```python
def broken_search(nums: list, target: int) -> int:
    """Функция для поиска в сломанном массиве"""

    left, right = 0, len(nums) - 1
    while left <= right:
        middle = (left + right) // 2
        mid_value = nums[middle]
        if target == mid_value:
            return middle
        if mid_value <= nums[right]:
            if mid_value < target <= nums[right]:
                left = middle + 1
            else:
                right = middle - 1
        else:
            if nums[left] <= target < mid_value:
                right = middle - 1
            else:
                left = middle + 1
    return -1


def test():
    arr = [19, 21, 100, 101, 1, 4, 5, 7, 12]
    assert broken_search(arr, 5) == 6
```
</details>

____

### Эффективная быстрая сортировка
Тимофей решил организовать соревнование по спортивному программированию, чтобы найти талантливых стажёров. Задачи подобраны, участники зарегистрированы, тесты написаны. Осталось придумать, как в конце соревнования будет определяться победитель.

Каждый участник имеет уникальный логин. Когда соревнование закончится, к нему будут привязаны два показателя: количество решённых задач Pi и размер штрафа Fi. Штраф начисляется за неудачные попытки и время, затраченное на задачу.

Тимофей решил сортировать таблицу результатов следующим образом: при сравнении двух участников выше будет идти тот, у которого решено больше задач. При равенстве числа решённых задач первым идёт участник с меньшим штрафом. Если же и штрафы совпадают, то первым будет тот, у которого логин идёт раньше в алфавитном (лексикографическом) порядке.

Тимофей заказал толстовки для победителей и накануне поехал за ними в магазин. В своё отсутствие он поручил вам реализовать алгоритм быстрой сортировки (англ. quick sort) для таблицы результатов. Так как Тимофей любит спортивное программирование и не любит зря расходовать оперативную память, то ваша реализация сортировки не может потреблять O(n) дополнительной памяти для промежуточных данных (такая модификация быстрой сортировки называется "in-place").
<details>
<summary>Решение</summary>

**Формат ввода:** В первой строке задано число участников n, 1 ≤ n ≤ 100 000. В каждой из следующих n строк задана информация про одного из участников. i-й участник описывается тремя параметрами:

- уникальным логином (строкой из маленьких латинских букв длиной не более 20)
- числом решённых задач Pi
- штрафом Fi

Fi и Pi — целые числа, лежащие в диапазоне от 0 до 10**9.

**Формат вывода:** Для отсортированного списка участников выведите по порядку их логины по одному в строке.
```python
from random import randint


class Participant:
    """Класс участника с переопределенным методом сравнения"""

    def __init__(self, login: str, solved_tasks: str, penalty: str) -> None:
        self.login = login
        self.solved_tasks = int(solved_tasks)
        self.penalty = int(penalty)

    def __gt__(self, other):
        if self.solved_tasks == other.solved_tasks:
            if self.penalty == other.penalty:
                return self.login > other.login
            return self.penalty > other.penalty
        return self.solved_tasks < other.solved_tasks

    def __str__(self):
        return self.login


def inplace_quicksort(array: list, start: int, end: int) -> None:
    """Функция эффективной быстрой сортировки in-place"""

    if start >= end:
        return

    left, right = start, end
    pivot = array[randint(start, end)]

    while left <= right:
        while array[left] < pivot:
            left += 1
        while array[right] > pivot:
            right -= 1
        if left <= right:
            array[left], array[right] = array[right], array[left]
            left, right = left + 1, right - 1
    inplace_quicksort(array, start, right)
    inplace_quicksort(array, left, end)


if __name__ == '__main__':
    participants_count = int(input())
    participants = []
    for _ in range(participants_count):
        participants.append(Participant(*input().split()))
    inplace_quicksort(participants, 0, participants_count - 1)
    print(*participants, sep='\n')
```
</details>
