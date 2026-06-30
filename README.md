# numen-maven

A plain Maven repository hosting the published artifacts of
[**numen-api**](https://github.com/Dwinovo/numen-api) — a chat-capable
Minecraft AI-companion engine (Fabric + NeoForge). Tool packs such as
**numen-core** build on top of it.

No authentication needed — it's served as raw files over HTTPS.

## Each version ships two artifacts per loader

- **`…-api` (classifier `api`)** — a slim jar with only the public API surface
  (the `@NumenAction` authoring annotations, the tool contract / registration,
  the world-action task contract, and `NumenPlayer`). ~34 KB. Compile against
  this: it's small and stable, and it physically can't see engine internals.
- **the full jar** — the whole engine. This is what actually runs.

This is the same split Flywheel (`flywheel-…-api`), Create (`:slim`) and JEI
(`…-api`) use.

## Depending on numen-api (writing a tool pack)

```gradle
repositories {
    maven { url 'https://raw.githubusercontent.com/Dwinovo/numen-maven/main' }
}
```

**Fabric (Loom):**
```gradle
dependencies {
    // compile against the slim, stable API only
    modCompileOnlyApi 'com.dwinovo.numen:numen-api-fabric-1.21.1:0.0.2:api'
    // the full engine at runtime (dev testing). To ship: `include(...)` it so
    // your jar bundles the engine — players install one file (like Create+Flywheel).
    modRuntimeOnly    'com.dwinovo.numen:numen-api-fabric-1.21.1:0.0.2'
}
```

**NeoForge (ModDevGradle):**
```gradle
dependencies {
    compileOnly 'com.dwinovo.numen:numen-api-neoforge-1.21.1:0.0.2:api'
    runtimeOnly 'com.dwinovo.numen:numen-api-neoforge-1.21.1:0.0.2'
    // to ship one file: jarJar(implementation(...)) the full jar
}
```

The Minecraft version is baked into the artifactId (`numen-api-<loader>-<mcversion>`);
the trailing coordinate (`0.0.2`) is the engine's own version. The `:api` is the
classifier selecting the slim jar.

> The full engine **must** be present at runtime (the slim `:api` jar only has
> interfaces — a mod compiled against it alone won't run). Either `include`/`jarJar`
> it into your pack, or declare numen_api as a required dependency players install.

## Publishing (maintainers)

```
cd numen-api && ./gradlew publish    # writes the full + :api jars into this repo's working tree
cd ../numen-maven && git add -A && git commit -m "publish …" && git push
```
