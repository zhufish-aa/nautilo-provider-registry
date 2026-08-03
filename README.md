# Nautilo Provider Registry

Nautilo 桌面应用「插件市场」的官方注册表。应用通过 jsDelivr CDN 拉取本仓库的
[`registry.json`](https://cdn.jsdelivr.net/gh/zhufish-aa/nautilo-provider-registry@main/registry.json)
来展示可安装的 Provider 插件（不用 `raw.githubusercontent.com` 直连，避免部分网络下 TLS 不稳定）。

## 目录结构

```text
registry.json      # 插件市场数据源（应用直接读取）
packages/          # 官方插件的 .tgz 安装包（通过 raw URL 下载）
```

## 发布插件 = 提交 PR

想让自己的插件上架？向本仓库提 Pull Request：

1. **准备插件包**：按 [Nautilo 插件开发指南](https://github.com/zhufish-aa/Nautilo/blob/master/docs/provider-plugins.md)
   开发并构建插件，打出 `.tgz`（包一层顶层目录，内含 `agenthub-plugin.json` 和 `dist/`）。
2. **托管 tar 球**（二选一）：
   - 官方/信任插件：把 `.tgz` 放进本 PR 的 `packages/` 目录，
     URL 用 `https://cdn.jsdelivr.net/gh/zhufish-aa/nautilo-provider-registry@main/packages/<文件>`；
   - 第三方插件：发布到你自己仓库的 GitHub Release，使用 Release 资产 URL。
3. **计算 SHA-256**：`sha256sum your-plugin.tgz`（十六进制小写）。
4. **修改 `registry.json`**：在 `plugins` 数组追加条目：

   ```json
   {
     "id": "my-cli",
     "name": "My CLI",
     "version": "0.1.0",
     "vendor": "ACME",
     "description": { "zh-CN": "……", "en-US": "……" },
     "tarball": "<tgz 下载地址>",
     "sha256": "<tgz 的 sha256>",
     "minAppVersion": "0.1.0"
   }
   ```

5. **提 PR**，审核要点：清单字段完整、`id` 全局唯一（小写短横线）、
   `sha256` 与 tar 球一致、`apiVersion` 与宿主 `PROVIDER_API_VERSION`（当前 1）一致。

合并后用户在市场页点「刷新」即可看到新插件。

## 条目字段

| 字段 | 必填 | 说明 |
|---|---:|---|
| `id` | 是 | 插件 ID，必须等于清单 `agenthub-plugin.json` 的 `id` |
| `name` | 是 | 显示名 |
| `version` | 是 | 版本号，市场据此提示更新 |
| `vendor` | 是 | 作者/厂商 |
| `description` | 是 | 中英双语描述 |
| `tarball` | 是 | `.tgz` 下载地址（HTTPS） |
| `sha256` | 推荐 | tar 球校验和；安装时校验，缺失则跳过校验（不建议） |
| `minAppVersion` | 否 | 最低应用版本 |
