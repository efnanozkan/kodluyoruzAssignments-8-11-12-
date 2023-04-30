# kodluyoruzSQLAssignments (8-11-12)
## Assignment 8

### 1) test veritabanınızda employee isimli sütun bilgileri id(INTEGER), name VARCHAR(50), birthday DATE, email VARCHAR(100) olan bir tablo oluşturalım.
<code>  CREATE TABLE employee (
 id INTEGER PRIMARY KEY,
 name VARCHAR(50),
 birthday DATE,
 email VARCHAR(100)
 );
 </code>

### 2) Oluşturduğumuz employee tablosuna 'Mockaroo' servisini kullanarak 50 adet veri ekleyelim.
![datas](https://user-images.githubusercontent.com/107806946/235345729-5a9b5361-ff48-4386-aa1d-dc0722d025ac.JPG)

### 3) Sütunların her birine göre diğer sütunları güncelleyecek 5 adet UPDATE işlemi yapalım.
<code>UPDATE employee
SET name = 'john'
WHERE email ='johnnya1@yandex.ru'
RETURNING*;

UPDATE employee
SET email = 'salim-12@üni.edu.tr'
WHERE id = 1
RETURNING*;

UPDATE employee
SET birthday = '1999-07-26'
WHERE name = 'Sertaç'
RETURNING*;

UPDATE employee
SET name= 'Sena'
WHERE name LIKE 'T___'
RETURNING*;

UPDATE employee
SET name= 'Adam'
WHERE birthday = (select min(birthday) from employee)
RETURNING*; </code>

### 4) Sütunların her birine göre ilgili satırı silecek 5 adet DELETE işlemi yapalım.
<code>
DELETE FROM employee
WHERE name ='john'
RETURNING*;

DELETE FROM employee
WHERE id=32
RETURNING*;

DELETE FROM employee
WHERE email = 'senat99@yandex.com'
RETURNING*;

DELETE FROM employee
WHERE birthday in (select birthday from employee order by birthday asc limit 5 )
RETURNING*;

DELETE FROM employee
WHERE length(name)>(select avg(length(name)) from employee)
RETURNING*; </code>

## Assignment 11
### 1) actor ve customer tablolarında bulunan first_name sütunları için tüm verileri sıralayalım.
<code>
SELECT first_name FROM actor
UNION
SELECT first_name FROM customer;
</code>

### 2) actor ve customer tablolarında bulunan first_name sütunları için kesişen verileri sıralayalım.
<code> 
SELECT first_name FROM actor
INTERSECT
SELECT first_name FROM customer;
</code>

### 3) actor ve customer tablolarında bulunan first_name sütunları için ilk tabloda bulunan ancak ikinci tabloda bulunmayan verileri sıralayalım.
<code>
SELECT first_name FROM actor
EXCEPT
SELECT first_name FROM customer;
</code>

### 4) İlk 3 sorguyu tekrar eden veriler için de yapalım.
<code>
-- Tüm verileri sıralama
SELECT first_name FROM actor
UNION ALL
SELECT first_name FROM customer;

-- Kesişen verileri sıralama
SELECT first_name FROM actor
INTERSECT ALL
SELECT first_name FROM customer;

-- İlk tabloda bulunan ancak ikinci tabloda bulunmayan verileri sıralama
SELECT first_name FROM actor
EXCEPT ALL
SELECT first_name FROM customer;
</code>

## Assignment 12

### 1) film tablosunda film uzunluğu length sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır?
<code>
SELECT COUNT(*) AS film_count
FROM film
WHERE length > (SELECT AVG(length) FROM film);
</code>

### 2) film tablosunda en yüksek rental_rate değerine sahip kaç tane film vardır?
<code>
SELECT COUNT(*) AS film_count
FROM film
WHERE rental_rate = (SELECT MAX(rental_rate) FROM film);
</code>

### 3) film tablosunda en düşük rental_rate ve en düşün replacement_cost değerlerine sahip filmleri sıralayınız.
<code>
SELECT *
FROM film
WHERE rental_rate = (SELECT MIN(rental_rate) FROM film)
AND replacement_cost = (SELECT MIN(replacement_cost) FROM film);
</code>

### 4) payment tablosunda en fazla sayıda alışveriş yapan müşterileri(customer) sıralayınız.
<code>
SELECT customer_id, COUNT(*) AS transaction_count
FROM payment
GROUP BY customer_id
ORDER BY transaction_count DESC
LIMIT 10;
</code>



