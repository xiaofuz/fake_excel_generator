# easy

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
# 若没有requirements.txt，直接安装Django
pip install django==[你的Django版本，比如4.2.7]
```

#### 1.2 配置数据库（核心：解决数据库删除/重建问题）
项目默认使用 SQLite（轻量无需额外安装），若误删数据库文件或需重建，按以下步骤操作：

##### 步骤1：确认数据库配置（settings.py）
打开项目根目录下的 `[项目名]/settings.py`，确认数据库配置（默认如下，无需修改）：
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',  # 数据库文件路径，删除后可重建
    }
}
```

##### 步骤2：重建/初始化数据库
```bash
# 1. 生成数据库迁移文件（根据models.py创建表结构）
python manage.py makemigrations

# 2. 执行迁移，创建数据库及表（核心：重建被删除的数据库）
python manage.py migrate

# 可选：创建超级管理员（用于登录Django后台）
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

## 目录结构（可选）
```
[仓库名]/
├── [项目名]/          # 项目核心配置
│   ├── settings.py    # 数据库/全局配置
│   └── urls.py        # 路由配置
├── [应用名]/          # 业务应用
│   ├── models.py      # 数据库模型
│   └── views.py       # 视图逻辑
├── db.sqlite3         # SQLite数据库文件（删除后可通过migrate重建）
└── manage.py          # Django核心管理脚本
```

---

### 总结
1. 核心流程：**环境搭建 → 数据库配置/重建（makemigrations + migrate） → 启动项目**，重点覆盖了数据库删除后的重建操作；
2. 适配新手：包含虚拟环境、常见报错解决方案，无需额外配置复杂的数据库服务；
3. 可拓展：预留了切换 MySQL 的配置示例，后续可根据需求补充。

你只需要替换模板中 `[你的XXX]` 占位符，补充项目的核心功能描述，就能直接用在 GitHub 仓库的 README.md 里了。如果需要针对你的工具功能（比如 RPA/表格处理）定制更贴合的说明，告诉我具体功能，我再帮你调整。
