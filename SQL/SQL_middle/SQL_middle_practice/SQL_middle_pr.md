# Отбор сотрудников для премирования

**Описание:**  
Вы — HR-аналитик в крупной ритейл-компании. По трудовому договору сотрудники компании получают новогоднюю премию (дата выплаты — 2024-12-31) при условии, что за весь год они совершили от 15 продаж включительно, сумма которых составила строго более 100000 рублей, и при этом они не ушли рано с работы.

Нужно учесть, что премии могут получить только те сотрудники, которые были трудоустроены более чем за 1 год до даты выплаты премии (до 30 декабря 2023 включительно).

Для каждого филиала компании определите, какое количество его сотрудников получит премию.

**Формат ввода:**  
Таблица employees:
- employee_id (int) — уникальный идентификатор сотрудника
- department (string) — филиал компании
- employment_date (date) — дата трудоустройства
- sales_numb (int) — количество продаж сотрудника
- sales_sum (int) — сумма продаж сотрудника
- late_days (int) — кол-во опозданий

Данные не содержат пропусков или некорректных значений.

**Формат вывода:**  
Запрос должен вернуть таблицу с полями в таком порядке:
- department (string) — филиал компании
- bonus_total (int) — количество сотрудников с премией (≥0)

Выходные данные отсортированы по филиалу (по алфавиту от А до Я). Даже если у филиала ноль сотрудников с бонусом, его нужно включить в таблицу со значением bonus_total = 0.

**Код:**
```sql
CREATE TABLE employees (employee_id INT PRIMARY KEY,
 department VARCHAR(50) NOT NULL,
 employment_date DATE NOT NULL,
 sales_numb INT NOT NULL,
 sales_sum DECIMAL(10,2) NOT NULL,
 late_days INT NOT NULL);

INSERT INTO employees (employee_id, department, employment_date, sales_numb, sales_sum, late_days) VALUES
(100000, 'Центральный', '2024-10-03', 3, 48058, 15),
(100001, 'Юго-Западный', '2022-09-01', 19, 130000, 0),
(100003, 'Северный', '2022-01-01', 20, 150000, 0),
(100004, 'Юго-Западный', '2021-11-02', 7, 130940, 5),
(100009, 'Северо-Западный', '2023-10-22', 15, 110620, 1);
```

---

# Подсчет сметы для ремонта

**Описание:**  
Вам нужно посчитать стоимость ремонтных работ в отеле. Для формирования сметы необходимо отобрать номера, которые требуют ремонта. Номера категории «Люкс» требуют ремонтировать раз в два года, номера категории «Премиум» — раз в год, а номера категории «Базовый» — раз в 5 лет. Дата формирования отчета — 2024-06-01 (дата должна быть строго меньше указанного срока). К примеру, номер категории «Премиум», который ремонтировали 2023-05-31, требует ремонта, а тот, который ремонтировали 2024-06-01 — нет.

В базе данных не хранится информация о категориях номеров, но определить ее можно по названию номера: текст названия всегда содержит соответствующую категорию и только ее. Категория может содержаться в разном регистре.

Подсчитайте итоговую сумму ремонтных работ, исходя из следующих цен на ремонт (стоимость указана за 1 квадратный метр):
- Премиум — 250000 рублей
- Люкс — 100000 рублей
- Базовый — 50000 рублей

**Формат ввода:**  
Таблица rooms:
- room_number (int) — номер комнаты
- room_title (string) — название номера
- floor_area (float) — площадь номера в квадратных метрах
- last_fixed (date) — дата последнего ремонта номера

Данные не содержат пропусков или некорректных значений.

**Формат вывода:**  
Запрос должен вернуть таблицу со следующим полем:
- total_cost (float) — итоговая стоимость ремонта всех номеров, округленная до копеек (двух чисел после точки).

Если в отеле нет номеров, требующих ремонта, выводом будет 0.00.

**Код:**
```sql
CREATE TABLE rooms (room_number INT PRIMARY KEY,
 room_title VARCHAR(100) NOT NULL,
 floor_area DECIMAL(10,2) NOT NULL,
 last_fixed DATE NOT NULL);

INSERT INTO rooms (room_number, room_title, floor_area, last_fixed) VALUES
(1, 'Экстра базовый с дополнительным спальным местом', 21.76, '2015-01-11'),
(2, 'Видовой премиум с видом на город', 100.04, '2020-07-04'),
(3, 'Стандартный премиум с видом на море', 96.57, '2016-07-20'),
(4, 'Стандартный премиум с дополнительным спальным местом', 57.97, '2018-11-12'),
(5, 'Президентский люкс', 52.47, '2020-03-27');
```

---

# Конкурсный отбор абитуриентов

**Описание:**  
Приемная комиссия факультета юриспруденции получила список абитуриентов с их проходными баллами по 3 предметам (Русский язык, История, Обществознание), а также отдельную таблицу с перечнем дополнительных достижений. Дополнительные 10 баллов можно получить только за одно из личных достижений, остальные достижения не учитываются.

Отберите 25 студентов с наибольшим количеством баллов для зачисления на бюджет. Если сумма баллов студентов совпадает, преимущество отдается тем студентам, у которых выше балл по обществознанию. Отсортируйте студентов по сумме набранных предметов (средний балл округлить «вниз»).

Учитывайте, что для зачисления балл по каждому предмету у студента должен быть выше среднего балла всех студентов по этому предмету (средний балл округлить «вниз»).

**Формат ввода:**  
Таблица students:
- student_id (int) — уникальный идентификатор студента
- russian_language (int) — количество баллов по русскому языку
- history (int) — количество баллов по истории
- social_studies (int) — количество баллов по обществознанию

Таблица achievements:
- student_id (int) — уникальный идентификатор студента
- golden_medal (boolean) — флаг наличия золотой медали
- volunteer_activity (boolean) — флаг наличия волонтерской активности
- gto (boolean) — флаг наличия значка ГТО

В таблице students есть студенты, которых нет в achievements. Это означает, что у таких студентов нет ни одного достижения. Гарантируется, что остальные данные корректны.

**Формат вывода:**  
Запрос должен вернуть таблицу с полями в таком порядке:
- student_id (int) — уникальный идентификатор студента
- sum_score (int) — сумма баллов

Выходные данные отсортированы по убыванию sum_score.

**Код:**
```sql
CREATE TABLE students (
student_id INT NOT NULL,
russian_language INT NOT NULL,
history INT NOT NULL,
social_studies INT NOT NULL
);
CREATE TABLE achievements (
student_id INT NOT NULL,
golden_medal BOOLEAN NOT NULL,
volonteer_activity BOOLEAN NOT NULL,
gto BOOLEAN NOT NULL
);

INSERT INTO students (student_id, russian_language, history, social_studies) VALUES 
(10000, 55, 50, 55),
(10001, 79, 85, 27),
(10002, 22, 38, 14),
(10003, 20, 57, 11),
(10004, 42, 77, 13);

INSERT INTO achievements (student_id, golden_medal, volonteer_activity, gto) VALUES 
(10000, False, True, True),
(10001, True, True, True),
(10002, False, False, True),
(10003, True, True, True),
(10004, True, True, True);
```

---

# Определение победителей акции

**Описание:**  
Отдел SMM с 6 по 15 апреля включительно проводил акцию, победители которой получат купон на скидку 10%. Для победы нужно набрать наибольшее количество лайков на посте с репостом, а также подписаться на профиль компании.

Чтобы не допускать до розыгрыша мошенников, допускаются только те пользователи, которые подписались на аккаунт строго до объявления о начале розыгрыша (дата объявления — 1 апреля 2024 года), а также до сих пор являются подписчиками.

Выберите из списка всех репостов те аккаунты, которые входят в ТОП-10 по количеству набранных баллов: им будут направлены купоны. Учтите, что может быть несколько аккаунтов с этим числом репостов — все аккаунты с этим числом репостов будут объявлены победителями (например, если 11 человек набрали максимум — 1000 репостов — будет 11 победителей).

Используйте оконные функции в решении задачи.

**Формат ввода:**  
Таблица accounts:
- account_id (int) — уникальный идентификатор аккаунта
- reposts_count (int) — кол-во репостов
- is_subscriber (boolean) — является клиент подписчиком или нет
- sub_date (date) — дата подписки пользователя

Если пользователь не является подписчиком канала, то его sub_date будет равен NULL. Гарантируется, что остальные данные корректны и не содержат пропусков.

**Формат вывода:**  
Запрос должен вернуть таблицу с полями:
- account_id (int) — уникальный идентификатор аккаунта

Выходные данные отсортированы по возрастанию account_id, как и входная таблица. Гарантируется, что хотя бы один победитель есть.

**Код:**
```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    reposts_count INT NOT NULL,
    is_subscriber BOOLEAN NOT NULL,
    sub_date DATE
);

INSERT INTO accounts (account_id, reposts_count, is_subscriber, sub_date) VALUES
(1000, 59, TRUE, '2024-04-14'),
(1001, 65, TRUE, '2024-02-06'),
(1003, 61, TRUE, '2024-02-20'),
(1004, 88, FALSE, NULL),
(1007, 96, TRUE, '2024-01-30');
```

---
