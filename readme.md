##Explorer Mode - Matt Rice

#How many users are there?
```
SELECT COUNT(*) 
FROM users;
```
50
#______________________

#What are the 5 most expensive items?

```
SELECT price 
FROM items 
ORDER BY price 
DESC 
LIMIT 5;
```
$9,984
$9,859
$9,790
$9,390
$9,341
#______________________

#What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

```
SELECT MIN(price) 
FROM items 
WHERE category = 'Books';
```
$1,496

#______________________


#Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
```
SELECT first_name, last_name 
FROM users WHERE id = 
(SELECT user_id 
 FROM addresses 
 WHERE street = '6439 Zetta Hills');
```
Corrine Little

```
SELECT street, city, state 
FROM addresses 
WHERE user_id = 40;
```
Yes. 54369 Wolff Forges, Lake Byron, CA 31587
#______________________

#Correct Virginie Mitchell's address to "New York, NY, 10108".

```
UPDATE addresses 
SET city = 'New York', zip = '10108' 
WHERE state = 'NY' AND user_id = 
(SELECT user_id 
FROM addresses 
WHERE state = 'NY' AND user_id = 
(SELECT id 
FROM users 
WHERE first_name = 'Virginie'));
```

#______________________

#How much would it cost to buy one of each tool?
```
SELECT SUM(price) 
FROM items 
WHERE category 
IN ('Tools');
```
$7,383

#______________________

#How many total items did we sell?
```
SELECT SUM(quantity) 
FROM orders;
```
2,125


#______________________

#How much was spent on books?
```
SELECT sum(price) 
FROM items 
WHERE category 
IN ('Books');
```
$22,702

#______________________

#Simulate buying an item by inserting a User for yourself and an Order for that User.
```
INSERT INTO users (id,first_name,last_name,email)
VALUES (51,'Matt','Rice','mattrice12@outlook.com');
```
^Creates user

```
INSERT INTO orders (user_id, item_id,quantity)
VALUES (51, 55, 200);
```
^Creates order

```
SELECT * 
FROM orders 
WHERE user_id = 
(SELECT id 
FROM users 
WHERE email = 'mattrice12@outlook.com');
```
^Views order