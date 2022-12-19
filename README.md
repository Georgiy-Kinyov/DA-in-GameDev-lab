# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил:
- Кинев Георгий Ильич
- РИ211120

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | # | 60 |
| Задание 2 | * | 20 |
| Задание 3 | ? | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


## Цель работы
Изучить тонкости машинного обучения и систему Tensorboard.

## Задание 2
### Описать результаты, выводимые Tensorboard

![image](https://user-images.githubusercontent.com/114848093/208435545-64995e0e-4810-4190-8231-8cc27caba06d.png)

- Cumulative Reward - средняя награда за шаг по всем агентам. Чем успешнее агенты на данном шаге, тем она больше.
- Episode Length - средняя продолжительность шага по всем агентам.
- Entropy - показатель того. насколько случайны действия агента.
- Learning Rate - длина шага в пространстве возм. параметров агента. Уменьшается при приближении к оптимуму.
- Extrinsic Reward - ср. вознаграждение от среды.
- Extrinsic Value Estimate - предсказание оного вознаграждения.
- Policy Loss - насколько меняется процесс принятия решений.

## Выводы

Изучен принцип работы Tensorboard, получена информация о различных факторах машинного обучения.
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
