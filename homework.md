# Домашнее задание к занятию "Индексы" - Вебер Сергей


### Задание 1

Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.

select sum(DATA_LENGTH), sum(INDEX_LENGTH), concat(round((sum(INDEX_LENGTH) / sum(DATA_LENGTH)) *100), ' %') as Отношение_индексов_таблиц

from INFORMATION_SCHEMA.tables 

where TABLE_SCHEMA = 'sakila' ;

![image](https://github.com/GorkOrMork/index/assets/109193124/e1806b56-e055-4602-bdf6-72b94308410d)


### Задание 2

ыполните explain analyze следующего запроса:

select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)

from payment p, rental r, customer c, inventory i, film f

where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id

перечислите узкие места;

оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.
