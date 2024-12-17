# Баланс в играх - Идеальный баланс (Секретное задание)
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
Разработать / изменить баланс сложностей для 10 уровней игры Save RTF

## Задание 1. 
### Расширьте варианты доступного оружия в игре. Используйте шаблон таблицы для визуализации оружия игры Save RTF.
Для данного задания я решил добавить: Автомат, Арбалет, Лазерное оружие. С балансом цен было бы тоже неплохо разобраться, однако у нас такого задания не стоит

Ссылка на новую таблицу, в которую я добавил новые виды оружия, их точность и урон.
https://docs.google.com/spreadsheets/d/1Xkg3Se2efeM2RnxqieqsIunJJIdIhKmh

## Задание 2
### Визуализируйте параметры оружия в таблице.Используйте шаблон таблицы для визуализации оружия игры Save RTF
С помощью кода вычисляем:
- Среднеквадратическое отклонение (СКО)
- Разброс урона оружия
- Вариативность времени отклика игрока (реакция на события)

![Figure_1](https://github.com/user-attachments/assets/16069bde-44fe-41bb-8598-b779819c8e69)

``` Python
import numpy as np
import matplotlib.pyplot as plt
import random as rnd

def simulate_shots(weapon_name, num_shots, damage_per_shot, hit_probabilities, ax):
    # Генерация случайных выстрелов с отклонениями
    np.random.seed(rnd.randint(32, 64))
    shots_coords = np.random.normal(loc=0, scale=5, size=(num_shots, 2))

    # Вычисляем отклонения (расстояния от центра цели)
    distances = np.linalg.norm(shots_coords, axis=1)

    # Проверяем попадания
    hits, misses = [], []
    for i, distance in enumerate(distances):
        distance_index = min(int(distance), len(hit_probabilities) - 1)
        hit_chance = hit_probabilities[distance_index] / 100
        if np.random.rand() < hit_chance:
            hits.append(shots_coords[i])
        else:
            misses.append(shots_coords[i])

    hits = np.array(hits)
    misses = np.array(misses)

    # Выводим результаты
    print(f"{weapon_name}: {len(hits)} попаданий из {num_shots}")
    print(f"СКО отклонений: {np.std(distances):.2f} пикселей")

    # Визуализация
    if len(hits) > 0:
        ax.scatter(hits[:, 0], hits[:, 1], color='green', label='Попадания')
    if len(misses) > 0:
        ax.scatter(misses[:, 0], misses[:, 1], color='red', label='Промахи')
    ax.scatter(0, 0, color='blue', s=100, label='Цель')
    ax.set_xlim(-20, 20)
    ax.set_ylim(-20, 20)
    ax.axhline(0, color='black', lw=0.5)
    ax.axvline(0, color='black', lw=0.5)
    ax.set_title(f"{weapon_name}\nУрон за выстрел: {damage_per_shot}")
    ax.legend()
    ax.set_aspect('equal', adjustable='box')

# Параметры для различных оружий
weapons = [
    ("Автомат", 5, 1.7, [66,67,	66.67,	83.33,	100.00,	100.00,	100.00, 100.00, 83.33, 66.67,66.67]),
    ("Арбалет", 1, 15, [100,00,	100.00,	83.33,	66.67,	50.00,	33.33,	16.67]),
    ("Лазерное оружие", 5, 2, [50.00,	66.67,	66.67,	83.33,	83.33,	83.33,	83.33,	66.67,	66.67,	50.00]),
]

# Определяем количество строк и столбцов
num_weapons = len(weapons)
cols = 2
rows = (num_weapons + cols - 1) // cols  # Вычисляем минимальное количество строк

# Создаем фигуру и подграфики
fig, axs = plt.subplots(rows, cols, figsize=(12, rows * 6))
axs = axs.flatten()  # Преобразуем 2D массив в 1D для простоты использования

# Запускаем симуляцию для каждого оружия
for i, weapon in enumerate(weapons):
    simulate_shots(*weapon, axs[i])

# Убираем лишние подграфики, если их больше, чем нужно
for ax in axs[len(weapons):]:
    ax.axis('off')

plt.tight_layout()  # Упаковываем подграфики
plt.show()
```
## Задание 3
### №1. Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице. 

## Выводы
В результате проделанной работы я вроде научился работать с параметрами баланса, визуализировать их, расчитывать а также использовать алгоритм изменения параметров Unity с помощью Python и Google Sheets.
  

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
