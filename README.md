# ML_YP
# Обучение с учителем: качество модели
_____
## Описание исследования

Интернет-магазин «В один клик» продаёт разные товары: для детей, для дома, мелкую бытовую технику, косметику и даже продукты. Отчёт магазина за прошлый период показал, что активность покупателей начала снижаться. Привлекать новых клиентов уже не так эффективно: о магазине и так знает большая часть целевой аудитории. Возможный выход — удерживать активность постоянных клиентов. Сделать это можно с помощью персонализированных предложений.
«В один клик» — современная компания, поэтому её руководство не хочет принимать решения просто так — только на основе анализа данных и бизнес-моделирования. 

_____
## Цель исследования
    
Разработать решение, которое позволит персонализировать предложения постоянным клиентам, чтобы увеличить их покупательскую активность.
    
_____
## Задачи исследования
1. Нужно промаркировать уровень финансовой активности постоянных покупателей. В компании принято выделять два уровня активности: «снизилась», если клиент стал покупать меньше товаров, и «прежний уровень».
2. Нужно собрать данные по клиентам по следующим группам:
    - Признаки, которые описывают коммуникацию сотрудников компании с клиентом.
    - Признаки, которые описывают продуктовое поведение покупателя. Например, какие товары покупает и как часто.
    - Признаки, которые описывают покупательское поведение клиента. Например, сколько тратил в магазине.
    - Признаки, которые описывают поведение покупателя на сайте. Например, как много страниц просматривает и сколько времени проводит на сайте.
3. Нужно построить модель, которая предскажет вероятность снижения покупательской активности клиента в следующие три месяца.
4. В исследование нужно включить дополнительные данные финансового департамента о прибыльности клиента: какой доход каждый покупатель приносил компании за последние три месяца.
5. Используя данные модели и данные о прибыльности клиентов, нужно выделить сегменты покупателей и разработать для них персонализированные предложения.
_____
### Исходные данные.
    
Мы будем работать с тремя датасетами:
1. market_file.csv
2. market_money.csv
3. market_time.csv
4. money.csv
    
1. market_file.csv Таблица, которая содержит данные о поведении покупателя на сайте, о коммуникациях с покупателем и его продуктовом поведении.
    - id — номер покупателя в корпоративной базе данных.
    - Покупательская активность — рассчитанный класс покупательской активности (целевой признак): «снизилась» или «прежний уровень».
    - Тип сервиса — уровень сервиса, например «премиум» и «стандарт».
    - Разрешить сообщать — информация о том, можно ли присылать покупателю дополнительные предложения о товаре. Согласие на это даёт покупатель.
    - Маркет_актив_6_мес — среднемесячное значение маркетинговых коммуникаций компании, которое приходилось на покупателя за последние 6 месяцев. Это значение показывает, какое число рассылок, звонков, показов рекламы и прочего приходилось на клиента.
    - Маркет_актив_тек_мес — количество маркетинговых коммуникаций в текущем месяце.
    - Длительность — значение, которое показывает, сколько дней прошло с момента регистрации покупателя на сайте.
    - Акционные_покупки — среднемесячная доля покупок по акции от общего числа покупок за последние 6 месяцев.
    - Популярная_категория — самая популярная категория товаров у покупателя за последние 6 месяцев.
    - Средний_просмотр_категорий_за_визит — показывает, сколько в среднем категорий покупатель просмотрел за визит в течение последнего месяца.
    - Неоплаченные_продукты_штук_квартал — общее число неоплаченных товаров в корзине за последние 3 месяца.
    - Ошибка_сервиса — число сбоев, которые коснулись покупателя во время посещения сайта.
    - Страниц_за_визит — среднее количество страниц, которые просмотрел покупатель за один визит на сайт за последние 3 месяца.
2. market_money.csv Таблица с данными о выручке, которую получает магазин с покупателя, то есть сколько покупатель всего потратил за период взаимодействия с сайтом.
    - id — номер покупателя в корпоративной базе данных.
    - Период — название периода, во время которого зафиксирована выручка. Например, 'текущий_месяц' или 'предыдущий_месяц'.
    - Выручка — сумма выручки за период.
3. market_time.csv Таблица с данными о времени (в минутах), которое покупатель провёл на сайте в течение периода.
    - id — номер покупателя в корпоративной базе данных.
    - Период — название периода, во время которого зафиксировано общее время.
    - минут — значение времени, проведённого на сайте, в минутах.
4. money.csv Таблица с данными о среднемесячной прибыли покупателя за последние 3 месяца: какую прибыль получает магазин от продаж каждому покупателю.
    - id — номер покупателя в корпоративной базе данных.
    - Прибыль — значение прибыли.

    **Что сделала**
1. Построили модель, которая предскажет вероятность снижения покупательской активности клиента в следующие три месяца.
2. Используя данные модели и данные о прибыльности клиентов, выделили сегменты покупателей "Молодые мамы" и разработали  для них персонализированные предложения.

**Ход работы:**
1. загрузили и проверили 4 датафрейма: все данные в таблицах соответствовали описанию
2. Предобработка данных: пропущенные значения и явные дубликаты отсутствовали. Изменили в 3 столбцах типы данных. Удалили данные по 1 пользователю с аномальными значениями, проверили уникальность значений исправили орфографические ошибки
3. Исследовательский анализ данных: отобрали клиентов с покупательской активностью не менее трёх месяцев  Аномалии в данных отсутствовали. Построили графики зависимостей по критериям от целевого. Сделали вывод по распределению категорий сниженой покупательской активности и высокой. 
4. Объединили таблицы, удалили столбец 'id' и провели корреляционный анализ, выделили 3 признака с высокой корреляцией: Страниц_за_визит 0,75, минут_предыдущий_месяц 0,69, минут_текущий_месяц 0,58
5. используя один общий пайплайн для всех моделей и инструмент подбора гиперпараметров, определили параметры лучшей модели. Лучшая модель: Логистическая регрессия с C=1, penalty='l1', random_state=13, solver='liblinear' ROC-AUC равным 0.90 стала лучшей моделью. Она выявила ключевые факторы покупательской активности: время на сайте, количество просмотренных страниц и категорий, доля акционных покупок, количество неоплаченных товаров, количество маркетинговых акций, популярная категория товаров и сумма потраченных денег.
6. Оценили важность признаков для лучшей модели и построили график важности с помощью метода SHAP. Признаки “num_минут_предыдущий_месяц”, “num_Страниц_за_визит” и “num_Средний просмотр категории за визит”, являются наиболее значимыми, так как они имеют наибольшее влияние на покупательскую активность. “ohe_Популярная категория Товары для детей” и ”num выручка текущий месяц” - менее важны для модели.
7.Исходя из предыдущих наблюдений, попробуем сформулировать гипотезу и разработать стратегию влияния на пользовательскую активность.

**"Молодые мамы"**

Есть категория клиентов, которые проводят мало времени на сайте и просматривают мало категорий, покупают акционные товары и товары для детей. Предположим это мамы в декрете, заработок которых снизился, но при этом свободного времени для выбора товаров меньше + потребности в детских товаров выше и регулярнее. Как стратегия повышения покупательской активности: регулярный выпуск промокодов, акции - вместе дешевле, персонализированные рекомендации из других категорий товаров (например доставка еды/аптеки), бесплатная доставка, бесплатная примерка и тд.
"Потухшие" клиенты, которые редко посещают сайт и мало тратят: увеличивать количество маркетинговых коммуникаций с клиентами, чтобы повысить их лояльность и интерес к вашим товарам, предлагать новые категории
Возьмем категорию "Молодые мамы":
- "num_минут_предыдущий_месяц": Покупатели в этой группе проводят меньше времени на сайте, чем другие. Это может быть связано с ограничением свободного времени
- "num_Страницы_за_визит": Они просматривают меньше страниц за визит, что указывает на их фокусировку на конкретных товарах или категориях, например "Товары для детей".
- "num_Средний_просмотр_категории_за_визит": Они просматривают меньше категорий товаров за визит, что также указывает на их узкую фокусировку на определенных товарах или категориях.
- "num_Акционные покупки": Большая часть их покупок совершается по акции, что подтверждает их стремление к экономии.
- "num_Неоплаченые продукты штука квартал": Они часто оставляют товары в корзине без оплаты, возможно, ожидая снижения цены/или набирают до бесплатной доставки

Дополнительный анализ подтверждает гипотезу о категории покупателя - мамы в декрете

Подтвердившиеся признаки:

- Акционные покупки: в среднем совершают больше акционных покупок (0.9 против 0.21 у остальных покупателей).
- Длительность: Средняя длительность посещения сайта примерно одинакова для обеих групп покупателей (598 минут у молодых мам против 590 минут у остальных покупателей). Скорее всего времени на поиск товаров у данной категории покупателей достаточно
- Неоплаченные продукты: молодые мамы в среднем оставляют больше неоплаченных продуктов (5.0 против 2.0 у остальных покупателей). Необходимо проанализировать возможные причины (платная доставка до какой-то суммы, ожидание акции и тд)
- Общая выручка за 3 месяца: Общая выручка за последние три месяца примерно одинакова для обеих групп покупателей (15145.7 у молодых мам и 15107.75 у остальных покупателей). Таким образом есть рекомендация обратить внимание на данную категорию покупателей, возможно, увеличив объем данной категории или их выручку
- Общее время на сайте за 2 месяца: Остальные покупатели в среднем проводят на сайте больше времени (30.0 минут против 20.0 минут у молодых мам).
- Популярная категория: товары для детей, возможно, магазину необходимо проанализировать ценообразование на другие категории товаров чтобы расширить ассортимент
- Прибыль: Средняя прибыль от остальных покупателей немного выше, чем от молодых мам, возможно за счет акционных товаров, где маржинальность меньше (4.04 против 3.92).
- Разрешение на рассылку: Большинство покупателей из обеих групп разрешили рассылку.
- Средний просмотр категорий за визит: Остальные покупатели в среднем просматривают больше категорий за визит (4.0 против 2.0 у молодых мам). Признак гипотезы подтвердился
- Страниц за визит: Остальные покупатели в среднем просматривают больше страниц за визит (10.0 против 4.0 у молодых мам).

**Рекомендации по работе с сегментом "Молодые мамы" для увеличения покупательской активности:**

1. Увеличение количества акций: скидки, бонусы или персонализированные рекомендации
2. Оптимизация CJM для экономии времени на сайте и увеличив кол-во просмотренных страниц
3. Рекомендации по профилю 360 для экономии времени покупателя
4. Работа с неоплаченными продуктами: проработать вопрос с бесплатной доставкой, отправлять напоминания, гарантия возврата
5. Персонализированные предложения по популярной категории и рекомендуемой исходя из профиля 360, альтернативные товары с более высокой маржой
6. Проведение A/B тетсирования для подтверждения гипотез и приоритезации рекомендаций, оценки возможной прибыли