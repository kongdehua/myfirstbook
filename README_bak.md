# 如何利用Github+GitBook发布一本新书

如果熟用Markdown和Github，那么利用Gitbook搭建一本属于自己的在线书籍易如反掌。完成后的效果如下：

```
1. markdown语法。一点基础都没有，网上教程很容易
2. github账号
```

## 第一步：在github上创建一个仓库
## 第二步：创建summary.md文档
  SUMMARY.md的重要性体现在gitbook通过这个文件来生成整本书的目录。可以如下借鉴代码生成自己的目录。

```
  * [Introduction](README.md)
  * [预备周](ch0/preface.md)
    * [检索操作](ch0/find.md)
  * [第一讲：从现实问题到学科信息](ch1/preface.md)
    * [检索操作](ch1/find.md)
  * [第二讲：从现实问题到学科信息](ch2/preface.md)
    * [检索操作](ch2/find.md)
  * [备注](ps/handbooks.md)
    * [个人教程](ch2/find.md)
  * [参考文献](ps/handbooks.md)
```
## 第三步：登录gitbook，选择用githubz账号登录
  授权登录，创建organiztion，然后Create a new space。
  整个gitbook就好像是一个大书库，一个organization就是一个主题，而space是某一类别里面的书。当然只要知道一个gitbook可以包含多个organization，一个organization可以包含多个space。
  一直点击Next，到达最后的页面。
## 



