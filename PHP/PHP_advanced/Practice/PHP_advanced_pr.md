# Победители лотереи

**Описание:**  
Вы работаете над программой для проведения лотерей. Чтобы победить в лотерее, участник должен угадать загаданную последовательность цифр. Те, кто угадал сами цифры, но расположил их в неправильной последовательности, тоже получают призы. При этом размер приза зависит от близости последовательности к выигрышному значению.

Задача вашей программы — найти следующее меньшее положительное число с теми же цифрами, что и исходное. Если такого числа не существует или следующее меньшее число с такими же цифрами начинается с нуля, верните -1. Это значит, что других победителей в лотерее не будет.

**Формат ввода:**  
Одна строка из цифр.

**Формат вывода:**  
Одна строка, в которой есть следующее меньшее число. Если число не существует, верните -1.

**Код:**
```php
<?php
function next_smaller(string $n): string
{
	// ваш код
}


$inputString = trim(fgets(STDIN));
echo next_smaller($inputString) . PHP_EOL;
?>
```

**Пример 1:**  
Входные данные:  
531

Выходные данные:  
513

**Пример 2:**  
Входные данные:  
101

Выходные данные:  
-1

---

# Отчёты по продажам

**Описание:**  
Вы дорабатываете модуль для платформы CRM, который помогает менеджерам по продажам готовить автоматизированные отчёты. Данные о продажах поступают в формате «Дата:Продукт:Количество;Дата:Продукт:Количество;...».

Напишите программу, которая принимает информацию о продажах и возвращает консолидированный отчёт о продажах по месяцам в соответствии с требуемым форматом. Отчёт отражает тип продукта и его количество по месяцам, в порядке от января до декабря. Порядок задан в прекоде.

**Формат ввода:**  
Одна строка с данными в формате «Дата:Продукт:Количество;Дата:Продукт:Количество;...». Дата в формате YYYY-MM-DD, через двоеточие указано название продукта (в названии только символы русского языка) и ещё через одно двоеточие — целое число, указывающее на количество проданных товаров. Данные по каждому продукту разделены точкой с запятой.

**Формат вывода:**  
Набор строк, в котором выводится информация о продажах товаров. Сначала даётся название месяца с двоеточием, а после — маркированным списком с дефисом перечисляются товары и количество продаж через двоеточие. Месяцы должны идти по порядку, а продукты — по алфавиту (в названии продуктов только символы русского языка).

**Код:**
```php
<?php
class Item
{
	public string $date;
	public string $product;
	public int $quantity;


	public function __construct(string $date, string $product, int $quantity)
	{
    	$this->date 	= $date;
    	$this->product  = $product;
    	$this->quantity = $quantity;
	}


	public function getMonth(): string
	{
    	$months = [
        	"01" => "Январь",  "02" => "Февраль", "03" => "Март",
        	"04" => "Апрель",  "05" => "Май", 	"06" => "Июнь",
        	"07" => "Июль",	"08" => "Август",  "09" => "Сентябрь",
        	"10" => "Октябрь", "11" => "Ноябрь",  "12" => "Декабрь"
    	];
    	$m = explode('-', $this->date)[1] ?? '';
    	return $months[$m] ?? 'Неизвестный месяц';
	}
}


function generate_monthly_report(string $data): array
{
	// ваш код
}


$inputData 	= trim(fgets(STDIN));
$monthlyReport = generate_monthly_report($inputData);
foreach ($monthlyReport as $line) {
	echo $line . PHP_EOL;
}
?>
```

**Пример 1:**  
Входные данные:  
2023-01-15:Книга:10;2023-01-20:Флешка:5;2023-02-05:Наушники:8

Выходные данные:  
Январь:  
- Книга: 10  
- Флешка: 5  
Февраль:  
- Наушники: 8

---

# Предмет без отстающих

**Описание:**  
Вы работаете над модулем «Электронная зачётка» в системе для администрирования учебного процесса регионального вуза. Каждый студент может быть записан на несколько курсов, по каждому курсу у него есть итоговый балл.

Необходимо написать программу для учебного офиса, которая будет выбирать из базы те курсы, по которым нет ни одной академической задолженности. Курс без единой академической задолженности — это такой курс, где все студенты (у кого этот курс указан) набрали строго выше проходного балла по этому предмету. Проходной балл определяется для каждого курса отдельно.

**Формат ввода:**  
Первая строка содержит информацию о студентах, курсах и их оценках в формате: «имя_студента,курс,оценка;имя_студента,курс,оценка;...». В строке есть информация хотя бы об одном студенте. Вторая строка содержит проходные баллы по предметам в формате: «курс,проходной_балл;курс,проходной_балл;...». Гарантируется, что на все указанные в первой строке курсы есть проходной балл.

Все баллы являются целыми положительными числами, а все имена студентов уникальны.

**Формат вывода:**  
Названия курсов, где нет ни одной академической задолженности, каждое название с новой строки. Если таких курсов нет, выводится слово «Пусто» (без кавычек).

**Код:**
```php
<?php
class Student
{
	public string $name;
	public array $courses = [];


	public function __construct(string $name)
	{
    	$this->name = $name;
	}


	// ваш код
}


class CourseManager
{
	public array $students = [];


	// ваш код
}


$studentsInfo = trim(fgets(STDIN));
$scoresInfo   = trim(fgets(STDIN));
// ваш код
?>
```

**Пример 1:**  
Входные данные:  
Анна,Математика,85;Анна,Химия,90;Борис,Математика,75;Борис,История,80;Евгений,Математика,95;Евгений,История,85  
Математика,80;Химия,60;История,80

Выходные данные:  
Химия

**Пример 2:**  
Входные данные:  
Анна,Психология,8;Анна,Литература,9;Борис,Обществознание,8  
Психология,8;Литература,9;Обществознание,8

Выходные данные:  
Пусто

---

# Шифрование методом Цезаря

**Описание:**  
Вы разрабатываете программу для шифрования текстовых сообщений методом Цезаря. Этот метод подразумевает сдвиг каждой буквы текста на фиксированное количество позиций в алфавите. Например, при сдвиге на 3 позиции буква А становится Г, а Я становится В.

Ваша задача — написать функцию, которая принимает на вход строку и целое число (сдвиг), и возвращает зашифрованную версию этой строки по методу Цезаря. Алфавит уже задан в прекоде.

**Формат ввода:**  
Входные данные состоят из двух строк: первая строка содержит произвольный текст для шифрования (только строчные буквы русского алфавита и пробелы), вторая строка содержит целое число — величину сдвига.

**Формат вывода:**  
Выходные данные должны состоять из одной строки, содержащей зашифрованный текст. Пробел кодировать не нужно.

**Код:**
```php
<?php
function encode_string(string $string, int $shift): string
{
	$alphabet = 'абвгдеёжзийклмнопрстуфхцчшщъыьэюя';
	// ваш код
}


$inputString = trim(fgets(STDIN));
$inputNum	= (int)trim(fgets(STDIN));
echo encode_string($inputString, $inputNum) . PHP_EOL;
?>
```

**Пример 1:**  
Входные данные:  
абвгде  
1

Выходные данные:  
бгдеёж

**Пример 2:**  
Входные данные:  
это яблоко красное  
7

Выходные данные:  
эчх ёйтхсл сччшхл

---

# Система управления доступом

**Описание:**  
Вы работаете над внутрикорпоративной системой доступа пользователей. Реализуйте класс UserManager, который будет управлять доступом пользователей к системе.

У класса должны быть методы для добавления нового пользователя, удаления пользователя, повышения и понижения уровня доступа пользователя, а также для получения списка всех пользователей. Уровни доступа пользователей — это целые числа (0 ≤ x).

Класс UserManager должен поддерживать следующие методы, которые должны быть цепочками (кроме get_users):
- add_user() — добавляет нового пользователя с указанным уровнем доступа по умолчанию, равным 1;
- remove_user() — удаляет пользователя;
- promote() — увеличивает уровень доступа пользователя на 1;
- demote() — уменьшает уровень доступа на 1, если уровень доступа больше 0. Иначе ничего не происходит.
- get_users() — вернет список всех пользователей с их текущим уровнем доступа.

**Формат ввода:**  
Несколько строк, состоящих из команд add_user, remove_user, promote, demote, get_users. Входные данные гарантированно завершаются командой get_users.

**Формат вывода:**  
Несколько строк, в которой может быть один из вариантов:
- Пользователи с уровнем доступа если введена команда get_users;
- «не найдено», если пользователей в списке не осталось.

**Код:**
```php
<?php
class UserManager
{
	private array $users = []; // имя => уровень доступа


	public function addUser(string $name, int $level = 1): self
	{
    	// ваш код
	}


	public function removeUser(string $name): self
	{
    	// ваш код
	}


	public function promote(string $name): self
	{
    	// ваш код
	}


	public function demote(string $name): self
	{
    	// ваш код
	}


	public function getUsers(): array
	{
    	// ваш код
	}
}


$userManager = new UserManager();
$commands	= [];
while (($line = fgets(STDIN)) !== false) {
	$line = trim($line);
	if ($line === '') {
    	break;
	}
	$commands[] = $line;
}


// ваш код
?>
```

**Пример 1:**  
Входные данные:  
add_user Анна 1  
add_user Борис 2  
get_users

Выходные данные:  
Анна 1  
Борис 2

**Пример 2:**  
Входные данные:  
add_user Анна 1  
add_user Борис 2  
remove_user Анна  
get_users

Выходные данные:  
Борис 2

**Пример 3:**  
Входные данные:  
add_user Bob 3  
add_user Charlie 2  
remove_user Charlie  
get_users

Выходные данные:  
Bob 3

**Пример 4:**  
Входные данные:  
add_user Bob 3  
add_user Charlie 2  
remove_user Charlie  
remove_user Bob  
get_users

Выходные данные:  
не найдено

---

# Отчёты по продажам

**Описание:**  
Вы дорабатываете модуль для платформы CRM, который помогает менеджерам по продажам готовить автоматизированные отчёты. Данные о продажах поступают в формате «Дата:Продукт:Количество;Дата:Продукт:Количество;...».

Напишите программу, которая принимает информацию о продажах и возвращает консолидированный отчёт о продажах по месяцам в соответствии с требуемым форматом. Отчёт отражает тип продукта и его количество по месяцам, в порядке от января до декабря. Порядок задан в прекоде.

**Формат ввода:**  
Одна строка с данными в формате «Дата:Продукт:Количество;Дата:Продукт:Количество;...». Дата в формате YYYY-MM-DD, через двоеточие указано название продукта (в названии только символы русского языка) и ещё через одно двоеточие — целое число, указывающее на количество проданных товаров. Данные по каждому продукту разделены точкой с запятой.

**Формат вывода:**  
Набор строк, в котором выводится информация о продажах товаров. Сначала даётся название месяца с двоеточием, а после — маркированным списком с дефисом перечисляются товары и количество продаж через двоеточие. Месяцы должны идти по порядку, а продукты — по алфавиту (в названии продуктов только символы русского языка).

**Код:**
```php
<?php
class Item
{
	public string $date;
	public string $product;
	public int $quantity;


	public function __construct(string $date, string $product, int $quantity)
	{
    	$this->date 	= $date;
    	$this->product  = $product;
    	$this->quantity = $quantity;
	}


	public function getMonth(): string
	{
    	$months = [
        	"01" => "Январь",  "02" => "Февраль", "03" => "Март",
        	"04" => "Апрель",  "05" => "Май", 	"06" => "Июнь",
        	"07" => "Июль",	"08" => "Август",  "09" => "Сентябрь",
        	"10" => "Октябрь", "11" => "Ноябрь",  "12" => "Декабрь"
    	];
    	$m = explode('-', $this->date)[1] ?? '';
    	return $months[$m] ?? 'Неизвестный месяц';
	}
}


function generate_monthly_report(string $data): array
{
	// ваш код
}


$inputData 	= trim(fgets(STDIN));
$monthlyReport = generate_monthly_report($inputData);
foreach ($monthlyReport as $line) {
	echo $line . PHP_EOL;
}
?>
```

**Пример 1:**  
Входные данные:  
2023-01-15:Книга:10;2023-01-20:Флешка:5;2023-02-05:Наушники:8

Выходные данные:  
Январь:  
- Книга: 10  
- Флешка: 5  
Февраль:  
- Наушники: 8

---
