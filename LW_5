//Проаналізувати приклад універсального відношення. З'ясувати які його колонки містять надлишкові дані. Виконати нормалізацію універсального відношення, розбивши його на кілька таблиць.  
Надлишкові дані: новинка, видавництво, сторінки, формат, тираж, тема, категорія.
Головна таблиця: номер, код, назва, ціна.

//Скласти SQL-script, що виконує:
//a.	Створення таблиць бази даних. Команди для створення таблиці повинні містити головний ключ, обмеження типу null / not null, default, check, створення зв'язків з умовами посилальної цілісності
//b.	Завантаження даних в таблиці
DROP DATABASE IF EXISTS shop;
CREATE DATABASE IF NOT EXISTS shop;
CREATE TABLE main(
    code SMALLINT(4) PRIMARY KEY,
    title VARCHAR(100) NOT NULL DEFAULT '',
    price FLOAT UNSIGNED NOT NULL
);
CREATE TABLE is_new(
    is_new_id SMALLINT(2) NOT NULL PRIMARY KEY AUTO_INCREMENT,
    is_new CHAR(3) NOT NULL UNIQUE
);
CREATE TABLE publishers(
    publisher_id SMALLINT(2) NOT NULL PRIMARY KEY AUTO_INCREMENT,
    publishers VARCHAR(20) NOT NULL UNIQUE
);
CREATE TABLE formats(
    format_id SMALLINT(2) NOT NULL PRIMARY KEY AUTO_INCREMENT,
    formats VARCHAR(12) NOT NULL UNIQUE
);
CREATE TABLE topics(
    topic_id SMALLINT(3) NOT NULL PRIMARY KEY AUTO_INCREMENT,
    topics VARCHAR(25) NOT NULL UNIQUE
);
CREATE TABLE categories(
    category_id SMALLINT(3) NOT NULL PRIMARY KEY AUTO_INCREMENT,
    categories VARCHAR(25) NOT NULL UNIQUE
);
CREATE TABLE extra(
    code SMALLINT(4) PRIMARY KEY,
    is_new SMALLINT(2) DEFAULT NULL,
    publisher SMALLINT(2) DEFAULT NULL,
    pages SMALLINT UNSIGNED DEFAULT NULL,
    format SMALLINT(2) DEFAULT NULL,
    date DATE NULL,
    tirage INT(11) DEFAULT 5000,
    topic SMALLINT(3) DEFAULT NULL,
    category SMALLINT(3) DEFAULT NULL,
    FOREIGN KEY (code) REFERENCES main (code),
    FOREIGN KEY (is_new) REFERENCES is_new(is_new_id),
    FOREIGN KEY (publisher) REFERENCES publishers(publisher_id),
    FOREIGN KEY (format) REFERENCES formats(format_id),
    FOREIGN KEY (topic) REFERENCES  topics(topic_id),
    FOREIGN KEY (category) REFERENCES categories(category_id)
);
INSERT INTO is_new(`is_new`) VALUES
  ('No'),
  ('Yes');
INSERT INTO publishers(`publishers`) VALUES 
  ('BHV С.-Петербург'),
  ('Вильямс'),
  ('Питер'),
  ('МикроАрт'),
  ('DiaSoft'),
  ('ДМК'),
  ('Триумф'),
  ('Эком'),
  ('Русская редакция');
INSERT INTO formats(`formats`) VALUES
  ('70х100/16'),
  ('84х108/16'),
  ('60х88/16');
INSERT INTO categories(`categories`) VALUES 
  ('Підручники'),
  ('Апаратні засоби ПК'),
  ('Захист і безпека ПК'),
  ('Інші книги'),
  ('Windows 2000'),
  ('Linux'),
  ('Unix'),
  ('Інші операційні системи'),
  ('C&C++');
INSERT INTO topics(`topics`) VALUES 
  ('Використання ПК в цілому'),
  ('Операційні системи'),
  ('Програмування');
INSERT INTO main (`code`, `title`, `price`) VALUES
(5110, 'Аппаратные средства мультимедия. Видеосистема РС', 15.51),
(4985, 'Освой самостоятельно модернизацию и ремонт ПК за 24 часа, 2-е изд.', 18.90),
(5141, 'Структуры данных и алгоритмы.', 37.80),
(5127, 'Автоматизация инженерно-графических работ', 11.58),
(5199, 'Железо IBM 2001.', 30.07),
(3851, 'Защита информации и безопасность компьютерных систем', 26.00),
(3932, 'Как превратить персональный компьютер в измерительный комплекс', 7.65),
(4713, 'Plug- ins. Встраиваемые приложения для музыкальных программ', 11.41),
(5217, 'Windows ME. Новейшие версии программ', 16.57),
(4829, 'Windows 2000 Professional шаг за шагом с СD', 27.25),
(5170, 'Linux Русские версии', 24.43),
(860, 'Операционная система UNIX', 3.50),
(44, 'Ответы на актуальные вопросы по OS/2 Warp', 5.00),
(5176, 'Windows Me. Спутник пользователя', 12.79),
(5462, 'Язык программирования С++. Лекции и упражнения', 29.00),
(4982, 'Язык программирования С. Лекции и упражнения', 29.00),
(4687, 'Эффективное использование C++ .50 рекомендаций по улучшению ваших прог', 17.60);
INSERT INTO extra(`code`,`is_new`, `publisher`, `pages`, `format`, `date`, `topic`, `category`) VALUES
(5110, 1, 1, 400, 1, '2000-07-24', 1, 1),
(4985, 1, 2, 288, 1, '2000-07-07', 1, 1),
(5141, 1, 2, 384, 1, '2000-09-29', 1, 1),
(5127, 2, 3, 256, 1, '2000-06-15', 1, 1),
(5199, 1, 4, 368, 1, '2000-02-12', 1, 2),
(3851, 2, 5, 480, 2, '1999-02-04', 1, 3),
(3932, 1, 6, 144, 3, '1999-06-09', 1, 4),
(4713, 1, 6, 144, 1, '2000-02-22', 1, 4),
(5217, 1, 7, 320, 1, '2000-08-25', 2, 5),
(4829, 1, 8, 320, 1, '2000-04-28', 2, 5),
(5170, 1, 6, 346, 1, '2000-09-29', 2, 6),
(860, 1, 1, 395, 2, '1997-05-05', 2, 7),
(44, 1, 5, 352, 3, '1996-03-20', 2, 8),
(5176, 1, 9, 306, NULL, '2000-10-10', 2, 8),
(5462, 1, 5, 656, 2, '2000-12-12', 3, 9),
(4982, 1, 5, 432, 2, '2000-07-12', 3, 9),
(4687, 1, 6, 240, 1, '2000-02-03', 3, 9);
