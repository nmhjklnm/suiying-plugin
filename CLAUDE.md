# CLAUDE.md

Suiying (随影) - macOS Claude Code plugin: desktop notifications + code review.

## 开发模式

**本地开发**: 通过 symlink 连接到 `~/.claude/plugins/suiying`，不是通过 GitHub marketplace
**手动更新**: 修改文件后，需在 Claude Code 中手动重载插件生效

```bash
ln -s "$(pwd)" ~/.claude/plugins/suiying
```

## 核心文件

```
.claude-plugin/
  plugin.json           # 插件元数据，版本号在此
  marketplace.json      # Marketplace 配置，版本号需同步
agents/
  pragmatic-code-review.md
  design-review.md
commands/
  code-review.md
  design-review.md
  security-review.md
skills/design-principles/
  SKILL.md             # 自动激活的设计原则知识库
hooks/
  hooks.json           # UserPromptSubmit, Stop, Notification 事件
scripts/
  ccnotify.py          # 通知系统 + SQLite 会话追踪
```

## CCNotify 通知系统

**数据库**: SQLite `prompt` 表 (id, session_id, created_at, prompt, cwd, seq, stoped_at, lastWaitUserAt)

**通知格式**:
- 完成: `{项目} - 完成了` / `{提示预览} ({时长})`
- 权限: `{项目} - 需要权限` / `{消息}`
- 操作: `{项目} - 需要操作` / `{消息}`
- 问询: `{项目} - 问询` / `{消息}`

**点击**: 打开 Windsurf `/Users/apple/.codeium/windsurf/bin/windsurf "{cwd}"`

## 代码规范

**Python**: SQLite triggers 自增 seq, subprocess.run(check=False), 时长格式 "5s"/"2m30s"

**Agents/Skills**: YAML frontmatter (name, description, tools, model, color), 用 `<example>` 说明触发条件

**Hooks**: 路径用 `${CLAUDE_PLUGIN_ROOT}`, 事件名精确匹配 (UserPromptSubmit, Stop, Notification)

## 发布检查

1. 同步更新 `plugin.json` + `marketplace.json` 版本号
2. 验证 `hooks.json` JSON 结构
3. 测试通知流程
4. 更新 README（如有功能变更）
