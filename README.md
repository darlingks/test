

接口文档（ app端 ）

1.	获取项目列表（ 根据业务员id ）
	
	接口地址：http://jootu.synology.me:1234/construction_online/public/api/admin/getprojlist

	请求方式：post

	请求参数：
			参数名			数据类型			备注
			index 			tinyint(11)		搜索类型（1:根据业务员id查询	2:根据客户id查询）
			id			int(11)			业务id

	返回参数：
			参数名			数据类型			备注
			id 			int(11)			项目id
			name 			varchar(128)		项目名称
			client_id 		int(11)			客户id
			c_real_name		varchar(128)		客户姓名（client表关联查询）
			status 			tinyint(4)		项目状态（1-待开工2-施工中3-验收中4-已完工）
			money			int(11)			合同金额
			retainage		int(11)			尾款（金额减去finance的钱）

	备注信息：



2.	获取汇款记录（ 根据项目id ）
	
	接口地址：http://jootu.synology.me:1234/construction_online/public/api/admin/getpaymentlist/{id}

	请求方式：post

	请求参数：{id}:	项目id

	返回参数：
			参数名			数据类型			备注
			id 			int(11)			付款记录id
			created_at		date			付款创建日期
			payment_time		date			付款日期
			payment_amount		int(11)			付款金额
			status			tinyint(1)		审核状态（1-待审批2-已审批3-不通过）
			comment			longtext		备注

	备注信息：根据status	区分加载时间



3.	审核提交（ 根据汇款记录id 且如果审核未通过－则备注字段不能为空）
	
	接口地址：http://jootu.synology.me:1234/construction_online/public/api/admin/paymentcheck

	请求方式：post

	请求参数：
			参数名			数据类型			备注
			id 			int(11)			付款记录id
			ret_check		tinyint(1)		审核结果（1-通过	2-未通过）

	返回参数：成功返回0	失败返回-1	

	备注信息：接口中update status、update_at、payment_time字段



4.	新增汇款记录
	
	接口地址：http://jootu.synology.me:1234/construction_online/public/api/admin/addpayment

	请求方式：post

	请求参数：
			参数名			数据类型			备注
			project_id 		int(11)			项目id
			created_at		datetime		汇款创建时间（用户自定义）
			payment_amount		int(11)			付款金额
			comment			longtext		备注

	返回参数：成功返回0	失败返回-1

	备注信息：接口中created_at、updated_at取传入的created_at		payment_time为空		status默认为1（待审核）



5.	获取客户列表（ 根据用户id－用户只能查询自己开发的客户?? ）
	
	接口地址：http://jootu.synology.me:1234/construction_online/public/api/admin/getclientlist/{id}

	请求方式：post

	请求参数：{id}:	业务员id（salesman_id）

	返回参数：
			参数名			数据类型			备注
			real_name 		varchar(128)	业务员姓名（关联employee表获取）
			client_id 		int(11)			客户id
			wechat			varchar(128)	绑定微信(公众号自带openid)
			created_at		datetime		客户注册日期
			unique_name		varchar(128)	用户名
			c_real_name		varchar(128)	客户姓名
			contact			varchar(128)	联系方式
			description		varchar(1024)	描述


	备注信息：从项目表（project）关联查询客户表（client）获取到客户列表			关联employee表获取用户姓名



6.	获取单个客户资料（ 根据客户id ）
	
	接口地址：http://jootu.synology.me:1234/construction_online/public/api/admin/getclientdata/{id}

	请求方式：post

	请求参数：{id}:	客户id

	返回参数：
			参数名			数据类型			备注
			client_id 		int(11)			客户id
			wechat			varchar(128)		绑定微信(公众号自带openid)
			created_at		datetime		客户注册日期
			unique_name		varchar(128)		用户名
			c_real_name		varchar(128)		客户姓名
			contact			varchar(128)		联系方式
			description		varchar(1024)		描述

	备注信息：




7.	新增客户资料
	
	接口地址：http://jootu.synology.me:1234/construction_online/public/api/admin/addclientdata

	请求方式：post

	请求参数：
			参数名			数据类型			备注
			unique_name		varchar(128)		用户名
			c_real_name		varchar(128)		客户姓名
			contact			varchar(128)		联系方式
			description		varchar(1024)		描述
			salesman_id 		int(11)			业务员id

	返回参数：成功返回0	失败返回-1

	备注信息：插入一条数据到client表		created_at、updated_at取当前时间		wechat默认null




8.	施工计划列表
	
	接口地址：http://jootu.synology.me:1234/construction_online/public/api/admin/getconstructionlist/{id}

	请求方式：post

	请求参数：{id}:	项目id

	返回参数：
			参数名			数据类型			备注
			id			int(11)			施工计划id
			c_name 			varchar(255)		施工名称
			address 		varchar(255)		施工地址
			status 			tinyint(4)		施工状态（1-开始	2-施工	3-验收	4-完工	5-返工）

	备注信息：插入一条数据到client表		created_at、updated_at取当前时间		wechat默认null
	
	













