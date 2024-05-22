---
title: Reduction Factors in Horse Racing
linkTitle: Reduction Factors
description: A guide to understanding and computing reduction factors in horse racing to adjust betting odds.
weight: 20
type: docs
---

Reduction factors adjust the betting odds in horse racing when horses withdraw after bets have been placed. The odds offered for each remaining horse are reduced.

## Settlement & Refunds

When a horse is declared a non-runner in a race, any bets placed on that horse are usually voided, and the stake is refunded to the bettor. However, the presence of a non-runner also impacts bets already placed on other horses in the race. This is where reduction factors come into play.

Without adjusting the odds, the payouts would disproportionately favor bettors in light of the new, higher probability of winning.

For the most current rules and settlement guidelines, please consult the [Cloudbet Sportsbook Rules](https://www.cloudbet.com/en/help/rules).

## Computing Reduction Factors

Reduction factors are calculated based on the odds of the non-runners. The factor reflects the impact of the withdrawn horse on the race:

```math
\tag*{(1)} \text{ReductionFactor} = \frac{1}{\text{DecimalOdds}}
```

Where DecimalOdds are the odds of the non-runner.

### Application Threshold

It's worth noting that if the reduction factor for the withdrawn horse is less than 2.5% it is not applied. This policy is in place to avoid minor adjustments that have negligible impact on the odds and payouts.

### Applying Reduction Factors to Adjust Odds

The adjusted odds for remaining horses after a withdrawal can be computed using the formula:

```math
\tag*{(2)} \text{AdjustedOdds} = (\text{OriginalOdds} - 1) \times (1 - \text{ReductionFactor}) + 1
```

Example: Assume a non-runner had odds of 5.0, generating a reduction factor of:

\\( \text{ReductionFactor} = \frac{1}{5.0} = 0.20 \\)

If another horse in the race originally had odds of 8.0, the adjusted odds would be:

\\( \text{AdjustedOdds} = (8.0 - 1) \times (1 - 0.20) + 1 = 6.6 \\)

These adjusted odds now reflect the new potential payout considering the changed race conditions.
