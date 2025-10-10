# Jekyll + GitHub Pages 个人博客搭建全记录

## 前言

起因是我需要一种集免费、易用以及专注内容的搭建个人博客的方式，经过一番探索和实践，我成功使用 `Jekyll` 和 `GitHub Pages`搭建了个人博客。这篇文章将完整记录从环境搭建到主题配置，再到遇到的问题以及解决的整个过程。

### 为什么选择Jekyll+Github Pages

`Jekyll`是一种基于`Ruby`开发的静态网站生成器。`Jekyll` 的设计哲学就是简单易用。用户只需准备好 `Markdown` 格式的文本文件，`Jekyll` 就能利用模板将它们转化成一个完整的网站。对于博客这类以内容为核心的站点来说非常合适。对于非常大型的项目，`Jekyll`生成速度可能不如用 `Go` 语言编写的 `Hugo` 快。但综合来看，对于个人博客，`Jekyll` 在**易用性、与 GitHub 的集成度以及社区资源**方面，优势非常明显。

`GitHub Pages` 是一项静态站点托管服务，它直接从 `GitHub` 上的存储库获取 `HTML`、`CSS` 和 `JavaScript` 文件，（可选）通过构建过程运行文件，然后发布网站。

`Jekyll` 是 `GitHub Pages` 官方内置支持的静态站点生成器。[Github Pages 官方文档](https://docs.github.com/zh/pages)

## 环境准备（Windows 用户）

### 安装 Ruby 和 Jekyll

1. 安装`Ruby`

从 [ruby下载官网](https://www.ruby-lang.org/en/downloads/)  下载安装器。[安装教程-菜鸟教程 ](https://www.runoob.com/ruby/ruby-installation-windows.html) 注意勾选将 `Ruby` 添加到系统 `PATH` 的选项。

**验证安装**：安装完成后，打开终端或命令提示符，输入 `ruby -v` 并回车。如果显示 `Ruby` 的版本号，说明安装成功。

2. 安装`Jekyll`

```bash
# 安装 Jekyll 和 Bundler
gem install jekyll bundler
```

`Bundler` 是 `Ruby` 的依赖管理工具，用于管理项目所需的各种 `gem` 包。

### 博客主题选择与安装

#### 选择Jekyll主题

`Jekyll`的主题资源主要有两种，**Jekyll Themes官方主题（https://jekyllthemes.io/）**和**第三方兼容主题**。

不是所有的 `Jekyll` 主题都被 `GitHub Pages` 官方支持，`Github Pages`列出了一些它支持的官方主题。[GitHub Pages 官方支持的主题](https://pages.github.com/themes/)，个人认为这些主题过于简陋，所以我没有选择它们。

第三方主题可以在`Github`中直接搜索（关键词为 `jekyll-theme github-pages`），通过查看`README`文档确认该主题的`Github Pages`兼容性。实在不确定的时候直接部署测试。

#### 使用Jekyll主题

`Jekyll`主题的使用方式主要有两种，**使用 Gem-based 主题**和**直接克隆主题仓库**。

**方法一：使用 Gem-based 主题（易于维护）**

这种方式通过修改配置文件来引用主题包，后续更新主题方便。

1. **寻找主题**：
   访问官方主题网站（如 https://jekyllthemes.io/）。找到喜欢的主题后，记下它的 `gem` 名称，例如 `jekyll-theme-garland`。

2. **修改 `Gemfile`**：
   打开博客根目录下的 `Gemfile` 文件。找到 `gem "jekyll"` 这一行，在其下方添加选择的主题 `gem`名称，例如：

   ```ruby
   gem "jekyll-theme-garland"
   ```

3. **修改 `_config.yml`**：
   这是 `Jekyll` 站点的核心配置文件。找到 `theme:` 这一项，将其值修改为选择的主题 `gem` 名称，例如：

   ```yaml
   theme: jekyll-theme-garland
   ```

4. **安装新主题依赖**：
   在项目根目录下执行：

   ```bash
   # 根据更新后的Gemfile安装新的主题
   bundle install
   ```

**方法二：直接克隆主题仓库（快速开始，专注博客内容）**

某些第三方主题可能没有发布为 `gem` 包，这时可以直接 `fork` 或 `clone` 主题作者的仓库。

1. **找到主题仓库**：在 `GitHub` 上找到项目，例如 `flexible-jekyll` 或 `jekyll-clean`。

2. **克隆到本地**&**安装依赖并运行**：

   ```bash
   # 克隆步骤省略
   
   # 安装依赖
   bundle install
   # 启动本地服务，预览博客样式
   bundle exec jekyll serve
   ```

   之后，你就可以在这个项目的基础上修改 `_config.yml` 和内容文件了。我选择了这种方式，具体的配置在后续内容。

#### Chirpy主题安装配置

在对比多个主题后，我选择了 `Chirpy`，原因如下：

- 现代简约的设计风格
- 完善的侧边栏和目录功能
- 良好的中文支持

使用 Starter Template 安装：

1. 访问 https://github.com/cotes2020/chirpy-starter
2. 点击 "Use this template" 创建新仓库
3. 仓库名设置为：`用户名.github.io`
4. 克隆到本地，安装依赖并运行本地预览服务

## Chirpy主题核心配置详解

修改`_config.yml`文件。其他主题的配置应该类似，不会差太多。

### 基础信息配置

```yaml
# _config.yml
title: 你的博客网站名
tagline: 你的博客网站副标题
description: 你的博客网站简介
url: "https://用户名.github.io"
lang: zh-CN
timezone: Asia/Shanghai
```

### 社交信息配置

```yaml
# _config.yml
social:
  name: 你的笔名
  email: your-email@domain.com
  # links可以多放几个，比如知乎、博客园等等平台
  links:
    - https://github.com/用户名
```

### 头像配置

```yaml
# _config.yml
avatar: /assets/img/avatar.png
```

**注意**：头像文件应放置在 `assets/img/` 目录下，建议尺寸 200×200 像素。

### 评论系统配置（Giscus）

#### 什么是 Giscus？

`Giscus` 是一个基于 **GitHub Discussions** 的评论系统，特点：

- 🔒 **无需额外数据库**：使用 `GitHub` 现有基础设施
- 👥 **GitHub 账号登录**：技术读者都有 `GitHub`
- 🆓 **完全免费**：无任何费用
- 🔧 **高度可定制**：支持主题、反应等

#### 配置步骤

1. **启用 GitHub Discussions**

   - 进入你的 GitHub 仓库 `用户名/用户名.github.io`
   - 点击 **Settings** 选项卡
   - 在左侧菜单中找到 **Features**
   - 勾选 **Discussions**
   - 点击 **Set up discussions**，根据指引发表一条评论。

2. **安装 Giscus App**

   - 访问：https://github.com/apps/giscus
   - 点击 **Install**
   - 选择 **Only select repositories**
   - 选择你的博客仓库 `用户名/用户名.github.io`
   - 点击 **Install**

3. **获取配置信息**

   - 访问 https://giscus.app/zh-CN，填写仓库 `用户名/用户名.github.io`

   - **页面 ↔ discussion 映射关系：**选择 **pathname**

     **Discussion 分类**：选择 **Announcements**

     其他功能根据自己需要勾选

   - 配置完成后，页面会生成类似这样的代码：

     ```html
     <script src="https://giscus.app/client.js"
             data-repo="用户名/用户名.github.io"
             data-repo-id="R_kgDOJxxxxxxxx"          <!-- 这个就是 repo_id -->
             data-category="Announcements"
             data-category-id="DIC_kwDOJxxxxxxxx"    <!-- 这个就是 category_id -->
             ...>
     </script>
     ```

   - 复制`repo_id` 和 `category_id`，更新`_config.yml`文件中对应代码：

     ```yaml
     comments:
       provider: giscus
       giscus:
         repo: 用户名/用户名.github.io
         repo_id: R_kgDOJxxxxxxxx          # 替换为你的 repo_id
         category: Announcements
         category_id: DIC_kwDOJxxxxxxxx    # 替换为你的 category_id
         mapping: pathname
         strict: 1
         input_position: bottom
         lang: zh-CN
         reactions_enabled: 1
     ```

4. **测试评论系统**

   1. 推送修改到`Github`，查看博客文章底部是否有评论框。

## 遇到的问题与解决方案

### 问题一：博客文章在 GitHub Pages 不显示

**现象**：本地预览正常，但推送到 `GitHub`后文章不显示。

**原因**：文件名格式不正确或未来日期问题。`Jekyll`对于文件的命名格式极为严格。

**解决方案**：

```bash
# 正确的文件名格式，注意月份与日期需要补零
2025-10-06-my-post-title.md

# 避免使用未来日期
date: 2025-10-06  # 使用当前或过去日期
```

### 问题二：构建警告信息

**现象**：`bundle install` 时显示平台警告。

**解决方案**：这是无害警告，可安全忽略。

```text
[DEPRECATED] Platform :mingw, :x64_mingw, :mswin is deprecated. 
Please use platform :windows instead.
```

## 总结

通过 Jekyll + GitHub Pages 搭建博客是一个性价比极高的选择：

- ✅ 完全免费
- ✅ 无需服务器维护
- ✅ 版本控制天然集成
- ✅ 丰富的主题生态
- ✅ 良好的扩展性

虽然过程中遇到了一些配置问题，但通过查阅文档和社区支持都得到了解决。

---

*希望这篇总结能帮助到同样想要搭建个人博客的你。如果在搭建过程中遇到问题，欢迎在评论区交流讨论！*