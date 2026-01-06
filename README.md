## Carbon
## 下载jdk8，配置环境变量
详细安装步骤[JDK](https://www.bilibili.com/video/BV1uf48eFEkd/?spm_id_from=333.1391.0.0&vd_source=9c1dfb7f27c6eba1c15f9577bc0ce9aa)
## 下载redis，配置启动
详细安装步骤[redis](https://www.bilibili.com/video/BV1njEczKEas/?spm_id_from=333.337.search-card.all.click&vd_source=9c1dfb7f27c6eba1c15f9577bc0ce9aa)
## 下载mysql （本后端项目使用的 MySQL 账号配置为root@%）
详细安装步骤[mysql](https://www.bilibili.com/video/BV12q4y1477i/?spm_id_from=333.337.search-card.all.click&vd_source=9c1dfb7f27c6eba1c15f9577bc0ce9aa)
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
## 下载IDEA，配置maven，jdk详细安装步骤(https://www.bilibili.com/video/BV1P5bWzAEam/?spm_id_from=333.337.search-card.all.click&vd_source=9c1dfb7f27c6eba1c15f9577bc0ce9aa)
## 打开IDEA链接mysql选择carbon框架
## 打开carbon项目，点击bin目录，右键run.bat运行
## 打开carbon项目，点击neu-carbon-mapper\srs\main\resources\mapper\carbonReport,查看VMesEquipmentPowerDetailMapper.xml和VMesProductPowerDetailMapper.xml
--在VMesEquipmentPowerDetailMapper.xml下selectVMesEquipmentPowerDetailList里修改GROUP BY为GROUP BY equipment_id, equipment_name, plan_id, bom_id, order_id, product_date, material_id, process_id, product_line_id, power_consume, process_name, product_line_name
--在VMesProductPowerDetailMapper.xml下selectVMesProductPowerDetailList里修该GROUP BY为GROUP BY plan_id, bom_id, order_id, product_date, material_id, process_id, product_line_id, power_consume, process_name, product_line_name, material_name, material_model, material_specification, material_unit
## 在VWmsMaterialInventoryDetailServiceImpl.java下
     /**
     * 新增私有方法：计算单条库存数据的预警状态
     * 核心逻辑：对比当前库存与上下限，设置状态码和状态名称
     */
## 在VWmsMaterialInventoryDetailMapper.xml下修改sql      
     <sql id="selectVWmsMaterialInventoryDetailVo">
        SELECT
        t.wh_id,
        t.wh_region_id,
        t.wh_location_id,
        SUM(t.inventory) inventory,
        SUM(t.lock_inventory) lock_inventory,
        ANY_VALUE(t.batch_no) batch_no,
        ANY_VALUE(t.manufacturer) manufacturer,
        t.material_id,
        ANY_VALUE(t.max_inventory) max_inventory,
        ANY_VALUE(t.min_inventory) min_inventory,
        ANY_VALUE(t.material_name) material_name,
        ANY_VALUE(t.material_model) material_model,
        ANY_VALUE(t.material_specification) material_specification,
        ANY_VALUE(t.material_unit) material_unit,
        ANY_VALUE(t.wh_name) wh_name,
        ANY_VALUE(t.wh_region_name) wh_region_name,
        ANY_VALUE(t.wh_location_name) wh_location_name
        FROM
        v_wms_material_inventory_detail t
    </sql>