# fake_excel_generator

---

# [fake_excel_generator]
「基于 Django 开发的 Excel生成假数据工具，适配 Python 3.8+」

## 快速开始
### 1. 环境准备
#### 1.1 安装依赖
```bash
# 克隆仓库
git clone https://github.com/xiaofuz/fake_excel_generator.git
cd fake_excel_generator

# 安装依赖（建议先创建虚拟环境）
# 创建虚拟环境（可选但推荐）
python -m venv venv
# 激活虚拟环境
# Windows
venv\Scripts\activate
# Mac/Linux
source venv/bin/activate

# 安装Django及项目依赖
pip install -r requirements.txt

##### 步骤1：重建/初始化数据库
```bash
# 1. 生成数据库迁移文件（根据models.py创建表结构）
python manage.py makemigrations

# 2. 执行迁移，创建数据库及表（核心：重建被删除的数据库）
python manage.py migrate

# 3.创建超级管理员（用于登录Django后台）
python manage.py createsuperuser
# 按提示输入用户名、邮箱、密码即可
```

### 2. 运行项目
```bash
# 启动Django开发服务器
python manage.py runserver

# 启动后访问以下地址：
# 项目首页：http://127.0.0.1:8000/
# Django后台管理：http://127.0.0.1:8000/admin/（需先创建超级管理员）
```

## 常见问题
### Q1：执行 migrate 时报错「no such table」？
A1：先删除 `migrations` 文件夹下除 `__init__.py` 外的所有文件，再重新执行：
```bash
python manage.py makemigrations
python manage.py migrate --fake-initial  # 兼容首次迁移
```

### Q2：数据库文件删除后，数据丢失怎么办？
A2：SQLite 是文件型数据库，删除 `db.sqlite3` 后数据无法恢复，建议定期备份：
```bash
# 备份数据库（Windows）
copy db.sqlite3 db_backup.sqlite3
# Mac/Linux
cp db.sqlite3 db_backup.sqlite3
```

### Q3：想切换为 MySQL/PostgreSQL 怎么办？
A3：修改 `settings.py` 中的 `DATABASES` 配置，示例（MySQL）：
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '[你的数据库名]',
        'USER': '[数据库用户名]',
        'PASSWORD': '[数据库密码]',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
```
需额外安装依赖：`pip install mysqlclient`
---

V:myzytop
邮箱：981276532@qq.com

如果对你有帮助，您的支持是我最大的动力。
在线
| 截图1 | 截图2 |
| :---: | :---: |
| ![Clipboard - 2026-02-09 14 00 37](https://github.com/user-attachments/assets/def710c1-091e-4ad8-b835-21ba4b5b88a1) | ![Clipboard - 2026-02-09 14 00 24](https://github.com/user-attachments/assets/43a64312-a275-4923-9e43-3489d5b13ae3) |

