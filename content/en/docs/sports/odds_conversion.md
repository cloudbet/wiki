---
title: Odds Conversion
description: How to convert between different betting odds formats, including US, Decimal, and Exchange odds.
weight: 3
type: docs
---

There are different ways in which odds can be displayed for sports betting markets. Aside from the three primary types — American Odds, Decimal Odds, and Fractional Odds — Cloudbet also supports Hong Kong and Malaysian odds. The Cloudbet API is offered in Decimal Odds format, but you can convert these to other formats using the formulas below.

### Converting US Odds to Decimal Odds

US Odds can be converted to Decimal Odds using the following formulas based on whether the US Odds are positive or negative:

For positive US Odds:

```math
\tag*{(1)} \text{DecimalOdds} = 1 + \left(\frac{\text{USOdds}}{100}\right)
```

For negative US Odds:

```math
\tag*{(2)} \text{DecimalOdds} = 1 + \left(\frac{100}{|\text{USOdds}|}\right)
```

**Example:**
- For US Odds of -110: \\( \text{Decimal Odds} = 1 + \frac{100}{110} \approx 1.909 \\)
- For US Odds of +150: \\( \text{Decimal Odds} = 1 + \frac{150}{100} = 2.5 \\)


### Converting Decimal Odds to US Odds

Decimal Odds can be converted to US Odds using the following formula:

If \\(\text{DecimalOdds} \geq 2.0\\):

```math
\tag*{(3)} \text{USOdds} = (\text{DecimalOdds} - 1) \times 100
```

If \\(\text{DecimalOdds} < 2.0\\):

```math
\tag*{(4)} \text{USOdds} = -\frac{100}{\text{DecimalOdds} - 1}
```

**Example:**
- For Decimal Odds of 1.909: \\( \text{US Odds} = -\frac{100}{1.909 - 1} \approx -110 \\)
- For Decimal Odds of 2.5: \\( \text{US Odds} = (2.5 - 1) \times 100 = 150 \\)

### Converting Fractional Odds to Decimal Odds

Fractional Odds are commonly used in the UK and Ireland and represent the potential profit received on a bet relative to the stake. Here's how to convert between Fractional Odds and other formats:

To convert Fractional Odds to Decimal Odds, add 1 to the result of dividing the numerator by the denominator:

```math
\tag*{(7)} \text{DecimalOdds} = 1 + \left(\frac{\text{Numerator}}{\text{Denominator}}\right)
```

**Example:**
- For Fractional Odds of 3/2: \\( \text{Decimal Odds} = 1 + \frac{3}{2} = 2.5 \\)


### Exchange Odds to Standard Bookmaker Odds

Betting exchanges offer odds in a decimal format similar to standard bookmakers but include a commission on winnings. This section explains how to adjust exchange odds to reflect the equivalent odds offered by a standard bookmaker, accounting for the commission taken by the exchange.

For US Exchange Odds:

```math
\tag*{(5)} \text{EquivalentUSOdds} = \text{USExchangeOdds} - \left(\frac{\text{USExchangeOdds} \times \text{Commission}}{100 - \text{Commission}}\right)
```

For Decimal Exchange Odds:

```math
\tag*{(6)} \text{EquivalentDecimalOdds} = \frac{\text{DecimalExchangeOdds}}{1 - (\text{Commission} / 100)}
```

**Example (with 1% Commission):**
- For US Odds of -110: \\( \text{Adjusted US Odds} = -110 \times (1 - 0.01) \approx -111.10 \\)
- For Decimal Odds of 1.909: \\( \text{Adjusted Decimal Odds} = 1.909 \times (1 - 0.01) \approx 1.88991 \\)

