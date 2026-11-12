# 高股息研究站（gaoguxi）

> 鳄鱼派高股息体系：知识框架、策略 SOP、选定池子、观察清单。
> **数据快照截至 2026-11-12 收盘**，非实时行情。

## 在线地址

**https://w972241768-coder.github.io/gaoguxi/**

- [总览](docs/index.html) · [研究框架](docs/research.html) · [选定池子](docs/pool.html) · [观察清单](docs/watch.html)
- 手机浏览器打开后可「添加到主屏幕」，按 PWA 方式全屏使用（已带 manifest）。

## 内容结构

| 页面 | 内容 |
|---|---|
| `docs/index.html` | 五条核心结论、数据口径速查、导航 |
| `docs/research.html` | 七层知识框架、策略 SOP 七条、参数表（区分博主原话/工程化建议）、与「攒股的大叔」方案对照、全市场扫描漏斗 |
| `docs/pool.html` | 核心池 8 只 + 卫星池 9 只逐只数据，含三种票息、周线 MA60 买点、派息率、FCF 覆盖；4 只「定池∩买点」交叉清单 |
| `docs/watch.html` | A 类：点名但未入池 9 只（含否决原因）；B 类：全市场池外 TTM 股息率 ≥4% 的 64 只，可筛选/搜索 |
| `docs/data/` | 全部结构化数据（JSON）与可下载 CSV |

## 数据来源与口径

全部来自 **pandadata Connector** 真实返回，本地仅做纯计算：

- `get_stock_cash_dividend`（2021–2026 六个年度全市场，23,560 行）、`get_stock_dividend_amount`（预案/决案/方案实施）
- `get_stock_split`（送转复权对齐）、`get_stock_daily`（2026-11-12 收盘）、`get_stock_weekly`（原生周线 66 周）
- `get_stock_detail`（在市/ST/上市日）、`get_stock_equity_nature`（企业性质 5,565 只）、`get_fina_reports`（2025 年报）

关键口径：

- 每股股息 = `div_cash_gross ÷ round_lot(10)`，按 **ex_date 除权年度** 聚合；窗口内两次 10→14 送转已 `/1.4` 对齐。
- 三种票息（**均税前**）：中位 = 近 5 年年度每股股息中位 ÷ 收盘价；最新财年 = 2025 财年每股股息 ÷ 收盘价；TTM = 近 12 月实际除权股息 ÷ 收盘价。
- 派息率 = 2025 财年分红总额（**含中期分红**）÷ 归母净利；FCF = 经营现金流净额 − 购建固定资产支出；FCF 覆盖 = FCF ÷ 分红总额。**金融业 FCF 口径失真**。
- 周 MA60 = 原生周线最近 60 根收盘价算术平均（不是日线 MA60），最新周为 2026-11-06。
- 阈值（CV≤0.60、突增≤2.50、最新财年/中位∈[0.70,1.80] 等）是**工程化建议，非博主原话，未经参数稳定性检验**。

## 如何更新数据

本仓库是**研究快照**，站点不连行情接口，因此不会自动变动。需要刷新时：

1. 在 WorkBuddy 会话中让助手重新跑 pandadata 取数与分析脚本；
2. 重新生成本仓库 `docs/` 下的 HTML 与 `docs/data/`；
3. `git add -A && git commit -m "data: 更新至 YYYY-MM-DD" && git push`，Pages 约 1 分钟自动重建。

> 刻意**没有**接 CI 定时抓数：pandadata 凭据只在 WorkBuddy 会话内可用，放到公开仓库的 Actions 里既不可行也不安全。
> 若将来有可公开的数据源，可在 `.github/workflows/` 加定时作业，注意 `push.paths` 排除 `docs/` 防死循环。

## ⚠️ 公开仓库提示

本仓库为 **Public**，页面里的研究结论、池子名单与全部 CSV 任何人都能访问。
如不希望公开，请在 GitHub 仓库设置中改为 Private（但免费版 Private 仓库无法使用 Pages）。

## 免责声明

仅为方法论研究与数据整理，**不构成投资建议、不承诺收益、不含买卖或仓位指令**。
分红历史不代表未来，股息率未扣分红税与 FIFO 影响；决策请独立判断、风险自担。
