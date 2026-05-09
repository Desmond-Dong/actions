# GitHub Actions Collection / GitHub Actions 集合

可复用的 GitHub Actions 集合。

Collection of reusable GitHub Actions.

## Actions

### [双语变更日志生成器 / Bilingual Changelog Generator](./bilingual-changelog)

自动提取上一个 release 到当前的变更记录并翻译成双语格式。

Automatically extract changes from previous release to current and translate to bilingual format.

```yaml
- uses: Desmond-Dong/actions/bilingual-changelog@v1
  with:
    llm-api-key: ${{ secrets.LLM_API_KEY }}
```

[查看文档 →](./bilingual-changelog/README.md)

## License

MIT
