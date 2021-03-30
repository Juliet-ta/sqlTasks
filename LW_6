//Вивести значення наступних колонок: назва книги, ціна, назва видавництва. Використовувати внутрішнє з'єднання, застосовуючи where.
SELECT main.title, main.price, publishers.publishers FROM main, extra, publishers WHERE main.code = extra.code AND extra.publisher = publishers.publisher_id;

//Вивести значення наступних колонок: назва книги, назва категорії. Використовувати внутрішнє з'єднання, застосовуючи inner join.
SELECT main.title, categories.categories FROM main INNER JOIN (extra, categories) ON extra.category = categories.category_id AND main.code = extra.code;

//Вивести значення наступних колонок: назва книги, ціна, назва видавництва, формат.
SELECT main.title, main.price, publishers.publishers, formats.formats FROM main, extra, publishers, formats WHERE main.code = extra.code AND extra.publisher = publishers.publisher_id AND extra.format = formats.format_id;

//Вивести значення наступних колонок: тема, категорія, назва книги, назва видавництва. Фільтр по темам і категоріям.
SELECT topics.topics, categories.categories, main.title, publishers.publishers FROM main, extra, publishers, topics, categories WHERE main.code = extra.code AND extra.publisher = publishers.publisher_id AND extra.topic = topics.topic_id AND extra.category = categories.category_id AND topics.topics LIKE 'О%' AND categories.categories LIKE 'І%';

//Вивести книги видавництва 'BHV', видані після 2000 р
SELECT main.title FROM main, extra, publishers WHERE main.code = extra.code AND extra.publisher = publishers.publisher_id AND publishers.publishers LIKE 'BHV%' AND YEAR(extra.date) > 2000;

//Вивести загальну кількість сторінок по кожній назві категорії. Фільтр по спадаючій кількості сторінок.
SELECT categories.categories, SUM(extra.pages) FROM main INNER JOIN (extra, categories) ON main.code = extra.code AND extra.category = categories.category_id GROUP BY categories.categories ORDER BY SUM(extra.pages) DESC

//Вивести середню вартість книг по темі 'Використання ПК' і категорії 'Linux'.
SELECT AVG(main.price), topics.topics, categories.categories FROM main INNER JOIN (extra, topics, categories) ON main.code = extra.code AND extra.topic = topics.topic_id AND extra.category = categories.category_id WHERE topics.topics = 'Використання ПК' AND categories.categories = 'Linux' GROUP BY topics.topics, categories.categories;

//Вивести всі дані універсального відношення. Використовувати внутрішнє з'єднання, застосовуючи where.
SELECT main.*, is_new.is_new, publishers.publishers, extra.pages, formats.formats, extra.date, extra.tirage, topics.topics, categories.categories FROM main, extra, is_new, publishers, formats, topics, categories WHERE main.code = extra.code AND extra.is_new = is_new.is_new_id AND extra.publisher = publishers.publisher_id AND extra.format = formats.format_id AND extra.topic = topics.topic_id AND extra.category = categories.category_id;

//Вивести всі дані універсального відношення. Використовувати внутрішнє з'єднання, застосовуючи inner join.
SELECT main.*, is_new.is_new, publishers.publishers, extra.pages, formats.formats, extra.date, extra.tirage, topics.topics, categories.categories FROM main INNER JOIN (extra, is_new, publishers, formats, topics, categories) ON main.code = extra.code AND extra.is_new = is_new.is_new_id AND extra.publisher = publishers.publisher_id AND extra.format = formats.format_id AND extra.topic = topics.topic_id AND extra.category = categories.category_id

//Вивести всі дані універсального відношення. Використовувати зовнішнє з'єднання, застосовуючи left join / rigth join.
SELECT main.*, is_new.is_new, publishers.publishers, extra.pages, formats.formats, extra.date, extra.tirage, topics.topics, categories.categories FROM main LEFT JOIN (extra, is_new, publishers, formats, topics, categories) ON main.code = extra.code AND extra.is_new = is_new.is_new_id AND extra.publisher = publishers.publisher_id AND extra.format = formats.format_id AND extra.topic = topics.topic_id AND extra.category = categories.category_id;
SELECT main.*, is_new.is_new, publishers.publishers, extra.pages, formats.formats, extra.date, extra.tirage, topics.topics, categories.categories FROM  (extra, is_new, publishers, formats, topics, categories) RIGHT JOIN main ON main.code = extra.code AND extra.is_new = is_new.is_new_id AND extra.publisher = publishers.publisher_id AND extra.format = formats.format_id AND extra.topic = topics.topic_id AND extra.category = categories.category_id;

//Вивести пари книг, що мають однакову кількість сторінок. Використовувати само об’єднання і аліаси (self join).
SELECT main1.title '1_book_title', main2.title '2_book_title' FROM main main1 JOIN (main main2, extra ex1 JOIN extra ex2) ON main1.code = ex1.code AND main2.code = ex2.code AND ex1.pages = ex2.pages AND main1.code != main2.code AND main1.code < main2.code;

//Вивести тріади книг, що мають однакову ціну. Використовувати самооб'єднання і аліаси (self join).
SELECT main1.title '1_book_title', main2.title '2_book_title', main3.title '3_book_title' FROM main main1 JOIN (main main2, main main3) ON main1.code != main2.code AND main1.code != main3.code AND main1.price = main2.price AND main1.price = main3.price AND main1.code < main2.code AND main2.code < main3.code;

//Вивести всі книги категорії 'C ++'. Використовувати підзапити (subquery).
SELECT main.*, categories.categories FROM main, extra, categories WHERE main.code = extra.code AND extra.category = categories.category_id AND extra.category = (SELECT category_id FROM categories WHERE categories.categories = 'C&C++');

//Вивести книги видавництва 'BHV', видані після 2000 р Використовувати підзапити (subquery).
SELECT main.*, publishers.publishers, extra.date FROM main, extra, publishers WHERE main.code = extra.code AND extra.publisher = publishers.publisher_id AND extra.publisher = (SELECT publisher_id from publishers WHERE publishers.publishers = 'BHV С.-Петербург') AND YEAR(extra.date) > 2000;

//Вивести список видавництв, у яких розмір книг перевищує 400 сторінок. Використовувати пов'язані підзапити (correlated subquery).
SELECT publishers.publishers FROM publishers WHERE (SELECT MIN(pages) FROM extra WHERE extra.publisher = publishers.publisher_id) > 400;

//Вивести список категорій в яких більше 3-х книг. Використовувати пов'язані підзапити (correlated subquery).
SELECT categories.categories FROM categories WHERE (SELECT COUNT(*) FROM extra WHERE extra.category = categories.category_id) > 3;

//Вивести список книг видавництва 'BHV', якщо в списку є хоча б одна книга цього видавництва. Використовувати exists.
SELECT main.* FROM main, extra WHERE main.code = extra.code AND EXISTS (SELECT * FROM publishers WHERE publishers.publishers = 'BHV С.-Петербург' AND publishers.publisher_id = extra.publisher);

//Вивести список книг видавництва 'BHV', якщо в списку немає жодної книги цього видавництва. Використовувати not exists.
SELECT main.* FROM main, extra WHERE main.code = extra.code AND NOT EXISTS (SELECT * FROM publishers WHERE publishers.publishers = 'BHV С.-Петербург' AND publishers.publisher_id = extra.publisher) AND extra.publisher = (SELECT publisher_id FROM publishers WHERE publishers.publishers = 'BHV С.-Петербург');

//Вивести відсортований загальний список назв тем і категорій. Використовувати union.
((SELECT * FROM topics) UNION (SELECT * FROM categories)) ORDER BY topics;

//Вивести відсортований в зворотному порядку загальний список перших слів, назв книг і категорій що не повторюються. Використовувати union.
SELECT DISTINCT name FROM ((SELECT REGEXP_SUBSTR(TRIM(title), '^[^\\s]+') AS name FROM main) UNION (SELECT REGEXP_SUBSTR(TRIM(categories), '^[^\\s]+') as name FROM categories)) names ORDER BY name DESC;
