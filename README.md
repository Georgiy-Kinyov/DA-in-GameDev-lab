# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил:
- Кинев Георгий Ильич
- РИ211120

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


## Цель работы
Познакомиться с программными средствами для создания системы машинного обучения и её интеграции в Unity.

## Задание 1
### Реализовать систему машинного обучения в связке Python-Unity.

Ход работы:
1) Создать проект в Unity и построить в нём следующую сцену:

![Подготовка](https://user-images.githubusercontent.com/114848093/200549814-8d7ff405-3a4f-4d81-95ab-7c0fb4ea7353.png)

2) Добавить в проект библиотеки для организации машинного обучения:

![Пакеты](https://user-images.githubusercontent.com/114848093/200551059-ea0e730d-39c7-4677-9a83-cb95c0ac4eb4.png)

3) Добавить в проект скрипт C#, содержащий инструкции по обучению ML-агента:

![Код](https://user-images.githubusercontent.com/114848093/200550116-83789fd9-8c2a-45b8-8a65-de5116a2a097.png)

4) Подключить необходимые компоненты к сфере "RollerAgent":

![Настройка](https://user-images.githubusercontent.com/114848093/200551886-d15c5c92-3e72-4827-88d9-9964fdf27d61.png)

5) Добавить в корень проекта файл .yaml с конфигурацией нейронной сети.
6) Создать виртуальную среду в Anaconda и добавить в неё библиотеки для машинного обучения.
7) Произвести запуск обучения.
Результат: произвести обучение не удалось, поскольку Anaconda и Unity не могкут установить соединение.
8) Вставить в проект готовый файл с результатами обучения и подключить его к сфере:

![Модель](https://user-images.githubusercontent.com/114848093/200554228-f76b6b26-a683-4f53-be76-e5d9f3549a46.png)

9) Создать 16 копий обстановки:

![Размножение](https://user-images.githubusercontent.com/114848093/200553610-f0dbbb88-f505-443e-a75d-7e37ba5fffe0.png)

10) Запустить проект и наблюдать за результатами:

![Результат](https://user-images.githubusercontent.com/114848093/200554343-5f39d85c-78de-4253-a911-1f66da964a40.png)

## Задание 2
### Подробно описать каждубю строку файла конфигурации нейронной сети. Самостоятельно найти информацию о компонентах Decision Requester, Behavior Parameters.


## Выводы

Была построена сцена в Unity и создана среда в Anaconda, но из-за неопределённых проблем при интеграции пришлось использовать готовый файл с результатами обучения нейронной сети.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
