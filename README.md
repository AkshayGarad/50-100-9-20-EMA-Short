# EMA Crossunder Strategy

This is a simple trading strategy script written in Pine Script language for TradingView. The strategy is based on exponential moving average (EMA) crossovers and is intended for use in TradingView's built-in Pine Script editor.

## Overview

The EMA Crossunder Strategy is a trend-following trading strategy that generates buy and sell signals based on the crossover and crossunder of two exponential moving averages (EMAs). It also includes an exit condition based on the crossover of two additional EMAs.

## Strategy Code

```pinescript
//@version=4
strategy("EMA Crossunder Strategy", shorttitle="Modified EMA Cross", overlay=true)

// Input parameters
emaLengthShort = input(50, title="Short EMA Length")
emaLengthLong = input(100, title="Long EMA Length")

// Calculate EMAs
emaShort = ema(close, emaLengthShort)
emaLong = ema(close, emaLengthLong)

// Plot EMAs on the chart
plot(emaShort, color=color.blue, title="Short EMA")
plot(emaLong, color=color.red, title="Long EMA")

// Create strategy conditions
emaCrossUnder = crossunder(emaShort, emaLong)
emaCrossOver = crossover(emaShort, emaLong)

// Short and exit short conditions
strategy.entry("Short", strategy.short, when=emaCrossUnder)
strategy.close("Short", when=emaCrossOver)

// 9 EMA and 13 EMA
ema9 = ema(close, 9)
ema13 = ema(close, 13)

// Exit short position when 9 EMA crosses over 13 EMA
emaCrossOver9_13 = crossover(ema9, ema13)
strategy.close("Short", when=emaCrossOver9_13)
```

## How the Strategy Works

1. **Input Parameters**: The user can customize the lengths of the short and long EMAs using the `emaLengthShort` and `emaLengthLong` input parameters.

2. **Calculate EMAs**: The script calculates the short and long EMAs based on the closing prices.

3. **Plot EMAs**: The script plots the short and long EMAs on the chart for visual reference.

4. **Strategy Conditions**: It defines two main strategy conditions:
   - `emaCrossUnder`: This condition triggers a short position when the short EMA crosses under the long EMA.
   - `emaCrossOver`: This condition exits the short position when the short EMA crosses over the long EMA.

5. **Additional EMAs**: The script calculates two more EMAs with periods of 9 and 13.

6. **Exit Short Position**: It includes an exit condition for the short position when the 9 EMA crosses over the 13 EMA.

## How to Use

1. Open TradingView and create a new Pine Script strategy.

2. Copy and paste the provided code into the Pine Script editor.

3. Customize the EMA lengths and other parameters according to your trading preferences.

4. Apply the strategy to your chart.

5. Backtest and analyze the strategy's performance or use it for real-time trading.

Please note that this strategy is for educational and demonstration purposes only. Trading involves risks, and it's important to thoroughly test and understand any strategy before using it in a live trading environment.
