服务可用性监控和报警
====================

简介
----
可对redis,sds等服务进行监控,由crontab访问此项目下由你拼装好的的url,来指定监控特定服务的某方面的状况

如何使用
--------
    编辑好manifest后部署到某地址,比如url:http://yoursite.mi-ae.com.cn/
    url的形式:
      http://yoursite.mi-ae.com.cn/monitor/srv/$srv/action/$action?(:all) 
    其中 $srv, $action,  (:all) 请自己指定, 定义如下
参数
----
    $srv: 
        含义:要监测的服务 
        参数在url中的位置: segment3 
        必填 
        可选值:  
            redis 
            sds 
    $action: 
        含义:要监测的服务的动作 
        参数在url中的位置: segment5 
        必填 
        可选值范围 
            for sds: 
                scan,get,set 
            for redis: 
                get 
                set 
                目前没有区分get和set,无论写get还是set,都会同时监控get和set的可用性 
    (:all)为 querystring,可以包含以下内容: 
        reciever: 
            含义:邮件接受者的email地址 
            参数在url中的位置:  querystring 
            可选参数,如不填,则只发给cloude@smartdevices.com.cn,填的话,额外发给这个地址 
        address: 
            含义: 服务地址. 
            参数在url中的位置:  querystring 
            必填性: 目前只针对redis有效,且必填, 
        port 
            含义: 服务端口 
            参数在url中的位置:  querystring 
            必填性: 目前只针对redis有效,且必填
示例: 
-----
    监控redis的get和set操作:  
        http://localhost:8046/monitor/srv/redis/action/set?address=127.0.0.1&port=6379 
    监控sds的set操作,并附加一个收件人:  
        http://yoursite.mi-ae.com.cn/monitor/srv/sds/action/set?reciever=yourname@smartdevices.com.cn 

 
