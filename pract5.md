# Практическое занятие №5. Вопросы виртуализации

П.Н. Советов, РТУ МИРЭА

## Задача 1

Исследование виртуальной стековой машины CPython.

Изучите возможности просмотра байткода ВМ CPython.

```
import dis

def foo(x):
    while x:
        x -= 1
    return x + 1

print(dis.dis(foo))
```

Опишите по шагам, что делает каждая из следующих команд (приведите эквивалентное выражение на Python):

 11           0 LOAD_FAST                0 (x)
              2 LOAD_CONST               1 (10)
              4 BINARY_MULTIPLY
              6 LOAD_CONST               2 (42)
              8 BINARY_ADD
             10 RETURN_VALUE

```
             LOAD_FAST 0 (x):
Команда LOAD_FAST загружает локальную переменную x в стек. В данном случае, индекс переменной 0 соответствует переменной x.

LOAD_CONST 1 (10):
Команда LOAD_CONST загружает константу 10 в стек.

BINARY_MULTIPLY:
Команда BINARY_MULTIPLY умножает два верхних значения на стеке и помещает результат обратно на стек. Операции выполняются над переменными x и 10, которые были ранее загружены.

LOAD_CONST 2 (42):
Команда LOAD_CONST загружает константу 42 в стек.

BINARY_ADD:
Команда BINARY_ADD складывает два верхних значения на стеке и помещает результат обратно на стек. Операции выполняются над результатом умножения и константой 42.

RETURN_VALUE:
Команда RETURN_VALUE возвращает верхнее значение из стека в качестве результата выполнения функции.

Итог
result = (x * 10) + 42
return result
```


## Задача 2

Что делает следующий байткод (опишите шаги его работы)? Это известная функция, назовите ее.

```
  5           0 LOAD_CONST               1 (1)
              2 STORE_FAST               1 (r)

  6     >>    4 LOAD_FAST                0 (n)
              6 LOAD_CONST               1 (1)
              8 COMPARE_OP               4 (>)
             10 POP_JUMP_IF_FALSE       30

  7          12 LOAD_FAST                1 (r)
             14 LOAD_FAST                0 (n)
             16 INPLACE_MULTIPLY
             18 STORE_FAST               1 (r)

  8          20 LOAD_FAST                0 (n)
             22 LOAD_CONST               1 (1)
             24 INPLACE_SUBTRACT
             26 STORE_FAST               0 (n)
             28 JUMP_ABSOLUTE            4

  9     >>   30 LOAD_FAST                1 (r)
             32 RETURN_VALUE
```
```

LOAD_CONST 1 (1) Загружает константу 1 в стек. Это начальное значение для переменной r.

STORE_FAST 1 (r) Сохраняет значение 1 из стека в локальную переменную r.

LOAD_FAST 0 (n) Загружает значение переменной n в стек.

LOAD_CONST 1 (1) Загружает константу 1 в стек.

COMPARE_OP 4 (>) Сравнивает n и 1 на предмет того, больше ли n единицы.

POP_JUMP_IF_FALSE 30 Если результат сравнения n > 1 — False, то переход к строке 30 (к завершению функции). Иначе выполняется тело цикла.

Тело цикла (строки 12–28): LOAD_FAST 1 (r) Загружает значение r в стек.

LOAD_FAST 0 (n) Загружает значение n в стек.

INPLACE_MULTIPLY Умножает r на n и сохраняет результат в r.

STORE_FAST 1 (r) Обновляет значение переменной r на r * n.

LOAD_FAST 0 (n) Загружает значение n в стек.

LOAD_CONST 1 (1) Загружает константу 1 в стек.

INPLACE_SUBTRACT Уменьшает n на 1.

STORE_FAST 0 (n) Обновляет значение n на n - 1.

JUMP_ABSOLUTE 4 Переходит обратно к началу цикла (в строку 4), чтобы снова проверить условие n > 1.

Завершение функции: LOAD_FAST 1 (r) Загружает значение r в стек (это результат вычисления факториала).

RETURN_VALUE Возвращает значение r как результат выполнения функции.


def factorial(n):
    r = 1
    while n > 1:
        r *= n
        n -= 1
    return r
```

## Задача 3

Приведите результаты из задач 1 и 2 для виртуальной машины JVM (Java) или .Net (C#).
```
Код Java

package ru.qq;

public class Main {
    public static void main(String[] args) {
        foo(10);
    }

    private static int foo(int x){
        int result = (x * 10) + 42;
        return result;
    }
}
```

## Задача 4

Работа с qemu. Скачать и установить ISO-образ Alpine Linux для виртуальных машин с официального сайта.
Создать с помощью qemu образ жесткого диска (опция -f qcow2). Объем диска 500 Мб.
Запустить Alpine Linux с CD-ROM.
Установить систему на sda. Изменить motd.
Загрузиться уже с sda.
Прислать полный список команд для установки и загрузки, а также скриншот с motd, где фигурируют ваши имя и фамилия.

## Задача 5

(после разбора на семинаре и написания у доски базовой части эмулятора древней игровой приставки CHIP-8)

1. Реализовать вывод на экран.
2. Добиться запуска Тетриса.
3. Реализовать ввод с клавиатуры.
4. Добиться успешной работы всех приложений.

[Архив эмулятора CHIP-8](chip.zip)

## Полезные ссылки

Compiler Explorer: https://godbolt.org/

Байткод CPython: https://docs.python.org/3/library/dis.html

QEMU для Windows: https://www.qemu.org/download/#windows
http://sovietov.com/tmp/mqemu.zip

Документация по QEMU: https://www.qemu.org/docs/master/system/index.html

Старая документация по QEMU (рус.): https://www.opennet.ru/docs/RUS/qemu_doc/

Образы Alpine Linux: https://alpinelinux.org/downloads/

Документация по игровому компьютеру CHIP-8: http://devernay.free.fr/hacks/chip8/C8TECH10.HTM

Учебник по созданию миниатюрной ОС: https://www.cs.bham.ac.uk/~exr/lectures/opsys/10_11/lectures/os-dev.pdf

Nasm: https://nasm.us/

Прерывания BIOS: http://www.ctyme.com/intr/int.htm

Игры в загрузочном секторе: https://github.com/nanochess/Invaders
