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

opg2:

INSERT INTO employees VALUES (1601,"Kayed","Murched","9300","cph-mk420@cphbusiness.dk","2","1621","developers");
INSERT INTO employees VALUES (1701,"við_Neyst","Hallur","9400","cph-hn131@cphbusiness.dk","2","1621","developers");

INSERT INTO products VALUES ("S72_1234","Mercedes_e220","Classic Cars","1:30","Daimler AG","gray colored car amgcap diesel v6","830","67.31","97.50");INSERT INTO orders VALUES ("104256", "2019-02-22", "2019-02-25", "2019-02-23", "In Process", null, "103");

SHOW GRANTS FOR InventoryUser;
SHOW GRANTS FOR BookUser;
SHOW GRANTS FOR HResourcesUser ;
SHOW GRANTS FOR SalesUser ;
SHOW GRANTS FOR root; /*do one line at a time, else you will only see root privileges*/
