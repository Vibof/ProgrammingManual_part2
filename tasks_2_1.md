# Задания 1

Прежде всего следует ознакомиться с назначением и способвами использования следующих встроенных функций языка Julia:

- sort!(a), sort(a), sortperm!(a), sortperm(a)
- issorted
- size, length
- findall, findfirst, findlast, findprev, findnext
- findmin, findmax, findmin!, findmax!
- argmin, argmax
- collect
- view, @view
- zeros, ones
- Array, Vector, Matrix, fill, fill!,
- copy, deepcopy
- similar
- reverse, reverse!, reverseind
- reshape

## Список задач

1. Реализовать функцию, аналогичную встроенной функции `reverse!`, назвав её, например, `reverse_user!`, для следующих случаев:
a) аргумент функции - вектор
б) аргумент функции - матрица (2-мерный массив)

В обоих случаях имя функции должно быть одно и то же (это допустимо, поскольку в Julia реализована так называемая множественная диспетчеризация), но во втором случае должен быть еще второй *именованный* параметр с именем `dim`.

2. Аналогично, реализовать функцию, аналогичную встроенной функции `copy`для следующих случаев:
a) аргумент функции - вектор
б) аргумент функции - матрица (2-мерный массив)

(тут можно все свести к одному случаю, если воспользоваться встроенной функцией `reshape`, с помощью которой, например, одномерный массив можно переформатировать в многомерный)

3. Реализовать алгоритм сортировки методом пузырька, написав следующие 4 обобщенные функции: `bubblesort`, `bubblesort!`, `bubblesortperm`, `bubblesortperm!`, по аналогии со встоенными функциями `sort!`, `sort`, `sortperm!`, `sortperm`, ограничившись только случаем, когда входной параметр есть одномерный массив (вектор). 

4. На основе разработанных в пункте 1 функций, сотрирующих одномерный массив, написать соответствующие функции, которые бы могли получать на вход матрицу, и сортировать каждый из ее столбцов по отдельности. Имена функций оставить прежними, что были и в пункте 1, воспользовавшись механизмом множественной диспетчеризации языка Julia.
   
5. Написать функцию `sortkey!(a, key_values)`, получающую на вход некоторый вектор `a`, и соответствующий вектор `keyvalues` ключевых значений элементов вектора `a`, осуществляющую сортировку вектора `a` по ключевым значениям его элементов, и возвращающую ссылку на вектор `a`. (Для сортировки вектора ключевых значений можно востпользоваться одной из разработанных в пункте 1 функций, или соответствующей встроенной функцией).

С использованием разработанной функции `sortkey!` написать функцию высшего порядка, с тем же именем `sortkey!`, но получающую на вход ключевую функцию и массив элементов некоторого типа, на множестве значений которых должна быть определена данная ключевая функция.

С использованием этой последней функции отсортировать столбцы какой-либо заданной числовой матрицы в порядке
а) не убывания их сумм
б) не убывания числа нулей в них

6. Написать функцию `calcsort`, реализующую сортировку методом подсчета числа значений. Рассмотреть 2 варианта функции (2 метода - в терминологии Julia): в первом варианте возможные значения элементов сортируемого массива задаются некоторым диапазоном, во втором - некоторым отсортированным массивом (вектором).

Применить эту разработанную функцию для сортировки столбцов матрицы по числу находящихся в них нулей (в каком случае сортировка подсчетом даст выигрыш по сравнению с любым другим методом сортировки?).

7. Написать функции `insertsort!`, `insertsort`, `insertsortperm`, `insertsortperm!` (по аналогии с пунктом 1) реализующие алгоритм сортировки вставками

8. Реализовать ранее написанную функцию `insertsort!` с помощью встроенной функции `reduce`
(решение приведено в конце списка задач).

9. Дополнить функцию `insrtsort!` процедурой "быстрого поиска".

Указание. Предварительно написать функцию `quicsearch(iter,val)`, реализующую быстрый поиск. Эта функция должна получать некоторый итерируемый объект, содержащий предварительно отсортированную последовательность, и некоторое значение, и возвращать кортеж 2-х значений: первое значение должно быть типа `Bool` (`true` - если `val in itr`, и `false` - в противном случае), а второе значение - это индекс элемента itr, имеющий искомое значение, если таковое имеется, или - это номер позиции в `itr`, на которую следовало бы поместить значение val, чтобы сохранить отсортированность последовательности в `itr`.

Идея быстрого поиска основана на том, что последовательность, среди элементов которой ищется заданное значение, заранее отсортирована. Тогда, есле на каждом шаге алгоритма брать "середину" последовательности и искомое значение сравнивать с ней, то либо, при совпадении сравниваемых значений, поиск будет закончен, либо область дальнейшего поиска может быть сокращена вдвое (путем отбрасывания той половины последовательности, в которой искомое значение завндомо отсутствует - здесь используется факт отсортированности последовательности).

10. Написать обобщенную функцию (`nummax`), получающую на вход итерируемый объект, содержащий некоторую последовательность (элементы которой можно сравнивать по величине), и возвращающую число максимумов этой последовательности.

11. Написать обобщенную функцию (`findallmax`), получающую на вход итерируемый объект, содержащий некоторую последовательность (элементы которой можно сравнивать по величине), и возвращающую вектор, составленный из индексов элементов входной последовательности, имеющих максимальное значение.

Сравнить возможности этой пользовательской функции с возможностями встроенных функций `findmax` и `argmax`.

12. Написать обобщенную функцию `findallmax` высшего порядка, получающую на вход итерируемый объект, содержащий некоторую последовательность и некоторую функцию (значение типа ::Function), и возвращающую вектор, составленный из индексов элементов входной последовательности, на которых заданная функция достигает максимального значения (речь и дет о сужении заданной функции на заданной последовательности).

Указание. Аргумет функционального типа у функции высшего порядка в списке ее параметров должен находится на 1-ой позиции - это условие возможности применять для такой функции высшего порядка так называемый do-синтаксис.

## Решение задачи 8 

```julia
insertsort!(A)=reduce(1:length(A))do _, k # в данном случае при выполнении операции вставки  первый аргумент фуктически не используется
    while k>1 && A[k-1] > A[k]
        A[k-1], A[k] = A[k], A[k-1]
        k-=1
    end
    return A
end
```

Здесь, вместо того, чтобы передавать в функцию `reduce` сам массив `A`, передается массив его индексов (что также определяет последовательность элементов массива), это обусловленно тем, что для реализации операции вставки необходимо значение индекса текущей позиции (а соответствующие индексам значения последовательности могут просто извлечены из массива `A`, находящегося в области видимости).
