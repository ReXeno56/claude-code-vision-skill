# Claude Code Vision Skill

让不具备识图能力的模型（如 DeepSeek）通过调用外部 vision 模型来识别图片。

## 工作原理

```
用户发图片路径 → Skill 触发 → 调用 vision API → 返回描述 → 主模型基于描述回复
```

## 安装

```bash
# 安装到 Claude Code skills 目录
git clone https://github.com/<your-username>/claude-code-vision-skill.git
cp -r claude-code-vision-skill ~/.claude/skills/vision
```

## 配置

复制 `vision.env.example` 为 `~/.claude/vision.env`，填入你的 vision API 信息。

支持三种方式：

### A — Anthropic Claude API（效果最好）
```ini
VISION_API_PROVIDER=anthropic
VISION_API_BASE_URL=https://api.anthropic.com
VISION_API_KEY=sk-ant-...
VISION_MODEL=claude-opus-4-7
```

### B — OpenAI API
```ini
VISION_API_PROVIDER=openai
VISION_API_BASE_URL=https://api.openai.com/v1
VISION_API_KEY=sk-...
VISION_MODEL=gpt-4o
```

### C — 本地模型（Ollama 等）
```ini
VISION_API_PROVIDER=openai
VISION_API_BASE_URL=http://localhost:11434/v1
VISION_API_KEY=ollama
VISION_MODEL=llava
```

可选参数：
- `VISION_MAX_TOKENS` — 输出最大长度（默认 4096）

## 使用

直接在对话中说"看看这张图"，skill 自动触发。也可以手动调用：

```bash
python3 ~/.claude/skills/vision/scripts/describe_image.py screenshot.png
python3 ~/.claude/skills/vision/scripts/describe_image.py chart.png -p "分析这个图表的关键趋势"
```

## 支持的图片格式

PNG、JPEG、GIF、WebP、BMP

## 文件结构

```
vision/
├── SKILL.md              # Skill 定义
└── scripts/
    └── describe_image.py # Vision API 调用脚本（纯标准库，无依赖）
```
