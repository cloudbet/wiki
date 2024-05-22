---
title: Betting Outcomes and Probability Computations
linkTitle: Probability Computations
description: In-depth exploration of the mathematical foundations of betting probabilities and their implications for strategy.
weight: 4
type: docs
---

This page provides technical details for understanding and utilizing betting odds and probabilities that are foundational for developing sophisticated betting strategies.

- **True Odds**: The actual probabilities of outcomes without any bookmaker margin. True odds are rarely offered in sports betting as they do not provide any profit margin for the sportsbook.
- **Implied Odds**: These odds are derived from the betting odds offered by Cloudbet, indicating the implied chances of a particular outcome to be. Implied odds include the overround or vig, which is their built-in profit margin.
- **Fair Odds**: Also known as zero-vig or no-vig odds, these are calculated by removing Cloudbet’s overround from the implied odds. Fair odds show what the betting odds would be if Cloudbet did not apply a profit margin, providing a "fair" assessment of probability. Calculating fair odds is useful for bettors in assessing the value of the odds offered compared to the true likelihood of the event.

### Conversion from US Odds to Probability

US odds represent the amount won on a 100 unit bet when positive, and the stake needed to win 100 units when negative. The probability implied by US odds is calculated as follows:

When odds are positive:

```math
\tag*{(1)} P(Win) = \frac{100}{\text{USOdds} + 100}
```

When odds are negative:

```math
\tag*{(2)} P(Win) = \frac{|\text{USOdds}|}{|\text{USOdds}| + 100}
```

### Conversion from Decimal Odds to Probability

Decimal odds represent the total payout (stake + win) for each unit bet. The probability implied by decimal odds is simpler to calculate:

```math
\tag*{(3)} P(Win) = \frac{1}{\text{DecimalOdds}}
```

## Calculating Edge from Probability and Odds

The edge represents the expected value of a bet as a percentage of the bet amount. It indicates a player's advantage (or disadvantage) against the odds offered by the bookmaker.

Using decimal odds:

```math
\tag*{(4)} \text{Edge} = (\text{Probability} \times \text{DecimalOdds}) - 1
```

### Example: Calculating Edge from Probability and Odds

Let's say you are considering a bet on a tennis player to win a match. The bookmaker offers decimal odds of 1.8 for this player to win. You estimate that the probability of the player winning is 60% (or 0.60). Plug in your values:

\\( \text{Edge} = (0.60 \times 1.8) - 1 = 1.08 - 1 = 0.08 \\)

This result, 0.08 or 8%, represents your edge. It indicates that you have an 8% advantage against the odds offered by the bookmaker. This is a positive edge, suggesting that the bet has a positive expected value, making it a potentially profitable bet if your probability estimation is accurate.

### From Edge to Probability

Conversely, calculating the probability required to justify a bet at given odds can help bettors decide whether the bet has positive expected value.

Using decimal odds:

```math
\tag*{(5)} \text{Probability} = \frac{1 + \text{Edge}}{\text{DecimalOdds}}
```

### Example: Calculating Required Probability

Suppose a bookmaker offers odds of 2.5 for a particular team to win a game. You want to calculate the probability that justifies these odds, assuming you have determined an edge of 0.04 (or 4%). Plug in the values:

\\( \text{Probability} = \frac{1.04}{2.5} \approx 0.416 \\)

This result, 0.416 or 41.6%, is the minimum probability at which the expected value of the bet becomes neutral or positive, given the edge of 4%. It shows that if you estimate the true probability of the team winning is greater than 41.6%, the bet has a positive expected value, making it a potentially good bet.

### Decision Making

If your analysis or model suggests that the actual probability of the team winning is higher than 41.6%, say 45%, then the bet is favorable because your estimated probability exceeds the break-even probability calculated. This suggests an expected value that is positive, making it a rational bet under these assumptions.

If your estimate is lower, say 40%, the bet does not justify the odds, indicating a negative expected value, and it would be advisable to avoid placing the bet.
