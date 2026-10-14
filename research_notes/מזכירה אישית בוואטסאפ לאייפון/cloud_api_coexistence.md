# WhatsApp Business Platform (Cloud API) and Coexistence for a personal Claude assistant (Israel, as of October 2026)

*Method note for the report writer: in this session WebFetch failed with DNS errors for every domain, including developers.facebook.com, docs.n8n.io, respond.io, 360dialog, techcrunch.com and mumble.co.il. Every finding below therefore comes from search-engine result summaries of the cited pages, not from full-page reads. Meta's own developer docs could not be opened directly. Most sources are BSP or vendor blogs, so treat exact numbers as "reported by" rather than "confirmed by Meta". Today's date is 2026-10-14.*

---

## 1. Cloud API phone number requirements (SIM, eSIM, landline, virtual; verification; reuse in the apps)

### Takeaway
A Cloud API number has to receive a one-time code by SMS or voice call. Once it is registered on Cloud API it cannot also run in the regular WhatsApp or WhatsApp Business app; the only exception is Coexistence, and only for WhatsApp Business app numbers. For a dedicated bot, the simplest path is a new Israeli SIM or eSIM that has never been used on WhatsApp.

### Cited Findings
- To register on Cloud API, the number must be able to receive a one-time verification code from Meta by SMS or by phone call. Guides recommend confirming that the SIM or eSIM can receive SMS or voice verification before cutover. — [Wati: API prerequisites](https://www.wati.io/en/blog/whatsapp-api-prerequisites/); [Wetarseel migration guide](https://wetarseel.ai/how-to-migrate-an-existing-whatsapp-number-to-whatsapp-business-cloud-api/)
- Two-step verification has to be turned off on the number before migration. Some BSPs lock the number, so their support team may have to release it. — [respond.io: Phone number migration](https://respond.io/help/whatsapp/phone-number-migration-to-whatsapp-cloud-api); [Brevo help](https://help.brevo.com/hc/en-us/articles/4417368315538-Migrate-your-WhatsApp-phone-number-to-WhatsApp-Business-Platform-API)
- Meta's developer docs, as summarized: a number on WhatsApp Messenger (the personal app) must have its WhatsApp account deleted before it can be used on Cloud API. A WhatsApp Business app number must either be deleted from the app or be onboarded through a partner that supports business app number onboarding (Coexistence). Deleting the account loses its chat history, so back up first. — [Meta: Migrate an existing WhatsApp number to a business account](https://developers.facebook.com/documentation/business-messaging/whatsapp/solution-providers/migrate-existing-whatsapp-number-to-a-business-account)
- Once a number is registered on Cloud API, it cannot be used with the WhatsApp Business app again unless it is first deregistered from Cloud API. — [Meta migration doc (via search summary)](https://developers.facebook.com/documentation/business-messaging/whatsapp/solution-providers/migrate-existing-whatsapp-number-to-a-business-account); [HighLevel support](https://help.gohighlevel.com/support/solutions/articles/155000007590-how-to-migrate-your-existing-whatsapp-account-to-whatsapp-cloud-api)
- A number previously held by another API provider may need a cooldown of several weeks before it can be registered again. One source says the process can take up to a month on Meta's side. — [Wetarseel](https://wetarseel.ai/how-to-migrate-an-existing-whatsapp-number-to-whatsapp-business-cloud-api/); [BoldDesk](https://support.bolddesk.com/kb/article/17949/migrating-a-phone-number-from-bsp-to-whatsapp-cloud-api)
- Moving a number between WABAs (migration, not a fresh registration) requires the source and destination WABAs to be in the same Meta Business Manager, plus business verification and a payment method. This applies to the migration path, not to a fresh number. — [Callbell](https://callbellsupport.zendesk.com/hc/en-us/articles/25162523559580-Legacy-WhatsApp-API-vs-WhatsApp-Cloud-API-How-to-migrate)
- A production number is a new object with a new Phone Number ID, separate from the test number. — [oncloudapi: test vs production](https://oncloudapi.com/blogs/whatsapp-cloud-api-test-number-vs-production-number-how-to-go-live)

### Inferences
- For scenario (a), a dedicated bot number: buy a cheap Israeli prepaid SIM or eSIM, or reuse an old number that has never been on WhatsApp, register it on Cloud API, and message it from her personal WhatsApp. Her personal number is not touched.
- She should not register her personal number on Cloud API directly. That deletes or disables its use in the WhatsApp app, so she would lose her personal WhatsApp on that number.

### Gaps
- Landline and virtual (VoIP) numbers: no source fetched in this session confirmed that they are accepted. Meta's docs have historically said that numbers able to receive a voice call, including landlines, can verify by the voice option. Treat this as unverified and check Meta's "Phone numbers" page.
- No source confirmed whether Israeli VoIP or virtual providers' numbers pass Meta's verification.

---

## 2. Can an individual qualify? Business verification, unverified limits, number caps, display name

### Takeaway
Business verification is not needed to start sending; it is needed to scale. An unverified business portfolio can message up to 250 unique users per rolling 24 hours on business-initiated messages, a cap that does not matter for a bot whose only user is its owner. The real friction for an individual is display-name approval: a personal name on its own is typically rejected unless a business nature is shown.

### Cited Findings
- "Business verification isn't required to send messages to your customers." Verification is mainly needed to scale. After verification, the business name shows even if the user has not saved the contact. — [Microsoft Learn: WhatsApp business account FAQ (citing Meta)](https://learn.microsoft.com/en-us/azure/communication-services/quickstarts/advanced-messaging/whatsapp/whatsapp-business-account-faq)
- New or unverified business portfolios start with a messaging limit of 250 unique recipients per rolling 24h for business-initiated messages. Since October 2025 the limit is shared at the business-portfolio level across all numbers, so adding numbers does not add capacity. — [Chatarmin: Messaging limits 2026](https://chatarmin.com/en/blog/whats-app-messaging-limits); [Blueticks: API without Meta verification](https://blueticks.co/blog/whatsapp-api-without-meta-verification); [Wassenger](https://wassenger.com/blog/en/whatsapp-business-api-without-verification)
- Sources disagree on the tier after verification: some give 1,000 → 10,000 → 100,000 → unlimited, others 2,000. Meta reportedly re-evaluates tiers every 6 hours. — [Uptail.ai](https://www.uptail.ai/blog/whatsapp-business-message-limits-2026-broadcast-caps-tier-progression-what-happens-when-you-hit-the-ceiling); [Wetarseel](https://wetarseel.ai/whatsapp-api-rate-limits-messaging-tiers/); [Wati: rate limits](https://www.wati.io/en/blog/whatsapp-api-rate-limits/)
- Default throughput is about 80 messages per second per phone number. — [Unipile 2026 guide](https://www.unipile.com/whatsapp-api-a-complete-guide-to-integration/)
- Display name rules: every display name is manually reviewed by Meta. A name that includes a person's name must state the nature of the business, and that must also be visible on external sources. Example: "Tom Ford Chiropractor" is acceptable, "Tom Ford" alone is not. Generic terms, geographic-only names, "Official"/"Verified" and Meta product names are not allowed. The name should match external presence (website, Facebook Page, verification documents). — [DoubleTick display-name guidelines](https://learn.doubletick.io/display-name/display-name-guidelines-for-whatsapp-business-platform); [Wati support](https://support.wati.io/en/articles/11462959-guidelines-for-choosing-your-display-name); [HighLevel](https://help.gohighlevel.com/support/solutions/articles/155000002287-whatsapp-business-display-name-guidelines); [360dialog Display Names](https://docs.360dialog.com/docs/resources/phone-numbers/display-names)
- One vendor says a website must be verified in the business portfolio before a display name can be approved. This is a single-source claim. — [Flowella knowledge base](https://knowledge.flowella.io/meta/profile-setup)

### Inferences
- An individual can create a Meta developer app and business portfolio and use Cloud API without verification. Inbound-initiated replies to herself are not limited by the 250 cap, which applies to business-initiated (template) conversations to unique users.
- Display name: she may need a business-like name, such as "[name] Assistant" or "[name] Studio", plus some external presence. A rejected or pending display name may still let the number work with restrictions. This is not confirmed; see Gaps.
- Under Israeli law an individual can open an "עוסק פטור" (exempt dealer), which may help if verification is ever needed. This is an inference only; no source covered Israeli entity types.

### Gaps
- No source addressed unregistered individuals specifically, for either business verification eligibility or display-name approval.
- The maximum number of phone numbers for an unverified portfolio (historically reported as 2) was not confirmed in any source found this session.
- Whether a number can send or receive while its display name is pending or rejected was not confirmed.

---

## 3. The free test phone number in a Meta developer app

### Takeaway
Every Meta developer app with the WhatsApp product gets a free test number with Meta's test display name. It can message only up to 5 pre-verified recipient numbers, so technically it can serve one owner. It is meant for development, though, and its permanence is not documented in the sources found.

### Cited Findings
- The test number can only message up to five recipient numbers that you add and verify in Meta's developer tools. Each recipient gets a confirmation code in WhatsApp, and messages to anyone else fail with an error. — [respond.io: WhatsApp Cloud API](https://respond.io/help/whatsapp/whatsapp-cloud-api); [oncloudapi](https://oncloudapi.com/blogs/whatsapp-cloud-api-test-number-vs-production-number-how-to-go-live)
- A third-party writeup describes the test setup as allowing "unlimited free messages to/from five phone numbers". This is a blog characterization and should be verified. — [Medium / PythonIQ: Goodbye WhatsApp Web, Hello WhatsApp Cloud](https://medium.com/pythoniq/send-unlimited-whatsapp-messages-from-python-for-free-3f9f94c02aba)
- The test number shows Meta's test name. A production number shows your business name after Meta approves it. The test number cannot be used in production. — [oncloudapi](https://oncloudapi.com/blogs/whatsapp-cloud-api-test-number-vs-production-number-how-to-go-live)
- Temporary access tokens from the developer dashboard expire in about 23–24 hours, so a test setup using them stops working daily unless a System User token is used. — [Helpwise docs](https://docs.helpwise.io/articles/223933-setup-shared-whatsapp-cloud-inbox-in-helpwise); [oncloudapi: permanent token](https://oncloudapi.com/blogs/how-to-create-a-permanent-whatsapp-business-api-access-token-for-production)

### Inferences
- For a one-user assistant, the test number with a System User permanent token is technically workable and costs nothing in Meta fees. It is a fragile basis for a permanent service: no custom name, possible changes by Meta, and it is Meta's number, not hers. A cheap dedicated SIM in production mode is the robust choice.
- Whether test-number traffic is billed under the October 2026 service-message charging was not addressed by any source.

### Gaps
- No source states whether the test number or its recipient list expires, or whether Meta rate-limits or revokes test numbers over time.
- No source states whether test-number messages count toward billing or the 1,000 free service messages.

---

## 4. Pricing as of October 2026 (per-message model, 24h window, Israel rates, worked example)

### Takeaway
Since 1 July 2025 WhatsApp bills per delivered template message. **Effective 1 October 2026, service (free-form, in-window) replies are no longer unlimited-free.** Each business phone number gets 1,000 free service messages per month, after which they are charged at the market's utility rate, about $0.0053 in Israel per third-party rate tables. Utility templates sent inside the 24h window, which were free from July 2025 to September 2026, are reportedly billable again. For a one-owner bot with a daily summary, the cost should stay between $0 and about $1–3 per month in Meta fees, before any BSP fee.

### Cited Findings
- Per-message pricing has applied since 1 July 2025, replacing per-conversation pricing. Marketing and authentication templates are always charged, even inside the service window. — [Blueticks: Pricing 2026](https://blueticks.co/blog/whatsapp-business-api-pricing-2026); [Setsmart](https://setsmart.io/blog/whatsapp-business-api-pricing); [MEF: Business models 2023–2025](https://mobileecosystemforum.com/2026/02/26/whatsapp-business-platform-business-models-2023-2025-updates/)
- Service messages were free with no cap from November 2024. **Starting 1 October 2026 they are charged per message at the utility rate after 1,000 free service messages per month.** Most sources say the 1,000 is per business phone number (a WABA with 5 numbers gets 5 × 1,000). Unused messages do not roll over, and charging starts at message 1,001. — [360dialog blog: Service message charging starts 1 Oct 2026](https://360dialog.com/blog/whatsapp-service-message-charging-october-2026/); [YCloud](https://www.ycloud.com/blog/whatsapp-api-message-pricing-update-effective-october-1-2026); [ChatMaxima](https://chatmaxima.com/blog/whatsapp-service-message-pricing-october-2026/); [respond.io: Pricing change 2026](https://respond.io/blog/whatsapp-pricing-change-2026). Conflict: one source describes the allowance as per WABA rather than per number — [Chat2Desk](https://chat2desk.com/en/blog/articles/whatsapp-business-api-billing-to-change). Some older 2026 guides still describe service as free with no cap, which is now outdated — [Zernio blog (pre-October table)](https://zernio.com/blog/whatsapp-business-api-pricing)
- Utility templates inside an open 24h customer service window were free from July 2025 (one source says April 2025) through September 2026. They are reportedly billable again from 1 October 2026. Sources disagree; some describe only the service-message change. — [respond.io](https://respond.io/blog/whatsapp-pricing-change-2026); [Kemeny Studio](https://kemenystudio.com/whatsapp-service-message-pricing); [Wati: pricing changes](https://support.wati.io/en/articles/16954666-whatsapp-business-platform-api-pricing-changes-service-messages-and-click-to-message-ads)
- One vendor reports that a WABA without a payment method still gets its 1,000 free service messages delivered. After that, service messages are **not delivered** until a payment method is added or the month resets. This is single-source and unconfirmed. — [ChatMaxima](https://chatmaxima.com/blog/whatsapp-service-message-pricing-october-2026/)
- Free entry point: all messages, including templates, are free for 72 hours inside an open free-entry-point window (opened by a Click-to-WhatsApp ad or Page CTA). This stays free after October 2026, except for "Meta Business Agent" replies. — [Overads](https://overads.io/blog/whatsapp-business-api-pricing-october-2026); [Wati support](https://support.wati.io/en/articles/16954666-whatsapp-business-platform-api-pricing-changes-service-messages-and-click-to-message-ads)
- **Israel (+972) rates per message, USD, as listed by third parties for the 1 Oct 2026 rate card:** Marketing **$0.0353**. Utility, authentication and service (after the free 1,000) **$0.0053** each. Authentication-international is N/A for Israel. Calls are $0.0127/min. — [SleekFlow](https://sleekflow.io/en-us/blog/whatsapp-business-price); [Zernio calculator](https://zernio.com/whatsapp-api-pricing); [Whatsfly](https://whatsfly.net/whatsapp-business-api-pricing/). The same marketing and utility figures appear in an Israeli calculator citing the 1 April 2026 rate card — [Mumble.co.il calculator](https://mumble.co.il/messages-pricing-calculator/)
- Meta's 1 April 2026 rate changes named Saudi Arabia, India, Pakistan and Turkey; Israel was not listed among them. — [Meta pricing page (search snippet)](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing)
- Pricing depends on the recipient's country code. Volume tiers can lower rates. — [Whatsfly](https://whatsfly.net/whatsapp-business-api-pricing/)
- BSP overhead: Twilio adds about $0.005 per message on top of Meta's rates (and reportedly $0.001 per failed message). 360dialog charges a flat platform fee of about €49 (or $49) per month on its entry tier and passes Meta rates through. Direct Cloud API from Meta has no platform fee. — [EZContact comparison](https://ezcontact.ai/en/blog/whatsapp-api-pricing-comparison-meta-twilio-360dialog-ezcontact/); [Engrana: Twilio vs 360dialog](https://engrana.es/en/blog/twilio-vs-360dialog-whatsapp-business-api); [Chatmaid](https://www.chatmaid.net/blog/whatsapp-api-pricing-comparison-2026)

### Inferences
**Worked example: bot replies only to the owner, plus one daily morning summary, Israeli recipient, direct Cloud API with no BSP.**
- Replies to the owner are service messages, because each of her messages opens a 24h window. Up to 1,000 per month per number cost **$0**. Above that, each costs about $0.0053; for example 1,500 replies/month → 500 × $0.0053 ≈ **$2.65**.
- Morning summary, case A: she messaged the bot within the previous 24h, so the summary can be a free-form service message and is covered by the 1,000 free allowance → **$0**.
- Morning summary, case B: the window is closed, so a pre-approved template is required. As a utility template: 30 × $0.0053 ≈ **$0.16/month**. If Meta classifies it as marketing (a generic digest not tied to a transaction could be re-categorized): 30 × $0.0353 ≈ **$1.06/month**.
- Realistic total: **about $0–$1.10 per month in Meta fees** for normal personal use under 1,000 replies, plus about €49/month if a 360dialog-style BSP is used, or about +$0.005 per message with Twilio. Claude API and hosting costs are separate.
- A practical tip: if she messages the bot each evening, a morning summary sent within 24h of that message needs no template.
- Even with near-zero spend, a payment method should probably be added, given the reported non-delivery after 1,000 messages without one.

### Gaps
- Meta's official rate card could not be opened. The Israel figures come from third-party tables that agree with each other.
- Whether the 1,000 free allowance is per phone number or per WABA is mostly agreed (per number) but not unanimous.
- Whether test-number traffic is billed was not covered.

---

## 5. The 24-hour customer service window and template approval

### Takeaway
Free-form messages can only be sent within 24h of the user's last inbound message. Outside the window, only pre-approved templates (marketing, utility, authentication) can be sent. Templates are submitted through WhatsApp Manager or the API and reviewed by Meta, which can re-categorize them.

### Cited Findings
- Non-template messages inside the 24h customer service window are service messages. Utility templates inside the window were free from July 2025 to September 2026. Marketing and authentication templates are charged even inside the window. — [Blueticks](https://blueticks.co/blog/whatsapp-business-api-pricing-2026); [Wati templates guide](https://www.wati.io/en/blog/whatsapp-api-templates-guide/)
- Template types, pricing and best practices: more than 20 template types across marketing, utility and authentication. — [Wati: API templates guide](https://www.wati.io/en/blog/whatsapp-api-templates-guide/)

### Inferences
- A personal assistant mostly runs inside the window. Proactive pings such as reminders or the morning summary when she has not written in 24h need an approved utility template, for example "Your daily summary for {{1}}: {{2}}". Templates with a free-text variable carrying the whole summary may be rejected or re-categorized. Shorter structured templates are safer.

### Gaps
- Meta's template-review documentation (review time, re-categorization rules, limits on variable length) could not be fetched. Background knowledge says review is usually automated and takes minutes to 24h, but this was not verified this session.

---

## 6. Tokens, webhooks, and n8n, Make, Zapier, BSPs and unofficial APIs

### Takeaway
Production needs a permanent System User access token (expiry "Never", scopes `whatsapp_business_messaging` and `whatsapp_business_management`) and a publicly reachable HTTPS webhook with a verify token. n8n provides a WhatsApp Trigger (inbound) and a WhatsApp Business Cloud node (send), with a hard limit of one webhook per Meta app. Make has an equivalent "WhatsApp Business Cloud" app. Green API and similar WhatsApp-Web-based tools are unofficial and risk bans.

### Cited Findings
- Temporary tokens expire in under 24h (about 23h). A permanent token comes from a System User in Meta Business Manager: set expiry to "Never", assign the app and WABA, and grant `whatsapp_business_management` and `whatsapp_business_messaging`. The token is shown once and must be stored. — [oncloudapi: permanent token](https://oncloudapi.com/blogs/how-to-create-a-permanent-whatsapp-business-api-access-token-for-production); [Sevengits](https://sevengits.com/how-to-get-permanent-token-for-using-whatsapp-cloud-api/); [Helpwise](https://docs.helpwise.io/articles/223933-setup-shared-whatsapp-cloud-inbox-in-helpwise)
- The webhook is configured in the Meta developer dashboard with a public HTTPS URL and a verify token you choose. Meta sends a verification GET request, which must be answered with the challenge value. — [GuruSup: Cloud API guide](https://gurusup.com/blog/whatsapp-cloud-api); [Hookdeck: WhatsApp webhooks guide](https://hookdeck.com/webhooks/platforms/guide-to-whatsapp-webhooks-features-and-best-practices)
- n8n official docs: "WhatsApp only allows you to register a single webhook per app." Switching between n8n's test and production webhook URLs overwrites the registered URL, so only one WhatsApp Trigger can be active per Meta app. — [n8n docs: WhatsApp Trigger](https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.whatsapptrigger); [n8n docs: Facebook Trigger WhatsApp](https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.facebooktrigger/whatsapp)
- n8n credentials: community sources say the trigger uses an OAuth-type credential (Meta App ID and App Secret), while the WhatsApp Business Cloud send node uses an access token plus WhatsApp Business Account ID. A guide lists four items needed: access token, WABA ID, App ID and App Secret. — [n8n community: verification token thread](https://community.n8n.io/t/how-do-i-add-verification-token-for-whatsapp-business-cloud-trigger/93070); [Heltar guide](https://www.heltar.com/blogs/how-to-integrate-whatsapp-with-n8n-easy-guide); [Whatsable 2026 guide](https://whatsable.app/blog/connect-n8n-to-whatsapp-business-api-2026-guide)
- Known n8n issue: on some n8n Cloud instances the "WhatsApp Business Cloud API" credential type was missing. — [GitHub n8n-io/n8n #19158](https://github.com/n8n-io/n8n/issues/19158)
- n8n integration page: [n8n.io WhatsApp Business Cloud integrations](https://n8n.io/integrations/whatsapp-business-cloud/)
- Make: the "WhatsApp Business Cloud" app has an instant "Watch Events" trigger (webhook URL plus verify token). Community threads often report the trigger not firing even though sending works. A Make staff reply says Watch Events "currently supports only new WABA flow with Regular/Coexistence mode". — [Make help: WhatsApp Business Cloud](https://www.make.com/en/help/app/whatsapp-business-cloud); [Make community: Coexistence Watch Events no messages](https://community.make.com/t/whatsapp-business-coexistence-connected-successfully-but-watch-events-receives-no-incoming-messages/115426)
- Make's Watch Events does not expose the coexistence `smb_message_echoes` event, so messages the owner sends from the app are not seen. — [Make community thread](https://community.make.com/t/whatsapp-coexistence-watch-events-does-not-expose-smb-message-echoes/114713)
- Unofficial APIs: Green API and similar WhatsApp-Web-gateway services are not official. WhatsApp "actively and increasingly fights" them, and they are recommended only as prototype-grade and expendable. A competitor's page claims thousands of Saudi accounts were permanently banned for using such tools. This is marketing-sourced and should be treated with caution. — [Whatsloop: Green API alternatives](https://whatsloop.net/en/blog/green-api-alternatives-whatsapp-business); [WaHttp providers compared](https://wahttp.com/blog/best-whatsapp-api-providers-compared); [getkanal providers](https://getkanal.com/blog/whatsapp-business-api-providers-compared)

### Inferences
- n8n must be reachable over public HTTPS, either n8n Cloud or self-hosted with a domain and TLS (or a tunnel such as Cloudflare Tunnel). An n8n instance on a home PC behind NAT will not receive Meta webhooks without one.
- Because of the one-webhook-per-app limit, she should create a dedicated Meta app for the assistant and use only the n8n production URL once live.
- Direct Cloud API (no BSP) is cheapest for a single user. A BSP mainly adds value for Coexistence onboarding (Embedded Signup), which a solo developer cannot easily run without becoming a Tech Provider.

### Gaps
- Zapier's current WhatsApp (Cloud API) trigger and action capabilities were not found in search.
- Whether n8n's WhatsApp Trigger exposes coexistence events (`smb_message_echoes`, `history`, `smb_app_state_sync`) was not found. A generic n8n Webhook node with manual Meta subscription would likely be needed (inference).

---

## 7. Coexistence: WhatsApp Business app plus Cloud API on the same number

### Takeaway
Coexistence lets an existing **WhatsApp Business app** number be onboarded to Cloud API, through Embedded Signup by a BSP or Tech Provider, while still being used in the app. Inbound 1:1 messages arrive by webhook, app-sent messages arrive as echoes, and up to about 6 months (180 days) of 1:1 history plus contacts can be synced. **Groups are not synced.** Disappearing messages and view-once are disabled in 1:1 chats, broadcast lists become read-only, live location is restricted, and WhatsApp for Windows and WearOS companions are unsupported. Israel appears supported according to a vendor table, and since about April 2026 coverage is reportedly near-global. App messages stay free and API messages are billed normally.

### Cited Findings
- **Requirement:** WhatsApp Business app version 2.24.17 or later. — [360dialog: Using WhatsApp app and Cloud API simultaneously](https://docs.360dialog.com/partner/waba-management/phone-number-and-hosting/using-whatsapp-app-and-cloud-api-simultaneously); [ChakraHQ article](https://articles.chakrahq.com/article/whatsapp-coexistence-live-eu-uk-europe-whatsapp-business-for-api-live/)
- **Countries:** An older 360dialog guide listed Australia, EU/EEA, India, Japan, Nigeria, Philippines, Russia, South Korea, South Africa, Turkey and the UK as unsupported. Israel was not on that unsupported list. ChakraHQ says all countries became supported around April 2026, with South Africa and Nigeria added after that. Seven.io says to check Meta's docs. Wassenger lists only Nigeria and South Africa as excluded. — [360dialog](https://docs.360dialog.com/partner/waba-management/phone-number-and-hosting/using-whatsapp-app-and-cloud-api-simultaneously); [ChakraHQ: Now available globally (2026)](https://articles.chakrahq.com/article/whatsapp-coexistence-live-eu-uk-europe-whatsapp-business-for-api-live/); [Seven.io help](https://help.seven.io/en/whatsapp/whatsapp-coexistence); [Wassenger](https://wassenger.com/help/coexistence)
- **Israel specifically:** ChakraHQ's per-country table marks Israel as having full coexistence support. An older Manychat post (about a year old, from the beta period) also described Israel as in a good position. No Meta source was found. — [ChakraHQ: Coexistence support by country](https://chakrahq.com/product/whatsapp/tools/whatsapp-coexistence-support/); [Manychat blog](https://manychat.com/blog/whatsapp-coexistence-grow-and-keep-your-number/)
- **Onboarding:** done through Embedded Signup offered by a BSP or Tech Provider that supports "business app number onboarding" (a QR-code flow in the app). Meta's migration doc says a business app number must either be deleted or onboarded via such a partner. — [Meta migration doc (via search)](https://developers.facebook.com/documentation/business-messaging/whatsapp/solution-providers/migrate-existing-whatsapp-number-to-a-business-account); [360dialog Coexistence onboarding](https://docs.360dialog.com/partner/onboarding/whatsapp-coexistence); [Infobip docs: Coexistence](https://www.infobip.com/docs/whatsapp/manage-integration/coexistence)
- **What syncs (webhooks):** `history` is a one-time backfill of up to 180 days of 1:1 messages sent and received in the app, delivered only if the business opts in, minutes after onboarding. `smb_app_state_sync` syncs contacts, both existing ones and later changes. `smb_message_echoes` delivers messages the business sends from the app after onboarding, to the phone-number-level webhook. — [360dialog: Coexistence webhooks](https://docs.360dialog.com/partner/onboarding/whatsapp-coexistence/coexistence-webhooks); [GitHub bellopushon/whatsapp-cloud-api COEXISTENCE.md](https://github.com/bellopushon/whatsapp-cloud-api/blob/main/skills/whatsapp-cloud-api/references/COEXISTENCE.md)
- History caveats: media (images, audio, video) are reportedly not included in the import. The history choice is irreversible without disconnecting and reconnecting. — [Exabloom](https://exabloom.com/blog/whatsapp-coexistence-what-changes-for-your-business); [GetGabs](https://getgabs.com/blogs/whatsapp-coexistence-guide/)
- **Groups:** not synchronized to the API layer. "Calls work fine; groups don't sync." — [Wetarseel](https://wetarseel.ai/whatsapp-coexistence-whatsapp-business-app-api-together/); [ChakraHQ Coexistence FAQ](https://help.chakrahq.com/chat/faqs/coexistence-faqs)
- **Features disabled or changed in the app:** disappearing messages and view-once are disabled in 1:1 chats. Live location sharing is restricted. Broadcast lists: no new lists can be created and existing ones become read-only (one source says they "cannot be edited or utilized"). — [Wati: Coexistence](https://www.wati.io/en/blog/whatsapp-coexistence-solution/); [Woztell](https://woztell.com/coexistence-whatsapp-business-api-woztell/); [Z-API](https://z-api.io/blog/en/whatsapp-coexistence-how-to-use-the-app-and-api-with-the-same-number/); [Sandra.ch](https://sandra.ch/en/blog/whatsapp-coexistence-the-business-app-and-the-api-on-the-same-number)
- **Companion devices:** previously linked devices, such as WhatsApp Web, are unlinked during onboarding, and supported companions can be re-linked afterwards. WhatsApp for Windows and WearOS are not supported, and messages from them do not trigger webhooks. — [GetGabs](https://getgabs.com/blogs/whatsapp-coexistence-guide/); [360dialog Coexistence webhooks](https://docs.360dialog.com/partner/onboarding/whatsapp-coexistence/coexistence-webhooks); [Exabloom](https://exabloom.com/blog/whatsapp-coexistence-what-changes-for-your-business)
- **Keep-alive:** if the WhatsApp Business app on the primary phone is not opened for about 14 days, Meta may disconnect the number from coexistence or stop syncing. — [InstantReply: What syncs 2026](https://www.instantreply.co/blog/whatsapp-coexistence-what-actually-syncs-2026); [Whautomate](https://whautomate.com/whatsapp-coexistence); [ChakraHQ](https://chakrahq.com/help/learning-centre/whatsapp-business-api/all-about-whatsapp-coexistence)
- **Throughput:** 20 messages per second, shared between app and API. Some providers cite 5 mps for their setup. — [Infobip docs](https://www.infobip.com/docs/whatsapp/manage-integration/coexistence); [Whautomate](https://whautomate.com/whatsapp-coexistence)
- **Pricing:** messages sent from the Business app remain free. API-sent messages are billed per message by category and recipient country, under the standard rules in section 4. — [Wati: Coexistence for SMBs](https://www.wati.io/en/blog/coexistence-for-smbs/); [SendSeven guide 2026](https://sendseven.com/en/blog/whatsapp-coexistence-guide-2026)
- **Personal number → Business app:** third-party guides say a personal (Messenger) number can be moved to the WhatsApp Business app with chats, media, contacts and groups kept, by backing up and then restoring when verifying the same number in the Business app. The same number cannot run in both apps at once. One guide recommends using a different number instead. — [Infobip blog: change WhatsApp to business account](https://www.infobip.com/blog/change-whatsapp-to-business-account); [Enchant](https://www.enchant.com/convert-whatsapp-number-to-whatsapp-business); [QuickReply.ai](https://www.quickreply.ai/blog/how-to-convert-your-whatsapp-account-to-whatsapp-business-account)

### Inferences
- **Could Coexistence let an AI read her own incoming messages?** Technically yes, for 1:1 chats only. If she converts her personal number to the WhatsApp Business app and onboards it via a coexistence-capable BSP, every inbound 1:1 message from any contact reaches her webhook (n8n), her own app replies arrive as echoes, and up to 180 days of 1:1 history can be backfilled. **Group messages would not reach the API at all.**
- Real costs and caveats for a personal number:
  - (1) Her contacts would see a business account.
  - (2) Disappearing messages and view-once are lost in her 1:1 chats, and the WhatsApp Windows app is unsupported.
  - (3) She must open the Business app at least every ~14 days.
  - (4) Any API-sent reply to contacts is a business message under the 24h window and pricing rules.
  - (5) Contacts' private messages flow to a BSP, n8n and Anthropic. This is a privacy and consent issue for third parties, especially under Israeli privacy law (not researched here).
  - (6) A BSP with coexistence-capable Embedded Signup is needed, typically with a monthly fee. A solo developer would otherwise need Tech Provider status.
  - (7) The Meta AI-provider policy in section 8 adds risk.
- A safer design for a "secretary" that reads her messages is a separate bot number (scenario a) that she forwards messages to manually, or the official integration surfaces of her other tools. Coexistence on her primary personal number is a heavy, business-oriented change.

### Gaps
- **Launch date:** no source found gave Meta's official Coexistence launch or GA date. Vendor posts describe a beta period in roughly late 2024 to 2025 and "global" availability by 2026. Mark as unverified.
- No Meta source confirmed Israel's support status. The only evidence is ChakraHQ's table and an older Manychat post.
- Whether Twilio supports coexistence onboarding was not confirmed. 360dialog and Infobip clearly document it (links above).
- Whether a "personal use" number that converted to the Business app is acceptable under WhatsApp's Business Terms was not found.

---

## 8. Meta's general-purpose AI chatbot ban (WhatsApp Business Solution Terms, effective 15 Jan 2026)

### Takeaway
A new "AI Providers" clause, section 4.7 of the WhatsApp Business Solution Terms, bars providers of LLMs, generative AI platforms and general-purpose AI assistants from using the Business Platform when the AI itself is the **primary (rather than incidental or ancillary)** functionality, "as determined by Meta in its sole discretion". It applied to new users from 15 Oct 2025 and to all users from 15 Jan 2026. ChatGPT, Perplexity, Luzia and Copilot left WhatsApp. Businesses using AI for support, bookings and similar tasks are unaffected. In Italy and the EU, regulators forced Meta to reopen access, but those carve-outs do not cover Israel.

### Cited Findings
- The clause is titled "AI Providers" (section 4.7 in the current terms). Providers of AI technologies are "strictly prohibited from accessing or using" the WhatsApp Business Solution, directly or indirectly, when such technologies are the "primary (rather than incidental or ancillary) functionality being made available", as determined by Meta in its sole discretion. — [WhatsApp Business Solution Terms](https://www.whatsapp.com/legal/business-solution-terms); [Terms preview](https://whatsapp.com/legal/business-solution-terms/preview?amp=&amp=&amp=&lang=en); [MediaNama](https://www.medianama.com/2025/10/223-whatsapp-bans-external-ai-providers-business-api/)
- Timeline: new Business API users came under the terms on 15 Oct 2025, and all existing users on 15 Jan 2026. — [respond.io: General-purpose chatbots ban](https://respond.io/blog/whatsapp-general-purpose-chatbots-ban); [Business Standard](https://www.business-standard.com/technology/tech-news/meta-bans-ai-chatbots-from-whatsapp-business-api-chatgpt-to-shut-down-jan-2026-125102200335_1.html)
- Meta told TechCrunch the change does not affect businesses using AI to serve customers, such as a travel company's customer-service bot. It targets services where the chatbot is the product. The stated reason was infrastructure strain from AI message volume. — [TechCrunch, 18 Oct 2025](https://techcrunch.com/2025/10/18/whatssapp-changes-its-terms-to-bar-general-purpose-chatbots-from-its-platform); [Yahoo Tech mirror](https://tech.yahoo.com/ai/meta-ai/articles/whatssapp-changes-terms-bar-general-141214399.html)
- ChatGPT, Perplexity and Luzia were named as affected. OpenAI confirmed that ChatGPT on WhatsApp would end after the cutoff. — [Gulf News](https://gulfnews.com/technology/no-more-chatgpt-and-perplexity-on-whatsapp-meta-bans-major-ai-chatbots-from-2026-1.500316016); [The Daily Star](https://online91.thedailystar.net/tech-startup/news/whatsapp-plans-ban-chatgpt-ai-chatbots-2026-4018461)
- Post-deadline: on 15 Jan 2026 the terms took effect, blocking general-purpose AI assistants. — [Dataslayer](https://www.dataslayer.ai/blog/meta-bans-general-purpose-ai-chatbots-on-whatsapp-business); [Omago.ai: What actually changed](https://www.omago.ai/blog/meta-whatsapp-ai-chatbot-policy-2026-what-changed)
- **Italy:** AGCM imposed interim measures suspending the terms in Italy on 24 Dec 2025. Meta called the decision "fundamentally flawed" and appealed, but let rival chatbots back in Italy in January 2026. — [AI CERTs News](https://www.aicerts.ai/news/italys-whatsapp-ai-ruling-agcm-blocks-metas-anti-chatbot-terms/); [Yahoo News](https://www.yahoo.com/news/articles/italian-competition-authority-acts-against-152638928.html); [MobileAppDaily](https://www.mobileappdaily.com/news/italy-orders-meta-halt-whatsapp-ai-chatbot-terms)
- **EU:** the European Commission opened formal proceedings in December 2025, covering the EEA except Italy. On 4 March 2026 Meta revised the policy to allow general-purpose AI assistants in Europe for 12 months, but with an access fee, which the Commission viewed as possibly equivalent to a ban. On 9 June 2026 the Commission imposed interim measures (exact wording unconfirmed). One blog says Meta stopped charging AI providers for EU/EEA non-template messages on 12–13 May 2026; this conflicts with the June timeline and is single-source. — [Yahoo Finance: Meta to allow AI rivals on WhatsApp](https://finance.yahoo.com/news/meta-allow-ai-rivals-whatsapp-122729247.html); [GA Alliance: EU interim measures](https://www.ga-alliance.eu/en/eu-commission-imposes-interim-measures-on-meta/); [AIFray](https://aifray.com/meta-faces-parallel-antitrust-investigations-by-eu-commission-italian-competition-authority-over-ai-use-in-whatsapp/); [Omago.ai](https://www.omago.ai/blog/meta-whatsapp-ai-chatbot-policy-2026-what-changed)

### Inferences
- **Does it affect a personal Claude assistant for one's own use?** The clause targets "AI Providers" making AI available, typically to the public, as the primary function. A single individual wiring Claude through n8n to message only herself is not offering an AI service to others. On a plain reading she is a user of Anthropic's model, not an "AI Provider" distributing it, and Meta's public framing is about services like ChatGPT-on-WhatsApp.
- However, the bot's primary function is a general-purpose AI assistant, and Meta decides "in its sole discretion". There is a non-zero risk that such a number is classed as prohibited, especially if it is ever shared with others.
- Detection and enforcement risk for a one-user, low-volume number appears low, but no source addresses personal or self-use cases.
- Framing the bot as a narrow, task-oriented assistant (calendar, reminders, summaries of her own data) is closer to "AI as ancillary" than a free-form chat companion.
- Israel is outside the EU and Italy carve-outs, so the global terms apply in full.
- Coexistence on her personal number plus an AI reading all her contacts' messages is not a "business serving customers" pattern either. Its policy fit is uncertain.

### Gaps
- No source discusses single-user or self-use bots under the AI-Providers clause, and no Meta FAQ on edge cases was found.
- The full verbatim clause text (definitions of "AI Providers") could not be fetched.

---

## 9. Official Anthropic WhatsApp connector and third-party WhatsApp MCP servers

### Takeaway
As of mid-to-late 2026 there is **no official Anthropic or Claude WhatsApp connector**; WhatsApp is not in Anthropic's Connectors Directory. Options are third-party MCP servers. The most popular, lharries/whatsapp-mcp, uses the unofficial WhatsApp Web multi-device protocol on a personal account, not the Cloud API, so it carries ban risk. Business-API-based MCP servers exist from vendors.

### Cited Findings
- WhatsApp is absent from Anthropic's Connectors Directory, per a June 2026 guide. The workaround is a custom (third-party) MCP server added as a custom connector. One article says claude.com/connectors/whatsapp returns 404 (unverified). — [Carly: Claude + WhatsApp 2026](https://www.usecarly.com/blog/claude-whatsapp-integration/); [Carly: Claude Cowork and WhatsApp](https://www.usecarly.com/blog/claude-cowork-whatsapp/)
- lharries/whatsapp-mcp connects to a **personal** WhatsApp account through the WhatsApp Web multi-device API, stores messages locally in SQLite, and sends them to the LLM only when the agent calls tools. It is MIT-licensed, with about 6.3k stars as of 1 Oct 2026. — [GitHub lharries/whatsapp-mcp](https://github.com/lharries/whatsapp-mcp); [Pasquale Pillitteri](https://pasqualepillitteri.it/en/news/19773/whatsapp-mcp-server-claude-en)
- Other community MCP servers: [jlucaso1/whatsapp-mcp-ts](https://mcpservers.org/servers/jlucaso1/whatsapp-mcp-ts); [PodJamz/whatsapp-mcp](https://github.com/PodJamz/whatsapp-mcp). Vendor or Business-API-based: [AgentConnect: Connect WhatsApp to Claude](https://chat.agentconnect.chat/help/mcp-claude); [Setsmart: WhatsApp MCP server 2026](https://setsmart.io/blog/whatsapp-mcp-server)
- Custom connectors in claude.ai are called from Anthropic's cloud, so the MCP server must be publicly reachable. Claude Desktop and Claude Code can use local stdio servers. — [Carly](https://www.usecarly.com/blog/claude-whatsapp-integration/)

### Inferences
- For a Cloud-API-based design, n8n (or a small server) is the bridge: webhook in, Claude API call, Cloud API send out. An MCP server is optional.
- WhatsApp-Web-based MCP servers such as lharries/whatsapp-mcp could read all her personal chats, including groups. They are unofficial and risk an account ban, in the same category as Green API.

### Gaps
- No Anthropic primary source (docs or announcement) was found stating the absence of a WhatsApp connector. The evidence is third-party blogs.
- No open-source MCP server built specifically on the official Cloud API was verified this session.
