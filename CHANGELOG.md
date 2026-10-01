# CHANGELOG

> 记「改了什么 + 为什么」。数值调整必须写出 旧值 → 新值。
> 这份文件是解释"某个数字为什么长这样"的第一去处，CLAUDE.md 会指向它。
> 用 `/devlog` 让 Claude 自动追加。

## 2026-10-02

- 修复 GitHub Actions CI 检查步骤因时区与跨日导致生成物 diff 误报而部署失败的问题：
  - `tools/gen_geo.py`: 新增 `get_today()` 函数。在 CI 检查环境下（`CI=true` 或 `GITHUB_ACTIONS=true`）优先提取并沿用仓库已提交 `sitemap.xml` 中的日期，消除 GitHub Actions runner（UTC 默认时区）与本地提交（东八区 UTC+8）因时差产生 1 天日期差或跨日检查导致的 diff 误报。
  - `.github/workflows/pages.yml`: 设置全局 `TZ: Asia/Shanghai`。
  - `site.config.json`: 更新 `site.updated` 为 `2026-10-02`。

## 2026-09-28

- 工程初始化（aic 脚手架生成）
