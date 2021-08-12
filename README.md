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

DEMO
===========================

###########环境依赖
node v0.10.28+
redIs ~

###########部署步骤
1. 添加系统环境变量
    export $PORTAL_VERSION="production" // production, test, dev


2. npm install  //安装node运行环境

3. gulp build   //前端编译

4. 启动两个配置(已forever为例)
    eg: forever start app-service.js
        forever start logger-service.js


###########目录结构描述
├── Readme.md                   // help
├── app                         // 应用
├── config                      // 配置
│   ├── default.json
│   ├── dev.json                // 开发环境
│   ├── experiment.json         // 实验
│   ├── index.js                // 配置控制
│   ├── local.json              // 本地
│   ├── production.json         // 生产环境
│   └── test.json               // 测试环境
├── data
├── doc                         // 文档
├── environment
├── gulpfile.js
├── locales
├── logger-service.js           // 启动日志配置
├── node_modules
├── package.json
├── app-service.js              // 启动应用配置
├── static                      // web静态资源加载
│   └── initjson
│       └── config.js         // 提供给前端的配置
├── test
├── test-service.js
└── tools



###########V1.0.0 版本内容更新
1. 新功能     aaaaaaaaa
2. 新功能     bbbbbbbbb
3. 新功能     ccccccccc
4. 新功能     ddddddddd
