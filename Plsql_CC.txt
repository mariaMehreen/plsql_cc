create table Part( 
part_no number(6) NOTNULL,
part_name varchar2(20) NOTNULL,
in_stock Boolean,
part_price number(6,2) NOTNULL,
part_desc varchar2(50)
);
insert into part values(01,'ER',85,200,'abc');
insert into part values(02,'TC',23,210,'xyz');
insert into part values(03,'RS',99,220,'rst');
insert into part values(04,'WS',81,230,'tyu');
insert into part values(05,'RSD',90,240,'xcv');

Question 1:
create or replace procedure 
is
cursor N is select * from part where part_no=1;
CUS N% rowtype;
begin
open N;
loop
fetch N into CUS;
exit when N% notfound;
DBMS_output.put_line(CUS.part_no|| '  ' || CUS.part_name|| '  '||
CUS.in_stock|| '  '||CUS.part_price||' ' || CUS.part_desc);
end loop;
end;

Question:2
create table Back_up(
part_no number(6),
part_name varchar(20),
modify_date date);


create or replace trigger backup_trigger
After insert or update or delete  on part
for each row
declare 
cursor N is select * from part;
begin
if updating then
insert into Back_up values(:new.part_no,:new.part_price,sysdate);
end if;
end;

Question 3:
create or replace procedure 
 is
 cursor N is select * from part;
 DET N% rowtype;
 begin
 open N;
 loop
 fetch N into CUS;
 if CUS.in_stock<16 then
 update part set part_price=250;
 end if;
 end loop;
 end;
 
 Question 4:
 set serverout on;
 begin
 for A in (select * from part)
 loop
 DBMS_output.put_line('value of Part_name:' || a.part_name);
 end loop;
 end;