# java-architect-atlas
java架构师图谱



java-architect-atlas
	分布式
		数据一致性
		子主题 2
	微服务
		服务雪崩效应
			形成原因
				服务提供者不可用
					硬件故障
					程序BUG
					缓存击穿
					请求暴增
				重试加大流量
					用户触发重试
					代码逻辑重试
				服务调用者不可用
					同步调用，同步等待造成处理线程池资源耗尽，导致调用者的其他服务也处于不可用状态，引发雪崩
			应对策略
				流量控制
					网关限流：nginx+lua, openResty
					用户交互限流：增加等待动画，提交按钮添加强制等待时间
				改进缓存模式
					缓存预加载
					同步改成异步刷新
				服务自动扩容
				服务调用者降级服务
					资源隔离
						处理线程池隔离
					快速失败
						超时机制
						熔断器 & 熔断后的降级方法
			开源工具
				netflix的hystrix
					资源隔离：为每个依赖的服务分配独立的线程池进行资源隔离
					熔断器：通过metrics统计服务健康状态，来控制熔断器的打开和关闭
					命令模式：代理服务的接口，配合熔断器来调用 run() 或者 getFallback()
				alibaba的sentinal