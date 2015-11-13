# redis-sentinel

### Redis Sentinel Docker集群方案


#### 1.build<br/>
	build master镜像
	  	docker build -t redis:master .<br/>
	build slave镜像
	  	docker build -t redis:slave .<br/>
	  
#### 2.run<br/>
	
	$:master:docker run -d --name masterredis -p 6379:6379  redis:master /run.sh 
	  
	$:slave:docker run -d --name redisslave1 --link masterredis:masterredis redis:slave /run.sh

	  
#### 3.连接：<br/>

	 $:redis-cli -h ${masterip} -p 6379
	 $:auth dandan
	 $:info Replication
#### 效果展示
<img src="data:image/png;base64,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">
