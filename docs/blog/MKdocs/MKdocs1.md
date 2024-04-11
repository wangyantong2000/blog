---
title: Mkdocs使用教程-入门
tags:
  - Mkdocs
---

# 新建网站

在完成[Material for MkDocs 的安装][1]后，可以使用`mkdocs`相关命令来启动文档。转到要放置项目的目录，然后输入：

```
mkdocs new .
```

如果你正在使用的是 Docker 中的 Material for MkDocs，则使用以下命令：

=== "Unix"

    ```
    docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material new .
    ```

=== "Windows"

    ```
    docker run --rm -it -v "%cd%":/docs squidfunk/mkdocs-material new .
    ```

以上操作会新建以下结构的文件：

```
.
├─ docs/
│  └─ index.md
└─ mkdocs.yml
```

[1]: MKdocs.md

## 配置

### 最小配置

只需要简单的添加以下几行内容到`mkdocs.yml`即可启用主题。请注意，由于有几种不同的[安装][2]方法，因此配置可能会略有不同：

=== "pip, docker"

    ``` yaml
    theme:
      name: material
    ```

=== "git"

    ``` yaml
    theme:
      name: null
      custom_dir: mkdocs-material/material

      # 404 page
      static_templates:
        - 404.html

      # Necessary for search to work properly
      include_search_page: false
      search_index_only: true

      # Default values, taken from mkdocs_theme.yml
      language: en
      font:
        text: Roboto
        code: Roboto Mono
      favicon: assets/favicon.png
      icon:
        logo: logo
    ```

_如果是从 GitHub 克隆的 MkDocs from GitHub，那么应当列出所有主题的默认项，因为[`mkdocs_theme.yml`][3]不会作为[官方的描述文件][4]被自动载入_

[2]: MKdocs.md/#_2
[3]: https://github.com/squidfunk/mkdocs-material/blob/master/src/mkdocs_theme.yml
[4]: https://www.mkdocs.org/user-guide/custom-themes/#creating-a-custom-theme

## 预览

MkDocs 包含一个试试预览的服务，所有可以在撰写文档的过程中进行实时预览。当文档修改保存后，这个服务会自动重建整个网站的文档。使用以下命令启动：

```
mkdocs serve
```

如果使用的是 Docker 中的 Material for MkDocs，则使用以下命令：

=== "Unix"

    ```
    docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
    ```

=== "Windows"

    ```
    docker run --rm -it -p 8000:8000 -v "%cd%":/docs squidfunk/mkdocs-material
    ```

浏览器打开[localhost:8000][17]，应该就能看到类似下图所示的内容：

[![Creating your site][18]][18]

[17]: http://localhost:8000
[18]: ../../assets/creating-your-site.png

## 生成网站

当文档编辑完成后，可以通过以下命令将所有的 Markdown 文件生成一个静态网站：

```
mkdocs build
```

该目录中的内容就是项目文档/网站。因为是完全独立的，所以不需要操作数据库或者服务器。生成的网站可以托管在 GitHub Pages、GitLab Pages、CDN 网络或者其它的 web 服务器上。
