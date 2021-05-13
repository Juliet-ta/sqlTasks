//Розробити та перевірити скалярну (scalar) функцію, що повертає загальну вартість книг виданих в певному році.
DROP FUNCTION sumBookPriceInYear
GO
CREATE FUNCTION dbo.sumBookPriceInYear (@year INT)
RETURNS FLOAT
AS
BEGIN
	DECLARE @sumprices FLOAT;
	SELECT @sumprices = SUM(price) FROM main, extra WHERE main.code = extra.code AND YEAR([date]) = @year
	RETURN @sumprices;
END;
GO
SELECT dbo.sumBookPriceInYear (1999)

//Розробити і перевірити табличну (inline) функцію, яка повертає список книг виданих в певному році.
GO
CREATE FUNCTION dbo.booksPubInYear(@year INT)
RETURNS TABLE
AS RETURN (SELECT main.code, main.title, main.price, extra.is_new, extra.publisher, extra.pages, extra.format, extra.date, extra.tirage, extra.topic, extra.category FROM main, extra WHERE main.code = extra.code AND YEAR([date])=@year);
GO
SELECT * from booksPublishedInYear(1999)

//Розробити і перевірити функцію типу multi-statement, яка буде:
//a.	приймати в якості вхідного параметра рядок, що містить список назв видавництв, розділених символом ‘;’;  
//b.	виділяти з цього рядка назву видавництва;
//c.	формувати нумерований список назв видавництв.
CREATE FUNCTION TablePublishers(@publishers NVARCHAR(MAX))
RETURNS TABLE AS
RETURN (SELECT ROW_NUMBER() OVER(ORDER BY value ASC) AS number, value
			FROM STRING_SPLIT(@publishers,';'), publishers WHERE value LIKE publishers.publishers)
DECLARE @string NVARCHAR(MAX);
SELECT @string = string_agg(publisher_name, ';') FROM publishers;
SELECT * from dbo.publisherList(@string);

//Виконати набір операцій по роботі з SQL курсором: оголосити курсор;
//a.	використовувати змінну для оголошення курсору;
//b.	відкрити курсор;
//c.	переприсвоїти курсор іншої змінної;
//d.	виконати вибірку даних з курсору;
//e.	закрити курсор;
DECLARE 
    @book_name NVARCHAR(MAX), 
    @date  DATETIME;
DECLARE cursor_get_books CURSOR
FOR SELECT title, date FROM main, extra WHERE main.code = extra.code;
OPEN cursor_get_books;
FETCH NEXT FROM cursor_get_books INTO @book_name, @date;
WHILE @@FETCH_STATUS = 0
    BEGIN
	IF (2000=YEAR(@date))
		PRINT @book_name + CAST(YEAR(@date) AS NVARCHAR(40));
	FETCH NEXT FROM cursor_get_books INTO @book_name, @date;
    END;

//Звільнити курсор. Розробити курсор для виводу списка книг виданих у визначеному році.
CLOSE cursor_get_books;
DEALLOCATE cursor_get_books;
