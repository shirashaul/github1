# Privacy, legal constraints and architecture: a Claude-based WhatsApp assistant for an Israeli local-authority internal auditor whose single WhatsApp number mixes personal and work chats (as of 14 October 2026)

> These are research notes, not legal advice. Wherever the notes say "confirm", the authority's legal advisor (יועמ"ש הרשות), its information security officer (ממונה אבטחת מידע) and its privacy protection officer (ממונה הגנת פרטיות, if one has been appointed) need to sign off.
>
> Method caveat: the research environment could not open several primary sites directly: gov.il, Nevo, Wikisource, developers.facebook.com, privacy.claude.com, and law-firm websites (DNS or proxy blocks). The Hebrew statute text, Meta's documentation and Anthropic's consumer help pages are therefore cited through search-engine extraction of those pages, or through law-firm or secondary summaries. These are marked "(secondary)" or "(via search extract)". One primary page was retrieved in full on 14 Oct 2026: Anthropic's API retention documentation at platform.claude.com.

## Q1. Amendment 13 to the Protection of Privacy Law: obligations that matter here, and whether a household or personal-use exemption exists

### Takeaway
Amendment 13 came into force in August 2025 (14 Aug per most sources). It made "personal information" very broad and created a category of "information of special sensitivity". It also gave the Privacy Protection Authority (PPA) the power to impose large administrative fines without going to court. The database provisions still exclude a collection kept for personal use and not for business purposes. Two limits on that exclusion matter here:
- It never covered the privacy-infringement offences and torts in section 2, which apply to everyone. These include breach of a statutory secrecy duty and using information for a purpose other than the one it was given for.
- It plainly stops applying once the data is the authority's or relates to her public role. Work chats with colleagues and residents fall into that category.

### Cited Findings
- **Effective date.** Amendment 13 took effect in August 2025. Sources differ slightly: most say 14 Aug 2025 and some say 15 Aug 2025. — [IAPP](https://iapp.org/news/a/israel-marks-a-new-era-in-privacy-law-amendment-13-ushers-in-sweeping-reform); [Pearl Cohen summary](https://www.pearlcohen.com/the-knesset-enacted-a-key-amendment-to-the-israeli-protection-of-privacy-law-summery-version/); [Offlist (secondary)](https://www.offlist.me/what-is-israel-protection-of-privacy-law)
- **Terminology.** "מידע" became "מידע אישי" (personal information), defined as any data relating to an identified or identifiable person; one source says this includes IP addresses. "מידע רגיש" became "מידע בעל רגישות מיוחדת" (information of special sensitivity). "בעל מאגר" (database owner) became "בעל שליטה במאגר מידע" (database controller). — [Meitar (HEB PDF)](https://meitar.com/wp-content/uploads/2025/07/AMENDMENT-13-TO-THE-PRIVACY-PROTECTION-LAW-IS-ON-THE-HORIZON-HEB.pdf); [N-B Law Amendment 13 PDF](https://www.nblaw.com/SpecialProjects/Privacy/Amendment13.pdf); [Goldfarb](https://www.goldfarb.com/amendment-13-to-the-israeli-privacy-protection-law/)
- **What counts as specially sensitive.** Commentary says the category is aligned with GDPR terms and covers genetic data, biometric data, criminal records and location data, among other items. — [Pearl Cohen (secondary)](https://www.pearlcohen.com/the-knesset-enacted-a-key-amendment-to-the-israeli-protection-of-privacy-law-summery-version/); [MineOS (secondary)](https://www.mineos.ai/articles/israels-amendment-13-a-new-era-for-privacy). The full statutory list, which covers health, sexual life, opinions and beliefs, origin and more, was not retrieved; see Gaps.
- **PPA enforcement powers.** After Amendment 13 the PPA can impose fines without court approval, conduct criminal investigations, and order databases frozen or deleted. Before fining it can issue a warning, and it can require a cash deposit as a guarantee that a breach will stop. — [Pearl Cohen](https://www.pearlcohen.com/the-knesset-enacted-a-key-amendment-to-the-israeli-protection-of-privacy-law-summery-version/); [Globes](https://en.globes.co.il/en/article-1001517426)
- **Fine levels.** Fines can reach millions of shekels, with multipliers for large databases and for processing sensitive data. — [Pearl Cohen](https://www.pearlcohen.com/the-knesset-enacted-a-key-amendment-to-the-israeli-protection-of-privacy-law-summery-version/). One vendor blog says fines can reach 5% of turnover. This could not be corroborated, so treat it as unreliable. — [MineOS](https://www.mineos.ai/articles/israels-amendment-13-a-new-era-for-privacy)
- **Sanctions linked to outsourcing.** A law-firm note found in search lists administrative sanctions tiered by the database's security level, up to NIS 320,000 for high-security databases. The examples it gives include failing to update the database definitions document every year, and using an external service provider that processes personal data without an agreement imposing privacy and security requirements. — Law-firm note surfaced via search ([Gornitzky PDF](https://www.gornitzky.co.il/wp-content/uploads/pdf/post/30434_----------.pdf) / [EBN quarterly](https://ebnlaw.co.il/wp-content/uploads/2025/02/עדכון-לקוחות-רבעוני-1.2025-פרטיות.pdf)). The exact attribution between these two documents was not confirmed.
- **Registration.** Most private entities no longer have to register databases. Registration still applies to public bodies and data brokers; for public bodies, employee databases are excluded. — [Goldfarb](https://www.goldfarb.com/amendment-13-to-the-israeli-privacy-protection-law/); [Meitar HEB](https://meitar.com/wp-content/uploads/2025/07/AMENDMENT-13-TO-THE-PRIVACY-PROTECTION-LAW-IS-ON-THE-HORIZON-HEB.pdf)
- **Exclusions from "database".** The 1981 law's definition excludes "a collection for personal use not intended for business purposes" ("אוסף לשימוש אישי שאינו למטרות עסק"). — [WIPO Lex English text](https://www.wipo.int/wipolex/en/text/347462); [Kobsa/UCI English translation](https://ics.uci.edu/~kobsa/privacy/israel.htm). Post-amendment guidance still describes the personal-use exclusion. It also describes a conditional exclusion for contact-only collections (name, address, contact details) of up to 100,000 people, where the collection reveals nothing further and the controller holds no other database. — [Offlist (secondary)](https://www.offlist.me/what-is-israel-protection-of-privacy-law); [N-B Law campaign PDF](https://nblaw.com/media/5xfhyhcl/campaigns_5538a838-7765-4e1b-82ce-a6693521f548.pdf)
- **Section 2 applies to everyone, with no personal-use carve-out.** Section 1: "No person shall infringe the privacy of another without his consent." Section 2 lists the forms of infringement, among them:
  - 2(7): infringing a secrecy obligation imposed by law about a person's private affairs.
  - 2(8): infringing a secrecy obligation set by express or implied agreement.
  - 2(9): using or passing on information about a person's private affairs for a purpose other than the one for which it was given.

  Willfully infringing 2(1), 2(3)–(7) and 2(9)–(11) carries up to 5 years' imprisonment. Civil remedies such as compensation and injunctions are also available. — [WIPO Lex](https://www.wipo.int/wipolex/en/text/347462); [Kobsa/UCI](https://ics.uci.edu/~kobsa/privacy/israel.htm); [Mondaq overview](https://www.mondaq.com/privacy-protection/797222/data-protection-cybersecurity-2019)
- **Enforcement outlook for 2026.** Law-firm commentary expects enforcement to increase in 2026 following Amendment 13. This is a prediction, not reported outcomes. — [JD Supra, March 2026 digest](https://www.jdsupra.com/legalnews/data-privacy-and-cybersecurity-march-2698097/)

### Inferences
- **Personal chats with family and friends.** If she runs an assistant purely for her private life, she is most likely inside the personal-use exclusion from the database chapter. That would mean no controller obligations such as registration, a definitions document or the Data Security Regulations. Section 2 still applies, though. Forwarding a friend's confidential health disclosure to a cloud AI for a purpose the friend never contemplated could arguably fall under 2(8) or 2(9). The legal risk is low, but discretion is advisable.
- **Where the exclusion ends.** It stops at anything that is the authority's information or that she holds because of her public role: messages from residents, colleagues, complainants, audit subjects. Those messages are part of the authority's information assets, which sit in the authority's databases and are subject to its controller obligations. Sending them to a third-party AI service is effectively an "outsourced processing" event. Under the Data Security Regulations and Amendment 13, that requires an authorised processor with a written agreement. She has no such agreement in a personal capacity, so a personal AI account would be an unauthorised disclosure by an employee of the authority.
- **Statutory secrecy.** If an auditor's statutory confidentiality duty covers a message (see Q3), feeding it to an outside service could also be a section 2(7) infringement ("breach of a statutory secrecy obligation regarding private affairs"). That is a criminal-exposure category when willful.
- **Practical rule.** The safest line, and the easiest one to defend, is that no work-originated message ever reaches the AI, whatever the platform's retention settings.

### Gaps
- The consolidated post-Amendment 13 Hebrew text could not be fetched (Nevo, gov.il and Knesset were blocked). The following need checking against the text: the exact current wording of the personal-use exclusion in section 7; the full list of "information of special sensitivity"; the fine tables (per-data-subject amounts and caps); whether and how the fines apply to public bodies; and the mandatory privacy protection officer (DPO) duty for public bodies. My training data indicates Amendment 13 requires public bodies to appoint a DPO, but this was not verified in this session.
- The date and wording of any PPA guidance interpreting the personal-use exclusion were not found.

## Q2. Israeli government, PPA, Cyber Directorate and State Archives guidance on generative AI, WhatsApp for official business, and records

### Takeaway
The PPA published draft guidance on AI on 30 April 2025. It says privacy law applies across the AI lifecycle and asks organisations to adopt internal policies on employees' use of generative-AI tools. Those policies cover which tools are allowed, what data may be uploaded, prompt retention and training use. No final version was found as of October 2026. No public government-wide or Ministry of Interior rule on civil servants using WhatsApp or generative AI was found. Individual authorities do issue their own AI procedures; one regional council's August 2025 procedure is an example. The State Archives' position is that work communications in any format, including text messages, are state records that must be kept retrievable.

### Cited Findings
- **Draft guidance timeline.** The PPA draft "on the application of the Protection of Privacy Law to AI systems" was published on 30 Apr 2025, with public comments due by 5 Jun 2025. — [babl.ai](https://babl.ai/israels-privacy-authority-releases-draft-ai-guidance-for-data-protection-compliance/); [Pearl Cohen](https://www.pearlcohen.com/israeli-privacy-regulator-issues-draft-guidelines-on-privacy-in-ai/); [Gornitzky (May 11, 2025)](https://www.gornitzky.com/privacy-in-artificial-intelligence-systems-guidelines-of-the-israeli-privacy-protection-authority/)
- **Scope and legal basis.** Privacy law applies to AI systems that store, process or infer personal data. Inferences and predictions about identifiable people count as personal data. A legal basis is required at every lifecycle stage, and under the current law there are only two bases: consent, or authorisation in law. — [EBN Law](https://www.ebnlaw.co.il/media-center/draft-guidance-from-the-israeli-privacy-protection-authority/); [Shibolet (HEB)](https://www.shibolet.com/%D7%98%D7%99%D7%95%D7%98%D7%AA-%D7%94%D7%A0%D7%97%D7%99%D7%99%D7%AA-%D7%94%D7%A8%D7%A9%D7%95%D7%AA-%D7%9C%D7%94%D7%92%D7%A0%D7%AA-%D7%94%D7%A4%D7%A8%D7%98%D7%99%D7%95%D7%AA-%D7%91%D7%A2%D7%A0%D7%99/); [Goldfarb (HEB)](https://www.goldfarb.com/he/%d7%98%d7%99%d7%95%d7%98%d7%aa-%d7%94%d7%a0%d7%97%d7%99%d7%99%d7%aa-%d7%94%d7%a8%d7%a9%d7%95%d7%aa-%d7%9c%d7%94%d7%92%d7%a0%d7%aa-%d7%94%d7%a4%d7%a8%d7%98%d7%99%d7%95%d7%aa-%d7%aa%d7%97%d7%95%d7%9c/)
- **Transparency about bots.** Where it materially affects consent, people must be told they are interacting with an automated AI bot rather than a human. — [Shibolet / Goldfarb summaries, as above](https://www.shibolet.com/?p=20425)
- **Internal policies on employee use of generative AI.** The PPA recommends that organisations adopt internal policies covering third-party tools such as ChatGPT and Gemini. Suggested contents: who may use the tools and who authorises use, which tools are permitted, what types of data may be uploaded, limiting prompt retention, limiting use of inputs for training, and training employees on security risks. — [Gornitzky (EN)](https://www.gornitzky.com/privacy-in-artificial-intelligence-systems-guidelines-of-the-israeli-privacy-protection-authority/); [MoFo Israel AI tracker](https://www.mofo.com/artificial-intelligence/israel)
- **Vendor terms.** Commentary stresses checking the vendor's terms and privacy policy for external AI tools, especially whether the vendor uses input data to train models. — [Gornitzky HEB PDF](https://www.gornitzky.co.il/wp-content/uploads/pdf/post/27613_---------.pdf)
- **Specially sensitive data in training.** The PPA notes a high likelihood that training AI models processes information of special sensitivity at scale. — (via search extract of [Goldfarb HEB](https://www.goldfarb.com/he/%d7%98%d7%99%d7%95%d7%98%d7%aa-%d7%94%d7%a0%d7%97%d7%99%d7%99%d7%aa-%d7%94%d7%a8%d7%a9%d7%95%d7%aa-%d7%9c%d7%94%d7%92%d7%a0%d7%aa-%d7%94%d7%a4%d7%a8%d7%98%d7%99%d7%95%d7%aa-%d7%aa%d7%97%d7%95%d7%9c/))
- **Final version.** No final PPA AI guidance was found in searches as of October 2026. Treat the draft as the current indicator of PPA thinking. — (negative search result; see Gaps)
- **Local-authority AI procedure: Emek HaMaayanot Regional Council (מועצה אזורית עמק המעיינות).** The council has an AI-use procedure intended to "set clear and uniform rules for using AI technologies" while preserving information security and privacy. It defines sensitive information as information whose exposure could harm privacy, security or the authority's interests. The file timestamp suggests August 2025. — [Emek HaMaayanot procedure PDF](https://www.emek-maianot-region.muni.il/uploads/n/1755007955.8363.pdf) (via search extract)
- **State Comptroller on AI risks.** The Comptroller's AI readiness reporting lists the risks of government AI as privacy harm, unregulated data use, dependence on external vendors, information-security weaknesses, lack of transparency, and unclear accountability. — [State Comptroller 2024 Cyber/AI report summary](https://library.mevaker.gov.il/sites/DigitalLibrary/Documents/2024/2024.11-Cyber/2024.11-Cyber-107-AI-Taktzir.docx); [Comptroller multinational parallel audit on AI readiness](https://library.mevaker.gov.il/sites/DigitalLibrary/Pages/Publications/2148.aspx)
- **Records and archives.**
  - State Archives guidelines on managing digital documents and email (2020–21) treat documents that public employees create, send or receive in their work as state material that must stay retrievable, in any format including text messages. — [Archives guidelines PDF](https://catalog.archives.gov.il/wp-content/uploads/2021/03/הנחיות-לניהול-מסמכים-דיגיטליים-ודואר-אלקטרוני.pdf) (via search extract)
  - Under the Archives Law, the State Archivist supervises archives and archival material in state institutions and local authorities, including their destruction. — [State Comptroller 2024 report on the Archives](https://library.mevaker.gov.il/sites/DigitalLibrary/Documents/2024/2024.05/2024-05-104-Archives.pdf)
  - The State Archivist has said publicly that officials delete email in breach of the law. — [Globes tag page](https://www.globes.co.il/news/%D7%90%D7%A8%D7%9B%D7%99%D7%95%D7%9F_%D7%94%D7%9E%D7%93%D7%99%D7%A0%D7%94.tag)
- **Cyber Directorate warnings about WhatsApp.** The National Cyber Directorate's public WhatsApp warnings are aimed at the general public. They say never to pass on the 6-digit WhatsApp SMS code (account takeover) and not to join unknown investment groups. No public-servant-specific WhatsApp policy was found. — [Mako](https://www.mako.co.il/nexter-news/Article-c9b3476f78fbb81027.htm); [Maariv](https://www.maariv.co.il/business/tech/Article-672699)

### Inferences
- Even though it is still a draft, the PPA guidance points to what the authority's own policy should say: an approved tool list, data-type limits, no training use, and limited retention. She should assume her authority either has, or will soon have, a rule along these lines (the Emek HaMaayanot procedure shows authorities are writing them). Any personal assistant has to fit inside it.
- **Archives.** Work chats on her personal WhatsApp are probably authority records. Deleting them, exporting them to an AI service, or having a bot "clean up" the phone could conflict with Archives Law duties. Moving work communications to an official channel or work number solves both the archives problem and the AI problem.

### Gaps
- None of the following was found: a binding Israeli government-wide directive for civil servants on generative AI (National Digital Agency, Civil Service Commission or Ministry of Justice); a Ministry of Interior circular (חוזר מנכ"ל) for local-authority employees on AI or WhatsApp; a PPA guideline specific to WhatsApp work groups; or a State Archives directive specific to WhatsApp. These may exist as internal documents. She should ask the authority's CISO and legal advisor directly.
- Whether the PPA's AI guidance was finalised during 2025–2026 could not be verified, because gov.il was not reachable.

## Q3. Internal auditor obligations in a local authority: confidentiality of audit information and complaints

### Takeaway
The municipal auditor has a statutory right of access to documents, databases and staff under the Municipalities Ordinance and the Internal Audit Law. Publishing audit findings early, without her permission, is a criminal offence (section 170ג(ו) with section 334א of the Ordinance). Combined with the special confidentiality around complaints, including employee whistleblowing, everything she receives in her auditor role is high-sensitivity authority information. None of it should go to any external AI service without explicit, written institutional authorisation.

### Cited Findings
- **Duties (section 170א).** The Municipalities Ordinance sets the auditor's duties, among them checking whether the municipality acted lawfully and with integrity, and reviewing municipal employees' actions. — [Ramla municipality document](https://ramle.org.il/uploads/n/1614172984.7424.pdf)
- **Publication ban (170ג(ו)).** A report, or any part of it, may not be published before the date set for submitting it to the council, and audit findings may not be published without the auditor's permission. A breach carries one year's imprisonment under section 334א. — [Kfar Yona auditor's report](https://www.kfar-yona.muni.il/uploads/n/1721286676.4251.pdf); [Ramat HaSharon 2018 report](https://ramat-hasharon.muni.il/wp-content/uploads/2019/11/%D7%93%D7%95%D7%97-%D7%9E%D7%91%D7%A7%D7%A8-%D7%94%D7%A2%D7%99%D7%A8%D7%99%D7%99%D7%94-2018.pdf)
- **Independence.** The auditor, treasurer and legal advisor have a special statutory arrangement, and the National Labour Court has described its purpose as creating an independent status. — (via search extract of a Knesset Research Center document listed in [this result set](https://library.mevaker.gov.il/sites/DigitalLibrary/Documents/2020/71A/2020-71A-104-Shilton-Mekomi.docx))
- **Internal Audit Law, 5752-1992.** The law applies to public bodies. It sets rules on the auditor's appointment, reporting lines and working methods, including access to documents, information databases and staff. — [State Comptroller 2023 report on internal audit](https://library.mevaker.gov.il/sites/DigitalLibrary/Documents/2023/2023.5/2023.5-101-Bikoret-Pnimit.pdf); [gov.il internal audit unit page](https://www.gov.il/he/Departments/units/internal_auditing)
- **Public complaints commissioner.** Many municipal auditors also act as public complaints commissioner (ממונה על תלונות הציבור).
  - Any person may complain about the authority, its employees or office-holders.
  - A complaint is made in writing with the complainant's name and address.
  - The commissioner may hear the complainant, the person complained about and others, and may demand documents from authority staff.
  - Complaints by employees about their own employment are excluded unless a breach of law, regulations or a collective agreement is alleged.

  — [Kiryat Ata public complaints report](https://www.kiryat-ata.org.il/wp-content/uploads/2021/07/דוח-תלונות-ציבור-2015.pdf); [Yoav council document](https://yoav.org.il/uploads/n/1681721595.8095.pdf); [Afula document](https://www.afula.muni.il/uploads/n/1662901999.6812.pdf)
- **Section 2(7) link.** Under section 2(7) of the Privacy Law, breaching a secrecy duty imposed by law regarding a person's private affairs is itself an infringement of privacy. — [WIPO Lex](https://www.wipo.int/wipolex/en/text/347462)

### Inferences
- Her role makes her an unusually high-risk user. Audit working papers, draft findings, complainant identities and whistleblower material all reach her, and her personal number is likely to carry exactly these messages: residents and colleagues writing to "the auditor". If the publication ban is read together with complaint confidentiality and section 2(7), even a summary of such a chat created by an AI service amounts to transferring regulated information to a third party.
- **The rule should be absolute:** auditor-role content never touches the assistant. A per-message decision is not enough, because the mixed number makes per-message judgment unreliable.

### Gaps
- The exact text of the Internal Audit Law's confidentiality provisions could not be retrieved; Wikisource and Nevo were blocked. Specifically:
  - whether the law has an explicit secrecy duty for the internal auditor and the information they receive, and its section number;
  - the text of Ordinance section 170ב (access to information);
  - the confidentiality provisions of the Local Authorities (Public Complaints Commissioner) Law, 2008, on the complainant's identity.

  The authority's legal advisor should confirm these. Also relevant: the professional standards of the Institute of Internal Auditors (IIA) Israel / the Global Internal Audit Standards, which carry a confidentiality principle. These were not researched in this session.
- Whistleblower-identity protections for employee complainants, and how they apply at municipal level, were not verified.

## Q4. How Anthropic (consumer Pro/Max vs API) and Meta's WhatsApp Cloud API handle data, plus Meta's 2026 restriction on AI chatbots

### Takeaway
**Consumer Claude (Free, Pro, Max).** Since the 28 Aug 2025 terms update, chats are used for training only if the "help improve Claude" (Model Improvement) setting is on. With the setting on, data is retained for 5 years; with it off, 30 days. Incognito chats are never used for training. These terms do not apply to commercial or API use.

**Claude API (Commercial Terms).** As documented on 14 Oct 2026: no training without express permission, and prompts and outputs are not retained by default. The exception is "Covered Models", which require 30-day retention. Zero data retention (ZDR) is available through sales. Content flagged by trust and safety systems can be kept for up to 2 years under any arrangement.

**WhatsApp Cloud API.** It is not end-to-end encrypted in the strict sense, because Meta manages the keys and decrypts messages on its servers. Messages are stored encrypted for up to 30 days.

**Meta's 2026 restriction.** Since 15 Jan 2026, Meta's WhatsApp Business terms bar general-purpose AI assistants where AI is the primary functionality. The EU ordered interim relief in June 2026, but that relief covers the EEA, not Israel.

### Cited Findings
**Anthropic, consumer plans**
- **Terms update.** Announced 28 Aug 2025. It applies to Claude Free, Pro and Max, including Claude Code on those accounts. It does not apply to Claude for Work (Team and Enterprise), Claude Gov, Claude for Education, the API, or Bedrock and Vertex. — [Anthropic, "Updates to our consumer terms"](https://www.anthropic.com/news/updates-to-our-consumer-terms)
- **Retention.** "Extending data retention to five years, if you allow us to use your data for model training". Otherwise "you'll continue with our existing 30-day data retention period". The 5-year period also applies to feedback submitted. — [Anthropic](https://www.anthropic.com/news/updates-to-our-consumer-terms)
- **Deleted chats, deadline and scope.** Deleted conversations are not used for future training. The setting is changed at claude.ai/settings/data-privacy-controls. Existing users had to choose by 8 Oct 2025; some outlets said 28 Sep, and Anthropic's own page says 8 Oct. The setting applies only to new or resumed chats. — [Anthropic](https://www.anthropic.com/news/updates-to-our-consumer-terms); [ICAI article (conflicting date)](https://ai.icai.org/articles_details.php?id=260)
- **Opt-out design criticism.** In the consent pop-up, the large "Accept" button opts users in unless the smaller toggle is switched off first. — [Gigazine](https://www.gigazine.net/gsc_news/en/20250901-anthropic-claude-updates-consumer-terms-privacy-policy)
- **Incognito.** "Your Incognito chats are not used to improve Claude, even if you have enabled Model Improvement". Secondary sources say incognito chats are still retained for 30 days and are not available inside Projects. — [privacy.claude.com article 10023548 (via search extract)](https://privacy.claude.com/en/articles/10023548); [ai-toolbox (secondary)](https://www.ai-toolbox.co/claude-management-and-productivity/claude-incognito-chats-2026); [vibecodingacademy (secondary)](https://vibecodingacademy.ai/blog/claude-incognito-mode)
- **Not ZDR-eligible.** Consumer plans are explicitly outside ZDR: Free, Pro and Max on web, desktop and mobile, and Claude Code. — [Anthropic API & data retention doc](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)

**Anthropic, API (retrieved 14 Oct 2026)**
- **Data processor.** Anthropic is the data processor for the Claude API, Claude Platform on AWS and Claude in Microsoft Foundry. On Bedrock and Google Cloud the cloud provider is the processor. — [platform.claude.com](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- **Retention commitments.** "Retained data is never used for model training without your express permission." "Conversation content (your prompts and Claude's outputs) is not retained by default; the exception is Covered Models, which require 30-day retention." — [platform.claude.com](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- **Covered Models.** Claude Fable 5.1, Mythos 5.1, Fable 5 and Mythos 5 require 30-day retention, and ZDR is not available for them unless Anthropic expressly authorises it. — [platform.claude.com](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- **ZDR.** Under ZDR, Anthropic "does not store customer prompts or responses at rest after the API response is returned". It is requested through sales and enabled per organisation. Stateful features are not covered: Batch API, Files API, code execution (containers retained up to 30 days), Console/playground, and Managed Agents. — [platform.claude.com](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- **Retention regardless of arrangement.** "Even with ZDR or HIPAA arrangements in place, Anthropic may retain data where required by law or where it has been flagged by Anthropic's automated trust and safety systems ... up to 2 years." — [platform.claude.com](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- **Earlier retention period.** Secondary blogs report that standard API log retention was cut from 30 to 7 days on 14 Sep 2025. The current official page instead says content is "not retained by default". Rely on the official page. — [char.com blog](https://char.com/blog/anthropic-data-retention-policy) vs [platform.claude.com](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)

**Meta / WhatsApp Cloud API**
- **Encryption and keys.** The Cloud API "manages the encryption/decryption keys on behalf of the business in order to send and receive messages". Messages at rest are encrypted. — [Meta developer docs, Data Privacy & Security (via search extract)](https://developers.facebook.com/documentation/business-messaging/whatsapp/data-privacy-and-security)
- **Retention and use.** Messages are kept for a maximum of 30 days, which Meta says is needed for base functions such as retransmissions. The Cloud API uses messages only on behalf of and at the instruction of the business. — [Meta developer docs (via search extract)](https://developers.facebook.com/documentation/business-messaging/whatsapp/data-privacy-and-security); [360dialog architecture & security](https://docs.360dialog.com/docs/waba-basics/architecture-and-security)
- **Local Storage option.** This optional setting stores message data at rest in in-country data stores and deletes content from "data in use" storage after 60 minutes. — [Meta Cloud API Local Storage docs (via search extract)](https://developers.secure.facebook.com/docs/whatsapp/cloud-api/overview/local-storage/)
- **AI-provider restriction.** Meta announced it in October 2025. It took effect for new AI providers on 15 Oct 2025 and for existing ones on 15 Jan 2026. It bars AI providers where general-purpose AI is the "primary (rather than incidental or ancillary) functionality". Businesses using AI for customer service are not barred. OpenAI, Perplexity, Luzia and Poke were affected. — [TechCrunch](https://techcrunch.com/2025/10/18/whatssapp-changes-its-terms-to-bar-general-purpose-chatbots-from-its-platform/?rand=324); [Gulf News](https://gulfnews.com/technology/no-more-chatgpt-and-perplexity-on-whatsapp-meta-bans-major-ai-chatbots-from-2026-1.500316016); [Camposthomaz](https://camposthomaz.com/en/conhecimento-ct/european-commission-orders-whatsapp-to-grant-access-to-rival-ai-chatbots-amid-antitrust-probe/)
- **EU interim measures.** The European Commission opened case AT.41034 on 4 Dec 2025. On 9 Jun 2026 it adopted interim measures ordering Meta to restore rival AI assistants' access on the pre-October 2025 terms for the duration of the investigation. It said Meta's March 2026 paid-access offer was equivalent to the ban. Meta said it will appeal. — [AP via NY1](https://ny1.com/nyc/all-boroughs/ap-top-news/2026/06/09/eu-orders-meta-to-restore-whatsapp-access-for-rival-ai-chatbots); [Dow Jones via Morningstar](https://www.morningstar.com/news/dow-jones/202606095919/meta-gets-eu-antitrust-order-to-open-whatsapp-to-rival-ai-chatbots-update); [TechPolicy.Press](https://techpolicy.press/whatsapp-as-a-stress-test-for-interim-measures-in-the-eus-competition-law)
- **Italy and Brazil carve-out.** One outlet reports an exception for users with Italian and Brazilian numbers. This is a single-source claim. — [PPC Land](https://ppc.land/whatsapp-bars-ai-chatbots-as-meta-solidifies-messaging-monopoly/)

### Inferences
- **If she uses the consumer app (Pro or Max) directly:** turn off "help improve Claude" so retention is 30 days and there is no training. Use incognito for anything sensitive but personal. This is acceptable for private-life content only. Consumer plans give no processor agreement or ZDR, so they are unsuitable for any authority data.
- **If she builds a bot:** an API key under Commercial Terms is the stronger privacy posture. There is no training, content is not retained by default, and she can choose a non-Covered model to avoid the mandatory 30-day retention. Even so, the API does not make work data legitimate to send, because the authority, not she, is the controller of that data.
- **The WhatsApp hop is a second processor.** Meta's Cloud API sees plaintext and keeps it for up to 30 days. Every personal message sent to the bot is therefore exposed to both Meta and Anthropic.
- **The policy channel is uncertain in Israel.** A personal bot whose primary function is a general AI assistant plausibly falls under Meta's ban, and the EU interim measures do not cover Israel. Before building on the WhatsApp Cloud API, she should check the current WhatsApp Business Solution Terms, or use a different channel for the bot.

### Gaps
- The current wording of Anthropic's consumer retention article, including flagged-content retention for consumer plans and incognito retention, could not be fetched first-hand; privacy.claude.com was blocked.
- Meta's current (October 2026) WhatsApp Business Solution Terms text was not retrieved. Also unconfirmed: whether a single-user personal assistant on one's own WhatsApp Business Account (WABA) is treated as an "AI provider", and the status of Meta's appeal of the EU order.
- No official Anthropic-to-WhatsApp integration was researched; only third-party or self-built bridges were considered.

## Q5. Architecture patterns, and a recommended layered setup for this persona

### Takeaway
The decisive control is upstream separation, not AI-side settings. Work traffic needs its own number or channel. The bot needs a dedicated number of its own and must never be linked to her personal or work WhatsApp account. Data reaches the AI only by explicit push or through a deny-by-default allowlist. On top of that: drafts only, with a human sending; least-privilege tools; prompt-injection controls enforced in code; minimal logs; and written sign-off from the authority's legal advisor and CISO.

### Cited Findings
- **OWASP LLM06 (Excessive Agency).** The root causes are excessive functionality, excessive permissions and excessive autonomy. Mitigations: restrict permissions to the task, require human approval for consequential actions, and keep authorisation in external systems rather than delegating it to the LLM. Use read-only extensions where that is enough (for example, read-only email), and avoid open-ended tools such as a shell. — [Barracuda on OWASP 2025](https://blog.barracuda.com/2024/11/20/owasp-top-10-risks-large-language-models-2025-updates); [Aembit](https://aembit.io/blog/owasp-top-10-llm-risks-explained/); [unique.ai OWASP summary](https://docs.unique.ai/security-and-compliance/it-security/owasp-top-10-for-llm-applications-2025)
- **OWASP LLM01 (Prompt Injection).** Limit the LLM to essential operations, keep a human in the loop for critical tasks, use granular privilege controls, and log and monitor actions. Defences should be layered, and enforcement belongs in deterministic application logic, not only in system-prompt instructions. — [Barracuda](https://blog.barracuda.com/2024/11/20/owasp-top-10-risks-large-language-models-2025-updates); [DeepStrike](https://deepstrike.io/blog/owasp-llm-top-10-vulnerabilities-2025); [FutureAGI](https://futureagi.com/blog/owasp-llm-top-10-2025-risks-mitigations-2026/)
- **Data minimisation in the PPA draft.** The PPA's draft recommends policies that limit which data types are uploaded, limit prompt retention and limit training use. — [Gornitzky](https://www.gornitzky.com/privacy-in-artificial-intelligence-systems-guidelines-of-the-israeli-privacy-protection-authority/)
- **Building with ZDR.** Anthropic recommends server-side proxies, and ZDR organisations cannot use browser CORS calls. Data processed by third-party integrations falls outside Anthropic's arrangements. — [platform.claude.com](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- **WhatsApp Cloud API plaintext.** Meta processes Cloud API messages in plaintext and retains them for up to 30 days. — [Meta docs (via search extract)](https://developers.facebook.com/documentation/business-messaging/whatsapp/data-privacy-and-security)
- **Linked-device risk.** The IDF warned reservists that WhatsApp Web on shared computers gives a path into phones. This illustrates the risk of linked-device sessions. — (via search extract; IDF reservist communication, see [Mako](https://www.mako.co.il/nexter-news/Article-c9b3476f78fbb81027.htm) result set)

### Inferences (recommended layered setup; design recommendation, not sourced fact)
**Layer 0, governance (before anything is built).**
- Get a short written answer from the legal advisor and the CISO or DPO on four points:
  1. Is there an authority policy on AI or WhatsApp?
  2. Does the authority want work chats on an authority-issued device or number?
  3. What are the archive or retention expectations for existing work chats?
  4. Confirmation that a private assistant with zero work data is acceptable.
- Record her own rule: "auditor-role information never enters any AI tool outside approved authority systems".

**Layer 1, identity separation (the core fix).**
- Move work communication off the personal number. The preferred route is an authority-issued phone or number. Otherwise, use a second number (eSIM) running WhatsApp Business on the same iPhone, ideally under authority policy. Tell colleagues and residents about the new channel, and use it for complaints and audit matters.
- Before migrating, export or archive work chats according to the authority's archive instructions. Do not delete them unilaterally (see Q2).
- The personal number then carries only private life.

**Layer 2, the bot gets its own channel.**
- The assistant lives on a third, dedicated number or channel. She talks to it as a contact.
- The bot must never be logged into her personal or work account as a linked device or through WhatsApp Web scraping libraries. A linked-device bridge sees every chat, including work chats, and unofficial libraries also breach WhatsApp's terms.
- Because of Meta's 2026 general-purpose-AI restriction, consider a non-WhatsApp channel for the bot:
  - a Telegram bot;
  - the Claude iOS app, with iOS Shortcuts for quick capture;
  - the WhatsApp Cloud API only after checking the current terms.

**Layer 3, push-only ingestion and allowlisting.**
- **Push only.** By default the AI sees only what she deliberately sends or forwards to it.
- **Personal-chat summaries.** If she wants these, use a pre-AI filter that runs on her own device or server. It should pass only explicitly listed personal chat IDs, deny everything by default, and automatically exclude any chat containing a contact tagged as work. Strip phone numbers and attachments before upload.
- **Prefer manual export.** For selected personal chats, manual "export chat" plus upload is preferable to any always-on connector.

**Layer 4, model and account choice.**
- **Simplest path:** Claude consumer Pro or Max with "help improve Claude" off (30-day retention), and incognito for sensitive personal items.
- **For a bot:** an API key under Commercial Terms, using a model that is not a 30-day "Covered Model" so prompts are not retained by default. Request ZDR only if it is actually needed. Remember the 2-year retention for flagged content.
- Keep the bot's account personal and separate from any authority Claude or AI tenant.

**Layer 5, actions: drafts only.**
- The bot can draft replies, reminders and calendar suggestions. She copies and sends them herself.
- No tool can send messages, read her contacts or address book, or access email, Drive or calendar beyond scoped personal resources. Writes to the calendar require explicit confirmation.

**Layer 6, prompt-injection containment.**
- Treat all forwarded content as untrusted data.
- The bot accepts commands only from her own number; enforce this in code against the sender ID.
- The bot has no exfiltration-capable tools: no arbitrary URL fetch, no email or SMS sending, no file sharing.
- System-prompt rules are a backstop, not the control.

**Layer 7, logging and retention.**
- Log metadata only (time, message size, tool calls). Do not log message bodies.
- Encrypt at rest. Auto-delete the bot's store within a short TTL, for example 7–30 days. Keep secrets in a vault.
- Host in her personal cloud account, not on authority infrastructure.

**Layer 8, incident path.**
- If work data reaches the bot by mistake: delete the conversation or data, record what happened, and notify the CISO or DPO according to authority procedure.
- Review the allowlist and policy every quarter.

### Gaps
- These were not verified in this session:
  - whether WhatsApp on iPhone now supports two accounts in one app; the separate WhatsApp Business app alongside regular WhatsApp is a known option but was not re-verified;
  - whether Apple Shortcuts or on-device AI can export or filter WhatsApp chats programmatically. WhatsApp offers no official read API for personal accounts.
- No Israeli-specific technical guidance on AI-assistant architecture from the Cyber Directorate or the PPA was found.

## Q6. Israeli news and incidents, 2025–2026: public employees, WhatsApp, AI data leaks, PPA enforcement on AI

### Takeaway
The recurring Israeli incident pattern is state-backed (Iran-linked) takeover or phishing of officials' WhatsApp and Telegram accounts, followed by publication of their messages. No PPA enforcement action against AI use, and no municipal "AI data leak", was found for 2025–2026.

### Cited Findings
- **Shin Bet, December 2024.** Shin Bet attributed more than 200 phishing attempts against senior Israeli figures to Iran. Targets included security officials, politicians, journalists and academics, and the approaches came through WhatsApp, Telegram and email. — [Iran International](https://iranintl.com/en/202412025221)
- **Handala.** The Iran-linked group Handala claimed hacks of phones belonging to Israeli figures, including Naftali Bennett and his former chief of staff. It later claimed to have taken over former interior minister Ayelet Shaked's WhatsApp account and read her message history. It also claimed to have surveilled a Mossad agent. — [Yahoo News](https://www.yahoo.com/news/articles/iran-linked-hacker-group-claims-183533671.html); [Ynetnews](https://ynetnews.com/business/article/hyyrh1y7c)
- **Jerusalem footage.** Israeli police and the Jerusalem Municipality denied that footage published by the Iran-linked group Moses Staff came from their cameras. — [Ynetnews](https://www.ynetnews.com/article/hkkbkjhio)
- **Cyber Directorate warnings.** The National Cyber Directorate's public warnings cover WhatsApp verification-code scams (account takeover) and fake investment groups. — [Mako](https://www.mako.co.il/nexter-news/Article-c9b3476f78fbb81027.htm)
- **No PPA AI fine found.** No PPA fine or enforcement action against an AI provider or an AI-related use in Israel was found for 2026. The closest comparable action is abroad: Italy's regulator fined OpenAI over ChatGPT and ordered a six-month awareness campaign. — [ICE (HEB)](https://www.ice.co.il/digital-140/news/article/1043604)

### Inferences
- For a municipal auditor, the realistic threat is account takeover of a WhatsApp number that holds years of work and complainant chats, more than AI-vendor training. Separating numbers and adding WhatsApp two-step verification reduce this risk, and the AI architecture should not create new exposure, such as a linked-device bridge or a bot with broad access.

### Gaps
- No reported Israeli municipal-employee WhatsApp or AI leak was found, and no PPA decision on generative-AI use by public bodies was found. The PPA's enforcement decisions page on gov.il could not be accessed to confirm this.
