<h1>Assignment 4 in databases software development</h1>
<h3>made by Hallur vid Neyst and Murched Kayed</h3>

<h4>Exercise 1</h4>
<p>our discussions on the priveleges on the systems</p>
<ul>
  <li>the user responsible for <b>inventory</b> should be able to read and write because in addition to seeing the items, new items will also come in and should be placed in the database</li>
  <li>the user responsible for <b>bookkeeping</b> should be able to only read with the exception of writing in the status column in the orders table. This is because we think that messing with the actual order does not make sense, only the status where fex. "shipped" could be an option makes sense</li>
  <li>the user responsible for <b>human resources</b> should be able to read from offices, but in employees write and read. This is because we think that the offices aren't data that changes very often (if at all), but employees can change their positions in work at any time (f.ex he/she can be fired, promoted etc...)</li>
  <li>the user responsible for <b>sales</b> should be able to read from orders and orderdetails. The user has acces to help a customer with writing data to the order details table. And lastly, write in the comment column in the orders table if something is worth noting on a customer and the item</li>
  <li>The IT user should have access to all (so that there are no restrictions on fixing a database), much like the default root user</li>
  </ul>

<p>sqp code snippets on how we created the users/permissions:</p>

```sql
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
```



<h4>Exercise 2</h4>

INSERT INTO employees VALUES (1601,"Kayed","Murched","9300","cph-mk420@cphbusiness.dk","2","1621","developers");
INSERT INTO employees VALUES (1701,"við_Neyst","Hallur","9400","cph-hn131@cphbusiness.dk","2","1621","developers");

INSERT INTO products VALUES ("S72_1234","Mercedes_e220","Classic Cars","1:30","Daimler AG","gray colored car amgcap diesel v6","830","67.31","97.50");INSERT INTO orders VALUES ("104256", "2019-02-22", "2019-02-25", "2019-02-23", "In Process", null, "103");

SHOW GRANTS FOR InventoryUser;
SHOW GRANTS FOR BookUser;
SHOW GRANTS FOR HResourcesUser ;
SHOW GRANTS FOR SalesUser ;
SHOW GRANTS FOR root; /*do one line at a time, else you will only see root privileges*/


select * from mysql.general_log;

we logged in with the BookUser and tried to insert into the payments table, then we got the error message: command denied to user.

<h4>Exercise 3</h4>

CREATE USER 'ITUser'@'localhost' IDENTIFIED BY '123456';
GRANT ALL PRIVILEGES ON * . * TO 'ITUser'@'localhost';

mysqldump -u ITUser -p --opt --all-databases > testDump2.sql
docker cp 143ede981bd1:/testDump2.sql .
