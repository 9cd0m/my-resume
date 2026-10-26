# 在线简历（Hexo + GitHub Pages）

一个「简历为主体、技术笔记为附录」的个人站点。

- 首页 = 简历：教育背景 → 技能 → 荣誉与证书 → 技术笔记
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

## 待补充

- **项目经历**：`source/_posts/项目经历.md` 已删除（原内容是模板虚构的）。写好真实项目后新建该文件即可，首页顺序由 front-matter 里的 `date` 决定（`2025-01-03` 正好排在教育背景和荣誉之间）。
- **电话 / 城市**：`sidebar.pug` 里那两条 `li` 仍是注释状态，填好后取消注释即可上侧栏。
- **简历正文**：各篇内容基于就业推荐表填写，真实项目、成绩、比赛获奖自行补充。

## 本地开发

```bash
npm install          # 首次
npx hexo clean
npx hexo server      # http://localhost:4000
```

## 发布

```bash
git add .
git commit -m "content: 更新技能"
git push
```

推送后到仓库的 Actions 标签页看构建，绿了之后访问 `https://<你的用户名>.github.io`。

首次部署前记得在仓库 **Settings → Pages → Source** 选择 **GitHub Actions**。
