# netology_12-4
# Домашнее задание к занятию «SQL. Часть 2»

Задание можно выполнить как в любом IDE, так и в командной строке.

## Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
* фамилия и имя сотрудника из этого магазина;
* город нахождения магазина;
* количество пользователей, закреплённых в этом магазине.

## Решение 1
```
SELECT CONCAT(s.first_name , " ", s.last_name) AS 'Сотрудник магазина', cm.city AS 'Город нахождения магазина', COUNT(c.customer_id) AS 'Количество пользователей'
FROM staff AS s
JOIN address AS a ON a.address_id = s.address_id
JOIN city AS cm ON cm.city_id = a.city_id
JOIN store AS st ON st.store_id = s.store_id
JOIN customer AS c ON c.store_id = s.store_id
GROUP BY staff_id
HAVING COUNT(c.customer_id) > 300;
```
![](https://github.com/eskin-igor/netology_12-4/blob/main/12-4/12-04-01-1.JPG)
 
## Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

## Решение 2
```
SELECT COUNT(length) AS 'Количество фильмов больше средней продолжительности'
FROM film
WHERE length > (SELECT AVG(length) FROM film);
```
![](https://github.com/eskin-igor/netology_12-4/blob/main/12-4/12-04-02-1.JPG)

## Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

## Решение 3
```
SELECT DATE_FORMAT(payment_date, '%Y.%m') AS 'Год и месяц c наибольшей суммой платежей', COUNT(rental_id) AS 'Количество аренд за месяц'
FROM payment
GROUP BY DATE_FORMAT(payment_date, '%Y.%m')
ORDER BY SUM(amount) DESC
LIMIT 1;
```
![](https://github.com/eskin-igor/netology_12-4/blob/main/12-4/12-04-03-1.JPG)

