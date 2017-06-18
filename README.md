# PhpMyAdmin

系统介绍
----

 1. 基于PhpMyAdmin Version 4.6.4修改，增加部分安全机制，以更安全的在公网使用；
 2. 可以对指定IP范围授权，不做登录限制；
 3. 通过简单的修改配置文件，实现短信验证，目前支持的验证码平台是阿里大鱼；
 4. 短信验证通过后，登录环境会被记录，在接下来一段时间不再需要验证。
 
 ![登录界面截图](https://raw.githubusercontent.com/yanglihui/PhpMyAdmin/master/screenshots/login.png)
 
 keywords：数据库管理,PhpMyAdmin,短信验证码,安全性
 

配置说明
----
PhpMyAdmin的常规的配置文件，可以参考其官网文档。
关于本项目的扩展配置，可以参考config.inc.sample.php，在使用时，把名字改成config.inc.php。

**具体说明**

 1. IP白名单

	    //配置IP白名单，配置在这里的IP可以直接使用系统，不需要验证
	    $safeIpList = array(
	        '221.223.108.22',	//My Current IP
	        '192.168.1.101',
	    );

 2. 短信相关配置

	    $cfg['message_verify'] = array(
	            'enable'    => true,  //true启用短信验证，false禁用
	            
	            //以下配置适用于阿里大鱼，相关的参数在使用的时候自然就知道了
	            'appkey'    => "your app key",  //阿里大鱼AppKey
	            'secretKey' => "your app secret key", //阿里大鱼AppSecret
	            'sign'      => "PhpMyAdmin验证",
	            'template'  => "SMS_template_id",

	            'bit'       => 6,  //验证码位数，建议4位或者6位
				
			//以下配置用户名字和手机号的对应关系，避免被刷短信
	            'yanglihui' => 18888888888,
	            'someone'   => 18666666666,
	    );

修改详情
----

 - 阿里大鱼的PHP SDK存放在 /libraries/plugins/alidayu 针对PhpMyAdmin
 - 主要修改的文件包括：
	 - /libraries/plugins/auth/AuthenticationCookie.php
	 - /js/functions.js

最后
--

第一次分享程序，好紧张╮(╯_╰)╭