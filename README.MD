` # Лабораторна робота 1. Робота з СУБД  ``PostgreSQL``  та основи SQL `

`## Загальна інформація`

`**Здобувач освіти:** [Мельник Станіслав Павлович]`

`**Група:** [ІПЗ-33]`

`**Обраний рівень складності:** [1/2]`

`## Виконання завдань`

`Рівень 1`

`1. Основні SELECT запити `

` -- Отримати всі записи з таблиці  ``customers`

` SELECT * FROM  ``customers``;`

` -- Вивести тільки назви товарів і їхні ціни з таблиці  ``products`

` SELECT  ``product_name`` ,  ``unit_price``  FROM  ``products``;`

` -- Показати контактні дані всіх співробітників (ім'я, прізвище, телефон,  ``email``)`

` SELECT  ``first_name`` ,  ``last_name`` ,  ``phone`` ,  ``email``  FROM  ``employees`

<img src="https://github.com/N1ghtMare1q/lab01/blob/main/photo/photo_1.jpg?raw=true" width="500">

`2. Прості умови WHERE`

`-- Знайти всіх клієнтів з міста Київ`

` SELECT * FROM  ``customers``  WHERE  ``city``  = 'Київ'; `

`-- Вивести товари, які коштують більше 25000 грн`

` SELECT * FROM  ``products``  WHERE  ``unit_price``  > 25000; `

`-- Показати всі замовлення зі статусом '``delivered`` ' (виправлено на  ``order_status``)`

` SELECT * FROM  ``orders``  WHERE  ``order_status``  = ' ``delivered``';`

` -- Знайти співробітників, які працюють у відділі продажів (посада —  ``title``)`

` SELECT * FROM  ``employees``  WHERE  ``title``  ILIKE '%продаж%'; `

<img src="https://github.com/N1ghtMare1q/lab01/blob/main/photo/photo_2.jpg?raw=true" width="1000">

`3. Базове сортування ORDER BY`

`-- Відсортувати товари за зростанням ціни`

` SELECT * FROM  ``products``  ORDER BY  ``unit_price``  ASC; `

`-- Показати клієнтів в алфавітному порядку за іменем контактної особи`

` SELECT * FROM  ``customers``  ORDER BY  ``contact_name``  ASC; `

`-- Вивести замовлення від найновіших до найстаріших`

` SELECT * FROM  ``orders``  ORDER BY  ``order_date``  DESC; `

<img src="https://github.com/N1ghtMare1q/lab01/blob/main/photo/photo_9.jpg?raw=true" width="1000">

`4. Обмеження результатів LIMIT `

`-- Показати перші 10 найдорожчих товарів`

` SELECT * FROM  ``products``  ORDER BY  ``unit_price``  DESC LIMIT 10; `

`-- Вивести 5 останніх замовлень (за датою)`

` SELECT * FROM  ``orders``  ORDER BY  ``order_date``  DESC LIMIT 5; `

`-- Отримати перших 8 клієнтів в алфавітному порядку`

` SELECT * FROM  ``customers``  ORDER BY  ``contact_name``  ASC LIMIT 8; `



`Рівень 2`

`1. Пошук за зразком з LIKE`

`-- Знайти всіх клієнтів, чиї імена починаються на "Іван"`

` SELECT * FROM  ``customers``  WHERE  ``contact_name``  ILIKE 'Іван%'; `

`-- Вивести товари, в назві яких є слово "``phone``" або "телефон"`

` SELECT * FROM  ``products`` `

` WHERE  ``product_name``  ILIKE '% ``phone`` %' OR  ``product_name``  ILIKE '%телефон%'; `

`-- Самостійний 1 (початок): Клієнти з корпоративною поштою на домені gmail.com`

`-- Бізнес-логіка: вибірка бази для розсилки роздрібним клієнтам`

` SELECT * FROM  ``customers``  WHERE  ``email``  ILIKE '%@gmail.com'; `

`-- Самостійний 2 (кінець): Клієнти з прізвищем на "-``енко``"`

`-- Бізнес-логіка: персоналізація звернень за українськими прізвищами`

` SELECT * FROM  ``customers``  WHERE  ``contact_name``  ILIKE '% ``енко``%';`

`-- Самостійний 3 (містить): Товари з характеристикою об'єму пам'яті 128GB`

`-- Бізнес-логіка: швидкий пошук девайсів конкретної конфігурації під запит покупця`

` SELECT * FROM  ``products``  WHERE  ``product_name``  ILIKE '%128GB%'; `

<img src="https://github.com/N1ghtMare1q/lab01/blob/main/photo/photo_8.jpg?raw=true" width="1500">

`2. Логічні оператори AND, OR, NOT`

`-- Знайти товари дорожчі за 15000 грн і дешевші за 50000 грн`

` SELECT * FROM  ``products``  WHERE  ``unit_price``  > 15000 AND  ``unit_price``  < 50000; `

`-- Вивести клієнтів з Києва або Львова, які є юридичними особами`

` SELECT * FROM  ``customers`` `

`WHERE (``city``  = 'Київ' OR  ``city``  = 'Львів') AND  ``customer_type``  = ' ``company``';`

`-- Самостійний 1: Товари в наявності, які не зняті з виробництва`

`-- Бізнес-логіка: формування актуального каталогу для показу на вітрині`

` SELECT * FROM  ``products``  WHERE  ``units_in_stock``  > 0 AND NOT  ``discontinued``;`

`-- Самостійний 2: Замовлення, які ще не доставлені і не скасовані`

`-- Бізнес-логіка: вибірка замовлень, які потребують дій від менеджерів або кур'єрів`

` SELECT * FROM  ``orders``  WHERE  ``order_status``  != ' ``delivered`` ' AND  ``order_status``  != ' ``cancelled``';`

`-- Самостійний 3: Клієнти не з Києва, у яких вказано телефон`

` -- Бізнес-логіка: контактна база для регіонального  ``телемаркетингу`

` SELECT * FROM  ``customers``  WHERE NOT  ``city``  = 'Київ' AND  ``phone``  IS NOT NULL; `

` -- Самостійний 4: Дорогі або дефіцитні товари (ціна понад 40000 або залишок менше 5  ``шт``)`

` -- Бізнес-логіка: контроль преміальних позицій та сигналізація відділу  ``закупівель`

` SELECT * FROM  ``products``  WHERE  ``unit_price``  > 40000 OR  ``units_in_stock``  < 5; `

<img src="https://github.com/N1ghtMare1q/lab01/blob/main/photo/photo_7.jpg?raw=true" width="1500">

`3. Оператори IN, BETWEEN, IS NULL`

`-- Вивести клієнтів з міст Київ, Харків, Одеса, Дніпро`

` SELECT * FROM  ``customers``  WHERE  ``city``  IN ('Київ', 'Харків', 'Одеса', 'Дніпро'); `

`-- Знайти товари в ціновому діапазоні від 10000 до 30000 грн`

` SELECT * FROM  ``products``  WHERE  ``unit_price``  BETWEEN 10000 AND 30000; `

`-- Самостійний 1 (IN): Замовлення у процесі обробки`

`-- Бізнес-логіка: оперативний моніторинг посилок, що готуються або їдуть`

` SELECT * FROM  ``orders``  WHERE  ``order_status``  IN (' ``shipped``', '``processing``', '``pending``');`

`-- Самостійний 2 (IN): Співробітники на посадах керівництва та бухгалтерії`

`-- Бізнес-логіка: службова вибірка адміністративного персоналу`

` SELECT * FROM  ``employees``  WHERE  ``title``  IN ('Генеральний директор', 'Головний бухгалтер'); `

`-- Самостійний 3 (BETWEEN): Замовлення, оформлені за перші три місяці 2024 року`

`-- Бізнес-логіка: аналіз динаміки продажів за I квартал`

` SELECT * FROM  ``orders``  WHERE  ``order_date``  BETWEEN '2024-01-01' AND '2024-03-31'; `

`-- Самостійний 4 (BETWEEN): Товари із залишками на складі від 10 до 25 одиниць`

`-- Бізнес-логіка: контроль стабільного запасу без ризику затоварення`

` SELECT * FROM  ``products``  WHERE  ``units_in_stock``  BETWEEN 10 AND 25; `

`-- Самостійний 5 (IS NULL): Клієнти — фізичні особи (без зазначеної компанії)`

`-- Бізнес-логіка: розділення клієнтської бази для B2C акцій`

` SELECT * FROM  ``customers``  WHERE  ``company_name``  IS NULL; `

`-- Самостійний 6 (IS NOT NULL): Замовлення, які вже передані на доставку (мають дату відправки)`

` -- Бізнес-логіка: підтвердження початку перевезення для нарахування  ``трекінг``-днів`

` SELECT * FROM  ``orders``  WHERE  ``shipped_date``  IS NOT NULL; `

<img src="https://github.com/N1ghtMare1q/lab01/blob/main/photo/photo_6.jpg?raw=true" width="2000">

`4. Комбінування умов`

`-- Самостійний 1 (LIKE + AND): Ноутбуки або комп'ютери дорожчі за 40000 грн`

`-- Бізнес-логіка: сегментація флагманської комп'ютерної техніки`

` SELECT * FROM  ``products``  WHERE  ``product_name``  ILIKE '% ``MacBook`` %' AND  ``unit_price``  > 40000; `

`-- Самостійний 2 (BETWEEN + IN): Товари середнього діапазону з категорій 1 або 2`

` -- Бізнес-логіка: акційна  ``підбірка``  електроніки для  ``промо``-кампанії`

` SELECT * FROM  ``products``  WHERE ( ``unit_price``  BETWEEN 20000 AND 35000) AND  ``category_id``  IN (1, 2); `

`-- Самостійний 3 (IS NULL + OR): Клієнти, у яких відсутній контактний титул або компанія`

`-- Бізнес-логіка: вибірка клієнтів з неповною корпоративною карткою`

` SELECT * FROM  ``cust``omers``  WHERE  ``contact_title``  IS NULL OR  ``company_name``  IS NULL; `

`-- Самостійний 4 (LIKE + BETWEEN + NOT): Активні телевізори у діапазоні 25000–60000 грн`

`-- Бізнес-логіка: формування актуального каталогу домашніх медіа-центрів`

` SELECT * FROM  ``products`` `

`WHERE (``product_name``  ILIKE '%QLED%' OR  ``product_name``  ILIKE '%OLED%') `

`  AND (``unit_price``  BETWEEN 25000 AND 60000) `

`   AND NOT  ``discontinued``;`

` -- Самостійний 5 (IN + LIKE + AND): Корпоративні клієнти з Києва або Львова з поштою  ``ua`

`-- Бізнес-логіка: безпечна розсилка перевіреним юридичним особам`

` SELECT * FROM  ``customers`` `

` WHERE  ``city``  IN ('Київ', 'Львів')  `

`   AND  ``customer_type``  = ' ``company``' `

`   AND  ``email``  ILIKE '%. ``ua``';`

<img src="https://github.com/N1ghtMare1q/lab01/blob/main/photo/photo_5.jpg?raw=true" width="1500">

`5. Складне сортування та пагінація`

`-- Запит 1: Товари за зростанням категорії, а всередині — за спаданням ціни`

`-- Бізнес-логіка: відображення позицій від найдорожчих у кожному розділі каталогу`

` SELECT * FROM  ``products``  ORDER BY  ``category_id``  ASC,  ``unit_price``  DESC; `

`-- Запит 2: Клієнти за містом (алфавіт), а всередині — за датою реєстрації від нових`

`-- Бізнес-логіка: аналіз регіонального приросту користувачів`

` SELECT * FROM  ``customers``  ORDER BY  ``city``  ASC,  ``registration_date``  DESC; `

`-- Запит 3: Замовлення за статусом, а всередині однакових — від найновішої дати`

` -- Бізнес-логіка:  ``пріоритезація``  черги для складу `

` SELECT * FROM  ``orders``  ORDER BY  ``order_status``  ASC,  ``order_date``  DESC; `

`-- Пагінація Сторінка 1: перші 10 товарів за алфавітом`

`-- Бізнес-логіка: сторінка №1 каталогу`

` SELECT * FROM  ``products``  ORDER BY  ``product_name``  ASC LIMIT 10 OFFSET 0; `

`-- Пагінація Сторінка 2: наступні 10 товарів`

`-- Бізнес-логіка: сторінка №2 каталогу`

` SELECT * FROM  ``products``  ORDER BY  ``product_name``  ASC LIMIT 10 OFFSET 10; `



`## Висновки`

` Висновок: Під час виконання лабораторної роботи було опановано роботу з хмарною СУБД  ``PostgreSQL``  у середовищі  ``Supabase``. Було успішно розгорнуто навчальну базу даних «``ТехноМарт``», проаналізовано схему та зв'язки між таблицями. На практиці закріплено роботу з основними конструкціями мови SQL (DQL): оператором SELECT, механізмами фільтрації рядків WHERE, шаблонами LIKE/ILIKE, логічними операторами, перевіркою множин IN, діапазонів BETWEEN, специфікою опрацювання значень NULL, сортуванням ORDER BY за декількома стовпцями та організацією пагінації за допомогою LIMIT і OFFSET. Усі самостійні запити сформовано на базі реалістичних бізнес-сценаріїв електронної комерції.`

`**Самооцінка**: [4]`

`**``Обгрунтування`` **: [Повністю виконано всі завдання Рівнів 1 та 2 згідно з методичними вказівками. Кожен самостійний запит містить коментарі та опис практичної бізнес-логіки. Результати перевірено в середовищі  ``Supabase``, дані відповідають структурі схеми БД.]`

