# 依据与工具选择

## 设计来源

本规范从维护者已有的文字工作流整理而来。以下资料用于理解格式、公开范围和审查分类；除 LICENSE 中的标准许可文本外，本项目未复制上游代码、图片或成段说明，也不重新许可链接指向的第三方内容。

- [Agent Skills 格式](https://agentskills.io/specification)：SKILL.md 与按需 references 的目录约定。
- [GitHub 仓库可见性](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility)：公开会改变可访问范围，具体行为执行时复核。
- [GitHub 敏感数据移除](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)：当前文件、历史和外部副本需分别处理。
- [Open Source Guides：法律问题](https://opensource.guide/legal/)：公开访问与开源许可是不同判断。
- [oss-ready](https://github.com/vishnujayvel/oss-ready)：早期设计参考了隐私、密钥、路径与历史等检查分类；未复制实现，不继承其执行策略或并行扫描要求。

## 工具选择

优先使用已安装的本地工具。可按需参考 [Gitleaks](https://github.com/gitleaks/gitleaks) 等扫描器的官方说明；执行前核对当前版本、参数、范围、排除项及完整脱敏选项，不锁定某个工具或盲装 latest。

当前目录、Git 历史与资产分别检查。报告放在非发布位置，不把原始命中输出到聊天，不联网验证疑似凭证。成熟扫描器无发现不等于没有隐私或版权问题。若工具缺失，对很小且可完整阅读的纯文本候选可以人工逐文件核查并记录限制；无法覆盖必要风险时给 HOLD，不能把自写正则说成完整安全扫描。

媒体需要视觉与元数据检查，发布包需要检查最终包内容；文本扫描不能替代它们。读取限制同样约束历史检查与扫描器。

## 边界示例（均为虚构）

| 情境 | 应作出的判断 |
|---|---|
| 当前文件已删除私人材料，旧标签仍包含它 | 原历史发布 HOLD；不能仅凭 HEAD 干净放行 |
| 用户授权干净导出且保留旧私有历史 | 按白名单新建历史，检查新候选，不默认重写原历史 |
| 项目禁止读取某个文件 | 记录未查；缩小发布范围或就必要目标取得具体授权 |
| 截图已查，安装包带入旧数据库 | 包检查 HOLD；截图结果不能替代包结果 |
| 用户已授权公开且候选 READY、未变化 | 执行已授权步骤并回读，不重复索要发布权限 |
| 公开后新增截图或附件 | 重查受影响暴露面，更新候选指纹 |
