# numen-maven

A plain Maven repository hosting the published artifacts of
[**numen-api**](https://github.com/Dwinovo/numen-api) — a chat-capable
Minecraft AI-companion engine (Fabric + NeoForge). Tool packs such as
**numen-core** build on top of it.

No authentication needed — it's served as raw files over HTTPS.

## Usage (Gradle)

```gradle
repositories {
    maven { url 'https://raw.githubusercontent.com/Dwinovo/numen-maven/main' }
}

dependencies {
    // Fabric (Loom) — also bundle it with `include(...)` to ship one jar:
    modImplementation 'com.dwinovo.numen:numen-api-fabric-1.21.1:0.0.2'

    // NeoForge (ModDevGradle):
    // implementation  'com.dwinovo.numen:numen-api-neoforge-1.21.1:0.0.2'

    // Loader-agnostic engine classes (for a `common` source set):
    // compileOnly     'com.dwinovo.numen:numen-api-common-1.21.1:0.0.2'
}
```

The Minecraft version is baked into the artifactId (`numen-api-<loader>-<mcversion>`);
the trailing coordinate (`0.0.2`) is the engine's own version.

## Publishing

Artifacts are pushed here from the numen-api project:

```
cd numen-api && ./gradlew publish    # writes into this repo's working tree
cd ../numen-maven && git add -A && git commit -m "publish ..." && git push
```
