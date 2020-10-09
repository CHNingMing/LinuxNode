## Spring FTP依赖:

```xml
<dependency>
    <groupId>org.springframework.integration</groupId>
    <artifactId>spring-integration-ftp</artifactId>
</dependency>
```





### FtpRemoteFileTemplate列出文件出现乱码解决 ：

在创建DefaultFtpSessionFactory的时候,调用setControlEncoding函数设置一下编码格式:

```
FtpProperty ftpProperty = getFtpInfo(url);
		DefaultFtpSessionFactory sf = new DefaultFtpSessionFactory();
		//设置服务器编码格式
      	sf.setControlEncoding("GB2312");//GB2312 | UTF-8 | GBK | ISO8859-1
		sf.setHost(ftpProperty.getHost());
		sf.setPort(ftpProperty.getPort());
		sf.setUsername(ftpProperty.getUsername());
		sf.setPassword(ftpProperty.getPassword());
		sf.setClientMode(FTPClient.PASSIVE_LOCAL_DATA_CONNECTION_MODE);
		SessionFactory<FTPFile> ftpSessionFactory = new CachingSessionFactory<FTPFile>(sf);
		FtpRemoteFileTemplate fileTemplate = new FtpRemoteFileTemplate(ftpSessionFactory);
```



