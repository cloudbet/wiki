---
title: Understanding Cashouts
linkTitle: Cashouts
description: Explaining the concept of cashouts in sports betting, including how to calculate cashout amounts and the conditions for full and partial cashouts.
type: docs
weight: 2
---

Cloudbet allow bettors to settle bets early, securing a return before the event concludes with cashouts. This feature improves control over betting strategies, providing an opportunity to lock in profits or minimize losses based on real-time developments in the event.

### Cashout Calculation

The cashout amount depends on the potential return of the original bet and the odds available for the opposite outcomes at the time of cashout. The formula used is:

```math
\tag*{(1)} \text{CashoutAmount} = \text{CashedOutReturn} - \sum \left(\frac{\text{CashedOutReturn}}{\text{AgainstOdds}}\right)
```

- The formula subtracts the sum of the potential returns from opposing odds from the exhausted potential return amount to determine the cashout amount.
- This ensures that the cashout amount reflects current market conditions and the likely return if the bet were settled at that moment.

**Note**: The cashout amount must always be greater than zero.

#### Full Cashout Example

Consider a bet placed on a 3-way market. The initial bet was EUR 10 at odds of 1.4 (Home win), with a total potential return of EUR 14.

Suppose current odds are:

| Side | Odds |
|------|------|
| Home | 1.38 |
| Draw | 4.68 |
| Away | 8.81 |

Calculating the full cashout:

```math
\tag*{(2)} \text{CashoutAmount} = 14 - \left(\frac{14}{4.68} + \frac{14}{8.81}\right) = 9.419
```

After this cashout, the potential return is zero, and the bet is fully settled.

#### Partial Cashout Example

For a partial cashout, consider the same initial conditions but with different subsequent odds:

In this example, we assume the odds have shifted:

| Side | Odds |
|------|------|
| Home | 1.20 |
| Draw | 6.02 |
| Away | 18.1 |

To cash out EUR 8 of the potential return:

```math
\tag*{(3)} \text{CashoutAmount} = 8 - \left(\frac{8}{6.02} + \frac{8}{18.1}\right) = 6.229
```

The remaining stake (calculated based on the proportion of the potential return not cashed out):

```math
\tag*{(4)} \text{RemainingStake} = 10 \times \left(\frac{6}{14}\right) = 4.286
```

This remaining stake will continue under the normal settlement process. Later, if the bettor decides to cash out the rest:

We further assume the current odds:

| Side | Odds |
|------|------|
| Home | 1.82 |
| Draw | 3.51 |
| Away | 4.23 |

Final cashout for the remaining EUR 6 potential return:

```math
\tag*{(5)} \text{CashoutAmount} = 6 - \left(\frac{6}{3.51} + \frac{6}{4.23}\right) = 2.872
```

After this transaction, there is no remaining potential return, and the original bet is fully settled.

Cashouts provide a strategic tool for bettors to manage risk and secure returns under changing conditions.
