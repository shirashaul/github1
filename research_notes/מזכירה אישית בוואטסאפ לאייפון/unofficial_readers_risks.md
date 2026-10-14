# Unofficial / third-party ways to let Claude read, filter and summarize a personal WhatsApp account, and the risks (as of October 2026)

Research date: 2026-10-14. Researcher notes for the report writer. Several vendor domains (whatsapp.com, beeper.com, docs.openclaw.ai, whapi.cloud) could not be fetched directly from the research environment (DNS failure), so some claims rely on search-result extracts of those pages. They are marked "(search extract)". Claims from vendor or competitor blogs are labelled as such.

**Biggest finding (new in mid-2026):** around 2026-06-30, WhatsApp started a phased server-side rollout of a passkey/WebAuthn step ("SHORTCAKE") for linking new companion devices. Many reports say this broke *new* device linking for the main unofficial libraries: Baileys (used by OpenClaw, Evolution API and others), whatsmeow (used by lharries/whatsapp-mcp) and whatsapp-rust. Sessions that were already linked are reportedly not affected. As of the latest public comments (Aug–Sep 2026), no confirmed upstream fix was found. Details are in section 2.

---

## 1. OpenClaw (formerly Clawdbot / Moltbot): WhatsApp channel, chat filtering, hosting, security incidents, Claude subscription vs API key

### Takeaway
OpenClaw connects to WhatsApp by linking itself as a WhatsApp Web companion device through Baileys, using a QR code. It runs on a computer or server you control, not on the iPhone. Its config can restrict which DMs and groups reach the agent. Since February 2026 Anthropic has said that Claude Free/Pro/Max OAuth credentials may not be used in third-party tools, so in practice OpenClaw needs a paid Anthropic API key. Security has been poor: a one-click RCE CVE, tens of thousands of instances exposed to the internet, and hundreds of malicious skills on ClawHub. For a non-technical user who also handles work data, it is high-risk.

### Cited Findings
**How the WhatsApp channel works**
- The OpenClaw docs describe the WhatsApp channel as "production-ready via WhatsApp Web (Baileys)". The gateway owns the linked session and the reconnect loop — [OpenClaw docs, channels/whatsapp.md (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- "Login is QR-only": you run `openclaw channels login --channel whatsapp` and scan the QR code with the phone, which makes OpenClaw a linked device. The docs warn that on remote or headless hosts the QR code "can expire in transit" — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md); [docs2.openclaw.ai/channels/whatsapp](https://docs2.openclaw.ai/channels/whatsapp)
- The docs say "A separate WhatsApp number is recommended", while personal-number and self-chat setups are "fully supported" — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- `selfChatMode`: when true or unset, messages you send to yourself (the "message yourself" chat) are treated as agent input. When false, they are ignored — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- WhatsApp credentials are stored on disk at `~/.openclaw/credentials/whatsapp/<account>/creds.json`, with a backup at `creds.json.bak` — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- Read receipts are sent by default for accepted inbound messages. You can turn this off with `sendReadReceipts: false` — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- On reconnect, OpenClaw "can auto-reply to offline messages that Baileys delivers early in that reconnect". Unprocessed group messages are buffered and injected as context, 50 by default (`historyLimit`; 0 disables) — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)

**Allowlists and chat filtering**
- `dmPolicy` has four values: `pairing` (the default; unknown senders request pairing and the owner approves), `allowlist` (only senders in `allowFrom` are admitted), `open` (requires `"*"` in `allowFrom`) and `disabled` (blocks all DMs) — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- `allowFrom` takes E.164 phone numbers, e.g. `"+9725..."`. It "controls DM sender access only and does not gate explicit outbound sends to group JIDs or @newsletter channels" — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- Groups: `groupPolicy` is `open`, `allowlist` or `disabled`, and `groupAllowFrom` filters group senders. A `groups` block acts as a per-group allowlist: groups not in it are dropped "before session routing". If `groups` is omitted, all groups are eligible. Group replies require a mention by default (`requireMention`) — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- With no `channels.whatsapp` block at all, the runtime falls back to `groupPolicy: "allowlist"` and logs a warning — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- A third-party guide gives the troubleshooting order for ignored group messages as `groupPolicy` first, then `groupAllowFrom`/`allowFrom` — [findstack.com guide](https://findstack.com/resources/connect-openclaw-to-whatsapp)

**Where it runs**
- The Gateway needs Node.js (current official minimums are 22.22.3+/24.15+/25.9+; Node 26 recommended) on macOS, Linux, or Windows (native Windows Hub app, PowerShell installer, or WSL2). The always-on service runs as a LaunchAgent on macOS, a systemd user service on Linux/WSL2, or a Scheduled Task on Windows. Bun is "not recommended for the Gateway — known issues with WhatsApp and Telegram channels" — [OpenClaw install overview](https://docs.openclaw.ai/install/index.html) (search extract)
- The iOS and Android apps are companion "mobile nodes". The gateway itself runs on a desktop or server — [OpenClaw platforms page](https://docs2.openclaw.ai/platforms.md) (search extract)

**Claude subscription vs API key**
- Anthropic's official Claude Code legal page says OAuth authentication "is intended exclusively for purchasers of Claude Free, Pro, Max, Team, and Enterprise subscription plans and is designed to support ordinary use of Claude Code and other native Anthropic applications". It also says: "Anthropic does not permit third-party developers to offer Claude.ai login into their own applications, or to route requests through Free, Pro, or Max plan credentials on behalf of their users… developers may not collect, store, or intermediate Claude.ai credentials or session tokens", and "Anthropic reserves the right to take measures to enforce these restrictions and may do so without prior notice." — [Claude Code docs: Legal and compliance](https://code.claude.com/docs/en/legal-and-compliance) (fetched 2026-10-14)
- Reporting dates the restriction to a documentation and terms update on 2026-02-19/20. That update said consumer OAuth tokens are for Claude Code and Claude.ai only, and that using them in the Agent SDK or other tools is a consumer-terms violation — [Gigazine, 2026-02-20](https://gigazine.net/gsc_news/en/20260220-anthropic-third-party-block); [WinBuzzer, 2026-02-19](https://winbuzzer.com/2026/02/19/anthropic-bans-claude-subscription-oauth-in-third-party-apps-xcxwbn/); [LetsDataScience](https://letsdatascience.com/news/anthropic-revises-terms-to-bar-third-party-harnesses-b7377cc7)
- Secondary reports say server-side blocking of consumer OAuth in third-party clients began 2026-01-09. They also say Pro/Max subscriptions stopped working with OpenClaw specifically on 2026-04-04, with a one-time credit offered. These come from single secondary sources and are **unconfirmed by an Anthropic primary source** — [implicator.ai](https://www.implicator.ai/anthropic-cuts-openclaw-from-claude-subscriptions-citing-unsustainable-compute-costs/); [pasqualepillitteri.it](https://pasqualepillitteri.it/en/news/642/anthropic-blocks-openclaw-third-party-tools-claude-subscriptions); [CybersecurityNews](https://cybersecuritynews.com/claude-ends-openclaw-subscriptions/); [MindStudio](https://www.mindstudio.ai/blog/anthropic-openclaw-ban-oauth-authentication)
- OpenClaw's own Anthropic provider docs say: "For Anthropic accounts, we recommend using an API key". They still document a `claude setup-token` subscription path, and tell users who see "This credential is only authorized for use with Claude Code and cannot be used for other API requests" to switch to an API key — [OpenClaw Anthropic provider docs](https://docs.openclaw.ai/providers/anthropic/index.html) (search extract); [jsdelivr mirror v2026.2.1](https://cdn.jsdelivr.net/npm/openclaw1@2026.2.1/docs/providers/anthropic.md)
- Reports say OpenClaw's creator Peter Steinberger joined OpenAI in February 2026. Commentators linking this to Anthropic's enforcement are speculating — [pasqualepillitteri.it](https://pasqualepillitteri.it/en/news/642/anthropic-blocks-openclaw-third-party-tools-claude-subscriptions)

**Security incidents**
- **CVE-2026-25253 (CVSS 8.8, one-click):** the Control UI trusted a `gatewayUrl` query parameter, so a crafted link could make the victim's browser send its gateway auth token to an attacker, reportedly even for localhost-bound instances. It was fixed in v2026.1.29 (~2026-01-30). Sources disagree on the exact mechanism — [clawdocs known vulnerabilities](https://clawdocs.org/security/known-vulnerabilities); [Claude Market blog](https://claudemarket.ai/blog/openclaw-security-crisis-explained)
- **Exposed instances:** SecurityScorecard first reported ~40,000 internet-exposed OpenClaw instances, a figure later cited as 42,900 across 82 countries with ~15,200 vulnerable to RCE. Later scans reportedly found 135,000+. These are secondary write-ups, and the original SecurityScorecard and The Register articles were not fetched — [Techzine](https://www.techzine.eu/news/security/138633/over-40000-openclaw-agents-vulnerable/); [Claude Market blog](https://claudemarket.ai/blog/openclaw-security-crisis-explained); [DigitalOcean](https://www.digitalocean.com/resources/articles/openclaw-security-challenges)
- A Shodan-based analysis reported that 63% of exposed instances had authentication disabled and that exposed instances leaked API keys and chat histories (secondary, vendor blog) — [barrack.ai blog](https://blog.barrack.ai/openclaw-security-vulnerabilities-2026/)
- **Malicious skills on ClawHub ("ClawHavoc"):** Koi Security audited 2,857 ClawHub skills and found 341 malicious ones. 335 of them belonged to one campaign that used fake prerequisites to install Atomic Stealer (AMOS, a macOS infostealer). Lures included crypto trackers, Polymarket bots, YouTube utilities and Google Workspace integrations, and the campaign targeted always-on machines such as Mac minis — [The Hacker News, Feb 2026](https://thehackernews.com/2026/02/researchers-find-341-malicious-clawhub.html); [Koi Security](https://koi.ai/blog/clawhavoc-341-malicious-clawedbot-skills-found-by-the-bot-they-were-targeting); [SC World](https://www.scworld.com/news/openclaw-agents-targeted-with-341-malicious-clawhub-skills)
- Koi's 2026-02-16 update raised the count to 824 malicious skills out of 10,700+ — [Koi Security](https://koi.ai/blog/clawhavoc-341-malicious-clawedbot-skills-found-by-the-bot-they-were-targeting) (via search extract)
- Skills run with the agent's full privileges (filesystem and network). The only barrier to publishing was reportedly a GitHub account older than one week. OpenClaw responded by adding VirusTotal scanning and skill reporting — [Immersive Labs](https://www.immersivelabs.com/resources/c7-blog/openclaw-what-you-need-to-know-before-it-claws-its-way-into-your-organization); [elephas.app](https://elephas.app/resources/openclaw-ai-agent-security-risks) (secondary)
- One blog headline claims "138 security flaws in 63 days". Only the title was seen — [LobsterPack](https://www.lobsterpack.com/blog/openclaw-security-vulnerabilities-business/)

### Inferences
- OpenClaw can restrict which chats *trigger the agent* (`dmPolicy: "allowlist"` + `allowFrom`, `groupPolicy: "allowlist"` + a `groups` allowlist, or `groupPolicy: "disabled"`). However, as a linked device, Baileys still receives and decrypts *every* incoming message on the host machine. The filter decides what reaches the model; it does not limit what lands on the computer. Combined with a buffered group history and auto-reply-on-reconnect behavior, a misconfiguration could let municipality messages reach Claude.
- The "self-chat as command channel" pattern (`selfChatMode`), combined with `dmPolicy: "disabled"` and `groupPolicy: "disabled"`, looks like the tightest configuration: only notes you send to yourself reach the agent. That is not "read and summarize my incoming messages", though. Summarizing incoming chats requires admitting those chats.
- `allowFrom` does not gate outbound sends. An agent with send capability could still message arbitrary groups or channels if prompted or injected.
- Cost model: since the consumer-OAuth ban, running OpenClaw with Claude means paying per-token API rates on top of any Claude subscription.

### Gaps
- Whether OpenClaw's Baileys version has a working passkey-linking path after the June 2026 WhatsApp change (section 2). I found no OpenClaw-specific issue confirming or denying it.
- I found no primary Anthropic statement for the 2026-04-04 OpenClaw cutoff date or the credit offer.
- I could not verify whether DMs blocked by `dmPolicy` are fully discarded before any model call. The docs state this explicitly only for groups outside the `groups` block.
- There is no measured data on WhatsApp ban rates for OpenClaw users (only anecdotes; section 5).

---

## 2. Baileys / whatsapp-web.js / whatsmeow and products built on them (WAHA, Evolution API, Green API, Whapi): mechanism, ban risk, and the June 2026 passkey gate

### Takeaway
All of these tools reverse-engineer the WhatsApp Web / multi-device companion protocol and act as a linked device. They are explicitly outside WhatsApp's terms and can be banned at any time. Since about 2026-06-30, WhatsApp's new passkey/WebAuthn linking step has broken *new* device linking for Baileys, whatsmeow and whatsapp-rust for many users, and no confirmed fix appears in the public issue trackers as of Sep 2026.

### Cited Findings
**Mechanism and products**
- Evolution API is open source and legal, but its Baileys connector "violates the platform's terms of service and can get a number permanently banned". Meta can change the protocol at any time, breaking service until Baileys is updated — [pasqualepillitteri.it (Evolution vs Cloud API)](https://pasqualepillitteri.it/en/news/12969/integrate-whatsapp-evolution-api-vs-cloud-api)
- Evolution API's own docs say unofficial Baileys use carries ban risk when misused, and advise rate limiting and avoiding bulk messaging — [Evolution API docs (Mintlify)](https://mintlify.com/EvolutionAPI/evolution-api/whatsapp/baileys)
- Green API, an unofficial hosted gateway, concedes "there is always a risk of losing the option to use WhatsApp on your phone number" (vendor's own blog) — [Green API blog](https://green-api.com/en/blog/sravnivaem-green-api-i-officialnij-api/)
- Hosted unofficial sessions cost about $6/month per session, according to one listicle, which still warns about ban risk — [IndieHackers](https://www.indiehackers.com/post/best-10-evolution-api-alternatives-in-2026-tested-9fc702d744)
- A WhatsApp-automation agency comparison rated WAHA's ban risk "Moderate" and bulk messaging "Not recommended". This is an interested party, and the search extract did not clearly identify which page carried the table — [search results incl. achiya-automation.com](https://achiya-automation.com/en/blog/whatsapp-business-api-guide/) (attribution uncertain)
- A research note says Meta's Business API policy (effective 2026-01-15) bars general-purpose AI assistants, so unofficial libraries "like Baileys (used by Clawdbot) remain the only path for personal AI assistants, but carry significant risks including account bans and TOS violations" — [Zylos Research, 2026-01-26](https://zylos.ai/research/2026-01-26-whatsapp-api-automation)
- A vendor help page lists Baileys and WhatsApp Web automation as high-risk behaviors and claims "zero-warning direct bans" have been a trend since H2 2025. It gives no source for this — [ChatDaddy help](https://help.chatdaddy.tech/article/ban-type-distribution)
- A Baileys CVE allowed message spoofing. It was fixed in 6.7.22 and 7.0.0-rc12 — [CVE-2026-48063 entry](https://cve.threatint.com/CVE/CVE-2026-48063)

**June 2026 passkey / "SHORTCAKE" linking gate**
- Baileys issue #2672 was opened on 2026-06-30. After scanning a QR code or entering a pairing code, the phone shows "Keep the app open on both devices. You may need to scan another QR code to use your passkey", and linking times out. As of the last comment on 2026-08-24, the issue is still open with no maintainer response. Commenters say whatsmeow users see the same problem (whatsmeow #1184). Suggested workarounds include linking in real Chrome WhatsApp Web first and then importing the session via Puppeteer, which exposes full companion credentials. One commenter said the prompt mainly appears when the account is forced to create a passkey. Another, unverified, said the Go and Rust libraries had fixed it — [Baileys issue #2672](https://github.com/WhiskeySockets/Baileys/issues/2672)
- The ZeroClaw issue describes a "phased server-side rollout (~2026-06-30)" that adds a passkey/WebAuthn step to companion linking. The server sends a `passkey_prologue_request` that libraries drop, so linking stalls ("Couldn't link device, try again later"). Pair-code linking also fails. "Already-linked sessions are unaffected; the gate applies only at the link handshake." The issue was still open in Sep 2026 (milestones v0.8.5/v0.8.6 set 2026-09-10). It says the upstream whatsapp-rust fix (PR #928) "requires a real WebAuthn authenticator, which a headless server can't provide" — [zeroclaw issue #8627](https://github.com/zeroclaw-labs/zeroclaw/issues/8627)
- An OpenWA PR states that neither whatsapp-web.js 1.34.7 nor Baileys 7.0.0-rc14 implements the passkey step. It also documents a separate pairing-code rejection that is fixed by using a standard browser name — [OpenWA PR #1672](https://github.com/rmyndharis/OpenWA/pull/1672); [OpenWA issue #560](https://github.com/rmyndharis/OpenWA/issues/560)
- Whapi.Cloud, a commercial competitor, says headless servers cannot spoof the WebAuthn assertion and recommends migrating to its service. This is a vendor position — [Whapi.Cloud blog](https://whapi.cloud/blog/understanding-whatsapp-new-passkey-security-webauthn-explained) (search extract)

### Inferences
- For a user setting something up *now* (Oct 2026), the first practical obstacle for any Baileys/whatsmeow-based tool (OpenClaw, Evolution API, WAHA's Baileys/GOWS engines, lharries/whatsapp-mcp) may be that linking fails, especially if her WhatsApp account has a passkey. This is likely but not confirmed for every account, since it is a phased rollout.
- Workarounds that import a browser session into a library involve handling raw companion credentials. That raises the security stakes and pushes setup well beyond a non-technical user's reach.
- Hosted services (Green API, Whapi, hosted Evolution/WAHA) add a third party that holds the session keys and sees decrypted messages. That is an additional privacy and data-protection exposure for both the user's personal and municipal contacts.

### Gaps
- I found no authoritative statement from WhatsApp or Meta on the passkey rollout, and no confirmed Baileys release fixing it as of Oct 2026.
- I found no independent, quantified ban-rate data for WAHA vs Evolution vs Green API vs Whapi. Only vendor claims exist.
- Whether WAHA's WEBJS engine (a real Chromium running WhatsApp Web) can pass the passkey step was not researched.

---

## 3. Beeper (multi-messenger) and its Desktop API / MCP server

### Takeaway
Beeper Desktop exposes a local API and MCP server (launched Aug 2025, made stable for all users shortly after) that lets Claude Desktop or Claude Code read and send messages across all connected networks, including WhatsApp. It runs only while Beeper Desktop is open on a Mac/Windows/Linux computer. With "On-Device" connections, Beeper says WhatsApp messages do not pass through its servers. However, there is no documented per-chat allowlist or clearly documented read-only scope, so it cannot guarantee that work chats stay away from Claude.

### Cited Findings
- Beeper describes the Desktop API as "an experimental, locally hosted API and MCP server for all your chats across WhatsApp, Instagram, Telegram, Signal, Slack, and more", available "only when the app is running". It works with Claude Desktop, Claude Code and Cursor, and is enabled under Settings → Developers — [Beeper MCP page](https://www.beeper.com/mcp) (search extract)
- The Beeper blog (2025-09-03) says MCP is built on the Desktop API, which "lets you write scripts and build apps that can read all your chats and send messages across all your accounts" — [Beeper blog, Aug 2025 recap](https://blog.beeper.com/2025/09/03/beeper-august/) (search extract)
- The developer docs call it a "fully local API". The MCP endpoint is `http://localhost:23373/v0/mcp`, and by default it can't be accessed from other devices. Beeper "recommends the Desktop API for personal use only" because "sending too many messages might result in account suspension by the networks". When an account is first added, "only recent messages might be available" while it indexes, and On-Device Connections are recommended for best results — [Beeper Desktop API docs](https://developers.beeper.com/desktop-api/); [Beeper Desktop MCP docs](https://developers.beeper.com/desktop-api/mcp/) (search extracts)
- Changelog: v4.1.92 (2025-08-13) was the initial API and MCP release. v4.1.169 made the "Desktop API & MCP… available to everyone on the stable version". v4.1.239 (2025-09-26) added "Remote Access", which can expose the API to the internet — [Desktop API changelog v4.1.92](https://developers.beeper.com/desktop-api/changelog/version/v4-1-92---2025-08-13); [v4.1.239](https://developers.beeper.com/desktop-api/changelog/version/v4-1-239-2025-09-26) (search extracts)
- A 2026 Beeper Desktop release, v4.2.692 (dated 2026-03-31 by an aggregator), added account filters for Archived, Requests and Low Priority. This shows the app was still being developed in 2026 — [Releasebot (aggregator)](https://releasebot.io/updates/beeper)
- Authentication uses a bearer token created under Settings → Developers → "Approved connections", or OAuth 2.0 with PKCE. The official auth page found does not describe read-only scopes. A third-party CLI mentions a "read" permission (unverified) — [Beeper auth docs](https://developers.beeper.com/desktop-api/auth) (search extract)
- The third-party "beeperbox" MCP wrapper exposes 12 tools, including read tools (`list_inbox`, `list_unread`, `read_chat`, `search_messages`) and write tools (`send_message`, `react_to_message`, `archive_chat`). It describes no chat allowlist. It warns that binding to `0.0.0.0` without an auth token lets a same-network attacker reach the full tool surface — [GitHub hamr0/beeperbox](https://github.com/hamr0/beeperbox)
- With On-Device connections, "messages are sent directly from your device to the networks like WhatsApp and Signal, preserving end-to-end encryption", and messages "never leave your device and are not stored on Beeper servers". On-device accounts stay on the device where they were set up. Cloud connections pass data "securely through Beeper servers" — [Beeper help: on-device connections](https://help.beeper.com/using-on-device-chat-network-connections-in-beeper); [Beeper help: On-Device vs Cloud](https://help.beeper.com/troubleshooting/beeper-on-device-vs-beeper-cloud-what-goes-to-beeper-servers); [Beeper FAQ](https://www.beeper.com/faq) (search extracts)
- To stay connected you must open WhatsApp on the primary phone at least once every 12–14 days, or all linked devices, Beeper included, disconnect — [Beeper help: on-device connections](https://help.beeper.com/using-on-device-chat-network-connections-in-beeper) (search extract)
- Beeper's iOS app exists, and the generic setup is Settings → Chat Accounts → Add an account → On-device → WhatsApp. The WhatsApp guide found covers Desktop (QR) and Android, not iPhone specifically — [Beeper help: on-device connections](https://help.beeper.com/using-on-device-chat-network-connections-in-beeper); [Beeper WhatsApp guide](https://beeper.helpjuice.com/chat-networks/whatsapp); [App Store listing](https://apps.apple.com/FR/app/id6499013100) (search extracts)

### Inferences
- For Claude access, the iPhone app is irrelevant. The MCP server lives in Beeper **Desktop**, and because on-device accounts stay on the device where they were set up, WhatsApp must be connected *in Beeper Desktop on a computer that is running*. An iPhone-only user would need a Mac/PC left on.
- "On-device" is about Beeper's servers. Message content still goes to Anthropic whenever Claude calls a read or search tool. With Claude Desktop, the user can approve tool calls one by one, but there is no structural guarantee that only personal chats are queried. A broad request like "summarize my unread messages" would pull municipality chats too.
- Beeper connects to WhatsApp as a linked device, so it is also an unofficial client. Its own docs acknowledge suspension risk for heavy sending. Read-only personal use is plausibly lower risk than bulk sending, but this is not documented by WhatsApp.

### Gaps
- Beeper's ownership by Automattic (acquired 2024) was **not verified** in this session.
- Whether Beeper's WhatsApp on-device linking is affected by the June 2026 passkey gate was not found. Beeper's bridge technology was not verified either.
- No documentation was found for a read-only token scope or per-chat/per-account restriction in the Desktop API.
- The beeper.com, help.beeper.com and developers.beeper.com pages could not be fetched directly. Only search extracts were used.

---

## 4. Other options: GitHub WhatsApp MCP servers, commercial extensions/services, and manual chat export

### Takeaway
DIY MCP servers such as lharries/whatsapp-mcp copy the *entire* message history into a local SQLite database and give Claude both read and send tools. They require Go, Python and a running computer, and their own README warns about prompt-injection data exfiltration. Commercial Chrome extensions and services add yet another party that sees decrypted messages. Manually exporting a single chat ("Export Chat" on iPhone) and uploading it to Claude needs no linking and gives exact per-chat control, so it is the safest low-tech option, at the cost of being manual and not real-time.

### Cited Findings
**lharries/whatsapp-mcp**
- It connects to a personal account through the WhatsApp Web multi-device API using **whatsmeow**. A Go bridge handles QR authentication and stores message history in a local SQLite database. A Python MCP server exposes tools, and data goes to the LLM only when a tool is called — [GitHub lharries/whatsapp-mcp](https://github.com/lharries/whatsapp-mcp)
- Its tools search contacts, list messages and chats, get context, **send** text, files and voice messages, and download media — [GitHub lharries/whatsapp-mcp](https://github.com/lharries/whatsapp-mcp)
- The README warns the server is subject to the "lethal trifecta" and that "project injection could lead to private data exfiltration". It says re-authentication may be needed after about 20 days. It does not mention bans. Requirements are Go, Python, UV, and Claude Desktop or Cursor (plus a C compiler on Windows) — [GitHub lharries/whatsapp-mcp](https://github.com/lharries/whatsapp-mcp)
- **Invariant Labs (2025-04-07)** showed a malicious MCP server, offering a harmless-looking `get_fact_of_the_day()` tool with hidden instructions, hijacking an agent connected to the WhatsApp MCP. The agent sent the user's chat history to an attacker number, and the exfiltration was hidden in the message preview — [Invariant Labs](https://invariantlabs.ai/blog/whatsapp-mcp-exploited); [Simon Willison, 2025-04-09](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/); [Docker blog](https://www.docker.com/blog/mcp-horror-stories-whatsapp-data-exfiltration-issue/)
- Many other WhatsApp MCP servers are listed in directories, for example Whasapo (Go), fyimail/whatsapp-mcp2 (WhatsApp Web) and msaelices/whatsapp-mcp-server. Their quality and maintenance are unknown — [mcpservers.org Whasapo](https://mcpservers.org/ja/servers/toloco/whasapo); [mcpservers.org whatsapp-mcp2](https://mcpservers.org/servers/fyimail/whatsapp-mcp2); [Glama](https://glama.ai/mcp/servers/msaelices/whatsapp-mcp-server/inspect)

**Commercial extensions / services**
- Blueticks markets scheduling, campaigns and an "AI support agent" for WhatsApp Web, with generic "safe and secure" claims. No chat-summarization feature or data-flow detail was found — [blueticks.co](https://blueticks.co/); [TimelinesAI roundup](https://timelines.ai/whatsapp-web-chrome-extensions)
- The "WhatsApp Chat Summarizer" Chrome extension sends messages to OpenAI using the user's own API key and is not affiliated with Meta — [Chrome Web Store listing](https://chromewebstore.google.com/detail/dhmokoiiidgahafkclgngphfohnopigp)

**Manual chat export**
- On iPhone: open the chat → tap the contact or group name → Export Chat → "Attach Media" or "Without Media". The limits are about 10,000 recent messages with media and 40,000 without, and WhatsApp attributes them to email size limits. One vendor claims 100,000, which is unverified — [GuidingTech](https://www.guidingtech.com/export-whatsapp-chat-pdf/); [dev.to export guide (2026)](https://dev.to/chattopdf/whatsapp-chat-export-complete-guide-iphone-android-zip-pdf-2026-10lo); [AirDroid](https://airdroid.com/quick-guides/export-whatsapp-chat)
- **Advanced Chat Privacy** (announced April 2025) is a per-chat or per-group setting. When a participant enables it, others are blocked from exporting the chat, auto-downloading media, and "using messages for AI features". Screenshots remain possible — [BGR](https://bgr.com/tech/whatsapps-new-privacy-tool-blocks-others-from-exporting-chats-or-training-ai-with-your-data/); [AlternativeTo, Apr 2025](https://alternativeto.net/news/2025/4/whatsapp-introduces-advanced-chat-privacy-to-block-people-from-exporting-your-chat-history); [CyberInsider](https://cyberinsider.com/whatsapp-adds-advanced-chat-privacy-for-stronger-protection/)

### Inferences
- Export-and-upload is the only option where she chooses each chat explicitly before anything reaches an AI. It also involves no linked device, no always-on computer, no ToS-violating client and no ban risk from WhatsApp. It works directly from the iPhone share sheet to the Claude iOS app (inferred, not tested). The downside is that it is manual, retrospective and not filtered by sender inside the chat.
- If a contact or group has turned on Advanced Chat Privacy, exporting that chat is blocked. That is also a signal that the participants explicitly don't want their messages used with AI. Using a linked-device bot to read such a chat would arguably go against their stated wishes.
- lharries/whatsapp-mcp stores *all* chats in SQLite with no chat filter. Excluding work chats would require modifying code. That makes it unsuitable for this user's mixed personal/municipal number without developer help.

### Gaps
- How Anthropic's consumer apps handle uploaded chat exports (data retention, training opt-in) was not researched here. It belongs to another research track.
- The behaviour of Blueticks or other commercial tools with AI reading was not documented on their sites.

---

## 5. WhatsApp Terms of Service, how bans happen, whether read-only linked-device use is lower risk, and Meta enforcement

### Takeaway
WhatsApp's terms forbid accessing the service through automated means or unauthorized software, and its Help Center says linking an account to unofficial apps violates the terms and can lead to bans or restrictions. Enforcement is mostly automated, from 24-hour temporary bans to permanent bans. No official source says read-only use is safe, though practitioners consistently say low-volume personal use is lower risk than bulk or automated sending. Meta has also shut general-purpose AI assistants out of the official Business API since Jan 2026, outside the EU, Italy and Brazil, which leaves no official route for this use case.

### Cited Findings
- The WhatsApp ToS prohibits using the service, "directly or through automated means", to access, copy or modify it in unauthorized ways. Examples include reverse engineering, creating accounts through unauthorized or automated means, and building software or APIs that work like WhatsApp for third parties without authorization. Violations can lead to suspension or disabling — [WhatsApp Terms of Service](https://www.whatsapp.com/legal/terms-of-service) (search extract; exact current wording not fetched)
- WhatsApp Help Center "About unofficial apps": "using these apps or linking your WhatsApp account to unofficial versions of WhatsApp violates our Terms of Service". It names GB WhatsApp and FM WhatsApp as examples and says accounts may be banned or restricted — [WhatsApp FAQ: About unofficial apps](https://faq.whatsapp.com/1217634902127718) (search extract)
- WhatsApp Business Solution terms (section 4.7) restrict AI providers from using the platform for their own AI products in most cases — [WhatsApp Business Solution Terms](https://www.whatsapp.com/legal/business-solution-terms) (search extract)
- Since 2019-12-07, WhatsApp has said it will take legal action against "automated or bulk messaging, or non-personal use", including against those who help others do it, and even based on off-platform evidence. At that time it banned over 2 million accounts per month for bulk or automated behaviour, more than 75% without recent user reports, which indicates automated detection — [The News Minute, 2019](https://www.thenewsminute.com/article/whatsapp-sue-users-violating-its-terms-use-103591); [Mobile Ecosystem Forum, 2019-12-19](https://mobileecosystemforum.com/2019/12/19/whatsapp-will-sue-businesses-for-abusing-bulk-messaging/); [Business Insider India](https://www.businessinsider.in/whatsapp-can-sue-you-for-sending-bulk-messages/articleshow/69771841.cms) (older, 2019)
- Accounts using unofficial apps have received 24-hour suspensions, and keeping the unofficial app leads to repeated freezes — [FullPress](https://www.fullpress.it/en/whatsapp-suspension-of-some-accounts-here-are-the-reasons/) (undated news). Temporary bans are typically hours to days, and repeated violations can become permanent — [NinjaTeam guide](https://ninjateam.org/why-whatsapp-blocked-my-number-and-how-to-fix-it/) (secondary)
- WhatsApp reportedly uses machine learning to detect automation (marketing piece for an official-API vendor) — [bot.space](https://www.bot.space/blog/whatsapp-api-vs-unofficial-tools-a-complete-risk-reward-analysis-for-2025)
- OpenClaw-focused blogs say Baileys-based clients still get banned in 2026 "even when usage looks clean", that risk rises with datacenter IPs and automated-looking traffic, and that VoIP/virtual numbers are blocked aggressively. They report anecdotes of bans within 48 hours, while another blog calls the risk low for personal, moderate-volume use. WhatsApp caps linked devices at four. These are blog anecdotes, not measured rates, and the search did not map each claim to a specific page — [operator.io](https://operator.io/blog/debugging-openclaw-whatsapp-baileys); [stack-junkie](https://www.stack-junkie.com/blog/fix-openclaw-whatsapp-errors); [openclawvps.io](https://openclawvps.io/blog/openclaw-whatsapp-setup); [macaron.im](https://macaron.im/blog/openclaw-whatsapp-setup)
- **Business API AI ban:** in October 2025 WhatsApp changed its Business API policy to bar general-purpose chatbots, effective 2026-01-15 with a 90-day grace period. Affected services reportedly included ChatGPT, Perplexity and Poke — [TechCrunch, 2025-10-18](https://techcrunch.com/2025/10/18/whatssapp-changes-its-terms-to-bar-general-purpose-chatbots-from-its-platform); exemptions were granted for Italy and Brazil — [TechCrunch, 2026-01-15](https://techcrunch.com/2026/01/15/after-italy-whatsapp-excludes-brazil-from-rival-chatbot-ban); the EU opened an antitrust probe — [The Register, 2025-12-04](https://www.theregister.com/2025/12/04/eu_probes_meta_whatsapp_ai/); in March 2026 Meta offered EU access for a per-message fee (€0.0490–€0.1323) — [TechCrunch, 2026-03-05](https://techcrunch.com/2026/03/05/meta-will-allow-rival-ai-chatbots-on-whatsapp-in-europe-but-for-a-fee/)

### Inferences
- A user in Israel falls under the general (non-EEA) WhatsApp terms. Israel is not covered by the EU or Brazil carve-outs, and those concern the *Business* API anyway, not personal accounts. There is no sanctioned way to connect Claude to a *personal* WhatsApp account.
- Read-only, low-volume use from a residential IP is *plausibly* lower risk than sending. Still, the ToS and Help Center make no read/write distinction: linking an unofficial client is itself the violation. A ban would hit her single number, which carries both personal and municipality traffic, so the operational impact of a ban is high.
- The ToS reference to people who "help others" and legal action targets bulk/commercial abusers. I found no evidence of WhatsApp suing individual personal users of linked-device tools.

### Gaps
- The exact current WhatsApp ToS wording could not be fetched (whatsapp.com unreachable). Wording is from search extracts.
- No 2025–2026 Meta lawsuit specifically against unofficial-client or library developers was found in this session.
- No official WhatsApp data on read-only linked-device bans exists.

---

## 6. Security: prompt injection via incoming messages, send capability, E2EE implications, message databases

### Takeaway
Every incoming WhatsApp message is untrusted input that an attacker can write. Once Claude reads it and also holds tools that can send messages or touch files, prompt injection can turn into data exfiltration. With any linked-device bridge, end-to-end encryption ends on that bridge machine, where messages, credentials and often a full database sit in plaintext. That machine becomes a high-value target.

### Cited Findings
- The lharries/whatsapp-mcp README warns about the "lethal trifecta": access to private data, exposure to untrusted content, and the ability to communicate externally. It notes that injection could lead to private data exfiltration — [GitHub lharries/whatsapp-mcp](https://github.com/lharries/whatsapp-mcp)
- In the Invariant Labs demo (April 2025), a poisoned tool description from another MCP server made an agent use WhatsApp send-message to forward chat history to an attacker number without user alerts. Secondary sources report it was reproduced against Cursor and Claude Desktop — [Invariant Labs](https://invariantlabs.ai/blog/whatsapp-mcp-exploited); [Simon Willison](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/); [Docker](https://www.docker.com/blog/mcp-horror-stories-whatsapp-data-exfiltration-issue/)
- One arXiv-based figure cited by Docker says 5.5% of MCP servers exhibit tool poisoning (secondary) — [Docker blog](https://www.docker.com/blog/mcp-horror-stories-whatsapp-data-exfiltration-issue/)
- OpenClaw's `allowFrom` "does not gate explicit outbound sends to group JIDs or @newsletter channels". Quoting or replying to the bot "satisfies mention gating but does not grant sender authorization" — [OpenClaw docs (GitHub)](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- Plaintext at rest: OpenClaw stores WhatsApp companion credentials in `~/.openclaw/credentials/whatsapp/.../creds.json` — [OpenClaw docs](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md); whatsapp-mcp stores message history in local SQLite — [whatsapp-mcp](https://github.com/lharries/whatsapp-mcp); exposed OpenClaw instances leaked API keys and chat histories — [barrack.ai](https://blog.barrack.ai/openclaw-security-vulnerabilities-2026/) (secondary)
- ClawHub malware (Atomic Stealer) targeted always-on agent machines. An infostealer on the bridge machine could take WhatsApp session credentials and message stores — [The Hacker News](https://thehackernews.com/2026/02/researchers-find-341-malicious-clawhub.html)
- Beeper on-device keeps end-to-end encryption up to the device, and messages do not go to Beeper servers. Its Remote Access option (v4.1.239) can expose the API to the internet — [Beeper help](https://help.beeper.com/using-on-device-chat-network-connections-in-beeper); [Beeper changelog v4.1.239](https://developers.beeper.com/desktop-api/changelog/version/v4-1-239-2025-09-26) (search extracts)
- A Baileys spoofing CVE was fixed in 6.7.22 / 7.0.0-rc12 — [CVE-2026-48063](https://cve.threatint.com/CVE/CVE-2026-48063)

### Inferences
- Safer pattern: read-only tools only (no send, no file or shell access), human-in-the-loop approval for every tool call, and no other untrusted MCP servers or skills in the same client session. None of the surveyed WhatsApp integrations ships a clear documented read-only mode. OpenClaw and whatsapp-mcp both include send capability by design.
- A linked-device bridge can decrypt and send as the user. If the bridge machine is compromised, an attacker can impersonate her on WhatsApp, including to municipality contacts.
- Third-party privacy: the people writing to her (family, residents, colleagues) never consented to their messages being decrypted on a bridge and sent to an AI provider. This matters more for municipal contacts, and Advanced Chat Privacy signals explicit objection where enabled.

### Gaps
- No documented real-world incident (as opposed to a demo) of WhatsApp prompt injection against a personal-assistant user was found.
- Israeli privacy-law implications (Protection of Privacy Law, Amendment 13) and municipal or government AI-use policy were not researched in this track.

---

## 7. Filtering by chat (allowlist/denylist) BEFORE messages reach the AI, given a mixed personal/municipal number

### Takeaway
Of the unofficial options, only OpenClaw documents config-level per-sender and per-group allowlists, and even it receives every message on the host. Beeper MCP and lharries/whatsapp-mcp expose all chats to Claude's tools without a documented chat filter. Manual export is the only approach where non-selected chats never touch any AI pipeline. Using a separate, dedicated WhatsApp number or keeping work on a separate account remains the cleanest separation, but it changes her setup.

### Cited Findings
- OpenClaw: `dmPolicy: "allowlist"` with `allowFrom` admits only listed DM senders. `groupPolicy: "allowlist"` plus a `groups` block drops non-listed groups "before session routing". `groupPolicy: "disabled"` blocks all group inbound — [OpenClaw docs](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- OpenClaw recommends "A separate WhatsApp number" — [OpenClaw docs](https://github.com/openclaw/openclaw/blob/main/docs/channels/whatsapp.md)
- Beeper Desktop API: the read tools (`list_inbox`, `search_messages`, `read_chat`) span all chats. No chat allowlist is documented, and `MCP_ALLOWED_HOSTS` is a host filter, not a chat filter — [beeperbox](https://github.com/hamr0/beeperbox); [Beeper auth docs](https://developers.beeper.com/desktop-api/auth) (no scopes documented; search extract)
- whatsapp-mcp: all history goes into SQLite, and the tools list and search any chat — [whatsapp-mcp](https://github.com/lharries/whatsapp-mcp)
- Export: the user picks one chat at a time — [GuidingTech](https://www.guidingtech.com/export-whatsapp-chat-pdf/)

### Inferences
**Comparison for a non-technical iPhone user in Israel (Oct 2026):**

| Option | Connection | Needs always-on computer? | Setup effort | Chat filter before AI | Ban / ToS risk | Main extra risks |
|---|---|---|---|---|---|---|
| OpenClaw + WhatsApp | Baileys linked device (QR) | Yes (Mac/PC/VPS) | High (Node, CLI, JSON config, API key) | Yes, config allowlists (DM and group); all messages still decrypted on the host | ToS violation; ban anecdotes; new linking possibly blocked by passkey gate | Exposed instances, CVEs, malicious skills, outbound sends not gated, API costs |
| lharries/whatsapp-mcp (and similar) | whatsmeow linked device | Yes | High (Go + Python + config) | None (all chats in SQLite) | ToS violation; passkey gate | Send tool and prompt injection (Invariant demo) |
| Beeper Desktop + MCP | Beeper on-device linked device | Yes (Beeper Desktop running) | Medium (GUI app, toggle, MCP config) | None documented | Unofficial client; Beeper warns of suspension for heavy sending | Read and send across *all* networks; Remote Access option |
| Hosted gateways (Green API, Whapi, WAHA/Evolution cloud) | Baileys/web linked device on vendor servers | No (vendor runs it) | Medium–High (developer-oriented) | Only what you build | ToS violation | A third party holds session keys and decrypted messages |
| Chrome extensions (e.g. summarizers) | Run inside WhatsApp Web | Computer with browser | Low–Medium | Per-chat (manual) | Grey area; unofficial | The extension vendor / AI provider sees chats |
| Manual export → Claude app | No linking | No (iPhone only) | Low | Yes, she picks each chat | None from WhatsApp | Third-party consent; Advanced Chat Privacy may block export; manual |

- Given her requirement that work (municipality) data must never reach an AI, live-bridge options fail this requirement by architecture. At minimum the work messages are decrypted on a machine running an AI agent. Only OpenClaw offers a config allowlist, and one misconfiguration or default (`groups` omitted means all groups are eligible) would leak them.
- The data supports the manual-export approach, or moving to a separate number or account for work, as the low-risk paths. Any live integration would be best on a dedicated secondary number that receives only forwarded personal content. That matches OpenClaw's own recommendation.

### Gaps
- None of the tools document a *denylist* ("everything except these municipal chats"). OpenClaw's model is allowlist-only.
- I found no tool that filters on the phone side before messages reach the linked device. WhatsApp sends all messages to all linked devices by design (inferred from the linked-device model; not explicitly sourced here).
