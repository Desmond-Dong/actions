# GitHub Actions Collection / GitHub Actions 集合

可复用的 GitHub Actions 集合。

Collection of reusable GitHub Actions.

## Actions

### [双语变更日志生成器 / Bilingual Changelog Generator](./bilingual-changelog)

自动提取上一个 release 到当前的变更记录并翻译成双语格式。

Automatically extract changes from previous release to current and translate to bilingual format.

```yaml

- name: Generate changelog
  id: changelog
  if: github.event_name != 'release' && steps.check_tag.outputs.exists == 'false'
  uses: Desmond-Dong/actions/bilingual-changelog@main
  with:
    llm-api-key: ${{ secrets.LLM_API_KEY }}
    llm-api-url: ${{ secrets.LLM_API_URL }}
    llm-model: ${{ secrets.LLM_MODEL }}
```

[查看文档 →](./bilingual-changelog/README.md)

## License

MIT
