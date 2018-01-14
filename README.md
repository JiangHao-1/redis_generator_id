# redis_generator_id
generator id by redis lua
基于redis的分布式ID生成器。
利用redis的lua脚本执行功能，在每个节点上通过lua脚本生成唯一ID。
生成的ID是14位的：
如：2018年1月15日生成的ID：180150000000001，前两位年份，中间三位是该年第几天,后面九位是自增序列。每天自增序列零点置零。
    year     day			seq
	18 		 015 		0000000001
前两位年份  该年第几天     自增序列

集群实现原理
假定集群里有3个节点，则节点1返回的seq是：
0, 3, 6, 9, 12 ...

节点2返回的seq是
1, 4, 7, 10, 13 ...

节点3返回的seq是
2, 5, 8, 11, 14 ...

这样每个节点返回的数据都是唯一的。

redis 2.8以上即可支持
每日可满足9亿级ID生产不重复，支持传入表名称生成获取该表趋势增长的ID
