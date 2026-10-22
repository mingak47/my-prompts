# My Prompts · 我的提示词库

个人提示词库：一个提示词一个文件，可检索、可复用、可回滚。用 Git 管理版本，改坏了随时 `git diff` 看回来。

## 目录结构

```
my-prompts/
├── README.md              # 本文件：说明 + 索引
└── prompts/
    ├── _template.md       # 新建提示词的模板
    ├── writing/           # 写作：润色、改写、文案
    │   └── polish-zh.md
    ├── coding/            # 编程：审查、重构、调试
    │   └── code-review.md
    └── analysis/          # 分析：估算、拆解、决策
        └── estimate.md
```

分类按**使用场景**划分，不按模型划分。新场景出现时直接加目录，例如 `translation/`、`product/`。

## 提示词索引

| 分类 | 名称 | 用途 | 文件 |
| --- | --- | --- | --- |
| 写作 | 中文润色 | 去翻译腔、修语病，保持原意 | [polish-zh.md](prompts/writing/polish-zh.md) |
| 编程 | 代码审查 | 按严重程度分级报问题，附改法 | [code-review.md](prompts/coding/code-review.md) |
| 分析 | 快速测算 | 费米估算，给量级与上下界 | [estimate.md](prompts/analysis/estimate.md) |

## 文件格式

每个提示词都是独立 Markdown 文件，结构固定：

1. **YAML frontmatter** —— `title` / `category` / `tags` / `model` / `version` / `updated`
2. **用途** —— 一句话说清解决什么问题
3. **变量** —— `{{变量名}}` 占位符及其含义
4. **提示词正文** —— 用标有 `text` 的代码块包裹，方便整段复制
5. **使用示例** —— 输入与预期输出
6. **调整建议** —— 常见变体怎么改

### 变量约定

- 占位符统一写成 `{{name}}`，全小写、连字符或下划线分隔
- 变量只出现在「提示词正文」里，使用前替换成实际内容
- 可选变量在正文里写明默认行为（例如「未指定时使用清晰自然的中文」）

## 新增一条提示词

```bash
cp prompts/_template.md prompts/writing/my-new-prompt.md
```

1. 改名：`kebab-case.md`，能一眼看出用途
2. 填 frontmatter，`updated` 写当天日期，`version` 从 0.1 起
3. 把提示词正文放进标有 `text` 的代码块，变量用 `{{}}`
4. 在本文件「提示词索引」表里补一行
5. 改了就 `git add -A && git commit -m "新增：xxx"`

## 维护约定

- **一文件一提示词**，不要把多个版本塞进同一个文件
- 大改（换角色、换输出格式）时升 `version`，小改只更新 `updated`
- 废弃的提示词先移入 `prompts/_archive/`，观察一段时间后再删
- 提交信息用「新增 / 修改 / 删除：主题」的形式
