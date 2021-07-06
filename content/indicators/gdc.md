---
title: "Two Moving Averages and Golden and Death Cross"
date: 2021-07-05T17:41:48-05:00
draft: false
ShowToc: true
categories: ["pine scripts", "tradingview"]
tags: ["moving-averages"]
---

## Two Moving Averages and Golden/Death Crosses
![Golden and Death Cross](/posts/pine/gdc/gcdc.png#center)

A moving-average crossover occurs when, on plotting two moving averages each based on different degrees of smoothing, the traces of these moving averages cross. It does not predict future direction but shows trends. This indicator uses two moving averages, a slower moving average and a faster moving average. The faster moving average is a short term moving average. 

The 2MA Cross indicator provides 2 plotted moving averages of types EMA, SMA, RMA, WMA and VWMA. This also provides golden and death cross plot points and a wide variety of customization options.

The golden cross is a chart pattern that is a bullish signal in which a relatively short-term moving average crosses above a long-term moving average. The golden cross is a bullish breakout pattern formed from a crossover involving a security's short-term moving average (such as the 15-day moving average) breaking above its long-term moving average (such as the 50-day moving average) or resistance level. As long-term indicators carry more weight, the golden cross indicates a bull market on the horizon and is reinforced by high trading volumes. 

The death cross is a technical chart pattern indicating the potential for a major sell-off. The death cross appears on a chart when a stock’s short-term moving average crosses below its long-term moving average. Typically, the most common moving averages used in this pattern are the 50-day and 200-day moving averages.

#### Key Points
- Plots two moving averages, a *short-term moving average* and a *long-term moving average*.
  - Each moving average time frame can be changed by the user.
- Plots a symbol for the *golden cross pattern*.
  - Occurs when a *short-term moving average* crosses **above** the *long-term moving average*.
- Plots a symbol for the *death cross pattern*.
  - Occurs when a *short-term moving average* crosses **below** the *long-term moving average*.

#### Pine Script
{{< highlight tv >}}
// © Pirate
//@version=4
study(title="[Pirate] 2 Moving Averages and Cross", shorttitle="2MA Cross", overlay=true)

//-------------------------------------//
//----------Default Variables----------//
//-------------------------------------//
fColorD=color.new(#1c4670, 5) // Fast MA Color - Blue
sColorD=color.new(#1dc690, 5) // Slow MA Color - Neon Green
gcColorD=color.new(#1dc690, 5) // Golden Cross Color - Neon Green
dcColorD=color.new(#1c4670, 5) // Death Cross Color - Blue
gctColorD=color.new(#eaeae0, 0) // Golden Cross Text Color - Ivory
dctColorD=color.new(#eaeae0, 0) // Death Cross Text Color - Ivory
noColor=color.new(#ffffff, 100) // No Color

//---------------------------------------------//
//----------Configurable Menu Options----------//
//---------------------------------------------//
oSource=input(title="Source:", type=input.source, defval=close) // Source
// Moving Average Type
oMA = input(title="Moving Average Type:", defval="Exponential", options=[
     "Exponential",
     "Simple",
     "Running",
     "Weighted",
     "Volume-Weighted"])
dFast=input(title="[Enable/Disable] Fast MA",type=input.bool, defval=true) // Enable/Disable Fast MA
dSlow=input(title="[Enable/Disable] Slow MA", type=input.bool, defval=true) // Enable/Disable Slow MA
fPeriod=input(title="Fast MA Period:", type=input.integer, defval=50) // Fast MA Time
sPeriod=input(title="Slow MA Period:", type=input.integer, defval=200) // Slow MA Time
fColor=input(title="Fast MA Color:", type=input.color, defval=fColorD) // Fast MA Color
sColor=input(title="Slow MA Color:", type=input.color, defval=sColorD) // Slow MA Color
fWidth=input(title="Fast MA Line Width:", type=input.integer, defval=2, minval=1, maxval=4) // Fast MA LW
sWidth=input(title="Slow MA Line Width:", type=input.integer, defval=2, minval=1, maxval=4) // Slow MA LW
dGC=input(title="[Enable/Disable] Golden Cross",type=input.bool, defval=true) // Enable/Disable Golden Cross
dDC=input(title="[Enable/Disable] Death Cross", type=input.bool, defval=true) // Enable/Disable Death Cross
gcColor=input(title="Golden Cross Color:", type=input.color, defval=gcColorD) // Golden Cross Color
dcColor=input(title="Death Cross Color:", type=input.color, defval=dcColorD) // Death Cross Color
dCT=input(title="[Enable/Disable] Cross Text", type=input.bool, defval=true) // Enable/Disable Cross Text
gctColor=input(title="Golden Cross Text Color:", type=input.color, defval=gctColorD) // Golden Cross Text Color
dctColor=input(title="Death Cross Text Color:", type=input.color, defval=dctColorD) // Death Cross Text Color

//---------------DO NOT CHANGE---------------//
//-----------------Functions-----------------//
//---------------DO NOT CHANGE---------------//
// Fast Moving Average Variable
fMA=(oMA == "Exponential" ? ema(oSource, fPeriod) :
     oMA == "Simple" ? sma(oSource, fPeriod) :
     oMA == "Running" ? rma(oSource, fPeriod) :
     oMA == "Weighted" ? wma(oSource, fPeriod) :
     oMA == "Volume-Weighted" ? vwma(oSource, fPeriod) :
     na)
// Slow Moving Average Variable
sMA=(oMA == "Exponential" ? ema(oSource, sPeriod) :
     oMA == "Simple" ? sma(oSource, sPeriod) :
     oMA == "Running" ? rma(oSource, sPeriod) :
     oMA == "Weighted" ? wma(oSource, sPeriod) :
     oMA == "Volume-Weighted" ? vwma(oSource, sPeriod) :
     na)
gCross=crossover(fMA, sMA) // Golden Cross Variable
dCross=crossunder(fMA, sMA) // Death Cross Variable
// Plot Fast MA
plot(dFast ? fMA : na,
     title="Fast MA",
     linewidth=fWidth,
     color=fColor)
// Plot Slow MA
plot(dSlow ? sMA : na,
     title="Slow MA",
     linewidth=sWidth,
     color=sColor)
// Plot Golden Cross
plotshape(dGC ? gCross : na,
     title="Golden Cross",
     style=shape.triangleup,
     color=gcColor,
     location=location.belowbar,
     size=size.small,
     text="GC",
     textcolor=dCT ? gctColor : noColor)
// Plot Death Cross
plotshape(dDC ? dCross : na,
     title="Death Cross",
     style=shape.triangledown,
     color=dcColor,
     location=location.abovebar,
     size=size.small,
     text="DC",
     textcolor=dCT ? dctColor : noColor)
{{< / highlight >}}

#### More Information
> [More information about Golden/Death Crosses](https://www.investopedia.com/ask/answers/121114/what-difference-between-golden-cross-and-death-cross-pattern.asp)
> 
> [View this indicator on GitHub](https://github.com/PirateCrypto/TradingView/blob/main/Indicators/%5BPirate%5D%202MA%20Cross.pine)