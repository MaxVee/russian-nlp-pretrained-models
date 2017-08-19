# b-labs-models [![Build Status](https://travis-ci.org/bureaucratic-labs/models.svg?branch=master)](https://travis-ci.org/bureaucratic-labs/models)

Готовые к использованию статистические модели для определения границ предложений и слов  
В качестве обучающего корпуса использовался словарь [OpenCorpora](http://opencorpora.org/) (4,000+ документов на конец мая 2017-года, в основном - новости и художественная литература)  

# Установка
```bash
$ pip install b-labs-models
```

# Определение границ предложений

Результат по F1-мере при кросс-валидации (1/3 данных использовались как тестовые): 0.99  

```python
from b_labs_models import SentenceSegmentator

text = '''
Разница цепей Маркова от сетей Маркова заключается в том, что первые генеративны (т.е. предсказывают вероятность следующего шага), а вторые — дискриминатины, т.е. рассчитывают вероятность текущего состояния.
Использовать тот или иной алгоритм зависит от решаемой задачи. А второе, и наиболее важное отличие — это то, что сети Маркова учитывают не только шаг (два и т.д.) вправо-влево по какому-либо из параметров, а по пучку взаимосвязанных параметров.
Скажем, для перевода это не только все его варианты, а и тематический контекст перевода, синтаксис и пр.
'''

segmentator = SentenceSegmentator()
sentences = segmentator.split(text)

assert len(list(sentences)) == 4
```

# Токенизация

F1-мера при кросс-валидации (условия те же): 0.98  
*Здесь стоит отметить то, что у проекта OpenCorpora свой взгляд на токенизацию: например, токены могут содержать внутри себя точки (как Яндекс.Деньги) или одно слово может быть разбито на несколько токенов (например, Жан-Поль - это три токена)*  

```python
from b_labs_models import Tokenizer

text = 'Плита дорожная железобетонная ПДН.м Серия 3.503.1-91, выпуск 1'
tokenizer = Tokenizer()

tokens = tokenizer.tokenize(text)

assert list(tokens) == [
    'Плита',
    'дорожная',
    'железобетонная',
    'ПДН',
    '.м',
    'Серия',
    '3.503.1-91',
    ',',
    'выпуск',
    '1',
]

```

## Обучение

TBD

## License

Source code licensed under MIT license, but source data (OpenCorpora annotated corpus, for example) may have different license.
