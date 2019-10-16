# java-interview-guide
### java面试指南

### 使用hugo完成页面制作
- 安装hugo（extension）
- 添加主题hugo-book（theme文件夹下）
- content/docs文件夹下填写内容，左侧菜单按照文件夹层级生成，每个文件夹都是一个菜单，默认_index.md文件，title决定展示的标题
- menu文件夹下填写左侧菜单跳转链接
- 本地调试命令：hugo server --theme=book
- 打包发布：hugo --theme=book，在public目录下生成目标文件，上传至gitpage即可访问
