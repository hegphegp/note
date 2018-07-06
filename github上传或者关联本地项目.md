# github关联本地项目

### 装好git软件后的第一步
```
git config --global user.name hgp
git config --global user.email xxxx@xx.com
git config --list
# 查看系统config
git config --system --list
# 查看当前用户（global）配置
git config --global --list
# 查看当前仓库配置信息
git config --local --list
```

```
# 一般来说创建项目的逻辑是：先用编辑器在本地创建项目，然后关联线上的GitHub仓库
# 注意以下几点
# 1) GitHub创建的空项目不要带 README.md 文件，该文件在本地编辑器创建上传比较好
# 2) GitHub创建的项目不要创建 .gitignore 文件, IntelliJ IDEA创建的项目会自动创建 .gitignore 文件
# 先在本地创建项目，再到本地项目用 git init 命令初始化
git init    # 初始化本地
# 本地的就不做任何的git操作
git remote add origin git@github.com:xxx/xxxx.git
git pull origin master # 从github到本地
git add .
git status
git commit -m "first"
git push origin master
```