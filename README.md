# Beats:
   codec:默认plain

   prot: 端口必填没有默认值

   host: ip地址，默认 0.0.0.0
   
   addFields: 需要添加的属性，map 结构

# Kafka:
   encoding:编码 默认 utf8

   codec:默认plain
 
   topic:必填，map结构，需要说明分区数（{dt_all_test_log: 6}）

   consumerSettings:必填 consumer 连接kafka的属性配置，map结构 {group.id: jlogstashvvvvv,zookeeper.connect: 127.0.0.1:2181,auto.commit.interval.ms:"1000",auto.offset.reset: smallest}

   addFields: 需要添加的属性，map 结构
   
# KafkaDistribute:
   encoding:编码 默认 utf8

   codec:默认plain
 
   topic:必填，map结构，需要说明分区数（{dt_all_test_log: 6}）

   consumerSettings:必填 consumer 连接kafka的属性配置，map结构 {group.id: jlogstashvvvvv,zookeeper.connect: 127.0.0.1:2181,auto.commit.interval.ms:"1000",auto.offset.reset: smallest}
   
   addFields: 需要添加的属性，map 结构 
   
  distributed: map结构，属性值不为空 说明要开启分布式（主要的应用场景是单个文件日志无序，有单行，有多行，需要后台做聚合和解析，需要把同一个日志发送     到同一台服务器）每种日志需要定制化开发聚合规则，现在的版本里有cms1.8 gc log 的日志聚合规则
    样本: {"zkAddress":"127.0.0.1:2181/distributed","localAddress":"127.0.0.1:8555","hashKey":"%{tenant_id}:%                {hostname}_%{appname}_%{path}"}
   
     
# Netty:
  codec:默认plain

  prot: 端口必填没有默认值

  host: ip地址，默认 0.0.0.0

  encoding:编码 默认 utf8

  codec:默认plain

  receiveBufferSize:接收缓存区大小 默认值20M

  delimiter:数据的分隔符 默认是根据系统的换行分隔符

  addFields: 需要添加的属性，map 结构
  
  whiteListPath: ip白名单路径（多个用逗号隔开）
  
  isExtract: true|false是否开启解压功能（gzip）

# Tcp:
  
  codec:默认plain

  prot: 端口必填没有默认值

  host: ip地址，默认 0.0.0.0

  encoding:编码 默认 utf8

  bufSize: 接收缓存区大小 默认值20M

  maxLineLength:一次接收最大的数据包大小 默认1M

  addFields: 需要添加的属性，map 结构

# Stdin:
  标准输入
  addFields: 需要添加的属性，map 结构


# File:
 addFields: 需要添加的属性，map 结构

 path:文件输入路径(可以是文件,文件夹),参数类型为list["home/admin/ysq.log"]

 pathcodecMap: 文件路径,参数是Map类型(key:文件路径,value:该文件类型对应的codec)

 --注意path参数和pathcodecMap参数不能同时为空

 exclude:排除文件路径(可以是文件,文件夹),参数类型为list

 encoding:读取文件的编码格式,默认是UTF-8

 maxOpenFiles:最大配置读取文件数量,默认为0(表示无上限)

 startPosition: 文件开始读取位置,["beginning", "end"],默认为end

 sinceDbPath:文件读取位置信息存储位置,默认"./sincedb.yaml"

 sinceDbWriteInterval:文件读取位置信息刷新到存储点的时间间隔,默认是15s

 delimiter:行分割符号,默认是'\n'

 readFileThreadNum:文件读取的线程数,默认是:cpu处理器数+1
 
 # Redis:
 host:redis服务主机地址
 
 key:键值，当data_type为channel或者channel_pattern时表示订阅的频道
 
 data_size:数据数量，只有当data_type为list和sorted_set时有效
 
 data_type:数据格式，取值范围为：string,list,set,sorted_set,hash,channel,channel_pattern,其中channel和channel_pattern表示订阅模式下所监听的频道
