# Test-task-Lesta-Games

## Вопрос №1
На языке Python написать алгоритм (функцию) определения четности целого числа, который будет аналогичен нижеприведенному по функциональности, но отличен по своей сути. Объяснить плюсы и минусы обеих реализаций. 

### Пример: 
```
def isEven(value):
      return value % 2 == 0
```

### Плюсы:
- Код читается легче, потому что такая реализация более привычна.
- Совместима с целыми числами, независимо от знака и размера.

### Минусы:
- Операция взятия остатка может быть менее эффективной, чем побитовое И, на некоторых процессорах.
- Потенциально чуть медленнее на больших данных, поскольку взятие остатка — арифметическая операция.
    
### Алгоритм с использованием побитового И:
```
def isEven(value):
    return (value & 1) == 0
```
### Плюсы:
- Операция побитового И обычно выполняется быстрее, чем взятие остатка, поскольку работает на уровне битов.
- Может быть предпочтительным в задачах, требующих высокой оптимизации и работы с низкоуровневыми операциями.

### Минусы:
- Менее читаемая для большинства программистов, так как проверка четности через побитовое И не так очевидна.
- Ограничена целыми числами; для вещественных чисел не подходит.

## Вопрос №2
На языке Python написать минимум по 2 класса реализовывающих циклический буфер FIFO. Объяснить плюсы и минусы каждой реализации.

## Вопрос №3
На языке Python предложить алгоритм, который быстрее всего (по процессорным тикам) отсортирует данный ей массив чисел. Массив может быть любого размера со случайным порядком чисел (в том числе и отсортированным). Объяснить, почему вы считаете, что функция соответствует заданным критериям.

Я считаю, что лучше всего будет использовать Timsort, поскольку сочетает преимущества сортировки слиянием и сортировки вставками. В Python есть готовый метод sort(), использующий Timsort.
```
def top_sort(arr):
    arr.sort()
    return arr
```
Если же использовать не готовую реализацию, то лучше всего подойдет быстрая сортировка с некоторыми улучшениями (выбор медианы из трёх в качестве опорного элемента (для снижения вероятности худшего случая) и переход к сортировке вставками на небольших подмассивах (поскольку это быстрее, чем рекурсивно вызывать быструю сортировку)).
```
def quicksort(arr, low, high):
    if high - low < 10: 
        insertion_sort(arr, low, high)
    elif low < high:
        pivot = median_of_three(arr, low, high)
        pi = partition(arr, low, high, pivot)
        quicksort(arr, low, pi - 1)
        quicksort(arr, pi + 1, high)

def median_of_three(arr, low, high):
    mid = (low + high) // 2
    if arr[low] > arr[mid]:
        arr[low], arr[mid] = arr[mid], arr[low]
    if arr[low] > arr[high]:
        arr[low], arr[high] = arr[high], arr[low]
    if arr[mid] > arr[high]:
        arr[mid], arr[high] = arr[high], arr[mid]
    arr[mid], arr[high - 1] = arr[high - 1], arr[mid]
    return arr[high - 1]

def partition(arr, low, high, pivot):
    left = low
    right = high - 1
    while True:
        while arr[left] < pivot:
            left += 1
        while arr[right] > pivot:
            right -= 1
        if left >= right:
            break
        arr[left], arr[right] = arr[right], arr[left]
    arr[left], arr[high - 1] = arr[high - 1], arr[left]
    return left

def insertion_sort(arr, low, high):
    for i in range(low + 1, high + 1):
        key = arr[i]
        j = i - 1
        while j >= low and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

def efficient_sort(arr):
    quicksort(arr, 0, len(arr) - 1)
    return arr

```
