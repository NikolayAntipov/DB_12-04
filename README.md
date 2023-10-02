# Домашнее задание к занятию «SQL. Часть 2» - Антипов Н.С.

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:  
фамилия и имя сотрудника из этого магазина;  
город нахождения магазина;  
количество пользователей, закреплённых в этом магазине.  

```sql  
select	concat(sf.first_name , ' ', sf.last_name)  as 'ФИО сотрудника',  
		cy.city as 'Город',  
		COUNT(cr.customer_id) as 'Количество пользователей магазина'  		
from sakila.store s  
inner join sakila.staff sf on sf.store_id = s.store_id   
inner join sakila.customer cr on cr.store_id = s.store_id  
inner join sakila.address a on a.address_id = s.address_id   
inner join sakila.city cy on cy.city_id = a.city_id   
group by sf.staff_id, cy.city_id   
having COUNT(cr.customer_id) > 300;  
```



### Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```sql
select COUNT(flm.title) as 'Количество'
from sakila.film flm  
where flm.`length` > (select AVG(`length`) from sakila.film);
```


### Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
