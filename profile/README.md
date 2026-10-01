<p align="center"><img src="/profile/assets/wordmark-auto.svg" alt="orbis" width="460"></p>
<p align="center"><b>your life, one dashboard.</b></p>

orbis is a self-hosted, modular life manager. one hub on your own hardware, one dashboard you design yourself, and modules for everything you want on it: todos, weather, calendar, smart home, media, whatever someone writes next. web, android/ios and (soon) e-ink displays all talk to the same hub.

| repo | what |
| --- | --- |
| [**orbis**](https://github.com/orbis-hub/orbis) | the hub (server), the web app, the mobile wrapper, the sdk and the first-party modules |
| [**registry**](https://github.com/orbis-hub/registry) | `index.json` the hub's module store reads; open a pr to list your module |
| [**module-template**](https://github.com/orbis-hub/module-template) | github template: a complete module to copy and build on |

### how it fits together

```
┌──────────── clients ────────────┐      ┌──────────── hub (node, docker) ──────────────┐
│ web (next.js static export)     │ REST │ auth · dashboards · settings · websocket     │
│ mobile (capacitor, same build)  │  +   │ module runtime · installer · registry client │
│ e-ink (esp32 fetches a png)     │  WS  │ device registry + network scanner            │
└─────────────────────────────────┘      └──────────────────────────────────────────────┘
```

a module is a folder with a `module.json`, a `dist/server.js` that runs inside the hub and a `dist/client.js` that renders widgets and pages in the app. modules are installed at runtime from a registry, no rebuild of the hub needed.

### quick start

```bash
git clone https://github.com/orbis-hub/orbis && cd orbis
docker compose up -d        # → http://<host>:3001, create the owner account, add widgets
```

### build a module

use the template, write `src/server.ts` and `src/client.tsx`, then `pnpm watch --dev=<hub data dir>` hot-reloads it into a running hub. `pnpm pack` produces the `module.tgz` a github release ships. details in the [orbis readme](https://github.com/orbis-hub/orbis#modules).
