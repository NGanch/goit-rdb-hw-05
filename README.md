# goit-rdb-hw-05
SELECT 
    order_details.*, 
    (SELECT customer_id FROM orders WHERE orders.order_id = order_details.order_id) AS customer_id
FROM order_details;
![p_1](https://github.com/NGanch/goit-rdb-hw-05/assets/86801593/52850676-0e02-407a-bf4e-485723d999fd)

SELECT *
FROM order_details
WHERE order_id IN (SELECT order_id FROM orders WHERE shipper_id = 3);
![p_2](https://github.com/NGanch/goit-rdb-hw-05/assets/86801593/52331159-616c-43e8-b321-909ee4bd6008)

SELECT order_id, AVG(quantity) AS avg_quantity
FROM (SELECT * FROM order_details WHERE quantity > 10) AS orders_filtered
GROUP BY order_id;
![p_3](https://github.com/NGanch/goit-rdb-hw-05/assets/86801593/19908849-2b61-4f64-ad80-15035f7757cc)

WITH temp AS (
    SELECT * FROM order_details WHERE quantity > 10
)
SELECT order_id, AVG(quantity) AS avg_quantity
FROM temp
GROUP BY order_id;
![p_4](https://github.com/NGanch/goit-rdb-hw-05/assets/86801593/2ba07673-a1d6-4203-9af5-53a0b17bd076)

-- Видаляємо функцію, якщо вона вже існує
DROP FUNCTION IF EXISTS divide_function;

-- Створюємо нову функцію з вказанням ключового слова DETERMINISTIC
DELIMITER //

CREATE FUNCTION divide_function(x FLOAT, y FLOAT)
RETURNS FLOAT
DETERMINISTIC
BEGIN
    DECLARE result FLOAT;
    SET result = x / y;
    RETURN result;
END//

DELIMITER ;
![p_5](https://github.com/NGanch/goit-rdb-hw-05/assets/86801593/5bff38be-ab5b-40e2-a9c5-3f95b188ea54)

SELECT divide_function(quantity, 2) AS divided_quantity FROM order_details;
![p_5_1](https://github.com/NGanch/goit-rdb-hw-05/assets/86801593/696e0a9e-cfb5-434f-888c-ef4a91c375d2)
