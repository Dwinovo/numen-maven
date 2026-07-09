# numen-maven

托管 **numen-api** 引擎发布产物的静态 Maven 仓库。通过 `raw.githubusercontent.com` 提供纯文件访问,无需认证,无需服务端。

[English](README.md) | 简体中文

## 在 Gradle 中使用

添加仓库,再按加载器和 Minecraft 版本依赖 `numen-api`:

```gradle
repositories {
    maven { url = 'https://raw.githubusercontent.com/Dwinovo/numen-maven/main' }
}

dependencies {
    compileOnly 'com.dwinovo.numen:numen-api-common-1.21.1:0.0.2-SNAPSHOT'   // 按加载器改用 -fabric / -neoforge
}
```

## 坐标规则

- **Group:** `com.dwinovo.numen`
- **Artifact:** `numen-api-<loader>-<mcversion>`
- **Version:** 引擎自身版本(如 `0.0.2-SNAPSHOT`)

`<loader>` 取 `common`、`fabric`、`forge`、`neoforge` 之一。Minecraft 版本直接写进 artifactId。

| MC 版本 | common | fabric | forge | neoforge |
|---------|:------:|:------:|:-----:|:--------:|
| 1.20.1  | ✓ | ✓ | ✓ |   |
| 1.20.2  | ✓ | ✓ | ✓ |   |
| 1.20.4  | ✓ | ✓ | ✓ |   |
| 1.20.6  | ✓ | ✓ |   | ✓ |
| 1.21.1  | ✓ | ✓ |   | ✓ |
| 1.21.4  | ✓ | ✓ |   | ✓ |
| 1.21.5  | ✓ | ✓ |   | ✓ |
| 1.21.8  | ✓ | ✓ |   | ✓ |
| 1.21.10 | ✓ | ✓ |   | ✓ |
| 1.21.11 | ✓ | ✓ |   | ✓ |
| 26.1.2  | ✓ | ✓ |   | ✓ |

Forge 覆盖 1.20.x;NeoForge 覆盖 1.20.6 及以上。

## 维护

本仓库由 numen-api 的发布任务生成并更新:

```
cd numen-api && ./gradlew publish
```

请勿手改产物目录,下一次发布会覆盖它。

## 生态

- [**numen-api**](https://github.com/Dwinovo/numen-api) — 此处发布的引擎
- [**Numen**](https://github.com/Dwinovo/minecraft-numen) — 模组本体
- [**numen-qq-mcp**](https://github.com/Dwinovo/numen-qq-mcp) — 基于 numen-api 构建的插件
- [**numen-mcp**](https://github.com/Dwinovo/numen-mcp) — 基于 numen-api 构建的插件
