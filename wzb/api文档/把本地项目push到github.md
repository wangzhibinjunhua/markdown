# 如何把本地项目上传到github
## 1.生成ssh key
- `ssh-keygen -t rsa -C "wangzhibin_x@foxmail.com"`
- 可以一路回车,不用设置密码
- 将生成的key加入到github上


## 2.github新建一个repository example

## 3.git remote add origin git@github.com:ooxx/exmaple.git
- git push -u origin master