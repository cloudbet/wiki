---
title: Margin Adjustments in Sports Betting
linkTitle: Margin Adjustments
description: Learn how to adjust margins in sports betting to set your own odds based on the data the Cloudbet B2B API supplies.
weight: 10
type: docs
---

You can integrate the Cloudbet B2B API and set your own odds based on the data supplied, enabling you to carve out a profitable margin for each transaction. Alongside margins, you can also take control of and share liability from the individual bets that players or customers place through your platform.

### Basic Implied Probability Calculation

The implied probability of an outcome is initially calculated from the given odds and the overround. For a specific betting market:

```math
\tag*{(1)} \text{Implied Probability} = \frac{1}{\text{Odds} \times \text{Overround}}
```

This calculation gives a base probability adjusted for the bookmaker's initial margin embedded within the odds.

### Adjusting the Overround

To reflect changes in market conditions, event specifics, or risk assessments, the overround is adjusted by adding a margin percentage:

```math
\tag*{(2)} \text{Adjusted Overround} = \text{Overround} + \text{Margin Percentage}
```

This formula ensures that the total market margin is adaptive and adjusts with the origin.

### Recalculating Odds with Adjusted Overround

After adjusting the overround, new odds are recalculated as follows:

```math
\tag*{(3)} \text{New Odds} = \frac{1}{\text{Implied Probability} \times \text{Adjusted Overround}}
```

This method of recalculating the odds maintains the relative value between different outcomes while adjusting the overall margin.

### Example Calculation

If the initial odds for a team winning are 2.0 with an overround of 1.05, the implied probability is:

```math
\text{Implied Probability} = \frac{1}{2.0 \times 1.05} = 0.4762
```

If the margin percentage is adjusted to 1.10, the new odds would be:

```math
\text{New Odds} = \frac{1}{0.4762 \times 1.10} = 1.91
```

These recalculated odds reflect the adjusted margin and provide a new market price for the outcome.
