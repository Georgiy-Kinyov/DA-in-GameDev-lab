# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил:
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
Изучить алгоритм работы перцептрона и организовать его обучение и работу в Unity.

## Задание 1
### В проекте Unity реализовать перцептрон, к-рый может проводить вычисления OR, AND, NAND, XOR; дать комментарий о корректности работы.

Ход работы:
1) Создать проект в Unity и пустой объект в нём;

2) Создать скрипт "Perceptron" и вставить в него следующий код:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	public double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			for(int t=0;t<ts.Length;t++){
				double error = ts[t].output - CalcOutput(t);
				totalError += Mathf.Abs((float)error);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}
```

NB: Да, этот код отличается от вашего. В вашем коде имеется ошибка, и мои указания на это вы благополучно игнорируете.

3) Прикрепить скрипт к созданномк ранее объекту, задать данные для обучения (таблица исходных данных и правильных ответов)
![image](https://user-images.githubusercontent.com/114848093/205439299-bc4d89e8-775c-4507-b391-0ec46a9c6012.png)
4) Запустить симуляцию. В выводе отображаются параметры перцептрона и ошибка обучения на каждом шаге, а также расчётные данные, полученные обученным перцептроном.
![image](https://user-images.githubusercontent.com/114848093/205439338-3c5c91bd-4a24-49e1-b729-eeead391a10a.png)

### Результат:

OR - корректно

AND - корректно

NAND - корректно

XOR -  неверно из-за нелинейности задачи.

## Задание 2
### Построить графики зависимости ошибки обучения от количества эпох [sic]. Указать, от чего зависит необходимое кол-во эпох обучения.

Для построения графиков необходимо найтисреднюю ошибку обучения на эпоху. Для этого создаём скрипт "PerceptronTest" (см. далее) и подключаем его к ещё одному пустому объекту.

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class PerceptronTest : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;
	double [] result = new double[10];

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
			}
			for(int t=0;t<ts.Length;t++){
				double error = ts[t].output - CalcOutput(t);
				totalError += Mathf.Abs((float)error);
			}
			result[e]+=totalError;
		}
	}

	void Start () {
		int n=1000000;
		for(int i=0;i<10;i++){
			result[i] = 0;
		}
		for(int i=0;i<n;i++){
			Train(10);
		}
		for(int i=0;i<10;i++){
			Debug.Log((i+1)+" steps --> mean error = "+result[i]/(double)n);
		}
	}
	
	void Update () {
		
	}
}
```

Запускаем симуляцию, на выходе получаем необходимые нам данные:
![image](https://user-images.githubusercontent.com/114848093/205439434-24a207da-ac57-404e-b781-9facd086af19.png)

Строим на их основе графики:
![image](https://user-images.githubusercontent.com/114848093/205439459-373f6a87-4877-49e4-8188-8f51484a7dd3.png)

Как видим, необходимое количество эпох обучения зависит от начальных параметров (различные наборы входных данных по-разному отличаются от результатов, получаемых необученным перцептроном; ergo, требуется различное количестов эпох для достижения корректного результата.

## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity.

Ход работы:
1) Создаём плоскость Floor, куб Target и шар Collider.

![image](https://user-images.githubusercontent.com/114848093/205439615-9a23735a-5f43-41e2-8328-908d192e4d95.png)
2) Подключаем к шару и кубу материалы и компоненты Rigid Body. Настраиваем Rigid Body следующим образом: 

![image](https://user-images.githubusercontent.com/114848093/205439498-5f65360a-af53-4258-87a3-787bb375b824.png) (Для куба)

![image](https://user-images.githubusercontent.com/114848093/205439549-2916a03b-2db5-4862-98db-96ab01f45cef.png) (Для шара)

3) Придаём шару постоянное ускорение в сторону куба.
4) Подключаем к кубу скрипт:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TargetB : MonoBehaviour
{
    public Material tm, cm;
    public Perceptron p;
    public int xt, xc;
    void Start()
    {
        if(xt==0){
            tm.color=Color.grey;
        }
        else {
            tm.color=Color.white;
        }
        if(xc==0){
            cm.color=Color.grey;
        }
        else {
            cm.color=Color.white;
        }
    }

    void OnCollisionEnter(Collision col) {
        if(col.gameObject.name=="Collider") {
            if(p.CalcOutput(xt,xc)==1){
                tm.color=Color.green;
            }
            else{
                tm.color=Color.red;
            }
            Destroy(col.gameObject);
        }
    }
}
```

5)  Подключаем к скрипту материалы куба и шара, объект класса Perceptron и входные данные: ![image](https://user-images.githubusercontent.com/114848093/205439709-50d49e0b-3bf7-4855-8c78-d858dfc58701.png)
6)  Запускаем симуляцию. Шар и куб окрашиваются в серый/белый цвета, если входные данные соответственно равны 0/1. При столкновении шар уничтожается, куб окрашивается в зелёный цвет при результате 1/красный при результате 0.

## Выводы

Изучен принцип работы перцептрона,  построена визуалицация его работы, проведён анализ зависимости ошибки обучения от количества эпох.
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
