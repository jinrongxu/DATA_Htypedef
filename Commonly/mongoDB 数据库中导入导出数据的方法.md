### MongoDB导出数据
[toc]
```
mongoexport -d 数据库名 -c 集合名 -o
```
 导出的地址及文件名称

```
mongoexport -d 1610C -c billList -o ./billList.json
```

参数说明
- -d 指明使用的库, 本例中为 ” 1610C ”
- -c 指明要导出的表, 本例中为 ”billList”
- -o 指明要导出的文件名, 本例中为 ”billList.json”

#### MongoDB导入数据

```
mongoimport -d 数据库名 -c 集合名
```
 导出的地址及文件名称

 
```
mongoimport -d 1610C -c bill_list ./billList.json
```


参数说明
- -d:指明数据库名，本例中为"1610C "
- -c:指明collection名，本例中为"bill_list "
- billList.json：导入的文件名

#### 命令操作：
在当前需要导出的目录位置<br>
shift + 右键 打开powershell窗口执行如上命令