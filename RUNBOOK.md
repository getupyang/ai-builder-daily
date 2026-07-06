# AI Builder Daily — RUNBOOK

## 目标

把 `~/research/topics/dev-digest/` 里生成的“原始日报”发布到公开站点：
- Repo: `https://github.com/getupyang/ai-builder-daily`
- Pages: `https://getupyang.github.io/ai-builder-daily/`

只发布原始版本，不发布实验版本。

---

## 目录

源日报目录：
- `/Users/getupyang/research/topics/dev-digest/`

公开站目录：
- `/Users/getupyang/ai-builder-daily/`

公开网页输出：
- `/Users/getupyang/ai-builder-daily/docs/index.html`
- `/Users/getupyang/ai-builder-daily/docs/reports/*.html`
- `/Users/getupyang/ai-builder-daily/docs/reports/*.md`

---

## 发布规则

### 1. 只发布这些文件

匹配：
- `YYYY-MM-DD-daily.md`

例如：
- `2026-05-01-daily.md`
- `2026-05-02-daily.md`

### 2. 不发布这些文件

忽略任何带后缀的实验/对比版本，例如：
- `*-Hermes.md`
- `*-hermes.md`
- `*-v2.md`
- `*-claude.md`
- 任何其他非原始版本

原则：
- **只发不带额外后缀的原始日报**

---

## 每次继续任务时，agent 要做什么

1. 读取：
   - `/Users/getupyang/research/topics/dev-digest/`
   - `/Users/getupyang/ai-builder-daily/`
2. 找出尚未发布的原始日报 `YYYY-MM-DD-daily.md`
3. 把 markdown 复制到：
   - `docs/reports/YYYY-MM-DD-daily.md`
4. 生成对应 HTML：
   - `docs/reports/YYYY-MM-DD-daily.html`
5. 更新首页 `docs/index.html`
   - 按日期倒序列出所有已发布日报
6. 在 repo 中执行：
   - `git add docs`
   - `git commit`
   - `git push origin main`
7. 确认 GitHub Pages 状态
8. 返回公开链接

---

## 首页文案

站点名：
- `AI Builder Daily`

描述：
- `A public daily digest on AI products, developer tools, and builder workflows.`

---

## 当前已发布

**以 `docs/reports/*.md` 为准**（不要手工维护清单，会烂）。查最新已发布：

```bash
ls docs/reports/*-daily.md | sort | tail -1
```

最近发布：`2026-07-06-daily`（含「深度长文/播客」专题，窗口拉到近一个月，补 The Batch 等错过内容）。

---

## 重开会话时的推荐启动词

```text
继续 AI Builder Daily。读取 /Users/getupyang/research/topics/dev-digest/ 和 /Users/getupyang/ai-builder-daily/。只发布不带后缀的原始日报版本，更新 GitHub Pages，并告诉我发布结果。
```

---

## 注意事项

1. 不要把 Hermes 实验版本公开顶替原始日报。
2. 如果同一天同时存在多个版本，优先原始 `YYYY-MM-DD-daily.md`。
3. 如果 GitHub Pages 还在 building，告诉用户稍等几分钟刷新。
4. 如果当天没有新的原始日报，不要瞎生成，直接报告“今天还没有可发布的原始日报”。
5. 如果需要自动化，优先把这套规则固化进脚本/cron，而不是依赖临时提示词。
