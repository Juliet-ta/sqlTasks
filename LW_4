//Вивести статистику: загальна кількість всіх книг, їх вартість, їх середню вартість, мінімальну і максимальну ціну
SELECT COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books`

//Вивести загальну кількість всіх книг без урахування книг з непроставленою ціною
SELECT COUNT(`n`) 'Загальна к-ть книг з ціною' FROM `books` WHERE `price` <> 0

//Вивести статистику (див. 1) для книг новинка / не новинка
SELECT `new` 'Новинка', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` GROUP BY `new`

//Вивести статистику (див. 1) для книг за кожним роком видання
SELECT YEAR(`dat`) 'Рік', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` GROUP BY YEAR(`dat`)

//Змінити п.4, виключивши з статистики книги з ціною від 10 до 20
SELECT YEAR(`dat`) 'Рік', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` WHERE `price` NOT BETWEEN 10 AND 20 GROUP BY YEAR(`dat`)

//Змінити п.4. Відсортувати статистику по спадаючій кількості.
SELECT YEAR(`dat`) 'Рік', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` GROUP BY YEAR(`dat`) ORDER BY COUNT(`n`) DESC

//Вивести загальну кількість кодів книг і кодів книг що не повторюються
SELECT COUNT(`n`) 'Загальна кількість кодів', COUNT(DISTINCT(`n`)) 'Загальна кількість унікальних кодів' FROM `books`

//Вивести статистику: загальна кількість і вартість книг по першій букві її назви
SELECT LEFT(`title`,1) ' ', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість' FROM `books` GROUP BY LEFT(`title`,1)

//Змінити п. 8, виключивши з статистики назви що починаються з англ. букви або з цифри.
SELECT LEFT(`title`,1) ' ', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість' FROM `books` WHERE LEFT(`title`,1) NOT BETWEEN 'A' AND 'Z' GROUP BY LEFT(`title`,1)

//Змінити п. 9 так щоб до складу статистики потрапили дані з роками більшими за 2000.
SELECT LEFT(`title`,1) ' ', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість' FROM `books` WHERE LEFT(`title`,1) NOT BETWEEN 'A' AND 'Z' AND YEAR(`dat`) > 2000 GROUP BY LEFT(`title`,1)

//Змінити п. 10. Відсортувати статистику по спадаючій перших букв назви.
SELECT LEFT(`title`,1) ' ', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість' FROM `books` WHERE LEFT(`title`,1) NOT BETWEEN 'A' AND 'Z' AND YEAR(`dat`) > 2000 GROUP BY LEFT(`title`,1) ORDER BY LEFT(`title`,1) DESC

//Вивести статистику (див. 1) по кожному місяцю кожного року.
SELECT CONCAT(MONTHNAME(`dat`), ' ', YEAR(`dat`)) 'Місяць рік', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` GROUP BY CONCAT(MONTHNAME(`dat`), ' ', YEAR(`dat`))

//Змінити п. 12 так щоб до складу статистики не увійшли дані з незаповненими датами.
SELECT CONCAT(MONTHNAME(`dat`), ' ', YEAR(`dat`)) 'Місяць рік', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` WHERE `dat` <> NULL GROUP BY CONCAT(MONTHNAME(`dat`), ' ', YEAR(`dat`))

//Змінити п. 12. Фільтр по спадаючій року і зростанню місяця.
SELECT CONCAT(MONTHNAME(`dat`), ' ', YEAR(`dat`)) 'Місяць рік', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` GROUP BY CONCAT(MONTHNAME(`dat`), ' ', YEAR(`dat`)) ORDER BY YEAR(`dat`) DESC, MONTH(`dat`) ASC

//Вивести статистику для книг новинка / не новинка: загальна ціна, загальна ціна в грн. / Євро / руб. Колонкам запиту дати назви за змістом.
SELECT `new` 'Новинка', ROUND(SUM(`price`),2) 'Загальна ціна', ROUND(SUM(`price`)*27.93,2) 'грн', ROUND(SUM(`price`)*0.83,2) 'євро', ROUND(SUM(`price`)*73.9,2) 'руб' FROM `books` GROUP BY `new`

//Змінити п. 15 так щоб виводилася округлена до цілого числа (дол. / Грн. / Євро / руб.) Ціна.
SELECT `new` 'Новинка', ROUND(SUM(`price`),0) 'Загальна ціна', ROUND(SUM(`price`)*27.93,0) 'грн', ROUND(SUM(`price`)*0.83,0) 'євро', ROUND(SUM(`price`)*73.9,0) 'руб' FROM `books` GROUP BY `new`

//Вивести статистику (див. 1) по видавництвах.
SELECT `pub` 'Видавництво', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` GROUP BY `pub`

//Вивести статистику (див. 1) за темами і видавництвами. Фільтр по видавництвам.
SELECT CONCAT(`pub`, ', ', `them`) 'Видавництво', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` WHERE `pub` IN ('BHV С.-Петербург', 'Вильямс') GROUP BY CONCAT(`pub`, ', ', `them`)

//Вивести статистику (див. 1) за категоріями, темами і видавництвами. Фільтр по видавництвам, темах, категоріям.
SELECT CONCAT(`kat`, ', ', `them`, ', ', `pub`) 'Видавництво', COUNT(`n`) 'Загальна к-ть книг', ROUND(SUM(`price`),2) 'Загальна вартість', ROUND(AVG(`price`),2) 'Середня вартість', MIN(`price`) 'Мінімальна ціна', MAX(`price`) 'Максимальна ціна' FROM `books` WHERE `pub` IN ('BHV С.-Петербург', 'Вильямс') GROUP BY CONCAT(`kat`, ', ', `them`, ', ', `pub`)

//Вивести список видавництв, у яких округлена до цілого ціна однієї сторінки більше 10 копійок. 
SELECT * FROM `books` WHERE ROUND(`price`, 0) / `page` * 27.77 >= 0.1
