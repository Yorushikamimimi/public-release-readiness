# 开源前隐私与发布检查

让 Agent 分开检查当前文件、拟公开 Git 历史、媒体、发布产物和远端内容，对明确候选给出 READY 或 HOLD。

这是给支持 Agent Skills 的 Agent 阅读的文字规范，不是应用、MCP 服务或自动扫描程序。

## 一个具体例子

以下输入和输出是虚构示意，不代表真实产品效果。

**使用前：** 一个虚构项目的当前目录看起来干净，但旧标签仍保留一份已删除的私人演示记录。

**使用后：** “HOLD：当前文件已查，旧标签包含不应公开的材料。保持原仓库私有；如已获授权，可从白名单建立干净公开版本。当前结论不授权重写历史。”

## 安装与触发

Codex 用户可将仓库直接安装到用户级 Skills 目录。需要 Git；目标目录必须不存在，已有同名 Skill 时先比较，不覆盖：

```sh
mkdir -p ~/.agents/skills
git clone https://github.com/Yorushikamimimi/public-release-readiness.git ~/.agents/skills/public-release-readiness
```

仓库根目录就是 Skill 目录，只有一份 [SKILL.md](SKILL.md)。若客户端没有发现，按客户端说明刷新或重启，再显式触发：

```text
请使用 $public-release-readiness，只读检查当前仓库 main 和全部拟公开标签，给出 READY 或 HOLD。报告放在仓库外，不推送或改可见性。
```

也可以把仓库克隆到自己的源码目录，然后按客户端支持的方式将该目录链接或复制到 Skills 目录。其他客户端的发现路径和触发方式需按各自文档核对；本项目不承诺所有平台兼容。

## 会交付什么

范围与覆盖表、脱敏问题列表、候选 commit/tree 或资产指纹、READY／HOLD、已执行和未执行的发布操作。

READY 表示候选可以进入已授权发布步骤，不是零泄露或零漏洞保证；历史、媒体、发布包、远端的必要未知项可能导致 HOLD。

使用者已有明确授权时直接执行；缺少且影响结果的权限才询问。调用 Skill 不自动授权读取凭证或私人资料、安装依赖、启动项目、派出多个 Agent、提交、推送或公开仓库。实际动作遵从使用者自己的项目规则和已有授权。

## 验证与限制

初始版本的隔离验证结果见 [当前进度](CURRENT_PROGRESS.md)。格式检查和虚构案例验证分别记录；本地验证不等于所有 Agent 平台、真实项目或生产环境通过。未提供 App、DMG 或 Release 安装包。

## 维护与来源

公开版本以本仓库根目录 SKILL.md 为维护源；复制安装的副本需要使用者主动比较、更新，符号链接则直接引用源码目录。已有的本机定制版不会因本仓库发布自动替换，也不要求使用维护者的账号、目录或工作流。

- [Agent Skills 格式](https://agentskills.io/specification)
- [Codex Skills 文档](https://developers.openai.com/codex/skills/)
- 具体写法或审查依据见 SKILL.md 末尾参考链接与 [资料说明](references/research.md)。链接材料的版权归各自作者，本项目未复制其代码或成段文案。
- [MIT 许可证](LICENSE)
