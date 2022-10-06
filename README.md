# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил:
- Кинев Георгий Ильич
- РИ211120

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


## Цель работы
Ознакомиться с основными операторами языка Python на примере реализации линейной регрессии.

## Задание 1
### Написать программы Hello World на Python и Unity

Скриншоты:

![2022-10-06_09-09-58](https://user-images.githubusercontent.com/114848093/194215966-af0ebb71-a1cf-4916-985e-80182f4c1541.png)

![2022-10-06_09-11-50](https://user-images.githubusercontent.com/114848093/194215991-3b16c0bd-5862-46ad-a3fb-32eda36a850e.png)

![2022-10-06_09-01-13](https://user-images.githubusercontent.com/114848093/194216041-29586adb-59c4-4fb0-b456-5086282cfe5a.png)

## Задание 2
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
Ход работы:
- Производим подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

```py

In [ ]:
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

plt.scatter(x,y)

```

- Определяем связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

```py

def model(a, b, x):
  return a*x + b
def loss_function(a, b, x, y):
 num = len(x)
 prediction=model(a,b,x)
 return (0.5/num) * (np.square(prediction-y)).sum()
def optimize(a,b,x,y):
 num = len(x)
 prediction = model(a,b,x)
 da = (1.0/num) * ((prediction -y)*x).sum()
 db = (1.0/num) * ((prediction -y).sum())
 a = a - Lr*da
 b = b - Lr*db
 return a, b
def iterate(a,b,x,y,times):
 for i in range(times):
  a,b = optimize(a,b,x,y)
 return a,b

```

- проводим 1000 итераций с выводом результатов каждой 200-й итерации. Используем тот факт, что значения переменных сохраняются между вызовами функции итерирования.

```py

#Подготовка исходных значений параметров рекурсии
a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001
#Итерируем
for i in range(5):
  a,b = iterate(a,b,x,y,200)
  prediction=model(a,b,x)
  loss = loss_function(a, b, x, y)
  print(a,b,loss)
  plt.plot(x,prediction)
#Отображаем исходные данные
plt.scatter(x,y)

```

Результат:

![image](https://user-images.githubusercontent.com/114848093/194221420-4f078065-f8ce-404a-9625-df7338161f51.png)

## Задание 3
### 1) Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.

Далеко не всегда. Величина loss равна нулю тогда и только тогда, когда все отклонения данных от предсказания модели равны нулю (т. е. все данные точно укладываются на прямую). Пример случая, когда это происходит:

```py

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
x = [1,2,3,4,5,6,7,8,9,10]
x = np.array(x)
y = [3,5,7,9,11,13,15,17,19,21]
y = np.array(y)
plt.scatter(x,y)

```

(Определения функций те же)

```py

a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
#Значение Lr изменено, поскольку иначе значения сходятся слишком медленно.
Lr = 0.0001
for i in range(5):
  a,b = iterate(a,b,x,y,200)
  prediction=model(a,b,x)
  loss = loss_function(a, b, x, y)
  print(a,b,loss)
  plt.plot(x,prediction)
plt.scatter(x,y)

```

Результат:

![image](https://user-images.githubusercontent.com/114848093/194219687-5e68815f-967d-4a9d-8742-256f3651bd73.png)

### 2) Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

Параметр Lr определяет величину шага против градиента. При бОльших значениях алгоритм сходится быстрее, но точность может упасть.

Демонстрация (код и исх. данные из задания 3, п. 1; 1000 итераций):

![image](https://user-images.githubusercontent.com/114848093/194219570-c5d211d5-551e-4d4a-9ca9-b123024bee00.png)
Lr=0.00001

![image](https://user-images.githubusercontent.com/114848093/194219687-5e68815f-967d-4a9d-8742-256f3651bd73.png)
Lr=0.0001

## Выводы

Был произведён расчёт линейной регрессии, даны ответы на вопросы по деталям работы алгоритма. Кроме этого, изучен базовый интерфейс программ Unity, Visual Studio Code, Google Colab.

NB: пакет Anaconda не использовался из-за несовместимости с моим ноутбуком

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
