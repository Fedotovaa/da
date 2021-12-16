1. записей в таблице - 32683 
2. количество мужчин - 13386
   количество женщин - 17910
3. Сколько не NAN в skills  - 8972
4. Получить заполненные скиллы 
5. Вывести зарплату только у тех, у которых в скиллах есть питон - 35000, 20000, 35000, 23000
6. Построить перцентили и разброс по з/п у мужчин и женщин.
7. Построить графики распределения по з/п мужчин и женщин (в зависимости от высшего образования)

```python
import pandas as pd
works = pd.read_csv('works.csv') 
```

Задание 1
```python
works.info() 
```

Задание 2
```python
gender = works.groupby('gender')['gender'].count()

count_of_men = gender.to_list()[1]
count_of_women = gender.to_list()[0]

print('количество мужчин ', count_of_men)
print('количество женщин ', count_of_women)
```

Задание 3
```python
works.info()
```

Задание 4
```python
skills = works['skills'].dropna().to_list()
```

Задание 5
```python
def function(value):
    arr = str(value).split(', ')
    if 'Python' in arr:
        return value
    else:
        return False


works['not_null_skills'] = works.skills.apply(function)
not_null_skills_salary = works.loc[works['not_null_skills'] != False]['salary']
not_null_skills_salary
```

Задание 6
```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(20, 10)) 
plt.title('Распределение зарплаты для мужчин и женщин')
plt.grid() 

sns.boxplot(x='salary',
            y='gender',
            data=works.loc[works['salary'] < 200000], 
            color='tab:pink')
plt.ylabel('Пол') 
plt.xlabel('Зарплата') 
plt.show()
```
![](https://sun9-9.userapi.com/impf/9-2HbYafsfuYjNIq5MPf93AA6TtV7OsnVD9PkA/StfwRUOyY-U.jpg?size=1144x566&quality=96&sign=55e8351458f073b81bed0592886d5036&type=album)

Задание 7
```python
plt.figure(figsize=(10, 10))  
plt.title('Распределение зарплаты для мужчин в зависимости от образования') 
plt.grid()

sns.boxplot(x='educationType',
            y='salary',
            data=works.loc[works['salary'] < 200000].loc[works['gender'] == 'Мужской'],
            color='tab:cyan')
plt.ylabel('Образование') 
plt.xlabel('Зарплата')
plt.show()

plt.figure(figsize=(10, 10))
plt.title('Распределение зарплаты для женщин в зависимости от образования') 
plt.grid() 

sns.boxplot(x='educationType',
            y='salary',
            data=works.loc[works['salary'] < 200000].loc[works['gender'] == 'Женский'],
            color='tab:pink')
plt.ylabel('Образование')
plt.xlabel('Зарплата') 
plt.show()
```
![](https://sun9-11.userapi.com/impf/rmSBNsr5tSz_-i14LUO4x-EseJa_iwxG1cmkLw/Y35b8gpVHlw.jpg?size=758x687&quality=96&sign=52b29eab60c2f7b1bfdb6058264bcbe0&type=album)
![](https://sun9-43.userapi.com/impf/IQW8xeQ3n_DERSBTF7Jkh2ZKLoe8fC03EqsAFQ/POy7OWTvkQw.jpg?size=851x700&quality=96&sign=785e60512364b55a6b98f8d5b4ee7a5c&type=album)