# Welcome to my world!
For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Github command--How to make changes
本地已有代码，需推送到现有远程仓库
```bash
cd ~/myproject
git init   # 执行后无特殊输出，可通过ls -a查看是否生成.git目录
git add .  # 执行后无输出，或显示新增/修改的文件列表
git commit -m "<Initial commit>"  # 输出提交摘要
git remote add origin git@github.com:Gaiake/gaiake.github.io.git
git push -u origin main  # 输出推送进度和结果
```
本地无代码，需要克隆远程仓库到本地，再修改并推送
```bash
git clone git@github.com:Gaiake/gaiake.github.io.git
cd gaiake.github.io
git add .
git commit -m "<Update index.html>" 
git push 
```
推送完成后，第一个办法是使用以下命令在本地仓库site/目录下生成.html文件并推送到gh-pages分支。注意本地仓库中的site/.html需要及时删除修改
```bash
source venv/bin/activate
mkdocs gh-deploy
deactivate
```

第二个办法是配置github workflows，方法如下

```bash
source venv/bin/activate
mkdir -p .github/workflows
touch .github/workflows/deploy.yml
deactivate
```
将下面的配置内容复制到 deploy.yml 中
```yaml
name: Deploy to GitHub Pages

permissions:
  contents: write

on:
  push:
    branches:
      - main  # 主分支有提交时触发部署

jobs:
  deploy:
    runs-on: ubuntu-latest  # 使用 Ubuntu 环境
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
        
      - name: Set up Python
        uses: actions/setup-python@v3
        with:
          python-version: 3.9
          
      - name: Install dependencies
        run: |
          pip install mkdocs mkdocs-material mkdocs-glightbox  # 安装 mkdocs、主题和 glightbox 插件
          
      - name: Build and deploy
        run: |
          mkdocs gh-deploy --force  # 执行部署，--force 覆盖旧提交
          
      - name: Clean up (确保本地不残留)
        run: |
          rm -rf site/  # 手动删除可能生成的 site/ 目录
```
提交，在Github Actions查看workflow亮起绿灯即可查看主页
