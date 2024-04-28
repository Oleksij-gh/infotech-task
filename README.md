# Infotech Test Task


**Задача**: 
Предложить вариант прогнозной модели по предсказанию задержки рейса авиакомпании на горизонте 24 часа; 
предполагается, что модель будет запускаться раз в сутки и давать прогноз исполнимости расписаний на следующие сутки. 

---
## Анализ

Во время визуального анализа сделаны следующие выводы:

1. Обнаружен явный дизбаланс классов, при мультиклассовости, для бинарной классификации ситуация становится лучше.
2. Не выявлена сильная корреляция между параметрами

**Графики и больше деталей в .ipynb**


Произведено обогащение датасета путём извлечения дополнительных категориальных признаков:

- день полёта
- месяц полёта
- день недели
- время взлёта
- время посадки


Все категориальные признаки были преобразованы через One-hot-encoder

## Модели

По полученным данным были построены следующие модели, без подбора гиперпараметров

### Sklearn
1. KNeighborsClassifier
2. GaussianNB
3. RandomForestClassifier
4. DecisionTreeClassifier
5. LinearSVC
6. LogisticRegression

![Без имени](https://github.com/Oleksij-gh/infotech-task/assets/72971918/2e6cf124-5908-41fe-94c0-3ca4bff0fce3)


### Neural Network PyTorch
- 6 линейных слоёв с Relu фунцией активации
- Сигмоида на выходе
- Adam optimizer
- В качестве метрики использовалась бинарная кросс-валидация

Все модели не показали хороших результатов

Лучший результат у **Decision Trees** и **Random Forest**, вероятно модели переобучились из-за отсутствия ограничения глубины дерева.

Если бы модели показали, хоть сколько-то значимый результат, то можно было запустить подбор гиперпараметров по сетке.

Также была произведена попытка обучения с синтетическим обогащением данных путём OverSampling, что также не показало результата.

## Предположения и выводы

Из исходных данных не представляется возможным построение модели

Идеи:

1. Обогатить датасет дополнительными параметрами, например:
- Прогноз погодных условий
- Кампания рейса
- Тип рейса (частный, коммерческий)
- Ожидаемое количество пассажиров

2. Использовать другой инструмент для кодирования категориальных признаков:
- Catboost
- LOOE

3. Указать некоторый порог, при котором будет считаться, что рейс прибыл раньше \ позже \ вовремя
