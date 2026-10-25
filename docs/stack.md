# AnyPS5 in the Innotel Platform Stack

**Role: BuilderOps** — Port executables to Linux and Windows without an emulator.

Part of the [Innotel Platform Stack](https://github.com/innotelinc/innotel-platform-stack).
The canonical definition of the stack, its shared layers and their owners lives
there; this file records only what AnyPS5 does inside it.

## Boundaries

### Owns

- the relinker
- the system PRX library implementations
- the build documentation

### Consumes

- binaries the user supplies
- the target platform's compiler and linker
- Cerulean Vault (deployment secrets, if hosted)

### Does not own

- the binaries being ported
- any proprietary firmware or keys
- identity (Cerulean)

## Service map

| Component | Technology | Job |
| --- | --- | --- |
| AnyPS5 | Node.js / TypeScript | Port executables to Linux and Windows without an emulator. |
| Identity | Cerulean Authentik | Sign-in and role claims, where the repo has a UI |
| Secrets | Cerulean Vault (KV v2) | Production credentials, referenced as `vault://` |
| Trust | Cerulean | DNS, TLS and the public hostname |
| Edge | NPM Edge | The public route in front of the service |

## In the ecosystem

- **Identity** comes from Cerulean Authentik; this repo holds no second account
  table and no password of its own.
- **Secrets** come from Cerulean Vault. `.env` is local only and is never
  committed; a `vault://` reference is resolved by the deployment.
- **Trust and edge** are Cerulean's and NPM Edge's. This repo does not write DNS
  records or call the NPM API directly.
- **Storage, billing and telephony** belong to ONYX, Magnate and Zeus
  respectively; AnyPS5 consumes them only where the boundaries above say
  so.

## See also

- [README](../README.md)
- [Innotel Platform Stack](https://github.com/innotelinc/innotel-platform-stack)
