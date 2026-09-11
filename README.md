# openclaw-workspace

**Agent 管线的派生状态与临时数据——不是一个独立项目。** 这个仓库里的东西都由别的仓库里的脚本生成，人工不要在这里改；下一次管线跑起来会覆盖。

主页面的 README 是这份说明；真正的工具在各自的仓库里（见下表的「所有者」列）。

## 里面有什么

| 路径 | 内容 | 由谁生成 | 现在的状态 |
|---|---|---|---|
| [`data/arxiv/`](data/arxiv/) | 每日论文清单（Markdown），每个文件末尾写着「_由 AI Paper Daily 自动生成_」 | [AI-Paper-Daily](https://github.com/alloevil/AI-Paper-Daily) | 24 个日文件，2026-07-31 → 2026-09-07 |
| [`data/arxiv_tracker_state.json`](data/arxiv_tracker_state.json) | 去重游标：`seen_ids`（509 条）与 `last_run`（`2026-09-07T18:01:00+08:00`） | 同上 | 决定下一次抓取只取新论文 |
| [`data/changelog_data.js`](data/changelog_data.js) | 变更日志快照（64 KB），供站点读取 | [agent-changelog](https://github.com/alloevil/agent-changelog) | 与 `agent-changelog` 仓库里的 `openclaw_data.js`（3.7 MB）不是同一份文件，别拿它当镜像 |
| [`scripts/github-discovery/`](scripts/github-discovery/) | [github-discovery](https://github.com/alloevil/github-discovery) 管线的一份**内嵌副本**（12 个文件） | 从该仓库拷入后各自演进 | 与独立仓库已经不一致（`diff -rq` 有多处差异），当快照看，不要当同步镜像 |

## 使用约定

### never

- 不手改 `data/` 下的任何文件——它们是生成物，下一次管线运行会覆盖
- 不把 `scripts/github-discovery/` 当成独立仓库的同步副本；要改那个管线，改 [github-discovery](https://github.com/alloevil/github-discovery) 本体

### ask-first

- 在这个仓库里新增数据目录（先确认它属于哪条管线、由哪个仓库生成）
- 删除 `data/arxiv/` 下的历史文件（去重游标 `seen_ids` 与它们相关，删文件不会让管线重新抓取，但会让历史断档）

<!-- 这是起点：agent 犯一次错就补一条边界，定期跑 agentsmd-lint。 -->
