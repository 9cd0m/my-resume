# 在线简历（Hexo + GitHub Pages）

一个「简历为主体、技术笔记为附录」的个人站点。

- 首页 = 简历：教育背景 → 技能 → 项目经历 → 荣誉与证书 → 技术笔记
- 顶部导航由 `source/_posts/` 里的文章标题自动生成（点一下滚动到对应章节）
- 技术笔记放在 `source/notes/`，用 `layout: page`，不会铺在首页正文里
- 部署：推送到 `main` 分支，GitHub Actions 自动构建并发布

## 目录导览

| 路径 | 作用 |
|---|---|
| `_config.yml` | 站点配置（标题、url、主题、分页） |
| `themes/anatole-core-resume/_config.yml` | 主题配置（姓名、GitHub、邮箱） |
| `themes/anatole-core-resume/layout/partial/sidebar.pug` | 侧栏：电话、城市（写死在模板里） |
| `source/_posts/*.md` | **简历正文**，每篇文章 = 简历的一节 |
| `source/notes/**/index.md` | 技术笔记（独立页面） |
| `.github/workflows/pages.yml` | 自动部署工作流 |

## 上线前必须替换的占位符

全局搜索这几个词，一个都别留：

- `你的名字` —— `_config.yml`、`themes/anatole-core-resume/_config.yml`
- `你的用户名` —— `_config.yml` 的 `url`、主题 `_config.yml` 的 `github`、`sidebar.pug`
- `你的邮箱` —— 主题 `_config.yml`、`sidebar.pug`
- `138-0000-0000`、`北京 · 可远程` —— `sidebar.pug`
- `某某大学`、`xxx` —— 各篇文章正文

## 本地开发

```bash
npm install          # 首次
npx hexo clean
npx hexo server      # http://localhost:4000
```

## 发布

```bash
git add .
git commit -m "content: 更新项目经历"
git push
```

推送后到仓库的 Actions 标签页看构建，绿了之后访问 `https://<你的用户名>.github.io`。

首次部署前记得在仓库 **Settings → Pages → Source** 选择 **GitHub Actions**。
