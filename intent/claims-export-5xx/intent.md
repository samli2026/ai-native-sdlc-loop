# Intent: 理赔导出接口 5xx 越界
Author: monitoring agent (status_5xx_rate, 3sigma). Status: draft.

## Problem
理赔导出端点 5xx 率读到 1.9%，30 天均值 0.2004%（σ=0.0201），命中 reading above 3 sigma。
时间窗口内有发布 4f2c9e1；导出改为流式写出后，claims-core 分页超时。

## Proposed outcome
5xx 回到基线以下，导出大范围时能降级而不是 500。

## Affected users and systems
理赔运营、claims-api、claims-core。

## Constraints
claims-core 限 50 rps；导出仍受 1 万行上限约束。

## Action already taken
已触发预先批准的 rollback-deploy runbook（staging 演练过）。

## Open questions
大范围导出是否改为异步任务 + 下载链接？
