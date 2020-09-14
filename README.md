[![Netlify Status](https://api.netlify.com/api/v1/badges/91174f7d-c24c-4fbe-92be-8eea0af51b61/deploy-status)](https://app.netlify.com/sites/py-101-camp/deploys)

# py101camp
> 蟒营: Python 入门班官网

## 背景

- `蟒营: Python 入门原型班` 马上成功毕业了
- 新一期课程也开始优化, 重启发布在际
- 原先纯通过朋友间推荐, 效果不错
- 但是, 没有正式官网的课程太不嗯哼了

## 分析

- 因为课程主体在课程社区仓库以及配套环境中进行
- 官网只需要一个简洁的关键信息阐述即可
- 核心要求:
    + 不丑
    + 用 `.md` 来维护内容
    + 用 `*-pages` 来免费发布
    + 有稳定的评论功能
    + 通过 git 进行协同

## 方案
> [SSGs](https://about.gitlab.com/2016/06/03/ssg-overview-gitlab-pages-part-1-dynamic-x-static/) 没跑了...


对比体验:

- [Top Ten Static Website Generators | Netlify](https://www.netlify.com/blog/2016/05/02/top-ten-static-website-generators/)
- [myles/awesome-static-generators: A curated list of static web site generators.](https://github.com/myles/awesome-static-generators)
- [pinceladasdaweb/Static-Site-Generators: A definitive list of tools for generating static websites.](https://github.com/pinceladasdaweb/Static-Site-Generators#lua)
- [StaticGen | Top Open Source Static Site Generators](https://www.staticgen.com/)
- [Static Site Generators](https://staticsitegenerators.net/)
- ...


## 追踪:
发现:

- 多数是 blog-style , 文档/官网类的不多
- 咱是 Python 课程, 当然只能用 Python 开发的了
- 以历史/文档/社区活性/成熟/星数/... 一系列综合考虑
- 选择了: [MkDocs](https://www.mkdocs.org/)

配置:

- 文档学习, 本地试用
- theme 选择...(这个最费时间)
- gl-pages 先部署, 发现反应太慢慢, DNS 配置好要半天才反应的过来
- 切回 gh-pages 的确非常快, 也简洁很多
- 就是有个问题:
    + 只支持 master 分支/ docs 目录 两种渠道发布
    + 而 MkDocs 不能配置指定编译输出目录
- 所以, 使用两个仓库配合维护:

> 190323 发现有 diss 隐患, 以下仓库删除:

    + 内容: [101camp/py101camp: Python 入门班官网](https://github.com/101camp/py101camp)
    + 发布: [101camp/py.101.camp: gh-pages -> 101camp/py101camp ->](https://github.com/101camp/py.101.camp)

>> 190323 紧急切换为以下流程

- 内容: `Private`[PythoniCamp / running / py.101.camp · GitLab](https://gitlab.com/pythonicamp/running/py.101.camp)
- 发布: `Private`[ZoomQuiet/ghpy101camp: py.101.camp pages public](https://github.com/ZoomQuiet/ghpy101camp)
- 评注: [Issues · 101camp/comments](https://github.com/101camp/comments/issues)


- 用本地 fabric2(inv 工具) 编写的自动化脚本来完成:
    + 编译
    + 资源同步
    + git 提交


> ༄  inv -l

    Available tasks:

      bu
      ccname
      gh
      pu
      pub
      sync4media

> ༄  inv pub


> ༄  inv pub


    /opt/data/Sites/101.camp/_running/gl_py.101.camp
    INFO    -  Cleaning site directory
    INFO    -  Building documentation to directory: /opt/data/Sites/101.camp/_running/gl_py.101.camp/site
    /opt/data/Sites/101.camp/_running/gl_py.101.camp
    On branch master
    Your branch is up-to-date with 'origin/master'.

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")
    [master 25d50e9] 👌 IMPROVE: inv(loc) MkDocs upgraded by DAMA (at 190325 1206 46.232)
     1 file changed, 16 insertions(+), 4 deletions(-)
    To gitlab.com:pythonicamp/running/py.101.camp.git
       7b44f49..25d50e9  master -> master

    ...


    no changes added to commit (use "git add" and/or "git commit -a")
    [master d0387e5] 👌 IMPROVE: pub(site) gen. by MkDocs as invoke (at 190325 1206 49.111)
     3 files changed, 4 insertions(+), 4 deletions(-)
    To github.com:ZoomQuiet/ghpy101camp.git
       1d94dcc..d0387e5  master -> master


- 访问:
    + https://py.101.camp/
    + https://www.101.camp/ (暂时指向 101.camp, 到课程发布时,指回 py.101.camp)

## 是也乎:


- 200911 ZoomQuiet 增补 Netlify badges 
- 190325 DAMA 增补说明文档
- 190324 DAMA 紧急 black-box 化内容维护过程
- 190321 内部发布
    + .5h 模板定制, 追加 utterances 作为评论功能
    + .5h 模板定制, 调整 logo/icon/许可证声明
    + 1.5h 首页内容撰写
    + .5h 运维文档增补
- 190320 临时方案
    + .5h 引擎选择
    + 1h theme 选择
    + .5h 仓库初始化/并发布
- 190315 初稿
- 190313 动议
