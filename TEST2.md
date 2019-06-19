#1.
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

#2.

#3.

#4.

#5.
select fname, lname, city, state from customer where city = 'Palo Alto' and state = 'CA'
union all
select fname, lname, city, state from employee where city = 'Palo Alto' and state = 'CA';
<pre>
[training@localhost ~]$ mkdir problem5
[training@localhost ~]$ cd problem5
[training@localhost problem5]$ vi solution.sql
[training@localhost problem5]$ 

</pre>

#6.

create table solution as
select id, fname, lname, address, city, state, zip, substring(birthday, 0, 5) birthday from employee;
