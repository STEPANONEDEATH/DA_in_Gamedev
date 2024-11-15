# Баланс в играх - Идеальный баланс
Отчет по лабораторной работе #3 выполнил(а):
- Сидоров Степан Павлович
- РИ-230930

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.

## Цель работы
Разработать / изменить баланс сложностей для 10 уровней игры Dragon Picker

## Задание 1. Начало работы
### Ознакомиться с презентацией третьей лекции. Оценить структуру игры Dragon Picker. Скачать и ознакомиться с прототипом игры Dragon Picker на Unity. Запустите игровую сцену, проанализируйте движение дракона:
### Какие переменные влияют на движение дракона на сцене? Укажите эти переменные
— На движение дракона влияют параметры: скорости и рандомное значение, отвечающее за то, будет ли дракон менять траекторию в определенный момент времени

### Какие переменные влияют на сложность игры на сцене? Укажите эти переменные
— На сложность игры влияют параметры: скорость дракона, частота появления яйца, скорость падения яйца, количество щитов, частота изменения направления движения дракона и размер щита

## Задание 2
### Начало работы с шаблоном google-таблицы для балансировки игры 
### Отметьте, как может быть использован шаблон таблицы для визуализации изменения уровней сложности в игре Dragon Picker?
— Шаблон может быть использован для того, чтобы отследить как меняются переменные "баланса" в зависимости от каждого уровня. Так же для удобства их можно визуализировать графиками.

## Задание 3
### №1. Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице. 
```Python

import gspread
import numpy as np

gc = gspread.service_account(filename='dragonpicker-8110f907cb46.json')
sh = gc.open("DragonPickerAnalis")

def update_indexes():
    for i in range(1, 11):
        sh.sheet1.update_acell(f"A{i+1}", str(i))

def update_dragon_speed(percent: str):
    current_speed = float(sh.sheet1.acell("B2").value)
    multiplier = 1 + float(percent) / 100
    for i in range(3, 12):
        current_speed *= multiplier
        formatted_speed = f"{int(current_speed)},{int((current_speed - int(current_speed)) * 100)}"
        sh.sheet1.update_acell(f"B{i}", formatted_speed)

def update_time_egg_drop(percent: str):
    tail = 1 - int(percent) / 100
    current_time = float(sh.sheet1.acell("C2").value)
    for i in range(3, 12):
        current_time *= tail
        formatted_time = f"{int(current_time)},{int((current_time - int(current_time)) * 100)}"
        sh.sheet1.update_acell(f"C{i}", formatted_time)

def update_shields_count():
    current_count = int(sh.sheet1.acell("E2").value)
    repeat = 1
    for i in range(3, 12):
        sh.sheet1.update_acell(f"E{i}", str(current_count))
        repeat += 1
        if repeat == 3:
            current_count -= 1
            repeat = 0

if __name__ == "__main__":
    update_indexes()
    update_dragon_speed("20")
    update_time_egg_drop("10")
    update_shields_count()
```
https://docs.google.com/spreadsheets/d/1GmpemND9ZYDorn7ckyxHTwsnB5gb_BmIGuvw1UWP2JA/edit?usp=sharing


![image](https://github.com/user-attachments/assets/5df28e1a-d96f-40fd-a109-2cba5c02cc1d)

* В результате имеем, что при значениях со 2 колонки мы слышим звуки в соотвествии со стоимостью товара в эквиваленте золота, например >5 - Horosho, от 5 до 2 - Sredve, а меньше Ploho 


## Выводы
В результате проделанной работы я познакомился с программными средствами для организции передачи данных между инструментами Google, Python и Unity.
  

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
