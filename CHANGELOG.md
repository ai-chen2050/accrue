# CHANGELOG

> 记「改了什么 + 为什么」。数值调整必须写出 旧值 → 新值。
> 这份文件是解释"某个数字为什么长这样"的第一去处，CLAUDE.md 会指向它。
> 用 `/devlog` 让 Claude 自动追加。

## 2026-10-02

- 官网实装 3D 全息空间剖析与立体数学演播舱，同步 Pro 订阅最新权益：
  - `site.config.json`: 扩充单一真源，新增「3D 空间数学与立体几何工作室」与「3D 空间剖析与全息数字孪生」两项核心功能卡片、对比表格「3D 空间孪生与数学」维度、FAQ Pro 权益说明与 3D 相关 SEO 关键词。
  - `index.html` & `index.en.html`:
    - 顶部导航栏新增「3D 空间剖析 / 3D Dissection」直达锚点；
    - 新增交互演播舱 `#spatial-dissection`：支持地球圈层剖切、DNA 组蛋白超螺旋、神经元轴突突触与 3D 双曲抛物面数学曲面 4 大预置模型；
    - 交互控制：配备 0~100% 自由滑动的「💥 爆炸拆解」滑块与微透毛玻璃「自动旋转 / 暂停自转」开关；
    - 热点联动：1-6 号圈层光晕序号可点击交互，实时投影更新右侧遥测面板（深度/温度/晶相/压强等关键参数、深度解剖综述与双链关联词条）；
    - 定价对比卡片与权益列表同步加入 3D 空间剖析高级模型库、LiDAR 实物扫描建模与 3D 数学函数曲面插入。
  - `style.css`: 新增 `.dissection-wrapper`、`.dissection-viewport`、`.dissection-telemetry` 等全套高保真暗黑全息毛玻璃视效样式。
  - 轻量原生引擎：完全基于纯原生 Vanilla JS + Canvas 2D 透视几何投影矩阵实现，零外部庞大三维库依赖，加载耗时 < 5ms。
  - `tools/gen_geo.py` & `tools/geo_check.py`: 运行 `make build` 全量更新生成多语言 head 标签、sitemap 及 llms.txt，并通过 `make geo-check` 严格验证。


- 修复 GitHub Actions CI 检查步骤因时区与跨日导致生成物 diff 误报而部署失败的问题：
  - `tools/gen_geo.py`: 新增 `get_today()` 函数。在 CI 检查环境下（`CI=true` 或 `GITHUB_ACTIONS=true`）优先提取并沿用仓库已提交 `sitemap.xml` 中的日期，消除 GitHub Actions runner（UTC 默认时区）与本地提交（东八区 UTC+8）因时差产生 1 天日期差或跨日检查导致的 diff 误报。
  - `.github/workflows/pages.yml`: 设置全局 `TZ: Asia/Shanghai`。
  - `site.config.json`: 更新 `site.updated` 为 `2026-10-02`。

## 2026-09-28

- 工程初始化（aic 脚手架生成）
