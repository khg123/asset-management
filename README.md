# 固定资产管理系统

## 项目简介

固定资产管理系统是一款基于Flask框架开发的企业级资产管理解决方案，旨在帮助企业高效管理固定资产全生命周期，包括资产登记、借用归还、查询统计等功能。

## 功能特性

### 核心功能
- **资产管理**：资产添加、编辑、删除、详情查看
- **资产借用归还**：闲置资产借用、借用资产归还
- **资产查询**：多条件组合查询、资产状态筛选、资产年限筛选
- **基础设置**：类别管理、部门管理、用户管理
- **操作日志**：自动记录资产相关操作
- **数据导入导出**：支持Excel格式导入导出

### 技术特性
- **响应式设计**：适配不同屏幕尺寸
- **权限管理**：基于角色的访问控制
- **数据安全**：密码加密存储、操作日志记录
- **用户友好**：直观的界面设计、完善的错误提示

## 技术栈

- **后端**：Python 3.9+, Flask 2.0+, SQLAlchemy
- **前端**：HTML5, CSS3, JavaScript, Bootstrap 3
- **数据库**：MySQL/MariaDB
- **认证**：Flask-Login, Passlib
- **表单处理**：Flask-WTF, WTForms

## 快速开始

### 环境要求
- Python 3.9 或更高版本
- MySQL 5.7 或 MariaDB 10.0 或更高版本
- 操作系统：Windows, Linux, macOS

### 安装步骤

1. **克隆项目**
   ```bash
   git clone <repository-url> asset-management
   cd asset-management
   ```

2. **创建虚拟环境**
   ```bash
   # Linux/Mac
   python3 -m venv venv
   source venv/bin/activate
   
   # Windows
   python -m venv venv
   venv\Scripts\activate
   ```

3. **安装依赖**
   ```bash
   pip install -r requirements.txt
   ```

4. **配置环境变量**
   创建 `.env` 文件：
   ```
   SECRET_KEY=your-secret-key
   DATABASE_URI=mysql+pymysql://root:password@localhost/asset_management
   ```

5. **初始化数据库**
   ```bash
   # 启动数据库服务
   # 创建数据库
   mysql -u root -p -e "CREATE DATABASE asset_management CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
   
   # 初始化表结构
   python -c "from app import app, db; with app.app_context(): db.create_all()"
   ```

### 运行项目

```bash
# 开发模式
python app.py

# 访问地址
# http://localhost:5000
```

## 系统功能

### 资产管理
- **资产列表**：查看所有资产信息
- **添加资产**：录入新资产信息
- **编辑资产**：修改现有资产信息
- **删除资产**：移除不需要的资产
- **资产详情**：查看资产详细信息和操作日志

### 资产借用归还
- **资产借用**：选择闲置资产进行借用
- **资产归还**：归还已借用的资产
- **借用记录**：查看历史借用记录

### 资产查询
- **多条件查询**：资产编号、部门、使用人等条件组合查询
- **状态筛选**：闲置、在用、借用中状态筛选
- **年限筛选**：超5年、超10年资产筛选

### 基础设置
- **类别管理**：添加、编辑、删除资产类别
- **部门管理**：添加、编辑、删除部门信息
- **用户管理**：添加、编辑、删除用户，设置用户角色

## 目录结构

```
asset-management/
├── app.py              # 主应用文件
├── requirements.txt    # 依赖包配置
├── README.md           # 项目说明
├── .env                # 环境变量配置（本地开发）
├── static/             # 静态文件
│   └── images/         # 图片资源
└── templates/          # 模板文件
    ├── dashboard.html  # 主页面
    ├── login.html      # 登录页面
    └── ...             # 其他模板文件
```

## 配置说明

### 环境变量配置 (`./.env`)

| 配置项 | 说明 | 默认值 |
|-------|------|-------|
| SECRET_KEY | 应用密钥，用于加密会话数据 | dev-secret-key |
| DATABASE_URI | 数据库连接字符串 | mysql+pymysql://root:password@localhost/asset_management |

### 数据库表结构

- **users**：用户信息
- **categories**：资产类别
- **departments**：部门信息
- **assets**：资产信息
- **asset_borrows**：资产借用记录
- **asset_transfers**：资产移交记录
- **asset_logs**：操作日志

## 部署指南

### 开发环境部署
参考「快速开始」部分的步骤。

### 生产环境部署

1. **服务器准备**
   - Ubuntu 20.04 LTS 或 CentOS 8
   - 2GB 内存以上
   - 50GB 磁盘空间以上

2. **安装必要软件**
   ```bash
   # Ubuntu
   sudo apt install -y python3 python3-pip nginx mysql-server
   
   # CentOS
   sudo yum install -y python3 python3-pip nginx mariadb-server
   ```

3. **配置 Gunicorn**
   ```bash
   pip install gunicorn
   ```

4. **配置 Nginx**
   创建 Nginx 配置文件，设置反向代理到 Gunicorn。

5. **创建系统服务**
   创建 Systemd 服务文件，管理应用进程。

详细部署步骤请参考项目文档。

## 常见问题

### 1. 数据库连接失败
- 检查 `.env` 文件中的数据库连接字符串
- 确认数据库服务是否运行
- 验证数据库用户名和密码是否正确

### 2. 资产借用后状态未更新
- 检查资产借用表单是否正确提交
- 确认数据库中资产状态字段是否更新

### 3. 导入Excel文件失败
- 确认Excel文件格式是否正确
- 检查表头是否与模板一致
- 验证必填字段是否填写

### 4. 导出Excel文件格式问题
- 确认是否安装了 openpyxl 依赖
- 检查导出文件是否被其他程序占用

## 许可证

本项目采用 MIT 许可证。详见 LICENSE 文件。

## 联系方式

如有问题或建议，欢迎通过以下方式联系：
- 邮箱：your-email@example.com
- GitHub：<https://github.com/yourusername/asset-management>

---

**版本信息**：v1.0.0
**最后更新**：2026-01-29