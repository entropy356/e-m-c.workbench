# 认可署名自动化机制

本文记录认可署名的当前自动化实现。署名权限、格式、范围与效力以[文档规则](../rules/documentation.md)为准。

## 执行时机

- GitHub Actions 工作流位于 `.github/workflows/endorsements.yml`，在推送到 `main` 后触发。
- 工作流先运行 `tests/` 中的测试；测试通过后，才执行署名归档与清理。
- 脚本以触发推送前后的提交为比较对象，检查该版本中的 Markdown 文件。
- 工作流使用完整 Git 历史，并通过并发组串行处理；缺少可验证的前一提交时，脚本会停止，不猜测历史状态。
- 工作流未成功完成前，不应将新署名视为已验证。

## 署名归档

脚本 `scripts/endorsements.py` 解析 Markdown 中的认可注释，并根据注释确定署名身份与认可范围。

对每条可归档的署名，脚本计算认可范围正文的 SHA-256 指纹。计算时会排除认可注释本身。归档记录包含：

- 文档路径；
- 署名身份；
- 认可范围；
- 所属标题路径；
- 正文指纹。

记录以带注释的 Git Tag 保存，命名空间为 `endorsements/v1/`，Tag 指向产生该署名的具体提交，Tag 消息保存上述元数据。工作流随后将新 Tag 推送到远端。

## 失效检测与清理

- 后续运行时，脚本根据文档路径、身份、范围、标题路径和正文指纹核对已有归档记录。
- 认可范围正文发生变化后，指纹不再匹配；原署名不会因仍留在文档中而自动续认。
- 需要对修改后的内容重新认可时，应先移除旧署名并提交，再为新内容添加署名。
- 无法验证的署名注释会从当前 Markdown 文档中移除；历史版本及其归档记录仍由 Git 保留。
- 如果清理导致 Markdown 文件发生变化，工作流会以 `github-actions[bot]` 提交清理结果并推送到 `main`。

## 实现位置

- 工作流：[.github/workflows/endorsements.yml](../.github/workflows/endorsements.yml)
- 实现脚本：[scripts/endorsements.py](../scripts/endorsements.py)
- 自动化测试：[tests/test_endorsements.py](../tests/test_endorsements.py)
