# Data analysis

# Wstęp
Projekt ten skupia się na analizie zbioru danych dotyczącego filmów. Celem analizy jest zrozumienie różnych aspektów związanych z filmami, takich jak kategorie, oceny, dochody oraz inne statystyki. Do opracowania wykorzystano środowisko Jupyter Notebook, poniżej zamieszczono kilka przykładowych wykresów i linijek kodu, a cała analiza znajduję się w pliku Movies_rating.

#Źródło danych
[Dataset on Kaggle] https://www.kaggle.com/datasets/harshitshankhdhar/imdb-dataset-of-top-1000-movies-and-tv-shows
Autorzy i współtwórcy: Harshit Shankhdhar

# Kroki Analizy:
Załadowanie bibliotek i danych:
Wykorzystano biblioteki takie jak NumPy, Pandas, Matplotlib, Seaborn i WordCloud.
```
import numpy as np
import pandas as pd
import os
import matplotlib.pyplot as plt
import seaborn as sns
from wordcloud import WordCloud, STOPWORDS
```
# Załadowanie i Wstępna Analiza Danych:

Sprawdzenie brakujących danych i ogólne informacje o zbiorze danych.
```
df = pd.read_csv("movies.csv")
print(df.isna().sum())
print(df.info())
print(df.describe())
```
# Eksploracyjna Analiza Danych (EDA):
Przeprowadzenie analizy eksploracyjnej, w tym generowanie wykresów.

# Przykładowe wykresy EDA
Utworzony wykres obrazuje, jakie gatinki filmów są najpopularniejsze.
```
df['category'].value_counts().plot(kind='pie', subplots=True, autopct='%1.2f', figsize=(10,10), 
                                   title='The most common categories')
```
![image](https://github.com/Jakub-Drabikowski/Data-analysis-/assets/83064196/3bc0032c-3841-4b4c-85c7-a154e15c2bba)


# Przetwarzanie Danych:
Konwersja kolumn do odpowiednich formatów (np. zmiana formatu kolumny gross_total).
Obróbka danych (np. usuwanie białych znaków, zamiana jednostek czasu).
```
df['gross_total'] = df['gross_total'].astype(str).str.lstrip('$').str.rstrip('M')
df['year_of_release'] = df['year_of_release'].str.replace('\(|\)','')
df['run_time'] = df['run_time'].apply(lambda x:float(x.split()[0].replace('min', '')))
```
# Analiza i Wizualizacja:
Przeprowadzenie analizy danych oraz generowanie wykresów. 
Kod generuje wykres punktowy, który pozwala zobaczyć, jak dochody różnią się w zależności od kategorii filmów.
```
fig, ax = plt.subplots(figsize = (20, 5))
plt.xticks(rotation = 90)
ax = sns.stripplot(y = 'category', x = 'gross_total', data = df).set(title = 'Сategory vs gross total')
plt.show(ax)
```
![image](https://github.com/Jakub-Drabikowski/Data-analysis-/assets/83064196/a03648c1-3b18-4c0c-9ca4-9d9d7fe1c17c)

Wykres pudełkowy pozwala zobaczyć, jak różnią się oceny filmów w poszczególnych kategoriach.
```
fig, ax = plt.subplots(figsize = (20, 5))
plt.xticks(rotation = 60)
ax = sns.boxplot(x = 'category', y = 'imdb_rating', data = df)
plt.show(ax)
```
![image](https://github.com/Jakub-Drabikowski/Data-analysis-/assets/83064196/b3474b6f-3900-49df-93d5-22ee063cc9e2)

Wykres słupkowy przedstawia, ile filmów znajduje się w każdej kategorii ocen IMDb.
```
plt.figure(figsize = (15, 10))
plt.xticks(rotation = 60)
sns.countplot(data = df, x = 'imdb_rating', palette = 'Pastel1').set(title = 'Movies vs Ratings')
plt.show()
```
![image](https://github.com/Jakub-Drabikowski/Data-analysis-/assets/83064196/24b65856-e390-4e98-af36-4eed3c950b7b)

# Podsumowanie
Projekt ten stanowi analizę danych dotyczących filmów, obejmującą różne aspekty takie jak oceny, dochody, kategorie itp. Projekt pozwala zidentyfikować, jak oceny IMDb rozkładają się w różnych kategoriach filmowych oraz jak często występują poszczególne oceny.
