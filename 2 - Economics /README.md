# Экономика - Нужно больше золота
Отчет по лабораторной работе #2 выполнил(а):
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
Познакомиться с программными средствами для передачи данных между инструментами Google, Python и Unity с помощью API 

## Задание 1
### Рассмотреть экономическую систему какой-нибудь игры на примере какого-то ресурса.
  Экономическая система в Red Dead Redemption 2 имеет несколько ключевых аспектов, которые создают уникальную динамику взаимодействия с деньгами. Она отражает экономику Дикого Запада конца XIX века, где важную роль играют наличные деньги, торговля, бартер и добыча ресурсов.
  
  Основные элементы схемы экономической системы в игре:

  1. Добыча денег:
     Основные способы получения дохода:
      - Миссии и задания: Выполнение сюжетных и побочных квестов (ограбления, защита ферм, контракты на ликвидацию).
      - Ограбления: Игрок может грабить поезда, дилижансы, магазины и даже банки.
      - Охота и рыбалка: Добыча шкур, мяса, рыбы и их продажа торговцам.
      - Сбор растений и материалов: Травы, ингредиенты и редкие предметы могут продаваться за деньги.
      - Воровство: Обворовывание NPC, домов, сундуков, карманов.
      - Игра в азартные игры: Покер и другие игры в салунах также могут принести прибыль (или убытки).
      - Продажа краденого: Через скупщиков можно продавать украденные вещи и награбленное.
  2. Торговля и экономика:
      - Покупка товаров: Деньги можно потратить на оружие, патроны, одежду, еду, снаряжение для лошадей и лагеря.
      - Динамическая экономика: Цены на товары могут варьироваться в зависимости от региона. Например, цены на шкуры и мясо могут быть выше в местах, где эти ресурсы редки.
      - Бартер и обмен: В некоторых ситуациях игрок может менять предметы или ресурсы вместо денег.
      - Скупщики: Они покупают у игрока краденое и уникальные предметы, часто по более низким ценам, чем обычные торговцы.
  3. Расходы денег:
      - Поддержание лагеря: У игрока есть возможность вкладывать деньги в улучшение лагеря банды (запасы, медикаменты, патроны).
      - Оплата штрафов и взяток: Если на игрока объявлена награда за преступления, можно заплатить штраф, чтобы снять обвинения.
      - Модификации и улучшения: Можно улучшать оружие, одежду и снаряжение лошади, а также покупать редкие предметы.
      - Потребности героя: Еда, лекарства, одежда и другие предметы необходимы для поддержания здоровья и стамины персонажа.
  4. Влияние репутации на экономику:
      - Карма: Действия игрока влияют на репутацию (карму), которая, в свою очередь, может влиять на цены. Высокая карма даёт скидки в магазинах, низкая — может привести к враждебному отношению со стороны NPC.
  5. Система наград и штрафов:
      - За совершение преступлений на игрока может быть назначена награда. Это влияет на его взаимодействие с миром, так как охотники за головами и законники будут охотиться за ним. Чтобы избавиться от награды, игроку нужно или заплатить штраф, или скрываться от властей.
      - Таким образом, деньги в Red Dead Redemption 2 играют центральную роль как в прогрессе игрока, так и в повествовательной части, отражая экономику того времени, где добыча, торговля и воровство были частью повседневной жизни. 

  Суть игры заключается в том, что мы являемся группой бандитов и играем за Артура Моргана. 
  В течении всей игры наша группа пытается найти способ выживать и тем самым пришли к идеи грабить банки.
  
  ![251D3B0C00001](https://github.com/user-attachments/assets/5942d614-585b-4d20-89ce-d3f344d46942)
  В игре достаточно много переменных, но основой всех являются деньги либо золотые слитки.

## Задание 2
### Реализация кода для переноса валюты 
Отредактировал 
Код Python-файла данного изначально, до необходимого вида. 
```Python
import gspread
import random

# Авторизация с помощью файла ключей
gc = gspread.service_account(filename='unitydatascience-436705-a152df01f67a.json')

# Открытие Google Таблицы
sh = gc.open("UnityScience")

# Данные об игровой валюте в RDR2 (вы можете изменять или добавлять типы валюты)
currency_types = [
    "Доллары",
    "Золотые слитки",
    "Ценные бумаги",
    "Охотничьи билеты",
    "Медвежьи шкуры"
]

# Генерация случайных данных для количества валюты и её стоимости в золоте
currency_data = []
for _ in range(len(currency_types)):
    amount = random.randint(50, 10000)  # Случайное количество валюты
    gold_value = round(random.uniform(0.5, 10), 2)  # Случайная стоимость в золоте
    currency_data.append((amount, gold_value))

# Заголовки столбцов
sh.sheet1.update('A1', 'Тип валюты')
sh.sheet1.update('B1', 'Количество')
sh.sheet1.update('C1', 'Стоимость в золоте')

# Заполнение таблицы данными о валюте
for i, (currency_type, data) in enumerate(zip(currency_types, currency_data), start=2):
    amount, gold_value = data
    
    # Заполнение данных в таблицу
    sh.sheet1.update(f'A{i}', currency_type)  # Тип валюты
    sh.sheet1.update(f'B{i}', str(amount))    # Количество
    sh.sheet1.update(f'C{i}', str(gold_value).replace('.', ','))  # Стоимость в золоте
    
    # Вывод данных для проверки
    print(f'{currency_type}: Количество = {amount}, Стоимость в золоте = {gold_value}')

print("Данные успешно внесены в таблицу.")
```

### Результат
   ![image](https://github.com/user-attachments/assets/fbf2790d-cb4c-47a2-b692-53fefc20b978)


## Задание 3
### Немного меняем значения, оставив те же звуки, т.к. не это важно, получаем такой код.
Однако стоит сразу сказать, что было бы неплохо поменять например код для Python, так как код на шарпах требует простой таблицы, а я вывожу код с названиями. 
Так что либо красота, либо работоспособность кода.
``` C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string, float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if (dataSet["Mon_" + i.ToString()] <= 2 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 2 & dataSet["Mon_" + i.ToString()] < 5 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] >= 5 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/135XFmHPcCenptt4Zt-rWGok9bUSEWSZBG5avPgRB73U/values/Лист1?key=someprivatekey");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[2]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}

```

 

![image](https://github.com/user-attachments/assets/5df28e1a-d96f-40fd-a109-2cba5c02cc1d)

* В результате имеем, что при значениях со 2 колонки мы слышим звуки в соотвествии со стоимостью товара в эквиваленте золота, например >5 - Horosho, от 5 до 2 - Sredve, а меньше Ploho 


## Выводы
В результате проделанной работы я познакомился с программными средствами для организции передачи данных между инструментами Google, Python и Unity.
  

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
