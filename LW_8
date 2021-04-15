//Реалізувати набір тригерів, що реалізують такі ділові правила:
//Кількість тем може бути в діапазоні від 5 до 10.
DROP TRIGGER IF EXISTS topics_5_10_insert;
DROP TRIGGER IF EXISTS topics_5_10_drop
DELIMITER $$
CREATE TRIGGER topics_5_10_insert BEFORE INSERT ON `topics`
FOR EACH ROW
IF (SELECT COUNT(*) FROM `topics`) > 10
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Кількість тем більша 10';
END IF;
$$
DELIMITER ;
DELIMITER $$
CREATE TRIGGER topics_5_10_drop BEFORE DELETE ON `topics`
FOR EACH ROW
IF (SELECT COUNT(*) FROM `topics`) < 5
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT ='Кількість тем менша 5 ';
END IF;
$$
DELIMITER ;

//Новинкою може бути тільки книга видана в поточному році.
DROP TRIGGER IF EXISTS new_insert;
DROP TRIGGER IF EXISTS new_update;
DELIMITER $$
CREATE TRIGGER new_insert BEFORE INSERT ON `extra`
FOR EACH ROW
IF YEAR(NOW()) = YEAR(NEW.date) AND NEW.is_new = 1
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Книга має бути новинкою';
ELSEIF NOT YEAR(NOW()) = YEAR(NEW.date) AND NEW.is_new = 2
THEN
 SET @err2 = 'Книга НЕ має бути новинкою';
END IF;
$$
DELIMITER ;
DELIMITER $$
CREATE TRIGGER new_update BEFORE UPDATE ON `extra`
FOR EACH ROW
IF ((YEAR(NOW()) = YEAR(NEW.date) AND NEW.is_new = 1) OR (YEAR(NOW()) = YEAR(OLD.date) AND NEW.is_new = 1) OR (YEAR(NOW()) = YEAR(NEW.date) AND OLD.is_new = 1))
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Книга має бути новинкою';
ELSEIF ((NOT YEAR(NOW()) = YEAR(NEW.date) AND NEW.is_new = 2) OR (NOT YEAR(NOW()) = YEAR(OLD.date) AND NEW.is_new = 2) OR (NOT YEAR(NOW()) = YEAR(NEW.date) AND OLD.is_new = 2))
THEN
 SET @err2 = 'Книга НЕ має бути новинкою';
END IF;
$$
DELIMITER ;

//Книга з кількістю сторінок до 100 не може коштувати більше 10 $, до 200 - 20 $, до 300 - 30 $.
DROP TRIGGER IF EXISTS pages_price_insert;
DROP TRIGGER IF EXISTS pages_price_update;
DELIMITER $$
CREATE TRIGGER pages_price_insert BEFORE INSERT ON `extra`
FOR EACH ROW
IF NEW.pages < 100 AND main.price >= 10
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Ціна має бути не більше 10$';
ELSEIF NEW.pages < 200 AND main.price >= 20
THEN
 SET @err2 = 'Ціна має бути не більше 20$';
ELSEIF NEW.pages < 300 AND main.price >= 30
THEN
 SET @err3 = 'Ціна має бути не більше 30$';
END IF;
$$
DELIMITER ;
DELIMITER $$
CREATE TRIGGER pages_price_update BEFORE UPDATE ON `extra`
FOR EACH ROW
IF NEW.pages < 100 AND main.price >= 10
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Ціна має бути не більше 10$';
ELSEIF NEW.pages < 200 AND main.price >= 20
THEN
 SET @err2 = 'Ціна має бути не більше 20$';
ELSEIF NEW.pages < 300 AND main.price >= 30
THEN
 SET @err3 = 'Ціна має бути не більше 30$';
END IF;
$$
DELIMITER ;

//Видавництво "BHV" не випускає книги накладом меншим 5000, а видавництво Diasoft - 10000.
DROP TRIGGER IF EXISTS BHVandDias_tir_insert;
DROP TRIGGER IF EXISTS BHVandDias_tir_update;
DELIMITER $$
CREATE TRIGGER BHVandDias_tir_insert BEFORE INSERT ON `extra`
FOR EACH ROW
IF NEW.publisher = (SELECT publisher_id FROM publishers WHERE publishers.publishers LIKE 'BHV%') AND NEW.tirage < 5000
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Мінімільний тираж BHV 5000';
ELSEIF NEW.publisher = (SELECT publisher_id FROM publishers WHERE publishers.publishers LIKE 'DiaSoft') AND NEW.tirage < 10000
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Мінімільний тираж Diasoft 10000';
END IF;
$$
DELIMITER ;
DELIMITER $$
CREATE TRIGGER BHVandDias_tir_update BEFORE UPDATE ON `extra`
FOR EACH ROW
IF OLD.publisher = (SELECT publisher_id FROM publishers WHERE publishers.publishers LIKE 'BHV%') AND NEW.tirage < 5000 OR NEW.publisher = (SELECT publisher_id FROM publishers WHERE publishers.publishers LIKE 'BHV%') AND OLD.tirage < 5000
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Мінімільний тираж BHV 5000';
ELSEIF OLD.publisher = (SELECT publisher_id FROM publishers WHERE publishers.publishers LIKE 'DiaSoft') AND NEW.tirage < 10000 OR NEW.publisher = (SELECT publisher_id FROM publishers WHERE publishers.publishers LIKE 'DiaSoft') AND OLD.tirage < 10000
THEN
 SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Мінімільний тираж Diasoft 10000';
END IF;
$$
DELIMITER ;

//Книги з однаковим кодом повинні мати однакові дані.
DROP TRIGGER IF EXISTS same_code_insert_main;
DELIMITER $$
CREATE TRIGGER same_code_insert_main BEFORE INSERT ON `main`
FOR EACH ROW
BEGIN
    SET @same_code = 0;
    SELECT COUNT(*) INTO @same_code FROM main
    WHERE code = NEW.code AND (
        title <> NEW.title OR
        price <> NEW.price);
    IF (@same_code > 0) THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Книги з однаковим кодом повинні бути з однаковими даними';
    END IF;
END
$$
DELIMITER ;
DROP TRIGGER IF EXISTS same_code_insert_extra;
DELIMITER $$
CREATE TRIGGER same_code_insert_extra BEFORE INSERT ON `extra`
FOR EACH ROW
BEGIN
    SET @same_code = 0;
    SELECT COUNT(*) INTO @same_code FROM extra
    WHERE code = NEW.code AND (
        is_new <> NEW.is_new OR
        publisher <> NEW.publisher OR
        pages <> NEW.pages OR
        format <> NEW.format OR
        date <> NEW.date OR
        tirage <> NEW.tirage OR
        topic <> NEW.topic OR
        category <> NEW.category);
    IF (@same_code > 0) THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Книги з однаковим кодом повинні бути з однаковими даними';
    END IF;
END
$$
DELIMITER ;
DROP TRIGGER IF EXISTS same_code_update_main;
DELIMITER $$
CREATE TRIGGER same_code_update_main BEFORE UPDATE ON `main`
FOR EACH ROW
BEGIN
    SET @same_code = 0;
    SELECT COUNT(*) INTO @same_code FROM main
    WHERE code = NEW.code AND (
        title <> NEW.title OR
        price <> NEW.price);
    IF (@same_code > 0) THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Книги з однаковим кодом повинні бути з однаковими даними';
    END IF;
END
$$
DELIMITER ;
DROP TRIGGER IF EXISTS same_code_update_extra;
DELIMITER $$
CREATE TRIGGER same_code_update_extra BEFORE UPDATE ON `extra`
FOR EACH ROW
BEGIN
    SET @same_code = 0;
    SELECT COUNT(*) INTO @same_code FROM extra
    WHERE code = NEW.code AND (
        is_new <> NEW.is_new OR
        publisher <> NEW.publisher OR
        pages <> NEW.pages OR
        format <> NEW.format OR
        date <> NEW.date OR
        tirage <> NEW.tirage OR
        topic <> NEW.topic OR
        category <> NEW.category);
    IF (@same_code > 0) THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Книги з однаковим кодом повинні бути з однаковими даними';
    END IF;
END
$$
DELIMITER ;

//При спробі видалення книги видається інформація про кількість видалених рядків. Якщо користувач не "dbo", то видалення забороняється.
DROP TRIGGER IF EXISTS dbo_delete;
DELIMITER $$
CREATE TRIGGER dbo_delete BEFORE DELETE ON main FOR EACH ROW
BEGIN
    IF (REGEXP_SUBSTR(TRIM(CURRENT_USER()), '^[^\@]+') <> 'root')
    THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Лише користувач dbo може видаляти книги';
    ELSE
    SET @is_new = (SELECT is_new.is_new FROM is_new INNER JOIN extra ON extra.code = OLD.code AND extra.is_new = is_new.is_new_id);
    SET @publisher = (SELECT publishers.publishers FROM publishers INNER JOIN extra ON extra.code = OLD.code AND extra.publisher = publishers.publisher_id);
    SET @pages = (SELECT pages FROM extra WHERE extra.code = OLD.code);
    SET @format = (SELECT formats.formats FROM formats INNER JOIN extra ON extra.code = OLD.code AND extra.format = formats.format_id);
    SET @date = (SELECT date FROM extra WHERE extra.code = OLD.code);
    SET @tirage = (SELECT tirage FROM extra WHERE extra.code = OLD.code);
    SET @topic = (SELECT topics.topics FROM topics INNER JOIN extra ON extra.code = OLD.code AND extra.topic = topics.topic_id);
    SET @category = (SELECT categories.categories FROM categories INNER JOIN extra ON extra.code = OLD.code AND extra.category = categories.category_id);
    INSERT INTO basket (`code`, `title`, `price`, `is_new`, `publisher`, `pages`, `format`, `date`, `tirage`, `topic`, `category`) VALUE	(OLD.code, OLD.title, OLD.price, @is_new, @publisher, @pages, @format, @date, @tirage, @topic, @category);
    DELETE FROM extra WHERE code = OLD.code;
    END IF;
END
$$
DELIMITER ;

//Користувач "dbo" не має права змінювати ціну книги.
DROP TRIGGER IF EXISTS change_price;
DELIMITER $$
CREATE TRIGGER change_price BEFORE UPDATE ON main FOR EACH ROW
BEGIN
    IF (REGEXP_SUBSTR(TRIM(CURRENT_USER()), '^[^\@]+') <=> 'root') AND NEW.price <> OLD.price
    THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Користувач dbo не може змінювати ціну';
    END IF;
END
$$
DELIMITER ;

//Видавництва ДМК і Еком підручники не видають.
DROP TRIGGER IF EXISTS not_publisher_insert;
DELIMITER $$
CREATE TRIGGER not_publisher_insert BEFORE INSERT ON extra FOR EACH ROW
BEGIN
    IF NEW.publisher = (SELECT publishers.publisher_id FROM publishers WHERE publishers.publishers LIKE '%ДМК%')
    THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'ДМК більше не видає підручники';
    ELSEIF NEW.publisher = (SELECT publishers.publisher_id FROM publishers WHERE publishers.publishers LIKE '%Эком%')
    THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Эком більше не видає підручники';
    END IF;
END
$$
DELIMITER ;
DROP TRIGGER IF EXISTS not_publisher_update;
DELIMITER $$
CREATE TRIGGER not_publisher_update BEFORE UPDATE ON extra FOR EACH ROW
BEGIN
    IF NEW.publisher = (SELECT publishers.publisher_id FROM publishers WHERE publishers.publishers LIKE '%ДМК%')
    THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'ДМК більше не видає підручники';
    ELSEIF NEW.publisher = (SELECT publishers.publisher_id FROM publishers WHERE publishers.publishers LIKE '%Эком%')
    THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Эком більше не видає підручники';
    END IF;
END
$$
DELIMITER ;

//Видавництво не може випустити більше 10 новинок протягом одного місяця поточного року.
DROP TRIGGER IF EXISTS not_10new_insert;
DELIMITER $$
CREATE TRIGGER not_10new_insert BEFORE INSERT ON extra FOR EACH ROW
BEGIN
    SET @publisher_newbooks_count = 0;
    SELECT COUNT(*) INTO @publisher_newbooks_count FROM extra
    WHERE extra.publisher = NEW.publisher AND extra.is_new = 2 AND YEAR(NOW()) = YEAR(extra.date) AND MONTH(NOW()) = MONTH(extra.date);
    IF (NEW.is_new <=> 2 AND @publisher_newbooks_count >= 10) THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Видавництво не може видавати більше ніж 10 новинок на місяць';
    END IF;
END
$$
DELIMITER ;
DROP TRIGGER IF EXISTS not_10new_update;
DELIMITER $$
CREATE TRIGGER not_10new_update BEFORE UPDATE ON extra FOR EACH ROW
BEGIN
    SET @publisher_newbooks_count = 0;
    SELECT COUNT(*) INTO @publisher_newbooks_count FROM extra
    WHERE extra.publisher = NEW.publisher AND extra.is_new = 2 AND YEAR(NOW()) = YEAR(extra.date) AND MONTH(NOW()) = MONTH(extra.date);
    IF (((OLD.is_new <=> 2) OR (YEAR(NOW()) = YEAR(OLD.date) AND MONTH(NOW()) = MONTH(OLD.date))) AND @publisher_newbooks_count >= 10) THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Видавництво не може видавати більше ніж 10 новинок на місяць';
    END IF;
END
$$
DELIMITER ;
DROP TRIGGER IF EXISTS not_10new_update2;
DELIMITER $$
CREATE TRIGGER not_10new_update2 BEFORE UPDATE ON extra FOR EACH ROW
BEGIN
    SET @publisher_newbooks_count = 0;
    SELECT COUNT(*) INTO @publisher_newbooks_count FROM extra
    WHERE extra.publisher = OLD.publisher AND extra.is_new = 2 AND YEAR(NOW()) = YEAR(extra.date) AND MONTH(NOW()) = MONTH(extra.date);
    IF (((NEW.is_new <=> 2) OR (YEAR(NOW()) = YEAR(OLD.date) AND MONTH(NOW()) = MONTH(OLD.date))) OR ((OLD.is_new <=> 2) OR (YEAR(NOW()) = YEAR(NEW.date) AND MONTH(NOW()) = MONTH(NEW.date))) AND @publisher_newbooks_count >= 10) THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Видавництво не може видавати більше ніж 10 новинок на місяць';
    END IF;
END
$$
DELIMITER ;

//Видавництво BHV не випускає книги формату 60х88 / 16.
DROP TRIGGER IF EXISTS not_publisher_insert;
DELIMITER $$
CREATE TRIGGER not_publisher_insert BEFORE INSERT ON extra FOR EACH ROW
BEGIN
    IF (NEW.publisher = (SELECT publishers.publisher_id FROM publishers WHERE publishers.publishers LIKE '%BHV%')) AND (NEW.format = (SELECT formats.format_id FROM formats WHERE formats.formats LIKE '60х88/16'))
    THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'BHV не видає підручники формата 60x88/16';
    END IF;
END
$$
DELIMITER ;
DROP TRIGGER IF EXISTS not_publisher_update;
DELIMITER $$
CREATE TRIGGER not_publisher_update BEFORE UPDATE ON extra FOR EACH ROW
BEGIN
    IF (((NEW.publisher = (SELECT publishers.publisher_id FROM publishers WHERE publishers.publishers LIKE '%BHV%')) AND (OLD.format = (SELECT formats.format_id FROM formats WHERE formats.formats LIKE '60х88/16'))) OR ((OLD.publisher = (SELECT publishers.publisher_id FROM publishers WHERE publishers.publishers LIKE '%BHV%')) AND (NEW.format = (SELECT formats.format_id FROM formats WHERE formats.formats LIKE '60х88/16'))) OR ((NEW.publisher = (SELECT publishers.publisher_id FROM publishers WHERE publishers.publishers LIKE '%BHV%')) AND (NEW.format = (SELECT formats.format_id FROM formats WHERE formats.formats LIKE '60х88/16'))))
    THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'BHV не видає підручники формата 60x88/16';
    END IF;
END
$$
DELIMITER ;
