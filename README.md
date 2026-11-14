# Kibo for Kotlin and Android

The Kibo secrets vault for Kotlin and Android: store, list and reveal secrets.

## Contents

**A. Get started**

1. [Packages](#1-packages)
2. [Install](#2-install)

**B. Reference**

3. [Appendix: links](#3-appendix-links)
   - 3.1 [About Kilimanjaro](#31-about-kilimanjaro)

## A. Get started

### 1. Packages

| Package | Registry name | What it is for |
|---|---|---|
| [`k9o-kibo-vault`](k9o-kibo-vault) | `dev.k9o:kibo-vault` | Kibo: store, list and reveal secrets |

### 2. Install

```kotlin
// build.gradle.kts
dependencies {
    implementation("dev.k9o:kibo-vault:1.5.2")
}
```

It comes from Maven Central and needs Android API 23 or later, or JVM 17. The project client and Gate are in [sdk-kotlin](https://github.com/k9o-platform/sdk-kotlin).
Each package has its own README with a complete example and the expected output.

[↑ Back to Contents](#contents)

## B. Reference

### 3. Appendix: links

- Website: <https://kilimanjaro.dev>
- Documentation: <https://docs.kilimanjaro.dev>
- Other SDKs and the CLI: <https://github.com/k9o-platform>
- Issues and discussions: use the tabs of this repository
- License: Apache-2.0

#### 3.1 About Kilimanjaro

Kilimanjaro is a modular developer platform for building secure enterprise applications.
You define AI agents, functions and data pipelines on the platform.
The SDKs let you deploy and invoke them, read and write your data, publish to and subscribe to streams, sign users in, and encrypt with keys you hold.

It provides four building blocks:

- **Keep**: AI security and governance. Guardrails and policy for the agents you run.
- **Pulse**: data intelligence and real-time stream processing. Streams, analytics and live feeds.
- **Gate**: customer identity and access management. Sign-in and sessions, and automatic data scoping so a signed-in user reaches only their own data.
- **Kibo**: cryptographic keys and secrets management. Client-side encryption with keys you hold, and a secrets vault.

[↑ Back to Contents](#contents)
