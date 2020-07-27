# Logback















































# 坑:

- Logback 配置好日志输出文件后不输出情况: 
  - logback 和 log4j冲突(冲突后控制台会提示)
  - 查看配置文件,配置路径是否重复
  - [已载进去] logback 配置文件(resouce下logback.xml配置有问题),控制台不会报错。- -