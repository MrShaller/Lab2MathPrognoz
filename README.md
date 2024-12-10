# Lab2MathPrognoz

Цель данной работы
---
построение и оценка линейной мультифакторной модели (ЛМФМ) для анализа факторов, влияющих на количество аренды велосипедов в зависимости от погодных и календарных условий.

Задачи исследования:
---
1. Провести предварительный анализ данных.  
2. Построить линейную мультифакторную модель (ЛМФМ) для анализа влияния различных факторов.
3. Провести отбор значимых факторов, исключая факторы с низкой статистической значимостью и высокой корреляцией.
4. Оценить адекватность модели на основе коэффициента детерминации (R²), F-статистики, RMSE и ошибки.
5. Построить прогноз на основе полученной модели и сравнить его с реальными данными.
6. Бонусное задание: Провести тюнинг ЛМФМ с помощью лагов.

Краткое описание процедуры построения и оценки ЛМФМ
---
1. Предобработка данных:

* Удалены дублирующие признаки (например, casual и registered), так как они суммируются в целевой переменной cnt.
* Даты преобразованы в отдельные временные характеристики: год, месяц, день недели.
* Данные нормализованы для обеспечения корректной работы модели.

2. Построение базовой модели:

* Модель строилась с использованием всех доступных факторов.
* В качестве регрессора использовался метод наименьших квадратов (OLS) из библиотеки statsmodels.

3. Отбор значимых факторов:

* Факторы с p-value выше порогового значения (по умолчанию 0.05) исключались как статистически незначимые.
* Факторы с высокой корреляцией между собой (например, r>0.7) исключались для устранения мультиколлинеарности.
* Учитывалась корреляция с целевой переменной: признаки с корреляцией ниже порога (по умолчанию 0.3) исключались.

4. Вычислены ключевые метрики:
* коэффициент детерминации(R^2), F-статистика, RMSE и ошибка 𝐸.
* Проверена адекватность модели на основе значимости коэффициентов и F-теста.

5. Сравнение полной и сокращенной моделей:

* Построены прогнозы для обеих моделей.
* Вычислены RMSE для тестовой выборки для обеих моделей.
* Проведена визуализация реальных и предсказанных значений для анализа различий.

Дополнительное задание. Файнтюнинг модели
---

В рамках дополнительного задания был проведен файнтюнинг линейной модели для улучшения качества предсказаний. Основные шаги включали:

1. Генерация дополнительных признаков:

* Добавлены полиномиальные признаки второго порядка (например, взаимодействия temp и hum), чтобы учесть нелинейные зависимости.
* Созданы логарифмические и экспоненциальные преобразования некоторых признаков (например, логарифмирование windspeed).

2. Регуляризация модели:

* Для уменьшения переобучения была протестирована линейная регрессия с регуляризацией (Lasso и Ridge) из библиотеки sklearn.
* Параметры регуляризации (α) оптимизировались с помощью поиска по сетке (GridSearchCV).

3. Файнтюнинг гиперпараметров:

* Настроены параметры модели, такие как порог отбора признаков и параметры регуляризации.
* Для оценки качества использовалась кросс-валидация с 5 фолдами.

4. Оценка качества улучшенной модели:

* Полученная модель показала улучшение RMSE на тестовой выборке на 25% по сравнению с базовой моделью.
