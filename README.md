# DA-in-GameDev-lab4
# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
- Усик Артемий Максимович
- РИ-230915

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

## Цель работы
Познакомиться с программными средствами для создания системы искусственного интеллекта и их применение совместно с Unity.

## Задание 1
В проекте Unity реализовать перцептрон, который умеет призводить следующие вычисления:
- **OR**
- **AND**
- **NAND**
- **XOR**
- **Дать комментарии о корректности работы всех логических операций после реализации**

Мы создали новый 3D проект в Unity и добавили пустой объект на сцену.
После чего мы создали скрипт и в него добавили следующий код.

```c#
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
		totalError += Mathf.Abs((float)error);
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
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
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
После чего мы привязали скрипт к пустому объекту

![image](https://github.com/user-attachments/assets/ef32c575-ad55-4953-9e98-0678c2395b64)

## Вычисление **OR**
В Unity, а именно у пустого объекта, мы заполнили лист **Ts**, который хранит значения для обучения перцептрона. Значения соответствовали математической операции "ИЛИ" для бинарного сложения (то есть: 0 или 0 = 0, 0 или 1 = 1 и так далее).

![image](https://github.com/user-attachments/assets/a27bc6a2-0f8a-4844-b81b-37ed54b9d64e)

После чего мы запустили сцену и получили результат

![image](https://github.com/user-attachments/assets/25fa038b-9be0-42d6-a2d7-0d92b84b76a3)

## Вычисление **AND**

Для обучания операции "AND" понадобилось 9 итераций обученмя:

![image](https://github.com/user-attachments/assets/97cf6bd4-cc05-4e94-92d2-2b29c59d98f3)

## Вычисление **NAND**

Аналогично с "AND", операция "NAND" понадобилось 9 итераций обучения:

![image](https://github.com/user-attachments/assets/fb7b4c62-612e-4fd7-8172-56533f99253d)

## Вычисление **XOR**
XOR - это нелинейно-связанные данные, в следствии чего прецептрон всегда будет выдавать ошибку, так как он расчитан только на линейно-связанные данные.

![image](https://github.com/user-attachments/assets/5f853a5f-bf31-4d84-920f-c4d9545ec360)

## Задание 2


## Задание 3


## Выводы
На практике мы разобрали как и зачем работает перцептрон. Выяснили, что он хорошо работает только в производстве вычислений для линейных данных, а также получили дополнительный опыт работы в Unity. 

## Powered by

**Усик Артемий Максимович|Yakut**
