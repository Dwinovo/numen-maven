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

**Numen**（[minecraft-numen](https://github.com/Dwinovo/minecraft-numen)）是那个 mod——AI 同伴本体,跑在 **[numen-api](https://github.com/Dwinovo/numen-api)** 引擎上(经 **[numen-maven](https://github.com/Dwinovo/numen-maven)** 发布),引擎对外开放一套小巧的公共 API。两类东西建在它之上： *(本仓库)*

**扩展一个同伴**——同伴自己的大脑仍然做主:
- **桥(Bridge)** 把一个外部渠道接进同伴:消息进来,同伴自己决定怎么做。基于 `NumenGateway`。→ **[numen-qq-bridge](https://github.com/Dwinovo/numen-qq-bridge)**(QQ),后续还有更多。
- **技能(Skill)** 教同伴怎么做事——markdown 注入它的上下文。随 Numen 内置,或社区编写。

**把 Numen 暴露出去**——把操控权交给外部大脑:
- **[numen-mcp](https://github.com/Dwinovo/numen-mcp)** 是一个 Model Context Protocol 服务器:任意外部智能体(比如 Claude)直接驱动同伴。基于 `NumenActuator`。
