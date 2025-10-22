# Git Hotspot AI - 使用示例

## 环境配置

首先设置 cursor-agent 路径：

```bash
# 方法1: 如果 cursor-agent 在 PATH 中
export CURSOR_AGENT_PATH=$(which cursor-agent)

# 方法2: 指定完整路径
export CURSOR_AGENT_PATH=/usr/local/bin/cursor-agent

# 方法3: 添加到 shell 配置文件
echo 'export CURSOR_AGENT_PATH=$(which cursor-agent)' >> ~/.zshrc
source ~/.zshrc
```

## 基本使用

### 1. 预览模式（不执行 AI 任务）

```bash
# 查看当前目录的热点文件
git-hotspot-ai --dry-run

# 查看特定数量的热点文件
git-hotspot-ai --dry-run --top 10

# 查看热点文件百分比
git-hotspot-ai --dry-run --top 15%
```

### 2. 执行 AI 分析任务

```bash
# 对前5个热点文件执行代码注释任务
git-hotspot-ai --top 5 --tasks "annotate"

# 执行多个任务
git-hotspot-ai --top 3 --tasks "annotate,structure,performance"

# 分析最近6个月的变更
git-hotspot-ai --since "6 months ago" --tasks "skills,mvp"
```

### 3. 过滤和筛选

```bash
# 忽略测试文件和文档
git-hotspot-ai --ignore "test_*,*_test.py,docs/*,*.md" --tasks "performance"

# 只分析至少有5次提交的文件
git-hotspot-ai --min-commits 5 --tasks "structure"

# 分析特定仓库
git-hotspot-ai --repo /path/to/other/repo --tasks "annotate"
```

## AI 任务说明

### annotate - 代码注释
为代码添加详细的注释和文档，提高代码可读性。

```bash
git-hotspot-ai --tasks "annotate" --top 5
```

### structure - 结构分析
分析代码结构，识别重构机会和架构改进建议。

```bash
git-hotspot-ai --tasks "structure" --top 3
```

### skills - 技能分析
识别代码所需的技能和专业知识，分析技术栈和最佳实践。

```bash
git-hotspot-ai --tasks "skills" --top 10%
```

### performance - 性能分析
分析性能特征，识别瓶颈并提出优化建议。

```bash
git-hotspot-ai --tasks "performance" --min-commits 3
```

### mvp - MVP 建议
生成最小可行产品建议，分析核心功能和简化方案。

```bash
git-hotspot-ai --tasks "mvp" --top 5
```

## 高级用法

### 组合使用

```bash
# 完整的代码质量分析流程
git-hotspot-ai --since "3 months ago" \
               --ignore "test_*,docs/*" \
               --min-commits 2 \
               --top 10 \
               --tasks "annotate,structure,performance"
```

### 自定义 cursor-agent 路径

```bash
# 临时指定不同的 cursor-agent
git-hotspot-ai --cursor-agent-path /custom/path/cursor-agent \
               --tasks "annotate"
```

## 输出示例

```
Hotspot ranking:
Repo: /path/to/your/repo
=== Top Files ===
001. src/main.py — commits: 25, lines: 1250, score: 150.0
002. src/utils.py — commits: 18, lines: 800, score: 98.0
003. src/config.py — commits: 12, lines: 400, score: 52.0

[AI] Processing src/main.py
  -> Running task: annotate
  ✓ Task 'annotate' completed successfully
  Output: 已为 src/main.py 添加了详细的函数注释和类文档...

[AI] Processing src/utils.py
  -> Running task: annotate
  ✓ Task 'annotate' completed successfully
  Output: 分析了 src/utils.py 的工具函数，添加了参数说明...
```

## 错误处理

如果遇到错误，工具会提供清晰的错误信息：

```bash
# 未设置环境变量
Error: CURSOR_AGENT_PATH environment variable is not set!
Please set the environment variable to point to your cursor-agent executable:
  export CURSOR_AGENT_PATH=/path/to/cursor-agent

# cursor-agent 路径无效
Error: cursor-agent not found at: /invalid/path
Please check your CURSOR_AGENT_PATH environment variable.

# 任务执行失败
[AI] Processing src/example.py
  -> Running task: annotate
  ✗ Task 'annotate' failed with return code 1
  Error: cursor-agent command failed
```
