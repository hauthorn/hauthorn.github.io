---
layout: post
title:  "The Danish language and UUIDs"
date:   2022-01-29 20:00:00 +0100
categories: questions danish language
excerpt: How many words in the danish language can you find in UUIDs?
image: /assets/images/dansk-sprognaevn.svg
---

I noticed that the UUID for a developer account I was prefixed with `cafe`. Showing the coincidence to a colleague, he asked "I wonder how many words of the danish language could be spelled using ABCDEF. I'm going to find out.

## The danish language
I have a copy of the [danish dictionary 2019](https://dsn.dk/ordboeger/retskrivningsordbogen/) lying around (turns out you can get it for free if you ask nicely).

First, let's load it as see what we have here.


```python
import re
import pandas as pd

dictionary = pd.read_csv("RO2012 fuldformer 2019.txt", delimiter=";")

dictionary
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="0" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grundform</th>
      <th>Bøjning</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1. A</td>
      <td>A</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1. A</td>
      <td>A'et</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1. A</td>
      <td>A'ets</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1. A</td>
      <td>A's</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1. A</td>
      <td>A'erne</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>412796</th>
      <td>åsyn</td>
      <td>åsyns</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>412797</th>
      <td>åsyn</td>
      <td>åsynene</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>412798</th>
      <td>åsyn</td>
      <td>åsynenes</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>412799</th>
      <td>åsyn</td>
      <td>åsyn</td>
      <td>sb.</td>
    </tr>
    <tr>
      <th>412800</th>
      <td>åsyn</td>
      <td>åsyns</td>
      <td>sb.</td>
    </tr>
  </tbody>
</table>
<p>412801 rows × 3 columns</p>
</div>




```python
dictionary.nunique()
```




    Grundform     64978
    Bøjning      388378
    Type             32
    dtype: int64



It seems like there's around 65 thousand words in their base form in the dictionary, and some words are counted more than once. I guess they are listed for each meaning they might have, for example seas _have_ and to have _at have_.

## UUID
The [format](https://en.wikipedia.org/wiki/Universally_unique_identifier#Format) of the textual representation of a UUID poses some limits on word length (32 hexadecimal digits, hyphens that split up the string into 8-4-4-4-12 and so on), I will count words in the dictionary that only consist of the following:

1. Letters a, b, c, d, e & f
2. Digits 0 through 9

On to the query:


```python
words = set(dictionary['Bøjning'].to_numpy())
regex = r"[a-fA-F0-9]"
count = 0
matched = []

for word in words:
    matches = re.finditer(regex, word)
    if len(tuple(matches)) == len(word):
        count += 1
        matched.append(word)

matched
```




    ['EA',
     'feed',
     'b',
     'ebbede',
     'badede',
     'bed',
     'F',
     'abe',
     'affede',
     'dB',
     'c',
     'C',
     'fa',
     'abbed',
     'affedede',
     'dada',
     'a',
     'ab',
     'aede',
     'ED',
     'cad',
     'ad',
     'ea',
     'AF',
     'e',
     'fade',
     'AD',
     'edb',
     'De',
     'af',
     'EDB',
     'fadede',
     'BA',
     'E',
     'fede',
     'da',
     'facade',
     'abede',
     'DAB',
     'de',
     'abc',
     'eb',
     'fad',
     'bede',
     'B',
     'ae',
     'ed',
     'D',
     'f',
     'fedede',
     'ABC',
     'fe',
     'CD',
     'cd',
     'dab',
     'fed',
     'affed',
     'CAD',
     'd',
     'bade',
     'bebe',
     'ba',
     'EF',
     'ebbe',
     'A',
     'bad']




```python
len(matched)
```




    66



I guess the answer can almost fit on your screen. 66 words.