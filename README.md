# CDM_report
### 代码高亮
``` sql
--自动手动备份历史记录
select b."name" 备份策略名称uuuuuuuuuuuuuuuuu ,x.strategy_id ,x."type",x.state,x.备份策略对应类型对应状态自动备份任务个数
from
(
	SELECT x.strategy_id ,x."type",x.state,count(x.strategy_id) 备份策略对应类型对应状态自动备份任务个数
	FROM public."event" x
	WHERE x."type" in(11,12) and x.scheduled in(true,false) and x.deleted_at =0
		  and to_timestamp(to_number(substring(to_char(x.created_at , '9999999999999999999'),1,14),'9999999999999')/1000) 
		  		between '2021-08-11 00:00:00' and '2021-08-11 23:59:59' -- '2021-04-09 23:30:00' and '2021-04-10 23:59:59'
--		  		and x.message not like '%客户端离线%' and x.message not like '%EOF%'
	group by x.strategy_id,x.state ,x."type" 
) x,protection_strategy b
where x.strategy_id = b.id  -- and b.app_kind in(2) -- and b.backup_kind in(1,2)
order by x.strategy_id desc
```
