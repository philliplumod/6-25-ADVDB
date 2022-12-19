# 6-25-ADVDB

### 6
`select distinct p.maker, l.speed from product p inner join laptop l on p.model = l.model where l.hd >= 10`

### 7
`select product.model, laptop.price from product inner join laptop  on product.model = laptop.model where product.maker = 'B'
union
select product.model, printer.price from product inner join printer on product.model = printer.model where product.maker = 'B'
union
select product.model, pc.price from product inner join pc on product.model = pc.model where product.maker = 'B'`

### 8
`select distinct maker from product where type = 'PC' and maker not in (select maker from product where type = 'laptop')`

### 9
`select distinct maker from product inner join pc on product.model = pc.model and pc.speed >= 450`

### 10
`select distinct model, price from printer where price = (select max(price) from printer)`

### 11
`Select avg(speed) from pc`

### 12
`Select avg(speed) from laptop where price > 1000`

### 13
`Select avg(speed) from pc inner join product on pc.model = product.model where product.maker = 'A'`

### 14
`SELECT cl.class, sh.name, cl.country
FROM Ships AS sh, Classes AS cl
WHERE sh.class = cl.class
AND numGuns >= 10`

### 15
`Select hd from pc
group by hd 
having count(hd) >= 2`

### 16
`select distinct p1.model, p2.model, p1.speed, p1.ram
from pc p1
inner join pc p2
on p1.speed = p2.speed
and p1.ram = p2.ram
and (p1.model > p2.model)
order by p1.speed, p1.ram`

### 17
`Select distinct 'Laptop' as Type, model, speed from laptop where speed < (select min(speed) from pc)`

### 18
`select distinct product.maker, printer.price 
from product 
inner join printer 
on product.model = printer.model
where printer.price = (select min(price) from printer where color = 'y')
and printer.color = 'y'`

### 19
`SELECT product.maker, avg(LAPTOP.screen) as [Average Screen Size]
FROM LAPTOP 
INNER JOIN PRODUCT on laptop.model = product.model
group by product.maker`

### 20
`select maker, count(distinct model) as Count_Model
from product where type = 'PC' group by maker 
having count(distinct product.model) >= 3`

### 21
`select product.maker, max(pc.price)  from product
inner join pc 
on product.model = pc.model
group by product.maker`

### 22
`SELECT speed, AVG(price)
FROM PC
WHERE speed > 600
GROUP BY speed`

### 23
`SELECT DISTINCT maker
FROM Product
WHERE maker IN (
	SELECT DISTINCT maker 
	FROM Product AS pr
	JOIN PC AS pc
	ON pr.model = pc.model
	WHERE pc.speed >= 750
)
AND maker IN (
	SELECT DISTINCT maker 
	FROM Product AS pr 
	JOIN Laptop AS l
	ON pr.model = l.model
	WHERE l.speed >= 750)`

### 24
`WITH MAX
AS (
	SELECT model, price FROM PC
	UNION 
	SELECT model, price FROM Laptop
	UNION 
	SELECT model, price FROM printer
)

SELECT model FROM MAX
WHERE price = (
	SELECT MAX(price) 
	FROM MAX
)`

### 25

`SELECT DISTINCT maker
FROM Product JOIN PC
ON Product.model = PC.model
WHERE ram = (
	SELECT MIN(ram)
	FROM PC
)
AND speed = (
	SELECT MAX(speed)
	FROM PC
	WHERE ram = (
		SELECT MIN(ram)
		FROM PC)
	)
AND maker IN (
	SELECT maker
	FROM Product
	WHERE TYPE='Printer'
)`
