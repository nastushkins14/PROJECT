# **ПРОЕКТ** :woman_factory_worker::nail_care:
**План:**
1. Выбор темы
2. Сбор данных
3. Предварительная обработка
4. Визуализация
5. Создание новых признаков
6. Гипотезы
7. Машинное обучение

**Команда:**
* Бычкова Анастасия :fairy_woman:
* Сысоева Кристина :elf_woman:
## **Шаг 1. Выбор темы**
Мы решили предсказать цены акций ПАО Сбербанк с помощью машинного обучения

## **Шаг 2. Сбор данных**
Файл этапа: data_collection_and_preprocessing.ipynb

**Результаты:**
Нашли различные датасеты с ценами для Сбербанка, индекса Мосбиржи и валютного курса. Собрав единый датасет,мы решили добавить информацию о ключевых макроэконмических показателях страны, которые будут отражать состояние эконмоики в целом. Для этого спарсили данные по ключевой ставке и инфляции в РФ за нужный период.
## **Шаг 3. Предварительная обработка**
Файл этапа: data_collection_and_preprocessing.ipynb

После того,как мы объединили все собранные датасеты в единый датафрейм, мы провели предварительную обработку данных для дальнейшей работы. С пропусками работать не пришлось, они отсутствовали. Данные с сайта ЦБ РФ спарсились без разделения на целую и дробную часть, поэтому мы их преобразовали. Чтобы проводить дальнейший анализ и визуализировать данные, ячейки были переведены из формата object в формат float (для которых это было необходимо).
## **Шаг 4. Визуализация**
Файл этапа: EDA_and_new_features_creating.ipynb

На этапе проведения разведочного анализа данных (EDA) мы обнаружили сильню положительную линейную связь между таргетом - ценами акций ПАО Сбербанк и ценами индекса IMOEX и валютной пары USD/RUB. Здесь же выдвинули гипотезу о том, что цены акций бывают несправделивыми в понедельник и пятницу из-за ожиданий инвесторов относительно выходных/отыгрывающихся новостей,произошедших в выходные, и решили в дальнейшем проверить её с помощью индекса IMOEX, так как он диверсифицирован и не отыгырвает на себя новости, касающиеся лишь одной компании. Также по построенной гистограмме для таргета выдвинута гипотеза о нормальности данных, так как распределение похоже на нормальное со смещением вправо и некоторыми выбросами на левом хвосте.
## **Шаг 5. Создание новых признаков**
Файл этапа: EDA_and_new_features_creating.ipynb

Создали новый признак - рабочий день,чтобы посмотреть, собирались ли данные по выходным. Эти данные для нас лишние, поскольку торги не проводятся, но датасет мог заполняться средними значениями. 
Еще один дополнительный признак - номер месяца. Это промежуточный этап, который необходим для создания более важного признака - окончания квартала. Так как компании выпускают свои ежеквартальные отчеты, то при окончании квартала среди цен может наблюдаться высокая волатильность. Этот признак позволит нам проверить гипотезу о влиянии ежеквартальной отчетности на цены акций ПАО Сбербанк и, при его наличии,учесть этот факт на этапе машинного обучения. И, наконец, последний созданный нами признак - день недели, который нужен для тестирования гипотезы о существенном изменении цен в понедельник и пятницу.
## **Шаг 6. Гипотезы**
Файл этапа: testing.ipynb

Проверили следующие гипотезы:
* Цены акций ПАО Сбербанк имеют нормальное распределение
* Ряд с ценами акций Сбербанка стационарен
* Окончание квартала существенно влияет на динамику цен акций Сбербанка
* На цены акций Сбербанка влияет изменение ключевой ставки ЦБ РФ
* Наличие автокорреляции в данных таргета
* В понедельник и пятницу в цены акций закладываются ожидания относительно выходных или же отыгрываются новости,произошедшие за субботу и воскресенье.
## **Шаг 7. Машинное обучение**
Файл этапа: ML.ipynb

Обучили линейную регрессию и в результате получили достаточно точную модель, коэффициент детерминации у которой близок к 1. 
