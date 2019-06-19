# 1.
select a.id, a.type, a.status, a.amount, (b.average - a.amount) difference from account a join 
(select type, avg(amount) average from account where status = 'Active' group by type) b
on a.type = b.type
where a.status = 'Active'
<pre>
[training@localhost ~]$ mkdir problem1
[training@localhost ~]$ cd problem1
[training@localhost problem1]$ ls -al
total 8
drwxrwxr-x   2 training training 4096 Jun 19 00:29 .
drwx------. 30 training training 4096 Jun 19 00:29 ..
[training@localhost problem1]$ vi solution.sql
[training@localhost problem1]$ pwd
/home/training/problem1
[training@localhost problem1]$ ls -al
total 12
drwxrwxr-x   2 training training 4096 Jun 19 00:30 .
drwx------. 30 training training 4096 Jun 19 00:30 ..
-rw-rw-r--   1 training training  230 Jun 19 00:30 solution.sql

</pre>

# 2.

# 3.
create table solution as
select b.id, b.fname, b.lname, b.hphone from account a join customer b on a.custid = b.id
where a.amount < 0

# 4.

# 5.
select fname, lname, city, state from customer where city = 'Palo Alto' and state = 'CA'
union all
select fname, lname, city, state from employee where city = 'Palo Alto' and state = 'CA';
<pre>
[training@localhost ~]$ mkdir problem5
[training@localhost ~]$ cd problem5
[training@localhost problem5]$ vi solution.sql
[training@localhost problem5]$ 

</pre>

# 6.

create table solution as
select id, fname, lname, address, city, state, zip, substring(birthday, 0, 5) birthday from employee;
<pre>
Solution table Created
</pre>
# 7.
select concat(fname, ' ',lname) from (select fname, lname from employee where city = 'Seattle' order by fname, lname) a;

<pre>
[training@localhost ~]$ mkdir problem7
[training@localhost ~]$ cd problem7
[training@localhost problem7]$ vi solution.sql
[training@localhost problem7]$ 

</pre>
# 8.

# 9.
create table solution as
select concat('A',id) id, fname, lname, address, city, state, zip, birthday from customer;

<pre>
Solution table Created
</pre>
# 10.
create table solution as
select b.id, b.fname, b.lname, b.city, b.state, a.charge, substring(a.tstamp,0,10) billdata from billing a join customer b on a.id = b.id
<pre>
Solution table Created
</pre>

# 11.
## a. 
select a.name from
(select count(prod_id) cnt, name from products where brand = 'Dualcore' group by name order by cnt desc limit 3) a;

## b.
select c.order_date, sum(a.price), sum(pmc)
  from (select prod_id, brand, name, price, cost, shipping_wt, price-cost pmc from products where brand = 'Dualcore') a 
  join order_details b on a.prod_id = b.prod_id 
  join (select order_id, cust_id, to_date(order_date) order_date from orders) c on b.order_id = c.order_id
 group by c.order_date;

## c.
select a.order_id, sum(b.price) sp 
from order_details a join products b on a.prod_id = b.prod_id 
group by a.order_id 
order by sp desc 
limit 10;
 