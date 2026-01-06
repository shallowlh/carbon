## Carbon
## 下载jdk8，配置环境变量
## 下载redis，配置启动
## 下载mysql （本后端项目使用的 MySQL 账号配置为root@%）
## 方法1
-- 1. 创建root@%用户（密码与root@localhost一致，123456）
      CREATE USER 'root'@'%' IDENTIFIED BY '123456';
-- 2. 授予和root@localhost完全相同的权限
      GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
-- 3. 刷新权限使配置生效
      FLUSH PRIVILEGES;
## 方法2
--修改后端数据库连接配置，将原本指向root@%的连接改为使用本地有效的root@localhost。
## 用 Navicat 可视化工具 
--打开 Navicat，连接你的 MySQL（输入主机localhost、端口 3306、用户名root、密码）。
  右键点击 “数据库”→“新建数据库”：
  数据库名填carbon
  字符集选utf8mb4（脚本里用的是 utf8mb4）
  排序规则选utf8mb4_general_ci
  选中新建的carbon数据库，右键→“运行 SQL 文件”，选择项目里的carbon.sql，点击 “开始”，等待脚本执行完成。
## 下载IDEA，连接数据库，配置maven，jdk
## 打开bin，双击run，