# 双语变更日志生成器 / Bilingual Changelog Generator

自动提取上一个 release 到当前的变更记录并翻译成双语格式。

Automatically extract changes from previous release to current and translate to bilingual format.

## 快速开始 / Quick Start

### 1. 创建 workflow 文件

在你的仓库创建 `.github/workflows/release.yml`：

```yaml
name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      
      - name: Generate changelog
        id: changelog
        uses: Desmond-Dong/actions/bilingual-changelog@v1
        with:
          llm-api-key: ${{ secrets.LLM_API_KEY }}
      
      - name: Create Release
        uses: softprops/action-gh-release@v1
        with:
          tag_name: ${{ github.ref_name }}
          name: Release ${{ github.ref_name }}
          body: ${{ steps.changelog.outputs.changelog }}
```

### 2. 添加 API Key

进入仓库 Settings → Secrets and variables → Actions → New repository secret
- Name: `LLM_API_KEY`
- Value: 你的 LLM API Key

### 3. 推送 tag

```bash
git tag v1.0.0
git push origin v1.0.0
```

完成！自动创建带双语 changelog 的 release ✨

## 参数 / Parameters

### Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `llm-api-key` | LLM API Key | Yes | - |
| `llm-api-url` | LLM Chat Completions API URL | No | `https://open.bigmodel.cn/api/paas/v4/chat/completions` |
| `llm-model` | LLM 模型名称 | No | `glm-4.7-flash` |

### Outputs

| Name | Description |
|------|-------------|
| `changelog` | 生成的双语 changelog |

## 自定义模型 / Custom Model

```yaml
- uses: Desmond-Dong/actions/bilingual-changelog@v1
  with:
    llm-api-key: ${{ secrets.LLM_API_KEY }}
    llm-model: 'glm-4-plus'
```

## 自定义 API / Custom API

```yaml
- uses: Desmond-Dong/actions/bilingual-changelog@v1
  with:
    llm-api-key: ${{ secrets.LLM_API_KEY }}
    llm-api-url: https://api.openai.com/v1/chat/completions
    llm-model: gpt-4o-mini
```

## 输出格式 / Output Format

```
- 修复登录问题 / *Fix login issue*
- 添加新功能：用户管理 / *Add new feature: user management*
- 优化性能 / *Optimize performance*
```

## License

MIT
