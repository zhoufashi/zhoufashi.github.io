##### 一、表级锁定：
读锁定：使用 LOCK TABLES 语句可以锁定一个或多个表格，直到当前会话结束或使用 ```UNLOCK TABLES```解锁。例如：

``` LOCK TABLES table_name READ; ```
写锁定：使用 LOCK TABLES 语句并指定 WRITE 关键字可以锁定一个或多个表格，直到当前会话结束或使用 UNLOCK TABLES 解锁。例如：
``` LOCK TABLES table_name WRITE; ```

###### 行级锁
- 在事务中使用 SELECT ... FOR UPDATE 语句可以锁定选定行，直到事务结束为止
```
START TRANSATCTION;
SELECT * FROM table_name WHERE condition FOR UPDATE;
--对选定行进行操作
COMMIT;
```
- 或者使用 SELECT ... FOR SHARE 语句可以锁定选定行，但是允许其他会话也可以读取这些行
```
START TRANSACTION;
SELECT * FROM table_name WHERE condition FOR SHARE;
-- 对选定行进行操作
COMMIT;
```
[返回](../) 