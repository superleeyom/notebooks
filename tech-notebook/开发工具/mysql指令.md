# mysql指令

- 登录 MySQL：`mysql -u用户名 -h地址 -p密码`
- 导出某个表：`mysqldump -h IP地址 -u用户名 -p 数据库名 表名 > /home/hadoop/表名.sql`
- 导出库结构：`mysqldump -h IP地址 -u用户名 -p --no-data --ignore-table=忽略导出的表 数据库名 > /home/hadoop/表名.sql`
- 导出库数据：`mysqldump -h IP地址 -u用户名 -p -c -t -e --ignore-table=忽略导出的表 数据库名 > /home/hadoop/表名.sql`
- 退出：`exit;`

# 函数
- 判断字符串（string）中是否包含另一个字符串（subStr）：`locate(subStr,string)`
    - 示例：`locate(subStr,string) > 0`