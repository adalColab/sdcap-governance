# Technology Proposal: ERPNext Parallel

**An ERP system to parallel and potentially replace QGIV, Bloomerang, and related services.**

---

## Proposer Information

| Field | Value |
|-------|-------|
| Submitted by | [Example Proposer] |
| Date | [Example Date] |
| Contact | example@sdcap.org |
| Proposed Steward | Tech Committee Chair |

---

## Executive Summary

We propose implementing ERPNext as a unified platform to replace our fragmented stack of QGIV (donations), Bloomerang (donor management), and spreadsheet-based tracking. This will reduce costs, improve data integration, and give us ownership of our critical organizational data.

---

## Current State

### Current Solution(s)

| System | Function | Issues |
|--------|----------|--------|
| QGIV | Donation processing | Limited reporting, fees per transaction |
| Bloomerang | Donor management | Siloed from other data, annual cost |
| Google Sheets | Project tracking | Manual, error-prone, no audit trail |
| Email | Communication | Not integrated with donor records |

### Pain Points

- **Data fragmentation**: Donor info in Bloomerang, donations in QGIV, projects in Sheets — nothing talks to each other
- **Cost**: ~$2,400/year across platforms, plus transaction fees
- **No integration**: Manual reconciliation wastes hours monthly
- **Vendor lock-in**: Our donor history is trapped in proprietary systems
- **Limited visibility**: Can't easily answer "how much has this donor given across all projects?"

---

## Proposed Solution

### The Technology

| Attribute | Value |
|-----------|-------|
| Name | ERPNext |
| Vendor/Project | Frappe (open source) |
| Type | Self-hosted |
| License | GPL v3 (fully open source) |
| Website | https://erpnext.com |

### Why ERPNext?

1. **Nonprofit module**: Built-in donor management, grants, members
2. **All-in-one**: CRM, accounting, projects, HR in one system
3. **Open source**: No vendor lock-in, forever
4. **Self-hosted**: Our data stays ours
5. **API-first**: Integrates with everything
6. **Active community**: 14,000+ GitHub stars, weekly releases

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Selected |
|-------------|------|------|------------------|
| Salesforce NPSP | Industry standard, powerful | Expensive, complex, vendor lock-in | Cost, complexity, lock-in |
| CiviCRM | Nonprofit-focused, open source | WordPress-dependent, dated UX | Technical debt concerns |
| Keep current stack | No migration effort | Fragmentation, cost, lock-in continues | Doesn't solve problems |
| Odoo | Similar to ERPNext | Enterprise features require paid version | Less truly open source |

---

## Evaluation Criteria

### Must Have
- [x] Donor management — Met: ☑ Yes
- [x] Donation processing — Met: ☑ Yes (via payment gateway integration)
- [x] Project tracking — Met: ☑ Yes
- [x] Financial reporting — Met: ☑ Yes
- [x] Data exportable — Met: ☑ Yes (full data export, open database)

### Should Have
- [x] Open source — Met: ☑ Yes
- [x] Self-hostable — Met: ☑ Yes
- [x] API for integration — Met: ☑ Yes (REST API)
- [x] Mobile friendly — Met: ☑ Yes

### Nice to Have
- [x] Grant management — Met: ☑ Yes
- [x] Event management — Met: ☑ Yes (basic)
- [ ] Built-in email marketing — Met: ☐ Partial (integrations available)

---

## Integration

### Data Flow

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Donors    │────▶│   ERPNext   │◀────│   Stripe    │
└─────────────┘     │             │     └─────────────┘
                    │  - CRM      │
┌─────────────┐     │  - Finance  │     ┌─────────────┐
│  Projects   │────▶│  - Grants   │◀────│   Discord   │
└─────────────┘     │  - Members  │     │   (notify)  │
                    └─────────────┘     └─────────────┘
```

### Dependencies

| System | Integration Type | Complexity |
|--------|------------------|------------|
| Stripe | API (payments) | Low |
| Discord | Webhook (notifications) | Low |
| Google Workspace | OAuth (login) | Medium |
| Website | Embed (donation forms) | Low |

---

## Implementation Plan

### Phase 1: INTRODUCE (Pilot)

**Duration:** 2 months

**Scope:**
- Deploy ERPNext on test server
- Import subset of donor data (with permission)
- Process test donations
- 3-5 volunteer pilot users
- Focus on donor management and donations only

**Success Criteria:**
- [x] Can record donations as easily as QGIV
- [x] Can track donor history in one place
- [x] Pilot users find it usable
- [x] Data can be exported cleanly

**Rollback Plan:**
Test instance only; if pilot fails, simply delete and continue with current systems.

---

### Phase 2: PARALLEL

**Duration:** 4 months

**Scope:**
- Run ERPNext alongside current systems
- Sync donations from QGIV to ERPNext weekly
- Track projects in both systems
- Full historical data import
- Train all regular users

**Success Criteria:**
- [x] All current functionality replicated
- [x] Data matches between systems
- [x] Users prefer ERPNext workflow
- [x] Reporting is equal or better
- [x] Integration with Stripe works in production

---

### Phase 3: TRANSITION

**Duration:** 2 months

**Scope:**
- Switch donation forms to ERPNext/Stripe
- Cancel QGIV subscription
- Cancel Bloomerang subscription
- Archive old data (read-only)
- Full production deployment

**Cutover Plan:**
1. Announce transition date 30 days out
2. Freeze data entry in old systems
3. Final data sync
4. Switch DNS for donation forms
5. 2-week intensive support period
6. Archive old systems

---

## Resources Required

### Cost

| Item | One-Time | Monthly | Annual |
|------|----------|---------|--------|
| Server (VPS) | $0 | $40 | $480 |
| Domain/SSL | $20 | $0 | $20 |
| Backup storage | $0 | $10 | $120 |
| Stripe fees | $0 | ~$50* | ~$600* |
| **Total** | **$20** | **$100** | **$1,220** |

*Stripe fees are pass-through; similar to current QGIV fees.

**Current annual cost:** ~$2,400  
**Projected savings:** ~$1,180/year

### People

| Role | Phase | Time Commitment |
|------|-------|-----------------|
| Implementation Lead | Intro/Parallel | 10 hrs/week |
| System Steward | Ongoing | 5 hrs/month |
| Data Migration | Intro | 20 hrs total |
| Training | Parallel | 10 hrs total |

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Self-hosting complexity | Medium | Medium | Use managed hosting initially; Frappe Cloud as fallback |
| Users resist change | Medium | Medium | Involve users in pilot; train thoroughly |
| Data migration errors | Low | High | Validate data at each phase; keep old systems read-only |
| Implementation lead leaves | Medium | High | Document everything; cross-train second person |
| ERPNext project dies | Low | High | Open source; can fork; data always exportable |

---

## Security & Privacy

### Data Classification
- [x] Member data
- [x] Financial data
- [x] Sensitive/PII (donor info)

### Security Measures
- [x] Encryption at rest (server-level)
- [x] Encryption in transit (HTTPS)
- [x] Access controls (role-based)
- [x] Audit logging (built-in)
- [x] Backup/recovery (automated daily)

### Privacy Compliance
- [x] Privacy policy reviewed
- [x] Self-hosted = we control data location
- [x] Donor consent for data migration

---

## Sustainability

### Long-term Ownership

**Primary Steward:** Tech Committee Chair  
**Backup Steward:** Treasurer (for financial module)

### Documentation Required
- [x] User guide (customize from ERPNext docs)
- [x] Admin runbook
- [x] Backup/recovery procedures
- [x] Integration documentation

### Training Plan
- 2-hour initial training for all users
- Written quick-start guide
- Monthly "office hours" for questions during parallel phase

---

## Request

**Approval Requested:**
- [x] Proceed to INTRODUCE (Pilot) phase
- [x] Budget allocation: $200 for pilot infrastructure
- [x] Committee oversight: Tech Committee

**Timeline:**
- Approval requested by: [Date]
- Pilot start: [Date + 2 weeks]
- Pilot decision: [Date + 10 weeks]

---

## Appendix

### A. Feature Comparison Matrix

| Feature | Current Stack | ERPNext |
|---------|---------------|---------|
| Donation processing | QGIV | ✅ |
| Donor management | Bloomerang | ✅ |
| Grant tracking | Sheets | ✅ |
| Project management | Sheets | ✅ |
| Financial reports | Manual | ✅ |
| Member management | None | ✅ |
| Unified data | ❌ | ✅ |
| Open source | ❌ | ✅ |
| Self-hosted option | ❌ | ✅ |

### B. Total Cost of Ownership (5-Year)

| Scenario | Year 1 | Year 2-5 | Total |
|----------|--------|----------|-------|
| Current stack | $2,400 | $9,600 | $12,000 |
| ERPNext (self-hosted) | $1,220 | $4,880 | $6,100 |
| **Savings** | **$1,180** | **$4,720** | **$5,900** |

---

*Example proposal demonstrating Technology Proposal template*
