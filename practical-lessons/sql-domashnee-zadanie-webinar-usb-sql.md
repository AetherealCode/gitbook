---
description: june 2021
---

# SQL домашнее задание \(Webinar USB SQL\)

## Введение 

[https://sql-academy.org/ru/trainer/tasks/1](https://sql-academy.org/ru/trainer/tasks/1)  
  
`select * from Trip;`  
Написать и выполнить поочередно скрипты вывода остальных 3х таблиц

## Определенные столбцы из таблицы  

[https://sql-academy.org/ru/trainer/tasks/1](https://sql-academy.org/ru/trainer/tasks/1)  
  
`select *  
from Trip;`  
- таблица Trip, вывести поля: ИД полета,  название самолета, город вылета.  
- поменять местами 1 и 2 поля запроса, добавить в конце поле «город прилета».  
- отсортировать запрос по «названию самолета»\(ORDER BY\), по увеличению списка, и в обратном порядке\(DESC\). Обратить внимание, как изменится результат вывода.

## Предложение WHERE 

[https://sql-academy.org/ru/trainer/tasks/1](https://sql-academy.org/ru/trainer/tasks/1)  
  
-  вывести все полеты из Singapore  
- применить условие  LIKE '..%. '  – вывести полеты из города, начинающегося на 'Sin'  
- вывести все полеты из города, если знаем окончание названия 'ris'. Какой город вывелся?  
- вывести все полеты из города, если не знаем первые 3 буквы в названии города вылета '   tov', Какой город вывелся?  
  
`select *   
from Trip  
WHЕRE 0=0  
--and town_from LIKE 'Sin%'  -- вылеты из Сингапура  
--and town_from LIKE '%ris'  -- вылеты из ....  
and town_from LIKE '___tov'`  
  


## Работа с текстовыми данными, несколько условий 

[https://sql-academy.org/ru/trainer/tasks/1](https://sql-academy.org/ru/trainer/tasks/1)  
  
- вывести полеты компании 5  на  самолетах 'Boeing'  из Лондона  
- вывести полеты компании 1  на  самолетах 'TU-134'  не в Москву  
  
`select *   
from Trip  
WHERE 0=0  
and company = 6  
and plane = 'Boeing'  
and town_from 'London'  
---- не из Москвы  
--and company = 1  
--and plane = 'TU-134'  
--and town_from NOT LIKE 'Mo%ou'`

## Строковые функции **LIKE, Length\(\), Left\(\), Right\(\), Substr\(\), Lower\(\), Upper\(\), Replace\(\)** 

[https://sql-academy.org/en/trainer/tasks/17](https://sql-academy.org/en/trainer/tasks/17)  
  
- вывести имя из таблицы FamilyMembers  
- вывести длину строки с именем,  
- вывести левые 4 символа имени,  
- вывести правые 2 символа имени,  
- вывести  после 3 символа 3 буквы имени,  
- вывести имя большими буквами,  
- вывести имя маленькими буквами.  
  
`select member_name,  
      LENGTH(member_name) as len,  
      LEFT(member_name, 4) as lft_4,  
      RIGHT(member_name, 2) as rgt_2,  
      SUBSTR(member_name, 3, 3) as sbs_3,  
      Lower(member_name) as lwr,  
      Upper(member_name) as upr  
from FamilyMembers  
where 0=0`

## Вкладывание функций друг в друга: 

[https://sql-academy.org/en/trainer/tasks/17](https://sql-academy.org/en/trainer/tasks/17)  
  
`select fm.member_name         
from FamilyMembers fm`  
  
--------------------------------------------------  
  
1- вывести 1ю букву имени, LEFT\(\)  
2- вывести 1ю букву большой, UPPER\(\)  
3- соединить 1ю букву и точку, CONCAT\(\)  
4- найти позицию пробела, LOCATE\(\)  
5- вывести имя со следующей позиции после пробела , SUBSTR\(\)  
6- соединить 1ю букву имени\(2\), точку, и фамилию\(5\),  CONCAT\(\)  
  
`select member_name,  
       LEFT(member_name,1) as n1,  
       UPPER(LEFT(member_name,1)) as up1,  
       CONCAT(UPPER(LEFT(member_name,1)), '.') as n1t,  
       LOCATE(' ', member_name) as loc,  
       SUBSTR(member_name, LOCATE(' ', member_name)+1) as fml,  
       CONCAT(UPPER(LEFT(member_name,1)), '.', SUBSTR(member_name, LOCATE(' ', member_name)+1)) as fio  
from FamilyMembers fm`  
  


## Операторы сравнения 

[https://sql-academy.org/en/trainer/tasks/17](https://sql-academy.org/en/trainer/tasks/17)  
  
1- вывести утроенное значение unit\_price ,  
2- отнять 167 и прибавить 1000,  
3- перемножить unit\_price на значение поля amount и разделить на значение family\_member,  
4- отнять от amount значение unit\_price и прибавить unit\_price в степени 2  
5- найдите в Гугл функция SQL Корень квадратный, и выведите значение корня из  unit\_price  
  
-------------------------------------------  
  
`select family_member,   
       unit_price*3 as zn_1,   
       unit_price-167+1000 as zn_2,  
       unit_price * amount / family_member as zn_3,  
       amount - unit_price + POW(unit_price, 2) as zn_4,  
       SQRT(unit_price) as zn_5  
from Payments;`  
  
[https://sql-academy.org/en/trainer/tasks/17](https://sql-academy.org/en/trainer/tasks/17)  
  
1- вывести сумму платы по каждой транзакции \(unit\_price – цена за единицу, amount – количество товара\), если код товара от 1 до 20 ,  
2- вывести то же значение, если цена за единицу больше или равна 1500,  
3- вывести то же значение с пред.условиями , но только по членам семьи 2 и 3  
  
------------------------------------------  
  
`select *,  
       unit_price * amount as price  
from Payments  
where 0=0  
and good between 1 and 20  
and unit_price > 1500  
and family_member in (2,3)`  
  


## DISTINCT 

[https://sql-academy.org/en/trainer/tasks/17](https://sql-academy.org/en/trainer/tasks/17)  
  
выведите уникальные значения статусов членов семьи.  
  
`select distinct family_member  
from FamilyMembers;`  
  
================================================================================

## Самостоятельная работа 1 

Работайте в окне построения запроса на странице  


### **Задача 1**:  

[https://sql-academy.org/ru/trainer/tasks/17](https://sql-academy.org/ru/trainer/tasks/17)

#### используя такие условия к данным в таблице Payments

* за 2005 год 
* по всем товарам с кодами от 4 до 9
* больше 4х покупок\(amount\)
* стоимость товара от 8 USD

#### выведите такую информацию: 

* год покупки, 
* код члена семьи,
* код товара,
* количество товаров\(единиц\),
* цену за 1 единицу товара,
* цену за 1 единицу товара, в гривне \(курс валюты 28 грн за 1 доллар\),
* общую цену за все купленные единицы товара, в гривне.

####  Подсказка: 

начните с простого – выведите все содержимое таблицы Payments за 2005 год, посмотрите на данные, а потом вместо \*  по очереди добавляйте условия в части WHERE, и выводимую информацию в части SELECT :  
  
`select YEAR(date),  
       family_member,  
       good,   
       amount,   
       unit_price,  
       unit_price * 28 as unit_price_uah,  
       unit_price * amount  as  amount_price_usd  
from Payments p  
where 0=0  
and YEAR(DATE) = 2005  
and good between 4 and 9  
and amount > 4  
and unit_price >= 8  
order by family_member`  
  


### **Задача 2**\(на строковые функции\).  

  
[https://sql-academy.org/ru/trainer/tasks/18](https://sql-academy.org/ru/trainer/tasks/18)  
  
Вывести название товара из таблицы Goods  в виде:   
1я большая буква названия, тире, вторая часть названия товара.  
  
`select good_name,  
       UPPER(substr(good_name,1,1)) as up_fst,  
       concat(UPPER(substr(good_name,1,1)),'-') as cnct1,  
       LOCATE(' ',good_name) as lc,  
       substr(good_name,LOCATE(' ',good_name)+1) as sec_word,  
       concat(UPPER(substr(good_name,1,1)),'-',substr(good_name,LOCATE(' ',good_name)+1)   
 ) as cnct2  
FROM Goods`  


