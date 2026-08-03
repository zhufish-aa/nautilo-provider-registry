## 插件上架申请

- 插件 id：
- 版本：
- 插件源码仓库：
- tar 球托管位置：<!-- 本仓库 packages/ 或外部 Release URL -->

### 自检清单

- [ ] `registry.json` 条目字段完整（id / name / version / vendor / description 双语 / tarball / sha256）
- [ ] `id` 与插件包内 `agenthub-plugin.json` 的 `id` 一致，且全局唯一
- [ ] `sha256` 与 tar 球实际校验和一致（`sha256sum <file>`，十六进制小写）
- [ ] 插件 `apiVersion` 为 1
- [ ] tar 球内包含 `agenthub-plugin.json` 和构建产物 `dist/`
- [ ] 已在本地 Nautilo 中通过「从本地目录安装」验证可用

### 插件简介

<!-- 简要说明插件接入的 CLI、能力和注意事项 -->
