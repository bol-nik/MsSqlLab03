������������ ������ �3
1.	���������� ������� ����������, ���������� ������� ��������� ���������� �����.
2.	������� � ���� ������� ������ � ���� ����������� � �������� (�������, �������� �������, ������������, ����, �������� ������, ���������� ���������� ������).
3.	���������� ������� ����������, ���������� ������� ���������  ������, ������������� ������ ����� ����.
4.	���������� ������� ����������, ���������� ������� ���������  ������, ������������� � ����.
5.	���������� ������� �����������, ��������� ������� ��������� ������ �� �������.
6.	���������� ������� �����������, ��������� ������� �������� � ������.
7.	���������� ������� ����������, ���������� ������� ��������� ���������� ����� �������� �� ������.
������� ������� �����������, ������������ ������� �������� 12% ������������:
I.	select s1.sp_name from sperson s1, sperson s2
where s2.comm=12 and s1.man_id=s2.sp_id;

II.	select s1.sp_name from sperson s1 join sperson s2
on s1.man_id=s2.sp_id
where s2.comm=12;

III.	select sp_name from sperson
where man_id in(select sp_id from sperson where comm=12);

������� ������� �������������, ���������� ������� ��������� �������:
I.	select distinct s2.sp_name from product  p, sale s , sperson s1, sperson s2
where p.p_desc='Sweater' and p.p_id=s.p_id and s1.sp_id=s.sp_id and s1.man_id=s2.sp_id

II.	select distinct s2.sp_name from sperson s2 join sperson s1 on s1.man_id=s2.sp_id
join sale s on s1.sp_id=s.sp_id join product p on p.p_id=s.p_id
where p.p_desc='Sweater';

III.	select sp_name from sperson where sp_id in
(select man_id from sperson where sp_id in
(select sp_id from sale where p_id=
(select p_id from product where p_desc='Sweater')));


������� ������� �������������, ���������� ������� ��������� ������ �������� �� ����.

select distinct s2.sp_name 
from customer c, country cn, sale sa,
sperson s1, sperson s2
where country='Chili'
and c.cn_id=cn.cn_id and
c.c_id =sa.c_id and
sa.sp_id=s1.sp_id and s1.man_id=s2.sp_id;

select distinct s2.sp_name 
from sperson s2 join sperson s1 
on s1.man_id=s2.sp_id join sale sa
on sa.sp_id=s1.sp_id join customer c
on c.c_id =sa.c_id join country cn
on c.cn_id=cn.cn_id
where country='Chili' ;

select sp_name from sperson where sp_id in
(select man_id from sperson where sp_id in
(select sp_id from sale where c_id  in
(select c_id from customer where cn_id=
(select cn_id from country 
where country='Chili'))));

������� ������� �����������, ������������ ������� ��������� ������ �� ����

select distinct s1.sp_name 
from country cn, manufact m, product p,
sale sa, sperson s1, sperson s2
where cn.country='Peru' and
cn.cn_id=m.cn_id and
m.m_id=p.m_id and
p.p_id=sa.p_id and
sa.sp_id=s2.sp_id and
s1.man_id=s2.sp_id;

select distinct s1.sp_name 
from sperson s1 join sperson s2
on s1.man_id=s2.sp_id join sale sa
on sa.sp_id=s2.sp_id join product p
on p.p_id=sa.p_id join manufact m
on m.m_id=p.m_id join country cn 
on cn.cn_id=m.cn_id
where cn.country='Peru' ;

select sp_name from sperson where man_id in
(select sp_id from sperson where sp_id in
(select sp_id from sale where p_id  in
(select p_id from product where m_id =
(select m_id from manufact where cn_id=
(select cn_id from country 
where country='Peru')))));


�������� ������� ������ ������ ��� ����������� ����� (����������, ��� ��� ��������)
select s1.sp_id, s1.sp_name, s.data, s.p_id, s.qty 
from sale s right join sperson s1 on s.sp_id=s1.sp_id;

