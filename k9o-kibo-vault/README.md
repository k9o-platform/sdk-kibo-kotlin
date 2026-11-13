# dev.k9o:kibo-vault

Official Kotlin SDK for [Kilimanjaro](#51-about-kilimanjaro) Kibo Vault.
Store, list and reveal secrets in the Kibo vault from your Android and Kotlin app.

## Contents

**A. Get started**

1. [Install](#1-install)
2. [Choose the right package](#2-choose-the-right-package)
3. [Quick start](#3-quick-start)

**B. Use Kibo**

4. [Behaviour to know about](#4-behaviour-to-know-about)

**C. Reference**

5. [Appendix](#5-appendix)
   - 5.1 [About Kilimanjaro](#51-about-kilimanjaro)

## A. Get started

### 1. Install

```kotlin
// build.gradle.kts
dependencies {
    implementation("dev.k9o:kibo-vault:1.5.0")
}
```

Requires Android API 23 or later (or JVM 17). It talks to the gateway over its HTTP API.

### 2. Choose the right package

| Package | Use it when you are… | Registry | Source |
| --- | --- | --- | --- |
| `dev.k9o:core-kotlin` | Calling the platform from an Android or Kotlin app as a signed-in user. | [Maven Central](https://central.sonatype.com/artifact/dev.k9o/core-kotlin) | [sdk-kotlin](https://github.com/k9o-platform/sdk-kotlin) |
| `dev.k9o:gate` | Signing users in: sign in, refresh and sign out. | [Maven Central](https://central.sonatype.com/artifact/dev.k9o/gate) | [sdk-kotlin](https://github.com/k9o-platform/sdk-kotlin) |
| `dev.k9o:kibo-vault` | Storing, listing and revealing secrets in the vault. | [Maven Central](https://central.sonatype.com/artifact/dev.k9o/kibo-vault) | [sdk-kibo-kotlin](https://github.com/k9o-platform/sdk-kibo-kotlin) |

### 3. Quick start

Vault functions are `suspend` functions. Call them from a coroutine.

```kotlin
import dev.k9o.kibo.vault.VaultClient

val vault = VaultClient(orgBaseUrl = "https://acme.api.k9o.io", projectSlug = "my-project")

vault.secrets.create(name = "db/pw", value = "hunter2")
val challenge = vault.secrets.revealChallenge("db/pw")
val revealed = vault.secrets.reveal("db/pw", challenge = challenge.challenge)
println(revealed.value)
```

```text
hunter2
```

Values are plaintext in your code. The SDK handles the wire encoding.

## B. Use Kibo

### 4. Behaviour to know about

- Reading a secret is a two-step flow: ask for a challenge, then reveal with it.
- `region` is optional on every named-secret method. It is sent only when you pass it.
- `get(name)` finds a secret by its exact name and returns its metadata, never its value.
- `get(name)` throws `VaultError.Api` with code `K9O_NOT_FOUND` when no secret has that name.
- `update()` returns `{id, name, version}`, not the full summary.
- `delete()` succeeds on any 2xx response.
- The client adds no `Authorization` header. To authenticate, pass an `httpClient` with an interceptor that adds it.

#### Methods

| Method | Meaning |
|---|---|
| `list(prefix, cursor, limit)` | List secret metadata |
| `get(name)` | One secret's metadata, found by exact name |
| `create(name, value, region, visibility, metadata)` | Create a secret |
| `revealChallenge(name, region, reason)` | Get a single-use challenge; `reason` is optional |
| `reveal(name, challenge, region)` | Read the plaintext value with a challenge |
| `update(name, value, region, metadata)` | Set a new value; returns `UpdateSecretResult` |
| `rotate(name, region)` | Re-wrap the secret under a new key |
| `move(name, newPath, region)` | Change the secret's path |
| `delete(name, region)` | Retire the secret |

Failures are thrown as `VaultError`: `Api` (with `code`, `statusCode`), `Network` or `Decoding`.

## C. Reference

### 5. Appendix

- [About Kilimanjaro](#51-about-kilimanjaro)

#### 5.1 About Kilimanjaro

Kilimanjaro is a modular developer platform for building secure enterprise applications.
You define AI agents, functions and data pipelines on the platform.
The SDKs let you deploy and invoke them, read and write your data, publish to and subscribe to streams, sign users in, and encrypt with keys you hold.

It provides four building blocks:

- **Keep**: AI security and governance. Guardrails and policy for the agents you run.
- **Pulse**: data intelligence and real-time stream processing. Streams, analytics and live feeds.
- **Gate**: customer identity and access management. Sign-in and sessions, and automatic data scoping so a signed-in user reaches only their own data.
- **Kibo**: cryptographic keys and secrets management. Client-side encryption with keys you hold, and a secrets vault.
