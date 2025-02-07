# Модуль 28. Многопоточная работа с данными 
# 28.9. Итоговое задание

В качестве окончательного завершения модуля предлагаем вам решить итоговое задание.

Звучит оно следующим образом:

- Доработайте алгоритм merge sort, описанный в 11 модуле, сделав его многопоточным.
- Используйте std::futurez в качестве инструмента для синхронизации результата работы потоков.
- Нужно определить независимые части алгоритма, которые могут быть распараллелены и запустить их вычисление в отдельных потоках, как это было сделано в юните 28.7.
- Потоки могут быть запущены через std::thread или std::async, но синхронизация строго через std::future. Также предусмотрите ограничение количества запускаемых потоков по примеру из юнита 28.7.


## Разбиение на потоки

Алгоритм создаёт дополнительные потоки `std::packaged_task` в количестве, равном числу **N** доступных ядер процессора.  \
В исходном массиве выделяются границы **N** частей одинаковой длины (разница в пределах единицы). \
Границы каждой из частей массива передаются в качестве аргументов в функции, исполняемые потоками в режиме `detach`. \
По завершении работы всех потоков (`std::vector<std::future<>>::get`) требуется слить в правильном порядке отсортированные участки массива. \
Это слияние осуществляется простым последовательным добавлением в функции `finalMerge`, что даёт сложность **O(N)**, но число потоков невелико и этим временем можно пренебречь. \
В основной функции определяется время исполнения в однопоточном и многопоточном режимах, а также проверка результата сортировки на правильность.





Решение: Александр Павлинов 2022.03.10