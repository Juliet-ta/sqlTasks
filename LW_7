//Вивести значення наступних колонок: назва книги, ціна, назва видавництва, формат.
CREATE PROCEDURE title_price_pub_form()
SELECT main.title, main.price, publishers.publishers, formats.formats FROM main, extra, publishers, formats WHERE main.code = extra.code AND extra.publisher = publishers.publisher_id AND extra.format = formats.format_id;
CALL title_price_pub_form;

//Вивести значення наступних колонок: тема, категорія, назва книги, назва видавництва. Фільтр по темам і категоріям.
CREATE PROCEDURE top_cat_title_pub()
SELECT topics.topics, categories.categories, main.title, publishers.publishers FROM main, extra, publishers, topics, categories WHERE main.code = extra.code AND extra.publisher = publishers.publisher_id AND extra.topic = topics.topic_id AND extra.category = categories.category_id AND topics.topics LIKE 'О%' AND categories.categories LIKE 'І%';
CALL top_cat_title_pub;

//Вивести книги видавництва 'BHV', видані після 2000 р
CREATE PROCEDURE after_year(y int)
SELECT main.title FROM main, extra, publishers WHERE main.code = extra.code AND extra.publisher = publishers.publisher_id AND publishers.publishers LIKE 'BHV%' AND YEAR(extra.date) > y;
CALL after_year(2000);

//Вивести загальну кількість сторінок по кожній назві категорії. Фільтр по спадаючій / зростанню кількості сторінок.
CREATE PROCEDURE cat_pages()
SELECT categories.categories, SUM(extra.pages) FROM main INNER JOIN (extra, categories) ON main.code = extra.code AND extra.category = categories.category_id GROUP BY categories.categories ORDER BY SUM(extra.pages) DESC;
CALL cat_pages;

//Вивести середню вартість книг по темі 'Використання ПК' і категорії 'Linux'.
CREATE PROCEDURE top_cat_price()
SELECT AVG(main.price), topics.topics, categories.categories FROM main INNER JOIN (extra, topics, categories) ON main.code = extra.code AND extra.topic = topics.topic_id AND extra.category = categories.category_id WHERE topics.topics = 'Використання ПК' AND categories.categories = 'Linux' GROUP BY topics.topics, categories.categories;
CALL top_cat_price;

//Вивести всі дані універсального відношення.
CREATE PROCEDURE all_info()
SELECT main.*, is_new.is_new, publishers.publishers, extra.pages, formats.formats, extra.date, extra.tirage, topics.topics, categories.categories FROM main, extra, is_new, publishers, formats, topics, categories WHERE main.code = extra.code AND extra.is_new = is_new.is_new_id AND extra.publisher = publishers.publisher_id AND extra.format = formats.format_id AND extra.topic = topics.topic_id AND extra.category = categories.category_id;
CALL all_info;

//Вивести пари книг, що мають однакову кількість сторінок.
CREATE PROCEDURE 2price()
SELECT main1.title '1_book_title', main2.title '2_book_title' FROM main main1 JOIN (main main2, extra ex1 JOIN extra ex2) ON main1.code = ex1.code AND main2.code = ex2.code AND ex1.pages = ex2.pages AND main1.code != main2.code AND main1.code < main2.code;
CALL 2price;

//Вивести тріади книг, що мають однакову ціну.
CREATE PROCEDURE 3price()
SELECT main1.title '1_book_title', main2.title '2_book_title', main3.title '3_book_title' FROM main main1 JOIN (main main2, main main3) ON main1.code != main2.code AND main1.code != main3.code AND main1.price = main2.price AND main1.price = main3.price AND main1.code < main2.code AND main2.code < main3.code;
CALL 3price;

//Вивести всі книги категорії 'C ++'.
CREATE PROCEDURE cat(c VARCHAR(20))
SELECT main.*, categories.categories FROM main, extra, categories WHERE main.code = extra.code AND extra.category = categories.category_id AND extra.category = (SELECT category_id FROM categories WHERE categories.categories LIKE c);
CALL cat('C&C++');

//Вивести список видавництв, у яких розмір книг перевищує 400 сторінок.
CREATE PROCEDURE pub_price(p int)
SELECT publishers.publishers FROM publishers WHERE (SELECT MIN(pages) FROM extra WHERE extra.publisher = publishers.publisher_id) > p;
CALL pub_price(400);

//Вивести список категорій за якими більше 3-х книг.
CREATE PROCEDURE cat_books(b int)
SELECT categories.categories FROM categories WHERE (SELECT COUNT(*) FROM extra WHERE extra.category = categories.category_id) > b;
CALL cat_books(3);

//Вивести список книг видавництва 'BHV', якщо в списку є хоча б одна книга цього видавництва.
CREATE PROCEDURE pub_like_exists(p VARCHAR(20))
SELECT main.* FROM main, extra WHERE main.code = extra.code AND EXISTS (SELECT * FROM publishers WHERE publishers.publishers LIKE p AND publishers.publisher_id = extra.publisher);
CALL pub_like_exists('%BHV%');

//Вивести список книг видавництва 'BHV', якщо в списку немає жодної книги цього видавництва.
CREATE PROCEDURE pub_like_NOTexists(p VARCHAR(20))
SELECT main.* FROM main, extra WHERE main.code = extra.code AND NOT EXISTS (SELECT * FROM publishers WHERE publishers.publishers = 'BHV С.-Петербург' AND publishers.publisher_id = extra.publisher) AND extra.publisher = (SELECT publisher_id FROM publishers WHERE publishers.publishers = 'BHV С.-Петербург');
CALL pub_like_NOTexists('%BHV%');

//Вивести відсортований загальний список назв тем і категорій.
CREATE PROCEDURE top_cat()
((SELECT * FROM topics) UNION (SELECT * FROM categories)) ORDER BY topics;
CALL top_cat;

//Вивести відсортований в зворотному порядку загальний список перших слів, назв книг і категорій що не повторюються.
CREATE PROCEDURE first_word()
SELECT DISTINCT name FROM ((SELECT REGEXP_SUBSTR(TRIM(title), '^[^\\s]+') AS name FROM main) UNION (SELECT REGEXP_SUBSTR(TRIM(categories), '^[^\\s]+') as name FROM categories)) names ORDER BY name DESC;
CALL first_word;
