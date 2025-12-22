# Technology Proposal: Discourse Parallel

**A forum platform to parallel and potentially replace current communication fragmentation.**

---

## Proposer Information

| Field | Value |
|-------|-------|
| Submitted by | [Example Proposer] |
| Date | [Example Date] |
| Contact | example@sdcap.org |
| Proposed Steward | Communications Committee |

---

## Executive Summary

We propose implementing Discourse as a persistent community forum to complement our real-time Discord chat. This addresses the problem of important discussions and decisions getting lost in chat history, while creating a searchable archive of community knowledge and a more accessible entry point for new members.

---

## Current State

### Current Solution(s)

| System | Function | Issues |
|--------|----------|--------|
| Discord | Real-time chat | Messages disappear into history, hard to search, overwhelming for new members |
| Email lists | Announcements | Low engagement, one-way, no threading |
| Google Docs | Long-form documents | Scattered, hard to find, no discussion |
| Nothing | Persistent Q&A | Gap — no way to build searchable knowledge base |

### Pain Points

- **Ephemeral conversations**: Important decisions made in Discord vanish into scroll-back
- **Onboarding difficulty**: New members face firehose of channels, can't find basics
- **Knowledge loss**: Same questions answered repeatedly; no archive
- **Accessibility**: Discord requires account, app, and real-time availability
- **Search**: Can't find "that discussion we had about X last year"

---

## Proposed Solution

### The Technology

| Attribute | Value |
|-----------|-------|
| Name | Discourse |
| Vendor/Project | Discourse.org (open source) |
| Type | Self-hosted or Discourse-hosted |
| License | GPL v2 |
| Website | https://discourse.org |

### Why Discourse?

1. **Designed for communities**: Trust levels, badges, moderation tools built-in
2. **Persistent and searchable**: Every discussion is findable forever
3. **Async-friendly**: Works for people not online 24/7
4. **Email integration**: Reply by email, digest notifications
5. **Open source**: No lock-in
6. **Proven**: Powers communities for Burning Man, many nonprofits

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Selected |
|-------------|------|------|------------------|
| Expand Discord use | Already using, no new tool | Ephemeral, hard to search, excluding | Doesn't solve core problems |
| Slack | Familiar | Not async-friendly, expensive at scale | Cost, same problems as Discord |
| Mighty Networks | Nice UX | Expensive, proprietary | Cost, lock-in |
| Facebook Groups | Free, familiar | Privacy concerns, algorithm-driven | Not aligned with values |
| Just email lists | Simple | No threading, low engagement | Doesn't build knowledge |

---

## Evaluation Criteria

### Must Have
- [x] Persistent, searchable discussions — Met: ☑ Yes
- [x] Email notification/reply — Met: ☑ Yes
- [x] Moderation tools — Met: ☑ Yes
- [x] Categories/organization — Met: ☑ Yes
- [x] Data exportable — Met: ☑ Yes

### Should Have
- [x] Open source — Met: ☑ Yes
- [x] Self-hostable — Met: ☑ Yes
- [x] Mobile app — Met: ☑ Yes
- [x] SSO/OAuth — Met: ☑ Yes

### Nice to Have
- [x] Discord integration — Met: ☑ Partial (webhooks)
- [x] Event calendar — Met: ☑ Plugin available
- [x] Wiki-like pages — Met: ☑ Yes

---

## Use Case Definition

### What Goes Where?

| Content Type | Discourse | Discord |
|--------------|-----------|---------|
| Announcements | ✅ Primary | ✅ Cross-post |
| Project proposals | ✅ Primary | Link only |
| Policy discussions | ✅ Primary | Link only |
| How-to guides | ✅ Primary | — |
| FAQs | ✅ Primary | — |
| Real-time coordination | — | ✅ Primary |
| Casual chat | — | ✅ Primary |
| Voice/video calls | — | ✅ Primary |

### Integration with Discord

```
Discourse                          Discord
┌─────────────────┐               ┌─────────────────┐
│ New Proposal    │───webhook────▶│ #announcements  │
│ Posted          │               │ "New proposal!" │
└─────────────────┘               └─────────────────┘

Discord                           Discourse  
┌─────────────────┐               ┌─────────────────┐
│ "Check Discourse│               │ Deep discussion │
│  for details"   │───link───────▶│ with history    │
└─────────────────┘               └─────────────────┘
```

---

## Implementation Plan

### Phase 1: INTRODUCE (Pilot)

**Duration:** 6 weeks

**Scope:**
- Deploy Discourse on test domain
- Import key existing documents (FAQs, how-tos)
- Invite 10-15 pilot users (board + active community)
- Test categories: Governance, Projects, General
- Gather feedback weekly

**Success Criteria:**
- [ ] Pilot users post without prompting
- [ ] Search returns useful results
- [ ] Email notifications work reliably
- [ ] New member can find basics without help

**Rollback Plan:**
Test instance only; if pilot fails, archive and continue with Discord-only.

---

### Phase 2: PARALLEL

**Duration:** 3 months

**Scope:**
- Open to full community (optional)
- Cross-post announcements both places
- Move proposal discussions to Discourse
- Discord remains primary for chat
- Build FAQ/knowledge base

**Success Criteria:**
- [ ] 50%+ of community has Discourse account
- [ ] All governance discussions on Discourse
- [ ] Knowledge base has 20+ useful articles
- [ ] Searchable history is valuable
- [ ] Email-only members can participate

---

### Phase 3: TRANSITION

**Duration:** Ongoing

**Scope:**
- Discourse is primary for persistent content
- Discord is primary for real-time
- Clear norms for "what goes where"
- Onboarding points to Discourse first

**Note:** This is not a full replacement — Discourse and Discord serve different purposes. Transition means establishing clear, stable roles for each.

---

## Resources Required

### Cost

**Option A: Self-Hosted**

| Item | One-Time | Monthly | Annual |
|------|----------|---------|--------|
| Server (VPS) | $0 | $20 | $240 |
| Domain | $15 | $0 | $15 |
| Mailgun (email) | $0 | $10 | $120 |
| **Total** | **$15** | **$30** | **$375** |

**Option B: Discourse Hosting (Standard)**

| Item | One-Time | Monthly | Annual |
|------|----------|---------|--------|
| Discourse hosting | $0 | $100 | $1,200 |
| **Total** | **$0** | **$100** | **$1,200** |

**Recommendation:** Start with self-hosted. Migrate to hosted if maintenance burden too high.

### People

| Role | Phase | Time Commitment |
|------|-------|-----------------|
| Implementation Lead | Intro/Parallel | 5 hrs/week |
| Community Manager | Ongoing | 3 hrs/week |
| Moderators (2-3) | Ongoing | 2 hrs/week each |

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Community doesn't adopt | Medium | High | Clear value prop, board models usage, cross-post from Discord |
| Splits community in two | Medium | Medium | Clear "what goes where" norms, integration |
| Moderation burden | Low | Medium | Discourse's trust levels reduce load; recruit mods |
| Technical complexity | Low | Low | Discourse is mature, well-documented |
| Content goes stale | Medium | Low | Assign content owner per category |

---

## Security & Privacy

### Data Classification
- [x] Member data (usernames, emails)
- [ ] Financial data (none)
- [x] Some discussions may be member-only

### Security Measures
- [x] HTTPS
- [x] SSO with existing accounts
- [x] Role-based access (categories can be restricted)
- [x] Audit logging
- [x] Automated backups

### Privacy Compliance
- [x] Clear privacy policy
- [x] User data export available
- [x] Account deletion supported

---

## Proposed Category Structure

```
SDCAP Community Forum
├── 👋 Welcome
│   ├── Start Here (pinned)
│   ├── Introductions
│   └── FAQ
├── 📋 Governance (members only)
│   ├── Proposals
│   ├── Board Updates
│   └── Policy Discussion
├── 🎨 Projects
│   ├── Active Projects
│   ├── Looking for Help
│   └── Show & Tell
├── 🛠️ SDCoLab
│   ├── Space Updates
│   ├── Tool Training
│   └── Build Parties
├── 🔥 Community
│   ├── Events
│   ├── Resources
│   └── Off-Topic
└── 📚 Knowledge Base
    ├── How-To Guides
    ├── Templates
    └── History & Archives
```

---

## Sustainability

### Long-term Ownership

**Primary Steward:** Communications Committee Chair  
**Content Owners:** One per major category  
**Moderators:** 2-3 community volunteers

### Documentation Required
- [ ] Moderation guidelines
- [ ] "What goes where" guide
- [ ] Admin runbook
- [ ] Category owner responsibilities

### Community Norms
- Welcome new members
- Move conversations to appropriate category
- Link Discord <-> Discourse as appropriate
- Archive stale content periodically

---

## Request

**Approval Requested:**
- [x] Proceed to INTRODUCE (Pilot) phase
- [x] Budget allocation: $100 for pilot infrastructure (3 months)
- [x] Committee oversight: Communications Committee

**Timeline:**
- Approval requested by: [Date]
- Pilot start: [Date + 1 week]
- Pilot decision: [Date + 7 weeks]

---

## Appendix

### A. Examples of Discourse in Similar Communities

| Community | URL | Notes |
|-----------|-----|-------|
| Burning Man | talk.burningman.org | Official BM discussion |
| Mozilla | discourse.mozilla.org | Open source community |
| Let's Encrypt | community.letsencrypt.org | Nonprofit tech |

### B. Discord vs. Discourse Feature Comparison

| Feature | Discord | Discourse |
|---------|---------|-----------|
| Real-time chat | ✅ Excellent | ❌ Not designed for |
| Voice/video | ✅ Built-in | ❌ None |
| Search (old content) | ⚠️ Poor | ✅ Excellent |
| Email participation | ❌ No | ✅ Full |
| Newcomer onboarding | ⚠️ Overwhelming | ✅ Progressive |
| Async discussion | ⚠️ Gets buried | ✅ Designed for |
| Mobile | ✅ Good app | ✅ Good app |
| Trust/reputation | ❌ None | ✅ Built-in |

---

*Example proposal demonstrating Technology Proposal template*
