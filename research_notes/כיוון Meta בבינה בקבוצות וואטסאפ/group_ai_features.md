# Meta's AI features in WhatsApp groups and Communities: dated timeline, inventory, Israel/Hebrew status (as of 14 Oct 2026)

> **Method note:** this session could not open any page. WebFetch got DNS failures (for example on blog.whatsapp.com), and direct HTTPS returned proxy 403 for wabetainfo.com and techcrunch.com.
> - Every finding comes from **search-engine summaries** of the cited pages, not full reads. Exact build numbers, menu labels and dates should be checked before quoting.
> - Dates marked "≈" were inferred from relative "X days ago" metadata in search results.
> - This file builds on `../מזכירה אישית בוואטסאפ לאייפון/builtin_tools.md` and does not repeat that file's non-AI organization tips (Lists, Highlights, archive, reminders).
>
> **Legend:**
> - Status: **[REL]** released (stable, at least in some markets) · **[BETA]** beta or limited test · **[DEV]** found in code, not testable · **[ANN]** announced, not shipped
> - Israel/Hebrew: **IL✅** confirmed · **IL⚠️** unclear or partial · **IL❌** confirmed not available · **IL?** unknown

---

## 1. What has Meta introduced for AI in WhatsApp groups (2023 → Oct 2026)? Timeline, inventory, and the "2026 AI in groups" news question

### Takeaway
Meta's group-AI strategy has three layers, and none of them is a Hebrew "summarize and filter my hobby groups" tool that is confirmed to work in Israel today:
- **(a) Public Meta AI in the group.** Members can @mention it [REL since 2024]. A newer, documented "Meta AI as a group member" mode lets it read all *new* group messages once a member adds it [REL per Help Center, date unknown].
- **(b) Private, per-user AI on Private Processing.** This covers Message Summaries [REL Jun 2025, US/English first], Writing Help and AI reply suggestions [REL Aug 2025 / Mar 2026], and **Side Chat**, a private "ask Meta AI about this chat / summarize it" panel [BETA since 27 Jun 2026].
- **(c) Cosmetic and generative extras**, such as AI group icons [BETA 2025].

I found **no single 2026 official "AI in groups" announcement**. The 2026 group items an Israeli user would most likely have seen in the news are:
- the Hebrew Meta AI launch (30 Jun 2026), whose coverage mentions @Meta AI tagging in groups;
- Side Chat (announced May 2026, beta from late June);
- Restricted chat, which replaces Advanced Chat Privacy, with group admins in control (betas Sep–Oct 2026);
- recurring viral chain letters claiming "Meta AI reads your groups" (Aug 2025, again Sep–Oct 2026), which Israeli and international fact-checkers debunked.

The 2026 *official* group feature drops (Jan, Aug 2026) were **non-AI**.

### Cited Findings

**2023–2024: Meta AI enters chats and groups**
- [REL] **Apr 2024:** Meta launched the Meta AI assistant on Llama 3 across Facebook, Instagram, WhatsApp and Messenger in several countries. WhatsApp had tested it, including in **one-on-one and group chats**, for about six months before that. — [Fonearena, Apr 2024](https://www.fonearena.com/blog/422135/meta-ai-llama-3-facebook-instagram-whatsapp.html/amp)
- Example use cases: asking Meta AI in a WhatsApp group for restaurants with vegan options. — [T2 Online explainer](https://t2online.in/tech/tech-news/explainer-what-is-meta-ai-and-how-to-use-it-/999364)
- **Mechanism:**
  - In groups you type "@Meta AI" plus a question, and the answer is visible to everyone in the group. — [en.tempo.co guide](https://en.tempo.co/read/1954653/how-to-use-meta-ai-in-whatsapp-group); [Alphr guide](https://www.alphr.com/how-to-chat-with-meta-ai-in-a-group-chat-on-whatsapp/)
  - TechCrunch (May 2026): "Today, a question to the AI in a group is visible to everyone in the chat." — [TechCrunch, 13 May 2026](https://techcrunch.com/2026/05/13/whatsapp-adds-an-incognito-mode-in-meta-ai-chats/)
- [LEAK, not group-specific] **2 Jul 2024:** "Imagine Me", an AI selfie and sticker generator, surfaced in a leak. — [Android Authority via search summary](https://www.androidauthority.com/whatsap-3456516); [Notebookcheck](https://www.notebookcheck.net/Generate-AI-stickers-of-yourself-on-WhatsApp-using-Image-Me-feature-powered-by-Meta-AI.855959.0.html)
- [REL, non-AI context] **Jul 2024:** "Context cards" show who added you to a group, who created it, and when, with a one-tap exit. This is an anti-scam feature. — [YourStory, Jul 2024](https://cwv.yourstory.com/2024/07/whatsapp-launches-context-card-group-messaging); [PhoneArena](https://www.phonearena.com/news/whatsapp-rolls-out-context-cards-to-combat-group-chat-spam_id160266)

**2025: generative group extras and private AI**
- [BETA] **6 Mar 2025:** **AI-generated group icons.**
  - Android beta (reported as 2.25.6.10): you describe the icon in a text prompt and Meta AI returns several options. Only the creator needs the beta; every member sees the result. Personal profile photos were not covered at that stage. — [GSMArena, 6 Mar 2025](https://m.gsmarena.com/whatsapp_infuses_more_ai_into_group_chats-news-66835.php); [Business Today, 10 Mar 2025](https://www.businesstoday.in/technology/news/story/whatsapp-to-introduce-more-meta-ai-features-with-new-widgets-and-ai-generated-group-icons-467342-2025-03-10); [Mezha](https://mezha.ua/en/news/whatsapp-adds-more-ai-capabilities-to-group-chats-300283/)
  - It reached more beta testers by 17 May 2025. Stable status and Israel availability: **IL?** — [Jang (citing WABetaInfo)](https://jang.com.pk/en/33049-whatsapps-meta-ai-now-lets-users-create-unique-group-chat-icons-news)
- [REL] **Apr 2025:** **Advanced Chat Privacy** launched as a per-chat or per-group setting. It blocks export, media auto-download, and "using messages for AI features". — [Forbes, 24 Apr 2025](https://www.forbes.com/sites/zakdoffman/2025/04/24/whatsapp-confirms-how-to-block-meta-ai-from-your-chats/); [EFF, Sep 2025](https://www.eff.org/deeplinks/2025/09/what-whatsapps-advanced-chat-privacy-really-does). Details are in §4.
- [REL US/EN] **25 Jun 2025:** **Private Message Summaries.** Coverage of group support conflicts; see §2. — [TechCrunch, 25 Jun 2025](https://techcrunch.com/2025/06/25/meta-is-adding-ai-powered-summaries-to-whatsapp/)
- [BETA] **Jul 2025:** **"Quick Recap"** summarizes unread messages across **up to 5 selected chats**, using Private Processing. It excludes chats with Advanced Chat Privacy. Found in Android beta 2.25.21.12. — [Beebom](https://gadgets.beebom.com/news/whatsapp-testing-meta-ai-powered-quick-chat-recaps); [GSMArena](https://m.gsmarena.com/newscomm-68699.php); [The Outpost, which describes it as "for summarizing group chats"](https://theoutpost.ai/news-story/whats-app-introduces-ai-powered-quick-recap-feature-for-summarizing-group-chats-17993/)
- [REL, EN only] **Aug 2025:** **Writing Help** rephrases, proofreads and changes tone. It works in **1:1 and group chats** (pencil-with-sparkles icon), in English, in the US and "several other countries". — [GSMArena](https://m.gsmarena.com/whatsapp_launches_aipowered_writing_help-amp-69249.php)
  - Israel: English only, with no Israel date (Aug 2025). — [Geektime: "ה-AI נכנס לתוך וואטסאפ. אבל מה עם ישראל?"](https://www.geektime.co.il/whatsapp-announces-writing-help/); [Ynet](https://www.ynet.co.il/digital/technews/article/by3dtotyee)

**2026: suggestions, Side Chat, Restricted chat**
- [REL, gradual] **26 Mar 2026:** **Writing Help now drafts suggested replies from conversation context.** It is opt-in, off by default, and runs on Private Processing. — [TechCrunch, 26 Mar 2026](https://www.techcrunch.com/2026/03/26/whatsapp-can-now-draft-ai-generated-responses-based-on-your-conversations/); [9to5Mac, 26 Mar 2026](https://9to5mac.com/2026/03/26/whatsapp-joins-the-appalling-trend-for-ai-written-replies-to-messages/); [Neowin](https://www.neowin.net/news/whatsapp-now-offers-ai-powered-reply-suggestions-for-incoming-messages/)
  - It is "not available in all regions yet". Group-specific behavior and Hebrew support: **IL?** — [WWeb Customizer blog](https://www.wwebcustomizer.com/blog/meta-ai-on-whatsapp-web-how-to-use-writing-help-imagine-ai-replies-2026)
- [ANN → BETA] **13 May 2026:** Meta launched **Incognito Chat** with Meta AI (1:1 with the bot, on Muse Spark, not saved) and announced **Side Chat**: "invoke Meta AI within chats to ask questions … privately without notifying or showing it to other people in the chat". — [TechCrunch, 13 May 2026](https://techcrunch.com/2026/05/13/whatsapp-adds-an-incognito-mode-in-meta-ai-chats/)
  - Engadget: in Side Chat you can "ask it questions about the chat or get it to summarize messages". — [Engadget](https://www.engadget.com/2171922/whatsapp-users-can-soon-have-private-conversations-with-meta-ai/) (search-summary quote)
  - Gulf Business (2 Jun 2026) says Side Chat is protected by Private Processing. — [Gulf Business](https://gulfbusiness.com/en/2026/application/whatsapps-new-ai-feature-promises-total-privacy-heres-what-it-means/)
- [BETA] **27 Jun 2026:** **Side Chat began a limited rollout** to "a very small number of users" on Android and iOS, expanding "over the coming weeks". — [WABetaInfo](https://wabetainfo.com/whatsapp-is-testing-a-private-side-chat-feature-with-meta-ai/); [WABetaInfo on X](https://x.com/WABetaInfo/status/2070644674901967025); [Deccan Herald](https://www.deccanherald.com/technology/artificial-intelligence/whatsapp-testing-private-side-chat-feature-with-meta-ai-4054926); [Sammy Fans, 27 Jun 2026](https://www.sammyfans.com/2026/06/27/whatsapp-side-chat-7-new-meta-ai-features/)
  - **How you open it** (one secondary source): swipe left in a chat and tap "Ask privately". — [Deccan Herald](https://www.deccanherald.com/technology/artificial-intelligence/whatsapp-testing-private-side-chat-feature-with-meta-ai-4054926)
  - **What it can do:** summarize recent messages, draft replies, explain unclear statements, and web search (on by default). — [Jordan News](https://www.jordannews.jo/Section-129/Technology/WhatsApp-Tests-Side-Chat-Feature-to-Discreetly-Consult-AI-52461)
  - **Where it is blocked:** reportedly unavailable when Disappearing messages or Advanced Chat Privacy is on. — [ARY News](https://arynews.tv/whatsapp-introduces-new-side-chat-with-meta-ai)
  - **Release:** no stable-release date. **IL?**
- [REL] **30 Jun 2026:** **Meta AI launched in Israel in Hebrew** (Muse Spark). See §3 for which group features are included.
- [REL per Help Center; launch date unknown] **"Groups with Meta AI as a member":**
  - **Joining:** any member can add Meta AI to a group. All members see a system message and a welcome message from Meta AI.
  - **What it reads:** it "can read and respond to messages sent after it was added". It "will only respond when it can add value to the conversation or if a member chooses to interact with it".
  - **Limits:** it cannot change group settings, and admins can remove it at any time.
  - **Meta's access:** "Meta can read new messages sent in the group to enable AI experiences", and Meta "may use your prompts, the messages you share, and feedback to improve AI quality".
  - **Listed uses:** quick information (weather, scores), planning activities, facilitating brainstorms, **creating polls**.
  - **Availability:** "only available in limited countries".
  - — [WhatsApp Help Center: About groups with Meta AI as a member](https://faq.whatsapp.com/1504605284095230) (search-summary quotes; page not opened)
- [BETA] **Mar 2026:** a **Meta AI tab replaced the Communities tab** in betas. Community groups move into the Chats list with a dedicated filter. — [BetaNews](https://betanews.com/article/the-meta-ai-tab-lands-in-whatsapp-for-some-users/); [WABetaInfo: Meta AI tab](https://wabetainfo.com/whatsapp-is-rolling-out-meta-ai-tab-to-centralize-ai-powered-tools/)
- [BETA] **Sep–Oct 2026:** **Restricted chat** replaces Advanced Chat Privacy and blocks Meta AI in a chat; see §4. — [Help Net Security, 14 Sep 2026](https://helpnetsecurity.com/2026/09/14/whatsapp-restricted-chat-feature); [WABetaInfo iOS beta](https://wabetainfo.com/whatsapp-is-rolling-out-the-restricted-chat-feature-on-ios-beta/)

**Official 2026 group feature drops (non-AI, worldwide, so presumably in Israel)**
- **7 Jan 2026:** per-group member tags, text stickers, and custom early event reminders. — [MacRumors, 7 Jan 2026](https://www.macrumors.com/2026/01/07/whatsapp-group-chats-three-new-features/); [Neowin](https://www.neowin.net/news/whatsapp-is-getting-new-features-for-group-chats/); Hebrew: [Gadgety](https://www.gadgety.co.il/356042/whatsapp-level-up-groups/)
- **4 Aug 2026:** anonymous polls, timed voting, poll edits within 15 minutes, **@all mentions**, and starting a group from an existing chat. — [TechRepublic](https://www.techrepublic.com/article/news-whatsapp-group-chat-collaboration-features-2026/); [zudro.es roundup](https://zudro.es/en/new-features-of-WhatsApp/)
- **Recent-history sharing for new group members** (date unclear, 2025–2026 coverage):
  - Up to 100 recent messages from the last 2 weeks; optional, not on by default; rolling out worldwide including Israel. — [Maariv](https://www.maariv.co.il/economy/tech/article-1287065)
  - Can be 25–100 messages and requires the adder's action. — [Gadgety](https://www.gadgety.co.il/?p=358126)
  - Admins can turn it off for non-admins. — [Srugim](https://www.srugim.co.il/1297416)
  - WABetaInfo report on the feature. — [WABetaInfo](https://wabetainfo.com/whatsapp-is-developing-a-recent-history-sharing-feature-for-group-chats/)

**Third-party AI in groups / business AI**
- Meta's WhatsApp Business policy bars **general-purpose AI chatbots** (ChatGPT, Perplexity and similar) from **15 Jan 2026**. This shuts off third-party "AI in WhatsApp" routes, except in the EU, where an interim order applies (§6). — [Gulf News](https://gulfnews.com/technology/no-more-chatgpt-and-perplexity-on-whatsapp-meta-bans-major-ai-chatbots-from-2026-1.500316016)
- I found no source on Meta "business AIs" or AI agents being addable to consumer groups or Communities.

**Paid tier (context)**
- [BETA] **WhatsApp Plus** subscription tests (Mar–Apr 2026, about $2.50/mo).
  - Confirmed perks are cosmetic: icons, themes, up to 20 pinned chats. A survey floated AI add-ons. — [WABetaInfo](https://wabetainfo.com/whatsapp-plus-launches-premium-features-for-a-monthly-fee/); [PiunikaWeb, 28 Apr 2026](https://piunikaweb.com/2026/04/28/whatsapp-plus-survey-ai-storage-add-ons/)
  - Gadgety reports testing at **₪9/month**. — [Gadgety](https://www.gadgety.co.il/?p=362895); [Israel Hayom](https://www.israelhayom.co.il/tech/tech-news/article/20073468)
  - Meta One plans bundle WhatsApp Plus (Jun 2026). — [WABetaInfo: Meta One](https://wabetainfo.com/whatsapp-is-testing-meta-one-subscription-plans-for-android/)
  - **No source confirms paid AI group summaries.** A search-engine summary of an Israel Hayom piece claimed this, but it could not be verified (see Gaps).

### Inferences
- Meta's direction is clear: AI in groups goes **private and per-user** (Summaries, Side Chat, reply suggestions on Private Processing) rather than **public bot in the group**. Side Chat with "summarize this group privately" is the feature closest to the user's need. As of Oct 2026 it is a **limited beta with no announced countries or languages**.
- "Meta AI as a member" is technically the only mode where Meta AI reads a whole group's new traffic. But it is public to all members and has Meta reading the messages (not Private Processing). It is designed for answering, planning and polls, **not** for private digests or filtering. It is a poor fit for summarizing hobby groups without everyone's consent.
- Nothing in the inventory is an AI **filter**, for example "only show me messages about X in this group". Filtering remains manual: Highlights notifications, mentions, the new @all, and Lists.

### Gaps
- **Launch date and countries of "Meta AI as a member" of groups:** the Help Center page is undated, and I found no WABetaInfo or press report of its rollout. It is unclear whether it is live in Israel.
- **Unverified claim:** a search summary said Israel Hayom reported WhatsApp Plus "would include AI summaries for busy groups". A follow-up search of Israel Hayom found only cosmetic perks. Treat it as unverified.
- **AI group icons:** stable launch date and Israel availability not found.
- **Sammy Fans list:** the "7 new Meta AI features" in its 27 Jun 2026 piece could not be read.

---

## 2. Message Summaries / Private Processing: do they cover groups now, and in which languages and countries (Oct 2026)? Hebrew? Israel?

### Takeaway
**Groups: very likely yes.**
- WABetaInfo describes per-chat Message Summaries as working in "both individual and group conversations", aimed at busy chats.
- One 2025 outlet said 1:1 only, so treat group support as probable but not officially documented in what I could read.

**Languages and countries: no dated expansion found.**
- The newest official help text found lists only **English, Indonesian, Portuguese, Spanish**, in "limited countries".
- **Hebrew: not listed (IL❌/⚠️).** One Hebrew-launch explainer (Geektime, ≈Jul 2026) lists "summarizing unread messages" among Meta AI features, but no source confirms Hebrew summaries actually work.

**Multi-chat summaries are still unreleased.**
- "Quick Recap" (Jul 2025, up to 5 chats) and the unified "Get a summary" button on the Unread filter (Apr 2026) are both **[DEV/BETA]**.

### Cited Findings
- **Group coverage:**
  - WABetaInfo describes the summary as available "in individual chats and group conversations". A button replaces "X unread messages" once enough unread messages pile up. It is auto-disabled in Advanced Chat Privacy chats. First seen in Android beta 2.25.18.18. — [WABetaInfo: private AI message summaries](https://wabetainfo.com/whatsapp-introduces-private-ai-message-summaries-to-catch-up-on-chats-faster/); [WABetaInfo Android 2.25.18.18](https://wabetainfo.com/whatsapp-beta-for-android-2-25-18-18-whats-new/)
  - 9to5Mac (Jun 2025) said testing covered unread messages in "chats, groups, and channels". — [9to5Mac, 11 Jun 2025](https://9to5mac.com/2025/06/11/whatsapp-testing-ai-message-summaries/)
  - **Conflict:** The Hacker News and other launch coverage said only one-on-one chats were supported. — [The Hacker News, Jun 2025](https://thehackernews.com/2025/06/whatsapp-adds-ai-powered-message.html)
- **Launch scope:** US, English, 25–26 Jun 2025, with "other languages and countries later this year". — [TechCrunch](https://techcrunch.com/2025/06/25/meta-is-adding-ai-powered-summaries-to-whatsapp/); [iDownloadBlog](https://www.idownloadblog.com/2025/06/26/meta-whatsapp-message-summaries-united-states-english-language/)
  - Later blog wording: "beginning to roll out in select markets" with expansion "soon". No markets named. — [WhatsApp Blog](https://blog.whatsapp.com/catch-up-on-conversations-with-private-message-summaries) (search summary)
- **Official language list (undated):** "only English, Indonesian, Portuguese, and Spanish are supported", "limited countries". — [WhatsApp Help Center: How to use Meta AI to summarize messages](https://faq.whatsapp.com/9004571389643912/?cms_platform=android)
- **Israeli coverage:**
  - Jun 2025: "לא אצלנו". The feature launched abroad and not in Israel. — [Mako Nexter](https://www.mako.co.il/nexter-news/Article-e5d706d855ba791027.htm)
  - Hebrew explainers of the feature and its privacy model. — [Geektime: Private Processing](https://www.geektime.co.il/whatsapp-private-processing-ai-privacy/); [The Verifier (Hebrew)](https://theverifier.co.il/73263/whatsapp-private-message-summaries-meta-ai/)
- **Hebrew-launch explainer, ≈Jul 2026:** Geektime's "מה אתם צריכים לדעת רגע לפני שאתם מכניסים את Meta AI לוואטסאפ" reportedly lists, as Meta AI's WhatsApp capabilities in the Hebrew rollout, **tagging @Meta AI in chats and groups, summarizing unread messages, and making stickers**. It also warns that group admins can turn on privacy settings that block AI features. — [Geektime](https://www.geektime.co.il/what-you-should-know-before-using-meta-ai-in-whatsapp/) (search summary only; the page could not be opened, and the date was inferred as ≈92 days before 14 Oct 2026)
- **Multi-chat, 2025:** "Quick Recap" summarizes up to 5 selected chats (Android beta 2.25.21.12, Jul 2025). Reports disagree on whether any beta user could access it. — [Beebom](https://gadgets.beebom.com/news/whatsapp-testing-meta-ai-powered-quick-chat-recaps); [Notebookcheck](https://www.notebookcheck.net/Quick-Recap-Upcoming-WhatsApp-feature-could-make-chats-more-convenient.1064834.0.html)
- **Multi-chat, 2026:** a unified "Get a summary" button at the top of the Chats tab when the **Unread** filter is selected. Spotted in iOS TestFlight; "still in development" on iOS and Android as of **21 Apr 2026**.
  - Reported as opt-in and off by default.
  - No source confirms group coverage for this version.
  - — [9to5Mac, 21 Apr 2026](https://9to5mac.com/2026/04/21/whatsapp-testing-multi-chat-ai-summaries-for-unread-messages/); [WABetaInfo](https://wabetainfo.com/whatsapp-beta-for-android-tests-private-summaries-of-unread-chats/); [Ubergizmo, Mar 2026](https://www.ubergizmo.com/2026/03/whatsapp-ai-summarize-unread-conv/); [MacObserver](https://www.macobserver.com/news/whatsapp-tests-unified-ai-summaries-for-multiple-unread-chats/); Hebrew: [TGspot](https://www.tgspot.co.il/whatsapp-is-testing-private-summaries-of-multiple-unread-chats/)
- **Private Processing model:** requests go to an isolated confidential-computing environment (TEE). Meta says "neither Meta nor WhatsApp" can see the messages or summaries, nothing is stored or linked to the user, and others in the chat aren't notified.
  - Side Chat is said to run on the same architecture, audited by NCC Group and Trail of Bits. — [WABetaInfo](https://wabetainfo.com/whatsapp-introduces-private-ai-message-summaries-to-catch-up-on-chats-faster/); [LetsDataScience on Side Chat](https://letsdatascience.com/news/whatsapp-tests-side-chat-integration-with-meta-ai-e6dd489a)
- **Translation (related, not summaries):**
  - Mar 2026 Android beta added 13 more on-device language packs. — [WABetaInfo](https://wabetainfo.com/whatsapp-beta-for-android-adds-13-language-packs-for-message-translations/)
  - Gadgety headline: auto-translation beta "ללא תמיכה בעברית". **IL❌ for Hebrew translation, as of that report.** — [Gadgety](https://www.gadgety.co.il/359720/whatsapp-auto-translate-beta/)
  - Original launch post. — [WhatsApp Blog: Introducing Message Translations](https://blog.whatsapp.com/introducing-message-translations)

### Inferences
- If Hebrew summaries arrive, the most likely vehicles are:
  1. per-chat Message Summaries, which already cover groups;
  2. Side Chat ("summarize this group privately");
  3. the unified Unread "Get a summary" button.

  All three run on Private Processing, so the privacy model would be the same. The blocker is **language and country gating**, not technology.
- Even at full rollout, these are **on-demand digests of unread messages**. None is a topic filter or a persistent "notify me only about X" rule for hobby groups.
- Geektime listing "summarize unread messages" in a Hebrew-launch article is weak evidence. It may describe the global feature set rather than a tested Hebrew feature. Check in-app: the summary button appears above unread messages in a busy group.

### Gaps
- No dated official statement after Jun 2025 names the markets or languages for Message Summaries. Hebrew and Israel status remains unconfirmed.
- No report on whether multi-chat summaries ("Get a summary" or Quick Recap) reached stable by Oct 2026.
- Geektime ≈Jul 2026: the article's actual wording on summaries could not be read.

---

## 3. Meta AI's Hebrew launch in Israel (30 Jun 2026, Muse Spark): which group features are included?

### Takeaway
**IL✅ Confirmed in Hebrew:**
- Meta AI chat (1:1 bot)
- image and video generation and editing
- photo and screenshot analysis inside WhatsApp

**IL⚠️ Group features:**
- @Meta AI tagging in groups is reported in Hebrew-launch explainers. It is very likely available, because it is the standard Meta AI entry point.
- Unread summaries, Writing Help and reply suggestions, Side Chat, AI group icons, and "Meta AI as a member": **no Israeli source confirms these work in Hebrew.**

The launch was explicitly **partial and staged**. Different users see different features, and "consistent Hebrew across all features" will "require more patience".

### Cited Findings
- **Launch:** Tuesday 30 Jun 2026, full Hebrew. Available in WhatsApp, the Meta AI app and meta.ai. — [Geektime](https://www.geektime.co.il/meta-ai-launched-in-israel-and-hebrew/); [Ynet](https://www.ynet.co.il/digital/technews/article/bktnrkbmfg); [Globes](https://www.globes.co.il/news/article.aspx?did=1001547383); [Walla](https://tech.walla.co.il/item/3849753); [Cryptobriefing, 30 Jun 2026](https://cryptobriefing.com/meta-ai-launches-israel-hebrew-whatsapp/)
- **Hebrew capabilities named:** natural-Hebrew chat, image and video generation, and photo upload for real-time analysis "without leaving WhatsApp". Model: Muse Spark. It can connect to Gmail and Outlook. — [Ynetnews](https://www.ynetnews.com/tech-and-digital/article/rk008bxwxge); [Gadgety](https://www.gadgety.co.il/364956/meta-ai-israel/)
- **Staged and partial rollout:**
  - An "Ask Meta AI" option appears gradually.
  - Hebrew is "not yet complete in every layer of the product".
  - Some users have Hebrew interfaces or responses; others lack them or lack the full capability set. — [HTMag: "Meta AI מגיעה לישראל, אבל ההשקה חלקית ומדורגת"](https://htmag.co.il/meta-ai-israel.html)
- **Group features in Hebrew-launch coverage:** tagging @Meta AI in chats and groups, summarizing unread messages, and stickers. Admins can enable privacy settings blocking AI. — [Geektime, ≈Jul 2026](https://www.geektime.co.il/what-you-should-know-before-using-meta-ai-in-whatsapp/) (search summary only)
- **Before the launch:**
  - ≈Mar 2026, Mako/N12: the tool "had not entered Israel" and had no target date; the blue button some Israelis saw was "probably a bug" (per Meta sources). — [Mako Nexter: "גילינו מה זה הכפתור החדש והמעצבן בוואטסאפ"](https://www.mako.co.il/nexter-news/Article-cde916394b9bc91026.htm)
  - Aug 2025: Writing Help was English-only, with no Israel date. — [Geektime](https://www.geektime.co.il/whatsapp-announces-writing-help/)
- **Business-facing Israeli explainer:** Meta AI comes to WhatsApp and Instagram in Israel, with a gradual Hebrew rollout. — [Status-d](https://status-d.co.il/professional/meta-ai-integration-whatsapp-instagram-israel/)
- **Official Hebrew landing page** for Meta AI in WhatsApp; it shows a group trip-planning example. — [whatsapp.com/meta-ai?lang=he](https://www.whatsapp.com/meta-ai?lang=he)
- **Related Israeli DIY trend:** an Israeli developer, frustrated with WhatsApp group chaos, built his own AI bot to organize groups. This is evidence that native tools did not meet the need. — [Geektime: "למפתח ישראלי נמאס מהבלאגן של קבוצות וואטסאפ…"](https://www.geektime.co.il/ai-agents-can-manage-your-whatsapp-groups/) (date not captured)

### Inferences
- An Israeli Hebrew speaker can most likely already type "@Meta AI סכם את 50 ההודעות האחרונות" in a group. But:
  - the answer is **public to the whole group**;
  - Meta AI only "sees" what is tagged or quoted, unless it was added as a member;
  - Meta processes the message outside end-to-end encryption.

  That is not a private digest.
- The private Hebrew digest the user wants depends on Meta adding Hebrew to Message Summaries or shipping Side Chat in Israel. Neither has a public date.

### Gaps
- No official Meta or WhatsApp Israel press release text was readable, so there is no definitive list of features included at launch.
- Hands-on Israeli tests of group summarization in Hebrew were not found.

---

## 4. Controls: can admins or members block Meta AI in a group? Can you disable Meta AI entirely? What does Meta AI see in a group?

### Takeaway
**What Meta AI sees.** By default it sees **only messages sent to it, tagged @Meta AI, or forwarded or quoted to it**. Fact-checkers (2025–2026) debunked "Meta AI reads all groups" claims.

There are two important exceptions:
- **(i) If a member adds Meta AI as a group member**, it can read **all new messages** from that point, and Meta can read them and use them to improve AI. Admins can remove it.
- **(ii) Private Processing features** (Summaries, Side Chat, reply suggestions) read the chat for the requesting user inside a TEE that Meta says it can't access.

**Blocking per group:**
- Advanced Chat Privacy (2025) blocks AI use in a chat; in groups admins can lock who can toggle it.
- **Restricted chat** (beta Sep–Oct 2026) replaces it. It blocks Meta AI, export, media auto-save and linked devices. In groups **only admins** can enable it, though some reports say beta is 1:1-only.

**No global off switch for Meta AI** as of 7 Oct 2026.

### Cited Findings
- **Meta AI as a group member:**
  - It reads and responds to messages sent after it was added, only in that group.
  - Admins can remove it; it can't change group settings.
  - "Meta can read new messages sent in the group to enable AI experiences."
  - Meta may use prompts and shared messages to improve AI.
  - — [WhatsApp Help Center](https://faq.whatsapp.com/1504605284095230)
  - Getkanal (Oct 2026) repeats this: when a member adds Meta AI to a group, Meta can read the new messages. — [Getkanal](https://getkanal.com/blog/meta-ai-whatsapp)
- **Tag-only default and fact-checks:**
  - Meta AI "only sees what you specifically share with it" (an @Meta AI tag or a forward). — [CyberPeace](https://cyberpeace.org/resources/blogs/factcheck-a-viral-claim-suggests-that-by-turning-on-advance-chat-privacy-meta-ai-can-avoid-reading-whatsapp-chats); [Factly](https://factly.in/meta-ai-cannot-access-whatsapp-groups-individual-chats-or-contact-details-the-viral-claim-is-fake/); [Fact Crescendo, 20 Aug 2025](https://english.factcrescendo.com/2025/08/20/whatsapp-meta-ai-advanced-chat-privacy-fact-check/)
  - The claim was debunked again in 2026. — [Fact Crescendo, 30 Sep 2026](https://english.factcrescendo.com/2026/09/30/meta-ai-reading-whatsapp-private-chats-advanced-chat-privacy-fact-check/)
  - WhatsApp says Meta AI "is not active until a user chooses to interact with it". — [Arbiterz, Oct 2026](https://arbiterz.com/whatsapp-meta-ai-access-cant-access-group-messages)
- **Israeli fact-checks of the Hebrew chain letter** ("enable advanced privacy or AI reads your groups"):
  - The setting is real but misrepresented: it stops export and AI use in that chat, but not screenshots, and it does not change encryption. Once you tag Meta AI, "Meta is the endpoint" and reads that message. — [The Verifier: "'פרטיות מתקדמת': המכתב הוויראלי בוואטסאפ שגורם לבהלה מיותרת"](https://theverifier.co.il/74516/whatsapp-chain-letter-ai/)
  - Walla: "לא, וואטסאפ לא קוראת הודעות פרטיות - די עם הפייק". — [Walla](https://tech.walla.co.il/item/3774951)
  - [irrelevant.org.il, 19 Aug 2025](https://www.irrelevant.org.il/2025/08/19/6574)
  - [PC.co.il on Advanced Chat Privacy](https://www.pc.co.il/thenewcom/429023/)
- **Advanced Chat Privacy (Apr 2025, released):**
  - Blocks export, media auto-download, and use of messages for AI features. — [Forbes, 24 Apr 2025](https://www.forbes.com/sites/zakdoffman/2025/04/24/whatsapp-confirms-how-to-block-meta-ai-from-your-chats/)
  - Any participant can toggle it; in groups admins can lock it via "Edit Group Settings". — [EFF, Sep 2025](https://www.eff.org/deeplinks/2025/09/what-whatsapps-advanced-chat-privacy-really-does)
  - It auto-disables Message Summaries and Quick Recap. — [WABetaInfo](https://wabetainfo.com/whatsapp-introduces-private-ai-message-summaries-to-catch-up-on-chats-faster/); [Beebom](https://gadgets.beebom.com/news/whatsapp-testing-meta-ai-powered-quick-chat-recaps)
  - It reportedly blocks Side Chat. — [ARY News](https://arynews.tv/whatsapp-introduces-new-side-chat-with-meta-ai)
- **Restricted chat (beta):**
  - **What it blocks:** keeps the chat on the primary phone (no linked devices or WhatsApp Web), and blocks gallery auto-save, export, and Meta AI features.
  - **Where it lives:** a per-chat toggle in chat info.
  - **Builds:** Android test reported first; iOS beta 26.39.10.20 reached limited testers in early Oct 2026. — [WABetaInfo: Android test](https://wabetainfo.com/whatsapp-is-testing-a-new-restricted-chat-feature-on-android/); [WABetaInfo: iOS beta](https://wabetainfo.com/whatsapp-is-rolling-out-the-restricted-chat-feature-on-ios-beta/); [Help Net Security, 14 Sep 2026](https://helpnetsecurity.com/2026/09/14/whatsapp-restricted-chat-feature); [iThinkDiff](https://www.ithinkdiff.com/whatsapp-restricted-chat-iphone-beta/)
  - **Groups, sources conflict:**
    - WhatsApp lists it for groups too, where **group admins control it**. — [iThinkDiff](https://www.ithinkdiff.com/whatsapp-restricted-chat-iphone-beta/); [WavesFlo citing the help centre](https://www.wavesflo.com/blog/meta-ai-whatsapp); [Pakera](https://pakera.pk/whatsapp-restricted-chat-replaces-advanced-chat-privacy-pakistan/)
    - Beta is **individual chats only**. — [Tbreak](https://tbreak.com/whatsapp-restricted-chat-android-ios-beta/); [Cybernews](https://cybernews.com/tech/whatsapp-restricted-chat-feature/)
  - **Migration:** existing Advanced Chat Privacy chats don't switch automatically (Help Center summary). — [GreenTick](https://greentick.ai/blogs/whatsapp-restricted-chats/)
  - **Limits:** it doesn't change encryption and doesn't block screenshots. — [Tbreak](https://tbreak.com/whatsapp-restricted-chat-android-ios-beta/)
  - **Public release:** no date. **IL?**
- **Disabling Meta AI entirely:**
  - No setting in the Help Center turns Meta AI off or removes it from the app, as of 7 Oct 2026. — [Getkanal](https://getkanal.com/blog/meta-ai-whatsapp); [WavesFlo](https://www.wavesflo.com/blog/meta-ai-whatsapp)
  - The 2025 backlash coverage: TechRadar's "WhatsApp just made its AI impossible to avoid – but at least you can turn it off" refers to per-feature toggles, not removal. — [TechRadar](https://www.techradar.com/computing/artificial-intelligence/whatsapp-just-made-its-ai-impossible-to-avoid-but-at-least-you-can-turn-it-off)
  - Private Processing features are off by default and toggled under Settings > Chats > Private Processing (see the earlier file).
- **Meta AI's own memory:**
  - Mar 2026 beta organizes Meta AI conversations into threads. Memory is shared across threads unless disabled from the contact info screen. — [Help Net Security, 2 Mar 2026](https://www.helpnetsecurity.com/2026/03/02/whatsapp-chats-meta-ai-user-privacy/)
  - Incognito Chat (May 2026) is not saved. — [TechCrunch](https://techcrunch.com/2026/05/13/whatsapp-adds-an-incognito-mode-in-meta-ai-chats/)

### Inferences
- For a hobby group where one member wants private AI digests:
  - If an admin turns on Advanced Chat Privacy or Restricted chat, **that member's own summaries and Side Chat stop working in that group**.
  - Group-level privacy settings and personal AI convenience are in direct tension, and admins hold the veto.
- The "Meta AI as member" mode is the only one where Meta itself reads all new messages. A privacy-conscious group should watch for the system message saying Meta AI was added.

### Gaps
- Restricted chat's final group behavior (admin-only toggle vs 1:1-only) is unresolved. No official WhatsApp blog post on it was found.
- Whether the "hide Meta AI button" toggle exists in Israel was not verified (see the earlier file).

---

## 5. What's in WhatsApp beta (WABetaInfo, 2026) that signals what's coming for AI in groups and Communities?

### Takeaway
The pipeline points to **private, per-user catch-up**, not group-level bots:
- Side Chat (summarize or ask about any chat privately; limited beta since 27 Jun 2026)
- unified multi-chat "Get a summary" on the Unread filter (dev, Apr 2026)
- context-based reply suggestions (released Mar 2026, gradual)
- Restricted chat (beta Sep–Oct 2026)
- a Meta AI tab that **displaced the Communities tab** (beta Mar 2026)

There are no reports of AI features built specifically for Communities: no AI announcements digests, AI moderation, or AI group descriptions.

### Cited Findings
- **Side Chat:** limited Android and iOS rollout from 27 Jun 2026, no stable date. — [WABetaInfo](https://wabetainfo.com/whatsapp-is-testing-a-private-side-chat-feature-with-meta-ai/); [Threads post](https://www.threads.com/@wabetainfo/post/DaEfOsfiH_l)
  - No Sep–Oct 2026 status update found. A roundup about a month old still calls it "planned". — [Analytics Insight](https://www.analyticsinsight.net/apps/whatsapp-features-to-know-in-2026-privacy-ai-messaging-tools)
- **Unified unread summary ("Get a summary"):** in development, Apr 2026. — [9to5Mac](https://9to5mac.com/2026/04/21/whatsapp-testing-multi-chat-ai-summaries-for-unread-messages/); [Deccan Herald](https://www.deccanherald.com/technology/artificial-intelligence/whatsapp-to-get-multi-chat-ai-summaries-for-unread-messages-2-3982885); [Beebom](https://gadgets.beebom.com/news/whatsapp-will-soon-let-meta-ai-summarise-all-your-unread-chats-at-once)
- **Meta AI tab replacing the Communities tab** (iOS beta 26.12.10.70, Mar 2026). Community groups move into Chats with a filter. — [WABetaInfo](https://wabetainfo.com/whatsapp-is-rolling-out-meta-ai-tab-to-centralize-ai-powered-tools/); [BetaNews](https://betanews.com/article/the-meta-ai-tab-lands-in-whatsapp-for-some-users/)
- **Meta AI threads and memory** (Android beta 2.26.9.4, Mar 2026). — [Help Net Security](https://www.helpnetsecurity.com/2026/03/02/whatsapp-chats-meta-ai-user-privacy/); [Sheetwa](https://sheetwa.com/news/whatsapp-meta-ai-document-sharing/)
- **Voice:** Meta AI voice chat and voice-call betas. — [PhoneArena](https://www.phonearena.com/news/whatsapp-beta-meta-ai-voice-chat_id161398)
- **AI-suggested topics** for Meta AI chats. — [Smallest.ai](https://smallest.ai/blog/whatsapp-beta-integrates-ai-suggested-topics-and-voice-chat-a-step-toward-smarter-messaging)
- **Restricted chat:** Android, then iOS beta 26.39.10.20 (Sep–Oct 2026). — [WABetaInfo](https://wabetainfo.com/whatsapp-is-rolling-out-the-restricted-chat-feature-on-ios-beta/)
- **Language packs:** 13 more for translation (Mar 2026), plus new voice-transcription languages. — [WABetaInfo: language packs](https://wabetainfo.com/whatsapp-beta-for-android-adds-13-language-packs-for-message-translations/); [WABetaInfo: voice transcriptions](https://wabetainfo.com/whatsapp-is-rolling-out-new-languages-for-voice-transcriptions/)
- **Paid tiers:** WhatsApp Plus and Meta One subscriptions. A survey hints at AI add-ons. — [WABetaInfo](https://wabetainfo.com/whatsapp-is-testing-meta-one-subscription-plans-for-android/); [PiunikaWeb](https://piunikaweb.com/2026/04/28/whatsapp-plus-survey-ai-storage-add-ons/)

### Inferences
- The most plausible "native solution" path for the user is Side Chat plus multi-chat summaries reaching stable **and** adding Hebrew. Rollout patterns support caution:
  - US/English first (Jun 2025);
  - Israel got Meta AI itself about 2 months after the rest of the world and only partially (see the earlier file).

  This suggests Hebrew group digests are **not imminent**, likely months away at best. This is an inference; Meta has given no date.
- No beta adds AI **filtering**, prioritization or "alert me when someone mentions X" for groups. A custom assistant would still be needed for that.

### Gaps
- WABetaInfo pages could not be opened. There may be Sep–Oct 2026 group-AI betas not surfaced by search.
- No reports were found of AI features specific to Communities or announcement groups.

---

## 6. Reactions: privacy criticism, regulatory scrutiny (EU, Israel), user backlash about Meta AI in groups

### Takeaway
- **User backlash** peaked in Apr–May 2025 over the unremovable blue Meta AI circle and button. Meta's response was "listening to feedback" and calling it "a good thing".
- **Recurring viral panic** about Meta AI "reading groups" has circulated, including in Hebrew in Israel (Aug 2025; again Sep–Oct 2026), and fact-checkers debunked it.
- **Privacy criticism** focuses on:
  - Meta AI chats sitting outside end-to-end encryption, with memory and ad personalization;
  - consent when one member shares or tags group content;
  - inference risks of reply suggestions.
- **Regulatory scrutiny** is mainly EU competition law over Meta's ban on rival AI chatbots: probe opened Dec 2025 → interim order 9 Jun 2026; separate Italian AGCM proceedings.
- **No Israeli Privacy Protection Authority action** on Meta AI in WhatsApp was found.

### Cited Findings
- **2025 backlash:**
  - Users "fume" over the Meta AI button they can't remove. — [TechRadar](https://www.techradar.com/computing/websites-apps/whatsapp-users-fume-over-new-meta-ai-button-that-you-cant-remove-heres-what-it-does)
  - WhatsApp says forcing the circle is "a good thing". — [TechRadar](https://www.techradar.com/computing/websites-apps/whatsapp-says-forcing-blue-meta-ai-circle-on-everyone-is-a-good-thing-despite-fierce-backlash)
  - Meta told the BBC it is "listening to feedback" and called the feature "entirely optional". — [Euronews, 11 May 2025](https://www.euronews.com/2025/05/11/metas-new-optional-ai-chatbot-in-apps-like-whatsapp-is-proving-controversial-heres-why)
  - Critics raised consent concerns when a participant shares a conversation with the bot. — [CO/AI](https://getcoai.com/news/whatsapps-new-ai-feature-sparks-user-privacy-concerns)
- **AI group icons:** mixed reactions, with critics citing WhatsApp's end-to-end encryption focus. — [Business Today](https://www.businesstoday.in/technology/news/story/whatsapp-to-introduce-more-meta-ai-features-with-new-widgets-and-ai-generated-group-icons-467342-2025-03-10)
- **Privacy criticism, 2026:**
  - Meta AI threads and memory "reopen privacy issues": messages to Meta AI fall outside the end-to-end encrypted user-to-user model. — [Help Net Security, 2 Mar 2026](https://www.helpnetsecurity.com/2026/03/02/whatsapp-chats-meta-ai-user-privacy/)
  - Meta may use AI interactions to personalize content and ads. — [LetsDataScience](https://letsdatascience.com/news/whatsapp-adds-meta-ai-chat-organization-c1d3e7bc)
  - 9to5Mac calls AI replies an "appalling trend". — [9to5Mac, 26 Mar 2026](https://9to5mac.com/2026/03/26/whatsapp-joins-the-appalling-trend-for-ai-written-replies-to-messages/)
  - Stanford researchers (as cited) warn of inference risks at scale. — [Implicator](https://www.implicator.ai/whatsapp-now-uses-ai-to-draft-reply-suggestions-based-on-your-conversations/)
  - Incognito Chat was framed as a response to privacy concerns. — [The Star / Reuters-syndicated, 14 May 2026](https://www.thestar.com.my/tech/tech-news/2026/05/14/meta-launches-whatsapp-039incognito039-mode-to-address-privacy-concerns-for-ai-chats)
  - Legal commentary on encrypted Meta AI chats. — [MIAI ai-regulation.com](https://ai-regulation.com/the-day-the-provider-stopped-reading-your-chats/)
- **Israel:**
  - Israeli coverage warns that Meta's push to refine ads may lead users to avoid attaching the assistant to private chats. — [Globes](https://www.globes.co.il/news/article.aspx?did=1001547383)
  - Hebrew chain-letter debunks (Aug 2025). — [The Verifier](https://theverifier.co.il/74516/whatsapp-chain-letter-ai/); [Walla](https://tech.walla.co.il/item/3774951)
  - Mako called it a "new annoying button" (≈Mar 2026). — [Mako](https://www.mako.co.il/nexter-news/Article-cde916394b9bc91026.htm)
  - Bizportal: "while Meta is in court, WhatsApp improves privacy". — [Bizportal](https://www.bizportal.co.il/BizTech/news/article/20016185)
  - Bloomberg-sourced report that US authorities are probing ex-contractor claims that Meta staff can access WhatsApp messages; Meta denies it. — [TipRanks Israel / The Fly](https://il.tipranks.com/news/the-fly/2856543)
  - **No Israeli Privacy Protection Authority (הרשות להגנת הפרטיות) statement found.**
- **EU antitrust:**
  - Formal probe opened Dec 2025 into Meta's WhatsApp Business policy excluding rival general-purpose AI assistants. — [Nasdaq](https://www.nasdaq.com/articles/eu-launches-formal-antitrust-probe-against-meta)
  - Statement of Objections Feb 2026, supplementary Apr 2026. — [CNBC, 9 Feb 2026](https://www.cnbc.com/2026/02/09/eu-interim-measures-meta-whatsapp-ai-policy-antritrust.html)
  - **Interim order, 9 Jun 2026:** restore free access for rival AI assistants, on pre-restriction terms, until the case ends. The Commission found prima facie EEA dominance since at least Jan 2023. — [Lawyer Monthly](https://www.lawyer-monthly.com/2026/06/eu-orders-meta-restore-ai-access-whatsapp/); [European Commission on X](https://x.com/EU_Commission/status/2064380051274019004?lang=en); [Geradin Partners](https://www.geradinpartners.com/geradin-partners-secures-landmark-interim-measures-for-interaction-in-meta-ai-whatsapp-case/)
  - Italy is excluded because AGCM runs its own proceedings; their outcome was not found. — [Lawyer Monthly](https://www.lawyer-monthly.com/2026/06/eu-orders-meta-restore-ai-access-whatsapp/)
  - Meta's 10-Q (FY2026 Q2) discusses EU matters. — [SEC 10-Q](https://www.sec.gov/Archives/edgar/data/0001326801/000162828026050705/meta-20260630.htm)

### Inferences
- The EU order matters for third-party assistants in the EEA. It does **not** apply in Israel, where Meta's Jan 2026 ban on general-purpose AI chatbots on the Business API presumably applies. That constrains a "build your own WhatsApp-connected assistant" route via official APIs.
- Social risk in hobby groups: adding Meta AI as a member, or tagging it, is visible and has triggered panic chain letters in Israel. Private, per-user tools (Summaries, Side Chat) avoid that, but they are not yet in Hebrew.

### Gaps
- No Israeli regulator action, Knesset discussion or formal complaint on Meta AI in WhatsApp was found.
- AGCM outcome, and any EU data-protection decision specific to Meta AI in WhatsApp groups, were not found.
- A search summary mentioned NOYB threatening legal action over Meta training AI on EU users' data (2025, Facebook/Instagram data). No citable page was captured, so it is left out of the findings.
- Fact Crescendo 30 Sep 2026 and Arbiterz Oct 2026 show the viral claim resurfaced in fall 2026. Whether a Hebrew version circulated again in Sep–Oct 2026 was not confirmed.
