# numen-maven

A plain Maven repository hosting the published artifacts of
[**numen-api**](https://github.com/Dwinovo/numen-api) — a chat-capable
Minecraft AI-companion **engine** (Fabric + NeoForge). The engine is a pure
scheduler: it runs your tool's `invoke(ToolCall)` and waits for `complete()` —
how a tool does its work (server packets, threads, external calls) is entirely
yours. Tool packs such as **numen-core** build on top of it.

No authentication needed — served as raw files over HTTPS.

> **Current version is `0.0.1-SNAPSHOT`** (active development). A tagged release
> version will follow once the API settles.

## Each version ships two artifacts per loader

- **`…:api` (classifier `api`)** — a slim jar with only the public API surface
  (`NumenTool` / `ToolCall`, the `@NumenAction` authoring annotations +
  `ToolSchema`, the task-result envelope, and `NumenPlayer`). Compile against
  this; it's small, stable, and physically can't see engine internals.
- **the full jar** — the whole engine. This is what actually runs.

Same split Flywheel (`flywheel-…-api`), Create (`:slim`) and JEI (`…-api`) use.

## Depending on numen-api (writing a tool pack)

```gradle
repositories {
    maven { url 'https://raw.githubusercontent.com/Dwinovo/numen-maven/main' }
}
```

**Fabric (Loom):**
```gradle
configurations.all { resolutionStrategy.cacheChangingModulesFor 0, 'seconds' }  // while it's a SNAPSHOT

dependencies {
    modCompileOnlyApi 'com.dwinovo.numen:numen-api-fabric-1.21.1:0.0.1-SNAPSHOT:api'
    modRuntimeOnly    'com.dwinovo.numen:numen-api-fabric-1.21.1:0.0.1-SNAPSHOT'
    // to ship one file (like Create bundles Flywheel): also `include(...)` the full jar
}
```

**NeoForge (ModDevGradle):**
```gradle
dependencies {
    compileOnly 'com.dwinovo.numen:numen-api-neoforge-1.21.1:0.0.1-SNAPSHOT:api'
    runtimeOnly 'com.dwinovo.numen:numen-api-neoforge-1.21.1:0.0.1-SNAPSHOT'
    // to ship one file: jarJar(implementation(...)) the full jar
}
```

The Minecraft version is baked into the artifactId (`numen-api-<loader>-<mcversion>`);
`0.0.1-SNAPSHOT` is the engine's own version. The `:api` classifier selects the slim jar.

> The full engine **must** be present at runtime (the slim `:api` jar is interfaces
> only). Either `include`/`jarJar` it into your pack, or require numen_api as a
> dependency players install.

## Publishing (maintainers)

```
cd numen-api && ./gradlew publish    # writes the full + :api jars (timestamped SNAPSHOT) here
cd ../numen-maven && git add -A && git commit -m "publish …" && git push
```
