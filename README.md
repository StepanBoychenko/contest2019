# Хитрые задачки для курса по iOS

## Задача раз
### Гномий фейс-контроль
В гномьем подземелье работает широко известный клуб «Мятый эльф» с очень строгим фейс-контролем. На входе в клуб находится охранник и проверяет посетителей по ряду критериев.

#### Данные
Есть критерии для отбора с кодовыми обозначениями и диапазонном значений.

Первичные:
- L - рослость [1..200]
- B - длина бороды [0…100]
- W - воинственность [0…10]
- G - рыжесть [0…10]

Вторичные:
- H - квадратность головы [0…10]
- E - запах пива [0…10]
- A - размер топора [0…300]

Некоторые качества строго положительны – чем больше, тем лучше. Это длина бороды, рыжесть и воинственность. Остальные параметры хороши не всегда. Вторичные параметры могут зависеть от первичных.

У охранника есть свои взгляды на мир и требования к посетителю.

Например, у Жралина такие требования:
- рослость – от 100 до 160
- длина бороды – от 30
- рыжесть – от 5
- квадратность головы – от 4 до 7
- размер топора – от рослости

А у Кралина такие:
- рослость – от 120
- длина бороды – от 40
- рыжесть – от 3
- размер топора – от 80 до рослости
- запах пива – от рыжести до воинственности

Краткая запись критериев имеет один из видов:
- `X:N-M`, где `X` - код качества, а `N` - либо целое число в соответствующем диапазоне, либо код другого критерия (если это вторичное качество). Для строго положительных качеств такой записи не может быть

- `X:N` - качество `X`, ограниченное только снизу значением `N` по той же логике
Например, `L:100-120` означает «рослость от 100 до 120», а `A:L` - «размер топора больше рослости».

Задача – проверить каждого посетителя по критериям охранника и либо впустить его в клуб с уважением, либо прогнать без уважения.

#### Вход
Оценочное суждение охранника вида
`L:100-120 B:30 G:5 H:4-7 A:L`

Качества посетителя вида
`L:132 B:40 W:4 G:8 H:1 E:8 A:222`

#### Выход
`true` или `false` – прошёл ли посетитель контроль.

#### Пример 1
Вход:
```
L:100-160 B:30 G:5 H:4-7 A:L
L:132 B:40 W:4 G:8 H:5 E:8 A:122
```
Выход:
```
false
```

#### Пример 2
Вход:
```
L:100-160 B:30 G:5 H:4-7 A:L
L:132 B:40 W:4 G:8 H:5 E:8 A:222
```
Выход:
```
true
```


## Задача два
### Орущие младенцы
Мы разрабатываем ПО для авиакомпании Пыщ-Авиа. Нам нужно внести доработку в систему автоматической рассадки людей в салоне самолёта.

Иногда в самолётах летают младенцы. Как правило, они орут. Если рядом с ещё не орущим младенцем сидит уже орущий, то он, скорее всего, тоже станет орущим, и они войдут во взаимную блокировку в процессе ора. Пассажирам это почему-то не очень нравится, так что ребята из Пыщ-Авиа заказали у нас такую доработку: нужно рассаживать младенцев в салоне так, чтобы между ними было наибольшее расстояние.

#### Данные
Имеется схема салона размера (n+1)\*m, где n - всегда чётное количество мест в ряду, m - количество рядов. Каждый ряд разделен проходом пополам. Пример:
```
000-000
0A0-000
000-00A
000-A00
C00-00A
```
`0` - незанятое место

`A` - место, занятое взрослым пассажиром

`C` - место, занятое младенцем (да, некоторые младенцы уже сидят в салоне, так что это придётся учесть)

`-` - проход между рядами

Считаем, что каждое место и проход имеют одинаковый размер по ширине и длине.

Пассажиров, которым уже назначены места, перемещать нельзя.

#### Вход
Таблица, как указано выше, затем количество младенцев. Если младенец всего один, то его можно посадить куда угодно.

#### Выход
Новая схема салона с сидящими в ней младенцами, такая, что сумма расстояний между младенцами максимальна. Если не всех младенцев удалось рассадить, то вывести отдельной строкой количество оставшихся.

#### Пример 1
Вход:
```
000-000
000-000
000-000
000-000
000-000
2
```
Выход:
```
С00-000
000-000
000-000
000-000
000-00С
```
#### Пример 2
Вход:
```
00-00
00-00
00-00
00-00
8
```
Выход:
```
С0-0С
С0-0С
С0-0С
С0-0С
```
#### Пример 3
Вход:
```
00-00
00-00
5
```
Выход:
```
СС-СС
СС-СС
1
```

## Задача три
### Счастливые билетики

"Счастливым билетиком" принято считать билет, у которого сумма первых N/2 цифр равна сумме последних N/2 цифр (где N - количество всех цифр в номере билета). Например, билет с номером "007412" является "счастливым", т.к. 0+0+7 = 7 (сумма первой половины цифр) и 4+1+2 = 7 (сумма второй половины цифр).

Необходимо написать программу, определяющую количество счастливых билетов в упаковке.

#### Данные
Рассмотрим пример для N=2. "Счастливыми" будут билеты с номерами: 00, 11, 22 .... 99. Таким образом, в упаковке билетов из двух цифр будет содержаться 10 счастливых билетов.

#### Вход
Входные данные состоят из единственного значения: количество цифр в упаковке с билетами. Количество цифр N в диапазоне от 2 до 10 включительно. N строго четное.

#### Выход
На выходе должно быть одно единственное число: количество счастливых билетов в упаковке.

#### Пример 1
Вход:

```
4
```
Выход:

```
670
```

В упаковке с билетами, состоящими из 4 цифр, будет содержаться 670 счастливых билетов
