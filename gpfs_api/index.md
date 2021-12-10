# GPFS API文档



<!--more-->


```
curl -k -u admin:admin001 -X POST --header 'content-type:application/json' --header 'accept:application/json' -d '{
  "filesetName": "fset007", 
  "path": "/gpfs/fset007", 
  "owner": "sunyh", 
  "permissions": "700"
}' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/filesets'
```



```
curl -k -u admin:admin001 -X POST --header 'content-type:application/json' --header 'accept:application/json' -d '{
  "filesetName": "fset007", 
  "path": "/gpfs/fset007", 
  "owner": "sunyh", 
  "permissions": "700"
}' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/filesets'
```



```
curl -k -u admin:admin001 -X POST --header 'content-type:application/json' --header 'accept:application/json' -d '{
  "filesetName": "fset007", 
  "path": "/gpfs/fset007", 
  "owner": "sunyh", 
  "permissions": "700",
  "inodeSpace": "root"
}' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/filesets'
```



```
curl -k -u admin:admin001 -X GET --header 'accept:application/json' 'https://192.168.1.50:443/scalemgmt/v2/jobs/1000000000013'
```



### 创建文件集

```
curl -k -u admin001:deepbay2010 -X POST --header 'content-type:application/json' --header 'accept:application/json' -d '{ "filesetName": "feitest", "owner" : "root", "path": "/gpfs/feitest", "permissions": "777" }' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/filesets'
```

注释：

filesetName ：文件集名称

owner： 新文件集所有者的用户ID，然后可选地加上组ID，例如“ root：”。 

path：文件集路径

permissions：权限， 相当于使用**chmod**设置的权限 

> tip：创建文件集的时候，path不能存在，否则会创建失败。



### 设置文件集配额

```
curl -k -u admin001:deepbay2010 -X POST --header 'content-type:application/json' --header 'accept:application/json' -d '{"operationType": "setQuota","quotaType": "FILESET","objectName": "feitest","blockSoftLimit": "1G","blockHardLimit": "1G"}' "https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/quotas"
```

注释：

objectName：文件集名称

blockSoftLimit：软限制 （警告）

blockHardLimit：硬限制



### 删除文件集

```
curl -k -u admin001:deepbay2010 -X DELETE --header 'accept:application/json' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/filesets/{feilSetName}'
```

注释：

路径最后为文件集名称

> tip：删除文件集会把该文件集对应路径下的所有文件删除



### 获取指定文件集信息

```
curl -k -u admin001:deepbay2010 -X GET --header 'accept:application/json' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/filesets/{feilSetName}'
```

​	

### 获取简略的所有文件集信息

```
curl -k -u admin001:deepbay2010 -X GET --header 'accept:application/json' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/filesets'
```



### 获取指定文件集配额信息

```
curl -k -u admin001:deepbay2010 -X GET --header 'accept:application/json' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/filesets/{feilSetName}/quotas'
```



### 获取配额使用信息    (所有的文件集)

```
curl -k -u admin001:deepbay2010 -X GET --header 'accept:application/json' 'https://192.168.1.50:443/scalemgmt/v2/filesystems/gpfs/quotas'
```

> tip：等效于 mmrepquota -g -v -a



### 注意事项

- 上传文件超过配额大小时，会中止上传，但是已上传的部分会留在磁盘内，建议删除已上传的部分。
- 不能使用root用户进行文件上传，否则上传配额失效。



gui页面  https://192.168.1.50

官网  https://www.ibm.com/support/knowledgecenter/STXKQY_4.2.3/com.ibm.spectrum.scale.v4r23.doc/bl1adm_apiv2postfilesystemfilesets.htm 

> 版本：4.2.3 ，V2
