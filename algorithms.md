# Алгоритмы

1. [Проверка на простоту числа](#проверка-на-простоту-числа)
2. [Определение простых чисел в диапазоне [0; n]](#определение-простых-чисел-в-диапазоне-0-n)
3. [Сортировка вставками](#сортировка-вставками)
4. [Сортировка слиянием](#сортировка-слиянием)
5. [Сортировка подсчетом](#сортировка-подсчетом)

### Проверка на простоту числа
```python
def is_prime(n: int) -> bool:
    if n == 1:
        return False
    i = 2
    while i * i <= n:
        if n % i == 0:
            return False
        i = i + 1
    return True


print(is_prime(7))
# True
```
Cложность: **O(n\*\*0.5)**

____

### Определение простых чисел в диапазоне [0; n]
```python
def get_least_primes_linear(n: int) -> list:
    lp = [0] * (n + 1)
    primes = []
    for i in range(2, n + 1):
        if lp[i] == 0:
            lp[i] = i
            primes.append(i)
        for p in primes:
            x = p * i
            if (p > lp[i]) or (x > n):
                break
            lp[x] = p
    return primes


print(get_least_primes_linear(11))
# [2, 3, 5, 7, 12]
```
Cложность: **O(n)**

____

### Сортировка вставками
```python
def insertion_sort(array: list) -> list:
    for i in range(1, len(array)):
        item_to_insert = array[i]
        j = i
        while j > 0 and item_to_insert < array[j - 1]:
            array[j] = array[j - 1]
            j -= 1
        array[j] = item_to_insert
    return array


print(insertion_sort([11, 2, 9, 7, 1]))
# [1, 2, 7, 9, 11]
```
Сложность: **O(n\*\*2)**

____

### Сортировка слиянием
```python
def merge_sort(array):
    if len(array) < 2:
        return array
    result = []
    mid = len(array) // 2
    left = merge_sort(array[:mid])
    right = merge_sort(array[mid:])
    l = 0
    r = 0
    while l < len(left) and r < len(right):
        if left[l] > right[r]:
            result.append(right[r])
            r += 1
        else:
            result.append(left[l])
            l += 1
    result += left[l:]
    result += right[r:]
    return result


print(merge_sort([7, 5, 1, 3, 7, 9]))
# [1, 3, 5, 7, 7, 9]
```
Cложность: **O(n*logn)**

____

### Сортировка подсчетом
Значения в массиве должны находятся в диапазоне [0, k)
```python
def counting_sort(array, k): # [5, 7, 1, 0, 1, 5, 11, 1]
    counted_values = [0] * k
    for value in array:
        counted_values[value] += 1 # [1, 3, 0, 0, 0, 2, 0, 1, 0, 0, 0, 1]

    index = 0
    for value in range(len(counted_values)):
        for count in range(counted_values[value]):
            array[index] = value
            index += 1


array = [4, 6, 1, 3, 11, 7]
counting_sort(array, 12)
print(array)
# [1, 3, 5, 7, 7, 9]
```
Cложность: **O(n*logn)**
