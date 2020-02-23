1) find all customers that live in London. Returns 6 records

    SELECT * FROM customers WHERE city='London';

2) find all customers with postal code 1010. Returns 3 customers

    SELECT * FROM customers WHERE postal_code='1010';

3) find the phone number for the supplier with the id 11. Should be (010) 9984510

    SELECT phone FROM suppliers WHERE supplier_id=11

4) list orders descending by the order date. The order with date 1998-05-06 should be at the top

    SELECT * FROM orders 
    ORDER BY order_date DESC

5) find all suppliers who have names longer than 20 characters. Returns 11 records

    SELECT * 
    FROM suppliers
    WHERE LENGTH(company_name) >20;

6) find all customers that include the word 'MARKET' in the contact title. Should return 19 records

    SELECT * 
    FROM customers
    WHERE UPPER(contact_title) LIKE '%MARKET%';

7) add a customer record for

    . customer id is 'SHIRE':
    . company name is 'The Shire'
    . contact name is 'Bilbo Baggins'
    . the address is '1 Hobbit-Hole'
    . the city is 'Bag End'
    . the postal code is '111'
    . the country is 'Middle Earth'

    INSERT INTO customers (customer_id,company_name,contact_name,address,city,postal_code,country)
    VALUES ('SHIRE','The Shire','Bilbo Baggins','1 Hobbit-Hole', 'Bag End','111','Middle Earth');

8) update Bilbo Baggins record so that the postal code changes to "11122"

    UPDATE customers
    set postal_code='11122'
    WHERE customer_id='SHIRE'

9) list orders grouped and ordered by customer company name showing the number of orders per customer company name. Rattlesnake Canyon Grocery should have 18 orders

    SELECT COUNT(orders.order_id),customers.company_name 
    FROM orders
    INNER JOIN customers
    ON orders.customer_id=customers.customer_id
    GROUP BY company_name
    ORDER BY company_name

10) list customers by contact name and the number of orders per contact name. Sort the list by number of orders in descending order. Jose Pavarotti should be at the top with 31 orders followed by Roland Mendal with 30 orders. Last should be Francisco Chang with 1 order

    SELECT COUNT(orders.order_id) as orderCount,customers.contact_name 
    FROM orders
    INNER JOIN customers
    ON orders.customer_id=customers.customer_id
    GROUP BY customers.contact_name
    ORDER BY orderCount DESC

11) list orders grouped by customer's city showing number of orders per city. Returns 69 Records with Aachen showing 6 orders and Albuquerque showing 18 orders

    SELECT COUNT(orders.order_id) as orderCount,customers.city 
    FROM orders
    INNER JOIN customers
    ON orders.customer_id=customers.customer_id
    GROUP BY customers.city


1) Data Normalization

a) Species

    id |  species
    --------------
    1  |  Dog
    2  |  Cat
    3  |  Turtle
    4  |  Horse
    5  |  Fish


b)  Person

    id |  Person_name  |    Fenced_yard |   City_dweller |
    ------------------------------------------------------
    1  |  Jane         |    No          |   Yes          |
    2  |  Bob          |    No          |   No           |
    3  |  Sam          |    Yes         |   No           |


c) Person_Pet

    Species | Pet_Name    |   Person_id  |
    --------------------------------------
        1   | Ellie       |   1          |
        4   | Joe         |   2          |
        1   | Ginger      |   3          |
        2   | Tiger       |   1          |
        2   | Miss Kitty  |   3          |
        3   | Turtle      |   1          |
        5   | Bubble      |   3          |