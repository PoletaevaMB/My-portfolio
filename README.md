# Портфолио: аналитик данных

## Обо мне 

Привет! Меня зовут Мария, я начинающий аналитик данных. 
``{about_me_brief}``
В этом репозитории вы можете найти некоторые из моих проектов, выполненных во время обучения и практики.
<br>

## Навыки и технологии
- Инструменты анализа данных: ``SQL``, ``Excel``: 
- Языки программирования и библиотеки: ``Python``, ``Pandas``, ``math`` 
- Системы управления базами данных: ``MySQL``, ``PostgreSQL``
- Средства визуализации данных: ``PowerBi``, ``Matplotlib``, ``seaborn``
- Инструменты для машинного обучения: ``scikit-learn``, ``TensorFlow``



## Проекты
<p> Проект 1: Калькулятор юнит-экономики онлайн-школы</p>
<p>Что нужно было сделать:<p>
<ol>
  <li>Настроить в калькуляторе учет корректировок планов маркетинга</li>
  <li>Пересчитать план найма преподавателей.</li>
</ol>

<p>Как решала(-а): краткое описание решения (автореферат)<p>


> <a href="https://github.com/Skyproportfolio/data-analytics/blob/242649f63be48c763f3165413f84fa6b06c4c0a4/%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82%20%E2%84%961.xlsx">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

<br> 

<p> Проект 2: Калькулятор юнит-экономики онлайн-кинотеатра</p>
<p>Что нужно было сделать:<p>
<ol>
  <li>Определить, что является юнитом в нашей экономике</li>
  <li>Посчитать юнит-экономику продукта и предложить сценарий по настройке параметров для выхода на 25%-ную маржинальность</li>
  <li>Выбрать оптимальный вариант расчета Retention</li>
  <li>Собрать визуализации основных бизнес-показателей</li>
  <li>Поисследовать данные о пользователях и их поведении</li>
</ol>

<p>Как решала(-а): краткое описание решения (автореферат)<p>

> <a href="https://drive.google.com/drive/folders/11HcEeqniyrCMjuwHZ0GLysX0A2SEv-_x">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

<br> 

<p> Проект 3:  Моделирование изменения балансов студентов с помощью SQL</p>
<p>Что нужно было сделать:<p>
<ol>
 <li>Изучить ифнормацию из БД</li>
   <li>Понять сколько всего уроков было на балансе **всех учеников** за каждый календарный день </li>
   <li>Понять как это количество менялось под влиянием транзакций (оплат, начислений, корректирующих списаний) и уроков (списаний с баланса по мере прохождения уроков). </li>
  <li>Создать таблицу, где будут балансы **каждого студента** за каждый день. </li>
</ol>

  
  
 <p>Процесс:<p>
<ol>
   <li>Узнать когда была первая транзакция для каждого студента. Начиная с этой даты собирается баланс уроков </li>
  <li>Собрать таблицу с датами за каждый календарный день 2016 года.</li>
  <li>Узнать за какие даты имеет смысл собирать баланс для каждого студента. Для этого объединим таблицы и создадим CTE all_dates_by_user, где будут храниться все даты жизни студента после того, как произошла его первая транзакция.  </li>
  <li>Найти все изменения балансов, связанные с успешными транзакциями. Выберать все транзакции из таблицы payments, сгруппировать их по user_id и дате транзакции (без времени) и найти сумму по полю classes. 
В результате получилось CTE payments_by_dates с полями: user_id, payment_date, transaction_balance_change (сколько уроков было начислено или списано в этот день). </li>
  <li>Найти баланс студентов, который сформирован только транзакциями. Для этого объединить all_dates_by_user и payments_by_dates так, чтобы совпадали даты и user_id. Использовать оконные выражения (функцию sum), чтобы найти кумулятивную сумму по полю transaction_balance_change для всех строк до текущей включительно с разбивкой по user_id и сортировкой по dt. 
В результате полулся CTE payments_by_dates_cumsum с полями: user_id, dt, transaction_balance_change — transaction_balance_change_cs (кумулятивная сумма по transaction_balance_change).</li>
  <li>Найти изменения балансов из-за прохождения уроков. 
Создать CTE classes_by_dates, посчитав в таблице classes количество уроков за каждый день для каждого ученика. 
Буз учета вводных уроков и уроков со статусом, отличным от success и failed_by_student. 
Получился результат с такими полями: user_id, class_date, classes (количество пройденных в этот день уроков). Причем classes умножился на -1, чтобы отразить, что - — это списания с баланса.</li>
  <li>По аналогии с уже проделанным шагом для оплат создается CTE для хранения кумулятивной суммы количества пройденных уроков. 
Для этого объедяется таблицы all_dates_by_user и classes_by_dates так, чтобы совпадали даты и user_id. Используютсяоконные выражения (функцию sum), чтобы найти кумулятивную сумму по полю classes для всех строк до текущей включительно с разбивкой по user_id и сортировкой по dt. 
В результате получился CTE classes_by_dates_dates_cumsumс полями: user_id, dt, classes — classes_cs(кумулятивная сумма по classes). При подсчете кумулятивной суммы заменяются пустые значения нулями.</li>
  <li>Создается CTE balances с вычисленными балансами каждого студента. Для этого объединяются таблицы payments_by_dates_cumsum и classes_by_dates_dates_cumsum так, чтобы совпадали даты и user_id..</li>
    <li>Выбрать топ-1000 строк из CTE balances с сортировкой по user_id и dt. Изучить изменения балансов студентов. </li>
   <li>Посмотреть как менялось общее количество уроков на балансах студентов. </li>
  <li>Визуализация (линейная диаграмму) итогового результата.  </li>
</ol>

> <a href="[https://drive.google.com/drive/folders/1wdD-mfSeIsHWgrMLJz8Tv_ClAuP_EAOQ?usp=sharing](https://docs.google.com/spreadsheets/d/1-y-6qr7syPcW5n7bYBLYK34m7efQ8lbP/edit?usp=drive_link&ouid=112320574611415082385&rtpof=true&sd=true)">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>За указанный год наблюдался существенный рост показателей, а в частности оборачиваемости.</li>
</ol>

<br> 
<p>Проект 4: Построение витрины для модели машинного обучения в банке </p> 
<p>Что нужно было сделать: специалисты по машинному обучению попросили вас составить витрину для их модели.<p>

<p>Как решала(-а): краткое описание решения (автореферат)<p>

> <a href="https://drive.google.com/drive/folders/1QOk5AAh6x7jK_yHgfKI2sUFYR7AWUi5u">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

<br> 

<p>Проект 5: Расчет маркетингового АБ Теста в ювелирном магазине </p> 
<p>Что нужно было сделать:<p>
<ol>
  <li>Провести A/B Тест, где тестовой группе вместо пуш-уведомления приходит смс-сообщение с таким же содержанием</li>
  <li>Проанализировать результаты A/B Теста.</li>
</ol>

<p>Как решала(-а): краткое описание решения (автореферат)<p>

> <a href="https://github.com/Skyproportfolio/data-analytics/tree/main/Проект%20№5">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

<br> 

<p>Проект 6: Ad hoc в агрегаторе такси </p> 
<p>Что нужно было сделать:<p>
<ol>
  <li>Построть график с количеством заказов по суточным часам (на оси Х - часы от 0 до 23)</li>
  <li>Узнать, на сколько за один час в среднем делается больше заказов в часы пик, чем в обычное время? (по всем городам вместе)</li>
  <li>Рассмотреть города по отдельности: для каждого города выведите разницу в количестве заказов (среднечасовом) между пиковыми и не-пиковыми часами</li>
  <li>Узнать, в каком городе наблюдается наибольшее отклонение конверсии Order2Ride в пиковые часы по сравнению с не-пиковыми часами?</li>
  <li>Изучите заказы в Хабаровске и Тюмени</li>
  <li>Узнать,на сколько процентных пунктов *Order2Ride* в среднем в них ниже, чем в других городах? </li>
  <li>Понять, за счет какого звена воронки достигается эта разница? Сделайте выводы по Хабаровску и по Тюмени по отдельности</li>
  <li>Дать рекомендации менеджерам</li>
  <li>Локализовать проблему и выделить города, в которых такое происходит чаще всего:некоторые водители “мимикрируют координаты”, то есть на самом деле не приезжают в точку А своего заказа, но в приложение посылают сигнал, что они в эту точку А приехали. Таким образом они вынуждают клиента отменить заказ после “прибытия ими в точку А”. </li>
  <li>Тариф “Доставка” был запущен недавно на всей России. Изучите конверсии в рамках данного тарифа по городам, локализуйте просадку конверсии Order2Ride*в рамках данного тарифа **и дайте рекомендации отделу операционистов, которые занимаются этим тарифом.</li>
</ol>

<p>Как решала(-а): краткое описание решения (автореферат)<p>

> <a href="https://github.com/Skyproportfolio/data-analytics/tree/main/Проект%20№6">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

<br> 

<p>Проект 7: Расчет банковских резервов по просроченной задолженности </p> 
<p>Что нужно было сделать:<p>
<ol>
  <li>Рассчитать суммарный объем резервов из расчета на 1 августа 2022 года</li>
  <li>Написать функцию, которая будет на вход брать отчетную дату (например, 1 августа 2022 года) и датафрейм по аналогии с файлом Client_Data_01082022 и будет рассчитывать суммарный объем банковских резервов на отчетную дату.</li>
  <li>Построить график суммарных резервов для набора отчетных дат от 1 до 30 августа (включительно) и оценить абсолютный и процентный прирост резервов за месяц</li>
  <li>Постройте в питоне визуализации, которые помогут отследить размер резервов (например, в разрезе продукта или размера выданного кредита)</li>
</ol>

<p>Как решала(-а): краткое описание решения (автореферат)<p>

> <a href="https://github.com/Skyproportfolio/data-analytics/tree/main/Проект%20№7">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

<br> 

<p>Проект 8: Геосегментация и анализ в агрегаторе доставки</p> 
<p>Что нужно было сделать: изучите динамику показателя конверсии в отдельных гексагонах и в городе в целом с помощью фильтрации.<p>

<p>Как решала(-а): краткое описание решения (автореферат)<p>

> <a href="https://github.com/Skyproportfolio/data-analytics/tree/main/Проект%20№8">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

<br> 

<p>Проект 9: Анализ маркетингового вебинара</p> 
<p>Что нужно было сделать:<p>
<ol>
  <li>Изучить конверсию в посещение вебинара из регистрации на вебинар с различных площадок. Выявить площадку (блогера / паблик / группу), которая накручивает регистрации</li>
  <li>Изучить посещаемость вебинара с точки зрения притока и оттока</li>
</ol>

<p>Как решала(-а): краткое описание решения (автореферат)<p>

> <a href="https://github.com/Skyproportfolio/data-analytics/tree/main/Проект%20№9">Ссылка на проект</a>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

<br> 

<p>Проект 10: Моделирование изменения балансов студентов</p> 
<p>Что нужно было сделать:получить запрос, который собирает данные о балансах студентов за каждый прожитый ими день.<p>

<p>Как решала(-а): краткое описание решения (автореферат)<p>

> <a href="https://github.com/Skyproportfolio/data-analytics/blob/main/Проект%2010.xlsx">Ссылка на проект</a>
<br>

<p>Выводы (итоги):<p>
<ol>
  <li>Итог №1</li>
  <li>Итог №2</li>
</ol>

## Контактная информация
- Email: name@email.com
- LinkedIn: https://www.linkedin.com/in/username/
- Личный сайт: https://www.username.com
