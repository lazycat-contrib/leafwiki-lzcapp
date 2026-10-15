# LeafWiki - LazyCat App

[LeafWiki](https://github.com/perber/leafwiki)（自托管 Wiki：单 Go 二进制 + SQLite + Markdown 落盘）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror）**：`ghcr.io/perber/leafwiki` 镜像经 `ghcr.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 semver tag（`channel: stable`），发现新版本自动更新版本号与镜像、构建 LPK、发布商店。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 配置

- 管理员密码：部署参数（默认随机 20 位），用户名 `admin`
- JWT 密钥：`{{ stable_secret "jwt_secret" }}` 自动生成
- 非 root 运行（`user: 1000:1000`），数据卷 `/lzcapp/var/leafwiki:/app/data`
- TLS 由 LazyCat 网关终止（X-Forwarded-Proto: https），无需 `LEAFWIKI_ALLOW_INSECURE`

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |

## 许可

MIT（上游）
