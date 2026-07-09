# WebMelior — Project Registry

> Source of truth for all active websites. Check this before starting any work session.
> Update status whenever a project launches, pauses, or completes.

---

## ⚠️ Before touching any file

1. Identify which project the user is asking about
2. Find it in this registry — confirm the exact folder path
3. Only touch files inside that project's folder
4. If a file path doesn't match the stated project, **stop and flag it**

---

## Active Projects

### 🔒 WebMelior Personal Site
| Field | Value |
|---|---|
| **Type** | Personal — WebMelior's own marketing site |
| **Folder** | `clients/home-services-demo/site/` |
| **Vercel URL** | `demo-hvac-orpin.vercel.app` |
| **GitHub repo** | `johndly/Demo-Webmelior` |
| **Custom domain** | TBD (Vercel domain in progress) |
| **Status** | 🟢 Live |
| **Guard file** | `clients/home-services-demo/PROJECT.md` |

> ⚠️ This is NOT a client project. Do not copy its files, content, or brand into client sites.
> Do not run `/frontend-design` on client sites — it loads WebMelior's personal brand.
> Use the PLAYBOOK.md instead when building client sites.

---

## Client Projects

> Add a new entry here when a client is onboarded.

<!--
### [Client Name]
| Field | Value |
|---|---|
| **Type** | Client |
| **Business** | [Business name & trade] |
| **Folder** | `clients/[client-slug]/site/` |
| **Vercel URL** | TBD |
| **GitHub repo** | TBD |
| **Custom domain** | TBD |
| **Status** | 🟡 In progress |
| **Guard file** | `clients/[client-slug]/PROJECT.md` |
-->

---

## Project Status Key
| Emoji | Meaning |
|---|---|
| 🟢 | Live on custom domain |
| 🟡 | In progress / building |
| 🔵 | Deployed, awaiting domain |
| ⚪ | Paused |
| 🔴 | Needs attention |
