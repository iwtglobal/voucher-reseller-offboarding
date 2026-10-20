# Reseller Offboarding Runbook

Steps for distribution operations and finance to close a voucher reseller account. Replace every figure with your own policy values.

## Day 0: decision

- [ ] Reason recorded: voluntary, contract end, performance, unpaid credit, or investigation
- [ ] If investigation: suspend only, no settlement until it closes
- [ ] Effective date and time agreed (one exact timestamp, used everywhere)
- [ ] New parent chosen for each downstream sub-dealer and retailer
- [ ] Retailers told the date and their new top-up contact

## At the effective time

1. Block new sales on API, POS, USSD and portal for the reseller account.
2. Block stock allocations and transfers to or from the account.
3. Re-parent downstream accounts. Confirm each keeps its own wallet and stock.
4. Switch commission chains for the moved accounts.

## Stock

- [ ] Unrevealed PINs listed by denomination and moved to the parent pool or operator reserve
- [ ] Revealed PINs listed (downloaded, displayed, printed)
- [ ] Redemption log checked for each revealed PIN
- [ ] Unredeemed revealed PINs blocked, or treated as sold, per contract
- [ ] No revealed PIN returned to the general pool

## Money

- [ ] Wallet balance confirmed
- [ ] Stock credits calculated at the reseller's buy price
- [ ] Final commission run for sales up to the effective time
- [ ] Credit line balance and any contract fees confirmed
- [ ] Clawback reserve deducted (**illustrative**: 30 days)
- [ ] Final statement approved by a second person, then paid or invoiced

## Access

- [ ] All portal users disabled
- [ ] API keys and certificates revoked; a test call is rejected
- [ ] IP allowlist entries removed
- [ ] POS terminals deactivated and collected if operator-owned
- [ ] Removed from daily settlement and report jobs

## Day 30 (illustrative)

- [ ] Reversals or disputes against the reserve applied
- [ ] Remaining reserve released
- [ ] Account balance zero, status closed, record retained
