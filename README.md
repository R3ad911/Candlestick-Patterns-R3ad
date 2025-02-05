# Candlestick Patterns R3ad

## Introduction
The **Candlestick Patterns R3ad** indicator is a technical analysis tool designed for **TradingView**. It automatically detects some of the most popular candlestick patterns used in trading, helping traders make informed decisions based on chart patterns.

## Features
- Automatically detects candlestick patterns on the chart.
- Colors candles based on their pattern for enhanced visualization.
- Adds visual signals above or below candles for easy identification.
- Works on all timeframes and markets supported by TradingView.

## Supported Patterns
### 1. **Doji Candle**
- Characterized by a very small body compared to the total range of the candle.
- Indicates market indecision.


### 2. **Hammer Candle**
- Forms when the lower wick is at least twice the size of the body.
- Suggests a potential bullish reversal when found at the bottom of a downtrend.


### 3. **Inverted Hammer Candle**
- Features a long upper wick, a small body, and a very short lower wick.
- Indicates a possible bullish reversal when appearing at the bottom of a downtrend.

### 4. **Shooting Star Candle**
- Characterized by a long upper wick, a small body, and a close lower than the open.
- Suggests a bearish reversal when found at the top of an uptrend.


### 5. **Bullish Engulfing Candle**
- Forms when a bullish candle opens within the body of the previous bearish candle but closes above its high.
- Indicates a strong potential for an upward reversal.


### 6. **Bearish Engulfing Candle**
- Forms when a bearish candle opens within the body of the previous bullish candle but closes below its low.
- Signals a strong potential for a downward reversal.

## Pine Script Code
```pinescript
//@version=5
indicator("Candlestick Patterns R3ad", overlay=true)

// Copyright: https://github.com/R3ad911

// Calculate body size and shadows
bodySize = math.abs(close - open)
candleRange = high - low
upperShadow = high - math.max(open, close)
lowerShadow = math.min(open, close) - low

// Define Doji candlestick
isDoji = bodySize < (candleRange * 0.1)

// Define Hammer & Inverted Hammer candlesticks
isHammer = lowerShadow > (bodySize * 2) and upperShadow < (bodySize * 0.5)
isInvertedHammer = upperShadow > (bodySize * 2) and lowerShadow < (bodySize * 0.5)

// Define Shooting Star candlestick
isShootingStar = upperShadow > (bodySize * 2) and lowerShadow < (bodySize * 0.5) and close < open

// Define Engulfing candlesticks (Bullish and Bearish)
isBullishEngulfing = close > open and close > open[1] and open < close[1]
isBearishEngulfing = close < open and close < open[1] and open > close[1]

// Candle coloring
barcolor(isDoji ? color.blue : na)
barcolor(isHammer ? color.green : na)
barcolor(isInvertedHammer ? color.orange : na)
barcolor(isShootingStar ? color.red : na)
barcolor(isBullishEngulfing ? color.lime : na)
barcolor(isBearishEngulfing ? color.maroon : na)

// Add signals above and below the candlesticks
plotshape(isDoji, location=location.abovebar, color=color.blue, style=shape.cross, title="Doji")
plotshape(isHammer, location=location.belowbar, color=color.green, style=shape.triangleup, title="Hammer")
plotshape(isInvertedHammer, location=location.abovebar, color=color.orange, style=shape.triangledown, title="Inverted Hammer")
plotshape(isShootingStar, location=location.abovebar, color=color.red, style=shape.triangledown, title="Shooting Star")
plotshape(isBullishEngulfing, location=location.belowbar, color=color.lime, style=shape.arrowup, title="Bullish Engulfing")
plotshape(isBearishEngulfing, location=location.abovebar, color=color.maroon, style=shape.arrowdown, title="Bearish Engulfing")
```

## How to Use the Indicator
1. **Adding the Indicator to TradingView:**
   - Copy the script from the `candlestick_patterns_r3ad.pine` file.
   - Open TradingView and navigate to the Pine Script editor.
   - Paste the script, click "Save," and then "Add to Chart."

2. **Reading the Signals:**
   - Candles are automatically colored based on the detected pattern.
   - Visual markers appear above or below candles for quick identification.

## License & Credits
- Developed by [R3ad911](https://github.com/R3ad911)
## Contributions
If you want to improve the indicator or add new features, feel free to open a Pull Request on the [GitHub Repository](https://github.com/R3ad911).

