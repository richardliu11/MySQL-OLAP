# MySQL-OLAP
窗口函数
SELECT
	window_practice.userid,
	window_practice.`本次购买数量`,
	window_practice.`本次购买金额`,
	window_practice.`购买产品名称`,
	window_practice.`购买时间`,
	SUM( window_practice.`本次购买金额` ) OVER ( PARTITION BY window_practice.userid ORDER BY window_practice.`购买时间` rows BETWEEN unbounded preceding AND unbounded following ) AS `历史购买金额总和`,
	SUM( window_practice.`本次购买数量` ) OVER ( PARTITION BY window_practice.userid ORDER BY window_practice.`购买时间` rows BETWEEN unbounded preceding AND unbounded following ) AS `历史购买数量`,
	MAX( window_practice.`本次购买金额` ) OVER ( PARTITION BY window_practice.userid ORDER BY window_practice.`购买时间` rows BETWEEN unbounded preceding AND unbounded following ) AS `历史单次购买最大金额`,
	MAX( window_practice.`本次购买数量` ) OVER ( PARTITION BY window_practice.userid ORDER BY window_practice.`购买时间` rows BETWEEN unbounded preceding AND unbounded following ) AS `历史单次购买最大数量` 
FROM
	window_practice 
ORDER BY
	window_practice.userid;
