# Voucher Reseller Offboarding

How an electronic voucher network closes down a distributor, dealer or retailer account cleanly: stopping sales, recalling unsold PIN stock, settling the wallet and credit line, paying final commission, moving the reseller's downstream retailers to a new parent, and revoking access. Applies to airtime PINs, eTopup and **gift card voucher distribution**. Written for distribution and finance teams evaluating [EVD System](https://evdsystem.com/) by [MoboGage](https://evdsystem.com/about-mobogage/).

---

## What reseller offboarding is

**Reseller offboarding** is the controlled process of ending a reseller's participation in a voucher distribution hierarchy. It settles everything the operator and the reseller owe each other, deals with stock the reseller still holds, and leaves the reseller's own retailers able to keep selling under someone else.

Onboarding gets a lot of attention because it brings in revenue. Offboarding gets far less, and that is why so many old dealer accounts sit half-closed with live API keys, a little stock and a credit balance nobody can explain.

## Why resellers leave

The reason decides the speed.

- **Voluntary exit or contract end.** Planned, with notice. Stock can be sold down and retailers moved over a few weeks.
- **Poor performance.** Usually planned, but the dealer may be less cooperative about handing over retailer contacts.
- **Unpaid credit.** Sales are stopped quickly to cap exposure, then the account is settled.
- **Suspected fraud or compliance breach.** Immediate suspension. Settlement waits for the investigation, and nothing is paid out until it closes.

Separate **suspension** (stop activity, keep everything as it is) from **closure** (settle and end). An investigation needs the first without the second.

## The offboarding sequence

```
Decision + effective date
   |
   1. Stop new sales            (API, POS, USSD, portal)
   2. Stop stock movements      (no new allocations, no transfers out)
   3. Re-parent downstream      (sub-dealers and retailers to a new parent)
   4. Recall stock              (unrevealed PINs back to parent pool)
   5. Deal with revealed stock  (downloaded or printed PINs)
   6. Final commission          (including any held reserve)
   7. Settle wallet and credit  (one net figure)
   8. Revoke access             (users, API keys, terminals, IP allowlist)
   9. Archive                   (records kept per retention policy)
```

The order matters. Re-parent before you recall stock, or the retailers lose their supply for the gap. Stop sales before you calculate anything, or the numbers move while you are counting.

## Stock: revealed versus unrevealed

**Unrevealed PINs** are PINs allocated to the reseller in the platform but never shown, downloaded or printed. Nobody outside the platform has seen them. They can be moved back to the parent's pool or the operator's reserve and sold again. Credit the reseller what they paid.

**Revealed PINs** have been downloaded to a print file, displayed in a portal or printed on cards. Someone may have copied them. Reselling them is risky because a PIN could be redeemed twice by two different buyers, and only one of them gets the airtime. The safe options are:

1. **Treat them as sold.** The reseller keeps them and the risk. Simple, but it pushes the reseller to dump cards on the street cheaply.
2. **Block and credit.** Check the redemption log, block every PIN that has not yet been redeemed, and credit the reseller for the blocked ones. PINs already redeemed were sold, so no credit.

Whatever you choose, never return revealed PINs to the general pool.

## Downstream retailers

A distributor might have dozens or hundreds of retailers underneath. Their accounts belong to them, not to the exiting distributor.

- Move each retailer to a new parent, or to the operator directly, with an effective date.
- Keep each retailer's own wallet balance and stock with the retailer. Do not sweep them up to the exiting parent.
- Change commission splits from the effective date. Sales before it pay commission up the old chain; sales after it pay up the new one.
- Tell the retailers. A retailer who finds their top-up line suddenly pointing at someone else will call the call centre, or stop selling.

## Money: wallet, credit and commission

Bring everything into one final statement.

| Line | Direction |
|------|-----------|
| Prepaid wallet balance | Operator owes reseller |
| Credit for recalled and blocked stock | Operator owes reseller |
| Final commission earned | Operator owes reseller |
| Drawn credit line | Reseller owes operator |
| Fees or penalties under the contract | Reseller owes operator |
| Clawback reserve | Held back for a set period, then released or used |

A **clawback reserve** covers things that surface after the account closes: a retailer reversal, a disputed sale, a late commission correction. Size it in the contract and release it on a fixed date.

## Access revocation

This is the step most often left half-done.

- Disable every portal user under the reseller, including staff accounts created years ago.
- Revoke API keys and certificates. Remove the reseller's IPs from the allowlist.
- Deactivate POS terminals and pull them back if the operator owns them.
- Remove the reseller from settlement and reporting jobs so it stops getting daily files.
- Keep the account record itself, in a closed state. Deleting it breaks the audit trail for past sales.

## Worked example (figures are illustrative)

All figures in this section are **illustrative**.

Dealer account D-0417 is leaving at contract end. Dealer buy price is 4.80 for a 5.00 PIN.

**Stock.** 3,600 unrevealed PINs are moved back to the operator's reserve and credited at cost: 3,600 × 4.80 = **17,280.00**. Another 600 PINs were downloaded to a print file last week. The redemption log shows 40 of them already redeemed by subscribers, so those count as sold. The remaining 560 are blocked and credited: 560 × 4.80 = **2,688.00**.

**Final statement**

| Line | Amount |
|------|--------|
| Prepaid wallet balance | +2,500.00 |
| Credit for 3,600 recalled PINs | +17,280.00 |
| Credit for 560 blocked PINs | +2,688.00 |
| Final commission | +340.00 |
| Drawn credit line | -1,800.00 |
| Clawback reserve (held 30 days) | -100.00 |
| **Payable to dealer now** | **20,908.00** |

If no reversals come in during the 30 days, the 100.00 reserve is paid out. The dealer's 25 retailers move to a neighbouring distributor on the effective date. Each keeps its own wallet balance.

## Things that go wrong

**Live API keys on closed accounts.** The account shows closed in the portal, but the integration still authenticates. Test it after revocation.

**Revealed PINs resold.** Printed stock goes back into the pool and some PINs get redeemed by the wrong buyer.

**Retailers stranded.** Stock recalled before re-parenting, so retailers cannot top up for days.

**Commission paid twice.** Sales near the effective date pay commission to both the old and new parent because the cut-over time was not exact.

**Credit balance left behind.** Small leftover balances sit for years on closed accounts and become an unreconciled liability.

The runbook for operations and finance is in [docs/offboarding-runbook.md](./docs/offboarding-runbook.md).

---

## FAQ

**What is reseller offboarding in voucher distribution?**
It is the process of ending a distributor's or retailer's place in the voucher hierarchy: stopping sales, recovering stock, settling money and moving their retailers to a new parent.

**What happens to unsold PINs when a voucher reseller leaves?**
PINs that were never revealed can be recalled and resold. PINs that were downloaded or printed should be blocked if unredeemed, and credited, or treated as sold. They should not go back into the general pool.

**What happens to the retailers under an exiting distributor?**
They are moved to a new parent or to the operator directly, keeping their own balances. Commission follows the new chain from the effective date.

**Should a closed reseller account be deleted?**
No. Close it and revoke access, but keep the record so past sales and audits remain traceable.

**What is a clawback reserve?**
An amount held back from the final payment for a fixed period to cover reversals or corrections that appear after closure.

**Does EVD System support multi-tier distribution?**
EVD System by MoboGage covers voucher generation, inventory and reseller channels, including multi-tier distributor and retailer hierarchies.

---

## Glossary

| Term | Meaning |
|------|---------|
| Offboarding | Ending a reseller's participation and settling the account |
| Suspension | Stopping activity without settling, for example during an investigation |
| Unrevealed PIN | A PIN allocated in the platform but never shown or exported |
| Revealed PIN | A PIN that has been downloaded, displayed or printed |
| Re-parenting | Moving a reseller to a different parent in the hierarchy |
| Clawback reserve | Part of the final payment held back for a set period |

## Further reading

- [Multi-tier reseller voucher distribution](https://evdsystem.com/evd-software/multi-tier-reseller-voucher-distribution/) on evdsystem.com
- [Electronic voucher distribution software](https://evdsystem.com/evd-software/electronic-voucher-distribution-software/) on evdsystem.com
- Related repo: [voucher-retailer-onboarding](https://github.com/iwtglobal/voucher-retailer-onboarding)

## License

MIT. See [LICENSE](./LICENSE). Educational material only, not legal or contractual advice.
