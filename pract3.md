# Практическое занятие №3. Конфигурационные языки

П.Н. Советов, РТУ МИРЭА

Разобраться, что собой представляют программируемые конфигурационные языки (Jsonnet, Dhall, CUE).

## Задача 1

Реализовать на Jsonnet приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

```
local groupTemplate(index) = "ИКБО-" + index + "-20";

local groups = [groupTemplate(i) for i in std.range(1, 24)];

local studentTemplate(name, age, group) = {
  age: age,
  group: group,
  name: name,
};

local students = [
  studentTemplate("Троецкий Т.Т.", 19, "ИКБО-4-20"),
  studentTemplate("Павлов П.П.", 18, "ИКБО-5-20"),
  studentTemplate("Сокол С.С.", 18, "ИКБО-5-20"),
  studentTemplate("Хайдаров С.Р.", 19, "ИКБО-65-23"),
];

{
  groups: groups,
  students: students,
  subject: "Конфигурационное управление",
}


```

```
{
  "groups": [
    "ИКБО-1-20",
    "ИКБО-2-20",
    "ИКБО-3-20",
    "ИКБО-4-20",
    "ИКБО-5-20",
    "ИКБО-6-20",
    "ИКБО-7-20",
    "ИКБО-8-20",
    "ИКБО-9-20",
    "ИКБО-10-20",
    "ИКБО-11-20",
    "ИКБО-12-20",
    "ИКБО-13-20",
    "ИКБО-14-20",
    "ИКБО-15-20",
    "ИКБО-16-20",
    "ИКБО-17-20",
    "ИКБО-18-20",
    "ИКБО-19-20",
    "ИКБО-20-20",
    "ИКБО-21-20",
    "ИКБО-22-20",
    "ИКБО-23-20",
    "ИКБО-24-20"
  ],
  "students": [
    {
      "age": 19,
      "group": "ИКБО-4-20",
      "name": "Троецкий Т.Т."
    },
    {
      "age": 18,
      "group": "ИКБО-5-20",
      "name": "Павлов П.П."
    },
    {
      "age": 18,
      "group": "ИКБО-5-20",
      "name": "Сокол С.С."
    },
    {
      "age": 19,
      "group": "ИКБО-65-23",
      "name": "Хайдаров С.Р."
    }
  ],
  "subject": "Конфигурационное управление"
}
```

![image](https://github.com/user-attachments/assets/eb8966dc-b54c-42c2-9189-ab78e5b1f1bc)


## Задача 2

Реализовать на Dhall приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.


```
let Group = List Text

let Student = { age : Natural, group : Text, name : Text }

let groups : Group =
      [ "ИКБО-1-20"
      , "ИКБО-2-20"
      , "ИКБО-3-20"
      , "ИКБО-4-20"
      , "ИКБО-5-20"
      , "ИКБО-6-20"
      , "ИКБО-7-20"
      , "ИКБО-8-20"
      , "ИКБО-9-20"
      , "ИКБО-10-20"
      , "ИКБО-11-20"
      , "ИКБО-12-20"
      , "ИКБО-13-20"
      , "ИКБО-14-20"
      , "ИКБО-15-20"
      , "ИКБО-16-20"
      , "ИКБО-17-20"
      , "ИКБО-18-20"
      , "ИКБО-19-20"
      , "ИКБО-20-20"
      , "ИКБО-21-20"
      , "ИКБО-22-20"
      , "ИКБО-23-20"
      , "ИКБО-24-20"
      ]

let students : List Student =
    [ { age = 19, group = "ИКБО-4-20", name = "Троецкий Т.Т." }
    , { age = 18, group = "ИКБО-5-20", name = "Павлов П.П." }
    , { age = 18, group = "ИКБО-5-20", name = "Сокол С.С." }
    , { age = 19, group = "ИКБО-65-23", name = "Хайдаров С.Р." }
    ]

in
  { groups = groups
  , students = students
  , subject = "Конфигурационное управление"
  }
```

```
groups:
  - "ИКБО-1-20"
  - "ИКБО-2-20"
  - "ИКБО-3-20"
  - "ИКБО-4-20"
  - "ИКБО-5-20"
  - "ИКБО-6-20"
  - "ИКБО-7-20"
  - "ИКБО-8-20"
  - "ИКБО-9-20"
  - "ИКБО-10-20"
  - "ИКБО-11-20"
  - "ИКБО-12-20"
  - "ИКБО-13-20"
  - "ИКБО-14-20"
  - "ИКБО-15-20"
  - "ИКБО-16-20"
  - "ИКБО-17-20"
  - "ИКБО-18-20"
  - "ИКБО-19-20"
  - "ИКБО-20-20"
  - "ИКБО-21-20"
  - "ИКБО-22-20"
  - "ИКБО-23-20"
  - "ИКБО-24-20"
students:
  - age: 19
    group: "ИКБО-4-20"
    name: "Троецкий Т.Т."
  - age: 18
    group: "ИКБО-5-20"
    name: "Павлов П.П."
  - age: 18
    group: "ИКБО-5-20"
    name: "Сокол С.С."
  - age: 19
    group: "ИКБО-65-23"
    name: "Хайдаров С.Р."
subject: "Конфигурационное управление"

```



Для решения дальнейших задач потребуется программа на Питоне, представленная ниже. Разбираться в самом языке Питон при этом необязательно.

```Python
import random


def parse_bnf(text):
    '''
    Преобразовать текстовую запись БНФ в словарь.
    '''
    grammar = {}
    rules = [line.split('=') for line in text.strip().split('\n')]
    for name, body in rules:
        grammar[name.strip()] = [alt.split() for alt in body.split('|')]
    return grammar


def generate_phrase(grammar, start):
    '''
    Сгенерировать случайную фразу.
    '''
    if start in grammar:
        seq = random.choice(grammar[start])
        return ''.join([generate_phrase(grammar, name) for name in seq])
    return str(start)


BNF = '''
E = a
'''

for i in range(10):
    print(generate_phrase(parse_bnf(BNF), 'E'))

```

Реализовать грамматики, описывающие следующие языки (для каждого решения привести БНФ). Код решения должен содержаться в переменной BNF:

## Задача 3

Язык нулей и единиц.

```
10
100
11
101101
000
```

```
import random


def parse_bnf(text):
    '''
    Преобразовать текстовую запись БНФ в словарь.
    '''
    grammar = {}
    rules = [line.split('=') for line in text.strip().split('\n')]
    for name, body in rules:
        grammar[name.strip()] = [alt.split() for alt in body.split('|')]
    return grammar


def generate_phrase(grammar, start):
    '''
    Сгенерировать случайную фразу.
    '''
    if start in grammar:
        seq = random.choice(grammar[start])
        return ''.join([generate_phrase(grammar, name) for name in seq])
    return str(start)


BNF = '''
S = A | B | C | D | E
A = 1 | 1 A | 1 B
B = 0 | 0 B
C = 1 1
D = 1 0 1 1 0 1
E = 0 0 0
'''

for i in range(10):
    print(generate_phrase(parse_bnf(BNF), 'S'))



```
![image](https://github.com/user-attachments/assets/7c106097-6cdd-444f-b981-3c9ed5793096)

## Задача 4

Язык правильно расставленных скобок двух видов.

```
(({((()))}))
{}
{()}
()
{}
```

```
BNF = '''
S = A | B | C
A = ( S ) | { S } | ε
B = ( A ) | { A }
C = ε
'''

for i in range(10):
    print(generate_phrase(parse_bnf(BNF), 'S'))
```

![image](https://github.com/user-attachments/assets/c69b8aab-23ef-4295-857d-df05a42c5e02)


## Задача 5

Язык выражений алгебры логики.

```
((~(y & x)) | (y) & ~x | ~x) & x
y & ~(y)
(~(y) & y & ~y)
~x
~((x) & y | (y) | (x)) & x | x | (y & ~y)
```

```
BNF = '''
S = E
E = E & T | E | T
T = T | F | ~T | ( E )
F = x | y
'''

for i in range(10):
    print(generate_phrase(parse_bnf(BNF), 'S'))
```

![image](https://github.com/user-attachments/assets/9e22255f-d405-43e2-8b0d-ab84d3a0caa4)


## Полезные ссылки

Configuration complexity clock: https://mikehadlow.blogspot.com/2012/05/configuration-complexity-clock.html

Json: http://www.json.org/json-ru.html

Язык Jsonnet: https://jsonnet.org/learning/tutorial.html

Язык Dhall: https://dhall-lang.org/

Учебник в котором темы построения синтаксических анализаторов (БНФ, Lex/Yacc) изложены подробно: https://ita.sibsutis.ru/sites/csc.sibsutis.ru/files/courses/trans/LanguagesAndTranslationMethods.pdf

Полезные материалы для разработчика (очень рекомендую посмотреть слайды и прочие ссылки, все это актуально и для других тем нашего курса): https://habr.com/ru/company/JetBrains-education/blog/547768/
