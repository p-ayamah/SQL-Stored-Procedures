# Stored Procedure

```sql
alter procedure customer_trans_history (@customer_name varchar(50))
as
select 
	p.productname
	,od.unitprice as price
	,od.qty as quantity
	,orderdate as [date ordered]
from [dbo].[Customers] c
left join [dbo].[Orders] o
on c.custid = o.custid
join [dbo].[OrdersDetails] od
on od.orderid = o.orderid
join [dbo].[Products] p
on p.productid = od.productid
where c.custid = 
(select custid from Customers where companyname = concat('customer ', @customer_name))
```
