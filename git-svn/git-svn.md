# 预备
  1. 安装[SVN Server](https://www.visualsvn.com/server/download/)
  1. 安装[SVN Client](http://rj.baidu.com/soft/detail/17682.html)
  1. 安装[Git Client](https://git-scm.com/downloads)

# 练习——git基本操作
1. 初始化git仓库
`
git init
`
1. 手动添加代码文件
1. 加入git文件监控
`
git add .
`
1. 创建新提交
`
git commit -m "add something"
`
1. 查看提交历史
`
git log
`

# 练习——git操作标准布局svn仓库
1. 在SVN Server上创建标准布局项目代码仓库
1. 使用git修改并提交代码到SVN Server
      ```
      git svn init <svn-url-without-trunk-directory> -s
      git svn fetch
      ```
      手动修改任意文件
      ```
      git add .
      git commit -m "add something"
      git svn dcommit
      ```

1. 查看SVN仓库历史

# 练习——git操作非标准svn仓库
1. 在SVN Server上创建一个空项目代码仓库
1. 在SVN Server创建一次提交
1. 使用git修改并提交代码到SVN Server
    ```
    git svn init <svn-url-without-trunk-directory>
    git svn fetch
    ```
    修改文件

    ```
    git add .
    git commit -m "add something"
    git svn dcommit
    ```
