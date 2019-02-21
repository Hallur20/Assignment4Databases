inventory? -> we think the user should write and read

bookkeeping -> only read from order and payments tables but can write in column status in order

human resources -> offices can only read, employees can update all.

Sales -> access to read orders / orderdetails, can help customer with creating order details / make a comment in orders.




CREATE USER 'InventoryUser';
GRANT SELECT, INSERT ON classicmodels.products TO InventoryUser;
GRANT SELECT, INSERT ON classicmodels.productlines TO InventoryUser;

FLUSH Privileges;



create user BookUser;
GRANT SELECT ON classicmodels.orders TO BookUser;
GRANT SELECT ON classicmodels.payments TO BookUser;

GRANT UPDATE (status) ON classicmodels.orders TO BookUser;

FLUSH Privileges;


create user HResourcesUser
GRANT SELECT ON classicmodels.offices TO HResourcesUser;
GRANT SELECT, INSERT ON classicmodels.employees TO HResourcesUser;

FLUSH Privileges;


create user SalesUser
GRANT SELECT ON classicmodels.orders TO SalesUser;
GRANT UPDATE  (comments) ON classicmodels.orders TO SalesUser;
GRANT SELECT, INSERT ON classicmodels.orderdetails TO SalesUser;
FLUSH Privileges;

