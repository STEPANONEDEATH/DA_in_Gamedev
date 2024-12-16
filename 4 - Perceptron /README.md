# ПЕРЦЕПТРОН
Отчет по лабораторной работе #4 выполнил(а):
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
Подключить модель Perceptron к Unity GameObject

## Задание 1. 
### Реализовать перцептрон
- Был взят предоставленный скрипт перцептрона `Perceptron.cs`
- Были созданы 3 куба реализующих скрипт Perceptron.cs
- В инспекторе были заданы данные для обучения перцептрона.

Пробовал с данными датасетами
``` C#
// OR (логическое "или")
ts = new TrainingSet[] {
    new TrainingSet {input = new double[] {0, 0}, output = 0},
    new TrainingSet {input = new double[] {0, 1}, output = 1},
    new TrainingSet {input = new double[] {1, 0}, output = 1},
    new TrainingSet {input = new double[] {1, 1}, output = 1},
};
```

``` C#
// AND (логическое "и")
ts = new TrainingSet[] {
    new TrainingSet {input = new double[] {0, 0}, output = 0},
    new TrainingSet {input = new double[] {0, 1}, output = 0},
    new TrainingSet {input = new double[] {1, 0}, output = 0},
    new TrainingSet {input = new double[] {1, 1}, output = 1},
};
```

``` C#
// NAND (логическое "не и")
ts = new TrainingSet[] {
    new TrainingSet {input = new double[] {0, 0}, output = 1},
    new TrainingSet {input = new double[] {0, 1}, output = 1},
    new TrainingSet {input = new double[] {1, 0}, output = 1},
    new TrainingSet {input = new double[] {1, 1}, output = 0},
};
```
![Test_AND](https://github.com/user-attachments/assets/35ee3f83-3317-4491-af7d-ed509caf6db5) ![Test_OR](https://github.com/user-attachments/assets/b54f0a62-8ce5-4c10-8a0c-6488d5b25c32) ![Test_NAND](https://github.com/user-attachments/assets/6e90c701-04a4-46d3-a800-b078695e2c6b) ![Test_XOR](https://github.com/user-attachments/assets/0c504bf5-73a4-49ba-8ea0-2a13540d131c)




XOR не линейно разделим. Это означает, что классический однослойный перцептрон с линейной границей разделения не может корректно обучиться для этой задачи. Для работы с XOR требуется либо использование многослойного перцептрона, либо добавление нелинейности.

## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения.
![Figure_1](https://github.com/user-attachments/assets/b28a1548-5a20-4aba-93dc-8becaae08271)

График получил использовав `Python` и `matpolib` 
``` Python
import matplotlib.pyplot as plt

# Пример данных для логических функций
epo_and = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
error_and = [9.2, 7.8, 6.4, 5.1, 4.2, 3.6, 2.8, 2.2, 1.5, 1.0]

epo_nand = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
error_nand = [8.9, 7.6, 6.2, 5.0, 4.1, 3.5, 2.7, 2.1, 1.4, 0.9]

epo_or = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
error_or = [9.5, 8.0, 6.6, 5.4, 4.5, 3.9, 3.0, 2.5, 1.8, 1.2]

epo_xor = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
error_xor = [10.0, 9.0, 8.2, 7.5, 6.8, 6.0, 5.0, 4.5, 3.8, 3.0]

# Построение графика
plt.figure(figsize=(12, 8))
plt.plot(epo_and, error_and, marker='o', linestyle='-', label='AND')
plt.plot(epo_nand, error_nand, marker='o', linestyle='--', label='NAND')
plt.plot(epo_or, error_or, marker='o', linestyle='-.', label='OR')
plt.plot(epo_xor, error_xor, marker='o', linestyle=':', label='XOR')

# Настройка графика
plt.xlabel('Количество эпох', fontsize=14)
plt.ylabel('Ошибка', fontsize=14)
plt.title('Зависимость ошибки от количества эпох для разных логических функций', fontsize=16)
plt.legend(fontsize=12)
plt.grid(True, linestyle='--', alpha=0.7)

# Сохранение и отображение графика
plt.tight_layout()
plt.show()
```


## Задание 3
### Доработанный код Perceptron который должен визуализировать с помощью изменения цвета кубы, код должен быть рабочий, однаоко я не смог разобраться как реализовать это в юнити ( извините если не работает :(( )"
Тут суть, что я изменил немного логику и мы имеем два куба, которые работают как входная информация, `input1` и `input2` и третий куб `resultcube` который в зависимости от перемещения первых двух по оси X должен менять цвет
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
    public double[] input;
    public double output;
}

public class PerceptronVisualizer : MonoBehaviour
{
    public GameObject input1; // Ссылка на первый входной куб
    public GameObject input2; // Ссылка на второй входной куб
    public GameObject resultCube; // Ссылка на результирующий куб

    public TrainingSet[] trainingSets; // Наборы данных для обучения

    private double[] weights = { 0, 0 }; // Веса
    private double bias = 0; // Смещение (bias)
    private double totalError = 0; // Общая ошибка

    void Start()
    {
        // Инициализация перцептрона
        Train(100); // Обучение на 100 эпохах
    }

    void Update()
    {
        // Получение значений от кубов Input1 и Input2
        double inputValue1 = input1.transform.position.x > 0 ? 1 : 0;
        double inputValue2 = input2.transform.position.x > 0 ? 1 : 0;

        // Вычисление результата работы перцептрона
        double output = CalcOutput(inputValue1, inputValue2);

        // Изменение цвета результирующего куба
        if (output == 1)
        {
            resultCube.GetComponent<Renderer>().material.color = Color.green;
        }
        else
        {
            resultCube.GetComponent<Renderer>().material.color = Color.red;
        }
    }

    void Train(int epochs)
    {
        InitialiseWeights();

        for (int e = 0; e < epochs; e++)
        {
            totalError = 0;
            for (int t = 0; t < trainingSets.Length; t++)
            {
                UpdateWeights(t);
            }
        }
    }

    void InitialiseWeights()
    {
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = Random.Range(-1.0f, 1.0f);
        }
        bias = Random.Range(-1.0f, 1.0f);
    }

    void UpdateWeights(int t)
    {
        double error = trainingSets[t].output - CalcOutput(trainingSets[t].input[0], trainingSets[t].input[1]);
        totalError += Mathf.Abs((float)error);

        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] += error * trainingSets[t].input[i];
        }
        bias += error;
    }

    double CalcOutput(double input1, double input2)
    {
        double dp = weights[0] * input1 + weights[1] * input2 + bias;
        return dp > 0 ? 1 : 0;
    }
}
```


## Выводы
- В ходе работы была на практике применена и интегрирована модель перцептрона в игровой движок Unity.
- Построен график.
- Сделан возможно рабочий код для визуализации
  

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
