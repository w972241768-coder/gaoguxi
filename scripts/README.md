# 更新脚本

生成脚本位于 WorkBuddy 工作区 `ETF轮动战法/_gaoguxi_site.py`，
依赖同目录 `out/` 下由 pandadata 生成的数据文件。

链路：`_dividend_pool_build.py` → `_dividend_pool_final.py` → `_div_extend.py` → `_ext_ma.py` → `_gaoguxi_site.py`。
这些脚本需要 WorkBuddy 会话中的 pandadata Connector，单独 clone 本仓库无法运行。
