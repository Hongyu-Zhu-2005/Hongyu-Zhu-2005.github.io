# 个人主页修改指南

这个仓库使用 Jekyll 和 al-folio。编辑源文件后，可以先在电脑上预览，确认无误再推送到 GitHub。

## 1. 启动本地预览

打开“终端”，运行：

```bash
cd /Users/steven/Desktop/Hongyu_Zhu.github.io
bundle exec jekyll serve --livereload
```

浏览器打开 <http://127.0.0.1:4000/>。终端保持打开；结束预览时按 `Control + C`。多数内容修改会自动刷新。修改 `_config.yml` 后，按 `Control + C` 停止，再运行一次启动命令。

如果出现依赖缺失，可以在仓库目录运行 `bundle install`。不需要为这个项目安装 Docker。

## 2. 常改的文件

| 内容                 | 文件                           | 做法                                                                              |
| -------------------- | ------------------------------ | --------------------------------------------------------------------------------- |
| 首页文字、头像旁信息 | `_pages/about.md`              | 修改第二个 `---` 以下的正文，以及 `subtitle`、`profile.more_info` 等字段          |
| 头像                 | `assets/img/prof_pic.jpg`      | 用自己的照片替换同名文件；若改文件名，同时改 `_pages/about.md` 的 `profile.image` |
| 网站标题、姓名、描述 | `_config.yml`                  | 修改文件开头的 `title`、`first_name`、`last_name`、`description`                  |
| 邮箱和社交链接       | `_data/socials.yml`            | 删除示例链接，填写自己的信息；不需要的行可删除或在行首加 `#`                      |
| 简历                 | `_data/cv.yml`、`_pages/cv.md` | 更新经历和 PDF 路径；示例简历目前是 Einstein 的内容                               |
| 项目                 | `_projects/*.md`               | 复制一个项目文件，改标题、描述、封面和正文；删除无用的示例项目                    |
| 论文                 | `_bibliography/papers.bib`     | 填入自己的 BibTeX 条目，删除示例论文                                              |
| 博客文章             | `_posts/YYYY-MM-DD-title.md`   | 以日期命名新文件，写 YAML 头和 Markdown 正文                                      |
| 新闻                 | `_news/*.md`                   | 修改或添加简短动态                                                                |
| 顶部导航             | `_pages/*.md`                  | 页面开头的 `nav: true` 控制是否显示；`nav_order` 控制顺序                         |
| 课程笔记列表         | `_data/course_notes.yml`       | 将 `status` 从 `forthcoming` 改为 `available`，并在 `files` 下添加 PDF 链接       |
| 课程笔记 PDF         | `assets/pdf/course-notes/`     | 把 PDF 放入此目录，再在 `_data/course_notes.yml` 中填写文件路径                   |

`_pages/about.md` 的开头位于两行 `---` 之间，叫作 YAML 头。例如：

```yaml
---
layout: about
title: about
permalink: /
subtitle: 数学系本科生，UNSW
profile:
  align: right
  image: prof_pic.jpg
  image_circular: false
  more_info: >
    <p>联系邮箱：name@example.com</p>
---
这里是首页正文。可以使用 **Markdown 加粗** 和 [链接](https://example.com)。
```

保留 `permalink: /` 才能让这页继续作为首页。YAML 用空格缩进，不要用 Tab。正文可以直接写中文。

### 添加一份课程笔记

先把 PDF 复制到 `assets/pdf/course-notes/`。然后在 `_data/course_notes.yml` 中找到相应条目，改成下面的形式：

```yaml
- title: UNSW MATH3701 course notes
  status: available
  description: Personal course notes for MATH3701 at UNSW.
  files:
    - label: Download PDF
      path: /assets/pdf/course-notes/MATH3701_course_notes.pdf
```

文件名建议只使用英文字母、数字、连字符和下划线。这样推送后，课程笔记页面会自动把该条目从“Forthcoming”移到“Available”。

## 3. 检查并发布

修改后先看本地预览，再在终端运行：

```bash
cd /Users/steven/Desktop/Hongyu_Zhu.github.io
git status
git diff
bundle exec jekyll build
git add _pages/about.md _config.yml _data/socials.yml
git commit -m "Update personal website"
git push origin main
```

`git add` 后面只填写这次实际修改的文件或目录。推送到 `main` 后，仓库的 `Deploy site` GitHub Actions 工作流会重新生成网站。到 GitHub 仓库的 **Actions** 页面确认它成功，再查看线上主页。

如果构建失败，先读终端末尾的错误信息；`git status` 可以查看哪些文件还没有提交。项目的详细英文文档在 `docs/CUSTOMIZE.md` 和 `docs/INSTALL.md`。
