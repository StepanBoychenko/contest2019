# Орущие младенцы (DEPRECATED)
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