# numen-maven

A static Maven repository hosting the published **numen-api** engine artifacts. Plain files served over `raw.githubusercontent.com` — no authentication, no server.

English | [简体中文](README_ZH.md)

## Consuming in Gradle

Add the repository, then depend on `numen-api` for your loader and Minecraft version:

```gradle
repositories {
    maven { url = 'https://raw.githubusercontent.com/Dwinovo/numen-maven/main' }
}

dependencies {
    compileOnly 'com.dwinovo.numen:numen-api-common-1.21.1:0.0.2-SNAPSHOT'   // + -fabric / -neoforge per loader
}
```

## Coordinate scheme

- **Group:** `com.dwinovo.numen`
- **Artifact:** `numen-api-<loader>-<mcversion>`
- **Version:** the engine's own version (e.g. `0.0.2-SNAPSHOT`)

`<loader>` is one of `common`, `fabric`, `forge`, `neoforge`. The Minecraft version is baked into the artifactId.

| MC version | common | fabric | forge | neoforge |
|------------|:------:|:------:|:-----:|:--------:|
| 1.20.1     | ✓ | ✓ | ✓ |   |
| 1.20.2     | ✓ | ✓ | ✓ |   |
| 1.20.4     | ✓ | ✓ | ✓ |   |
| 1.20.6     | ✓ | ✓ |   | ✓ |
| 1.21.1     | ✓ | ✓ |   | ✓ |
| 1.21.4     | ✓ | ✓ |   | ✓ |
| 1.21.5     | ✓ | ✓ |   | ✓ |
| 1.21.8     | ✓ | ✓ |   | ✓ |
| 1.21.10    | ✓ | ✓ |   | ✓ |
| 1.21.11    | ✓ | ✓ |   | ✓ |
| 26.1.2     | ✓ | ✓ |   | ✓ |

Forge covers the 1.20.x line; NeoForge covers 1.20.6 and up.

## Maintenance

This repository is generated and updated by numen-api's publish task:

```
cd numen-api && ./gradlew publish
```

Don't hand-edit the artifact tree — the next publish will overwrite it.

## Ecosystem

- [**numen-api**](https://github.com/Dwinovo/numen-api) — the engine published here
- [**Numen**](https://github.com/Dwinovo/minecraft-numen) — the mod
- [**numen-qq-mcp**](https://github.com/Dwinovo/numen-qq-mcp) — addon built against numen-api
- [**numen-mcp**](https://github.com/Dwinovo/numen-mcp) — addon built against numen-api
