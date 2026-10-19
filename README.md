# Huimin Xi 的个人学术主页与博客

学术主页：<https://shuoshu131.github.io/academic/>

原博客：<https://shuoshu131.github.io/>

## 仓库与发布方式

本仓库是 **Hexo 生成后的静态站点仓库**。原页面标记的生成器是 Hexo 7.3.0，主题是 Redefine 2.7.3。仓库不包含 Hexo 的 `package.json`、`_config.yml`、`source/` 或主题源代码，也不包含自定义 GitHub Actions 构建配置。

本次检查确认默认分支为 `main`。已有 `github-pages` 部署记录的来源同样为 `main`，站点内容对应仓库根目录。学术页直接增加在 `academic/index.html`，沿用原来的 Pages 发布机制，无需安装 Hexo 或执行前端构建。

原博客的文章、归档、图片、音乐、样式和脚本保留。仅在博客首页 `index.html` 的桌面与移动导航中增加学术主页入口。入口使用 `data-no-swup`，使浏览器完整加载学术页，避免博客的 Swup 页面切换逻辑沿用原主题的页面容器和样式。

## 页面文件

- `academic/index.html`：双语身份信息、研究兴趣、教育经历、联系方式及搜索元数据。
- `academic/styles.css`：独立的响应式样式，支持系统深浅色模式与打印。
- `index.html`：现有博客首页，增加学术主页入口。

学术页不执行客户端 JavaScript。`application/ld+json` 仅提供人物结构化数据，姓名、机构和邮箱也以普通 HTML 显示。页面复用仓库已有的 `/fonts/Geist/geist.css`、相应字体文件和 `/images/redefine-favicon.svg`；字体不可用时会使用系统字体。页面不加载第三方字体、统计服务或脚本。

修改邮箱时，需同时修改学术页中可见的两处邮箱、对应的 `mailto:` 链接和人物结构化数据。当前页面不列出论文、导师、入学年份或尚未提供的研究经历。

## 本地预览

在仓库根目录运行：

```sh
python3 -m http.server 4173 --bind 127.0.0.1
```

打开 <http://127.0.0.1:4173/academic/>。根路径预览可以同时验证共享字体、博客返回链接以及 `/academic/` 导航。提交前检查 `git diff --check`，并在桌面与手机视口中检查换行、页内导航和邮件链接。

## 后续 Hexo 重新部署：需要同步源项目

**直接执行旧源项目的 `hexo deploy`，可能删除本次新增的 `academic/` 目录，也可能覆盖首页中的学术主页入口。** 当前没有找到对应的本地 Hexo 源项目，因此没有建立或假定存在任何源项目同步。

找到真正的 Hexo 源项目后，执行下列同步，再重新生成和部署：

1. 将本仓库的整个 `academic/` 目录复制到源项目的 `source/academic/`。
2. 将 `academic/**` 合并到源项目 `_config.yml` 的 `skip_render` 列表中，保留原列表条目。例如：

   ```yaml
   skip_render:
     - "academic/**"
   ```

   这使 Hexo 将该目录原样复制到 `public/academic/`，避免把独立 HTML 再套入博客主题。
3. 在源项目的 Redefine 主题配置中，为导航增加 `Academic` 项，路径为 `/academic/`。独立学术页需要完整页面导航；在主题导航模板中为这个入口保留 `data-no-swup` 属性。
4. 确保源项目生成的站点仍提供上述共享字体和图标。若缺少字体，可把本仓库的 `fonts/Geist/` 复制到 `source/fonts/Geist/`，并保留 `images/redefine-favicon.svg`；也可将学术页改用系统字体和单独图标。
5. 执行 `hexo clean && hexo generate`，检查 `public/academic/index.html`、`public/academic/styles.css` 和首页入口，再用原有部署命令发布。重新访问公开地址确认。

这份说明记录覆盖风险；本次没有修改未知源项目，也没有新增后台同步任务。
