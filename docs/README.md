# Welcome to my world!
For full documentation visit [mkdocs.org](https://www.mkdocs.org).

$$a\in b$$
## Github command--How to make changes
#### 已有 GitHub 仓库（只需同步代码）
- 本地已有代码，需推送到现有远程仓库
```
cd ~/myproject
git init   # 执行后无特殊输出，可通过ls -a查看是否生成.git目录
git add .  # 执行后无输出，或显示新增/修改的文件列表
git commit -m "<Initial commit>"  # 输出提交摘要
git remote add origin git@github.com:Gaiake/gaiake.github.io.git
git push -u origin main  # 输出推送进度和结果
```
- 本地无代码，需要克隆远程仓库到本地，再修改并推送
```
git clone git@github.com:Gaiake/gaiake.github.io.git
cd gaiake.github.io
git add .
git commit -m "<Update index.html>" 
git push 
```
推送完成后，使用以下命令修改pages
```
source venv/bin/activate
mkdocs gh-deploy
deactivate
```
