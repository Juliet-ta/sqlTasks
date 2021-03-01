// Вивести книги у яких не введена ціна або ціна дорівнює 0
SELECT * FROM `books` WHERE `price` = 0 OR `price` = NULL

// Вивести книги у яких введена ціна, але не введений тираж
SELECT * FROM `books` WHERE `price` <> NULL AND `tir` = NULL

// Вивести книги, про дату видання яких нічого не відомо.
SELECT * FROM `books` WHERE `dat` = NULL

// Вивести книги, з дня видання яких пройшло не більше року.
SELECT * FROM `books` WHERE YEAR(CURRENT_DATE) - YEAR(`dat`) <= 1

// Вивести список книг-новинок, відсортованих за зростанням ціни
SELECT * FROM `books` WHERE `new` = 'Yes' ORDER BY `price`

// Вивести список книг з числом сторінок від 300 до 400, відсортованих в зворотному алфавітному порядку назв
SELECT * FROM `books` WHERE `page` BETWEEN 300 AND 400 ORDER BY `title` DESC

// Вивести список книг з ціною від 20 до 40, відсортованих за спаданням дати
SELECT * FROM `books` WHERE `price` BETWEEN 20 AND 40 ORDER BY `dat` DESC

// Вивести список книг, відсортованих в алфавітному порядку назв і ціною по спадаючій
SELECT * FROM `books` ORDER BY `title` ASC, `price` DESC

// Вивести книги, у яких ціна однієї сторінки < 10 копійок.
SELECT * FROM `books` WHERE `price`* 27.93 / `page` < 0.1

// Вивести значення наступних колонок: число символів в назві, перші 20 символів назви великими літерами
SELECT LENGTH(`title`), LEFT(UPPER(`title`), 20) FROM `books`

// Вивести значення наступних колонок: перші 10 і останні 10 символів назви прописними буквами, розділені '...'
SELECT LOWER(CONCAT(LEFT(title, 10), '...', RIGHT(title, 10))) FROM `books`;

// Вивести значення наступних колонок: назва, дата, день, місяць, рік
SELECT title `Назва`, dat `Дата`, DAYNAME(dat) `День`, MONTHNAME(dat) `Місяць`, YEAR(dat) `Рік` FROM `books`;

// Вивести значення наступних колонок: назва, дата, дата в форматі 'dd/mm/yyyy'
SELECT title `Назва`, dat `Дата`, DATE_FORMAT(dat, '%d/%m/%Y') 'dd/mm/yyyy' FROM `books`;

// Вивести значення наступних колонок: код, ціна, ціна в грн., ціна в євро, ціна в руб.
SELECT cod `Код`, price `Ціна`, ROUND(price*27.90,2) `Ціна в грн`, ROUND(price*0.82,2) `Ціна в євро`, ROUND(price*74.16,2) `Ціна в руб` FROM `books`;

// Вивести значення наступних колонок: код, ціна, ціна в грн. без копійок, ціна без копійок округлена
SELECT cod `Код`, price `Ціна`, TRUNCATE(price*27.90, 0) `Ціна в грн без копійок`, ROUND(price*27.90, 0) `Ціна в грн округлена` FROM `books`;

// Додати інформацію про нову книгу (всі колонки)
INSERT INTO books (`n`, `cod`, `new`, `title`, `price`, `pub`, `page`, `form`, `dat`, `tir`, `them`, `kat`)
VALUE (239, 1632, 'Yes', 'Этюд в багровых тонах', 6.8, 'Азбука-классика', 448, '130x200/16', '2017-04-04', 500, 'Шерлок Холмс', 'Детектив');
SELECT * FROM `books` WHERE 1

// Додати інформацію про нову книгу (колонки обов'язкові для введення)
INSERT INTO books (`n`, `cod`, `title`, `price`, `pub`, `page`, `dat`, `them`, `kat`)
VALUE (240, 1633, 'Этюд в багровых тонах', 6.8, 'Азбука-классика', 448, '2017-04-04', 'Шерлок Холмс', 'Детектив');
SELECT * FROM `books` WHERE 1

// Видалити книги, видані до 1990 року
DELETE FROM `books` WHERE YEAR(dat) < 1990;

// Проставити поточну дату для тих книг, у яких дата видання відсутня
UPDATE `books` SET `dat` = CURRENT_DATE WHERE dat = NULL;

// Установити ознаку новинка для книг виданих після 2005 року
UPDATE `books` SET `new` = 'Yes' WHERE YEAR(dat) >= 2005;
