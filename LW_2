// Вивести значення наступних колонок: номер, код, новинка, назва, ціна, сторінки
SELECT n, cod, new, title, price, page FROM `books`

// Вивести значення всіх колонок
SELECT * FROM `books`

// Вивести значення колонок в наступному порядку: код, назва, новинка, сторінки, ціна, номер
SELECT cod, title, new, page, price, n FROM `books`

// Вивести значення всіх колонок 10 перших рядків
SELECT * FROM `books` LIMIT 10

// Вивести значення колонки код без повторення однакових кодів
SELECT DISTINCT cod FROM library.books;

// Вивести всі книги новинки
SELECT * FROM `books` WHERE `new` = 'Yes';

// Вивести всі книги новинки з ціною від 20 до 30
SELECT * FROM `books` WHERE `new` = 'Yes' AND `price` BETWEEN 20 AND 30

// Вивести всі книги новинки з ціною менше 20 і більше 30
SELECT * FROM `books` WHERE `new` = 'Yes' AND `price` NOT BETWEEN 20 AND 30

// Вивести всі книги з кількістю сторінок від 300 до 400 і з ціною більше 20 і менше 30
SELECT * FROM `books` WHERE `page` BETWEEN 300 AND 400 AND `price` BETWEEN 21 AND 29

// Вивести всі книги видані взимку 2000 року
SELECT * FROM `books` WHERE (`dat` BETWEEN '2000-01-01' AND '2000-02-29') OR (`dat` BETWEEN '2000-12-01' AND '2000-12-31')

// Вивести книги зі значеннями кодів 5110, 5141, 4985, 4241
SELECT * FROM `books` WHERE `cod` = 5110 OR `cod` = 5141 OR `cod` = 4985 OR `cod` = 4241

// Вивести книги видані в 1999, 2001, 2003, 2005 р
SELECT * FROM `books` WHERE `dat` LIKE '1999-%-%' OR `dat` LIKE '2001-%-%' OR `dat` LIKE '2003-%-%' OR `dat` LIKE '2005-%-%'

// Вивести книги назви яких починаються на літери А-К
SELECT * FROM `books` WHERE `title` BETWEEN 'А' AND 'Л'

// Вивести книги назви яких починаються на літери "АПП", видані в 2000 році з ціною до 20
SELECT * FROM `books` WHERE `title` LIKE 'Апп%' AND `dat` LIKE '2000-%-%' AND `price`<= 20

// Вивести книги назви яких починаються на літери "АПП", закінчуються на "е", видані в першій половині 2000 року
SELECT * FROM `books` WHERE `title` LIKE 'Апп%е' AND `dat` BETWEEN '2000-01-01' AND '2000-06-30'

// Вивести книги, в назвах яких є слово Microsoft, але немає слова Windows
SELECT * FROM `books` WHERE `title` LIKE '%Microsoft%' AND `title` NOT LIKE '%Windows%'

// Вивести книги, в назвах яких присутня як мінімум одна цифра.
SELECT * FROM `books` WHERE `title` RLIKE '[0-9]'

// Вивести книги, в назвах яких присутні не менше трьох цифр.
SELECT * FROM `books` WHERE `title` RLIKE '.*[0-9].*[0-9].*[0-9].*'

// Вивести книги, в назвах яких присутній рівно п'ять цифр.
SELECT * FROM `books` WHERE `title` NOT RLIKE '.*[0-9].*[0-9].*[0-9].*[0-9].*[0-9].*[0-9].*' AND `title` RLIKE '.*[0-9].*[0-9].*[0-9].*[0-9].*[0-9].*'
