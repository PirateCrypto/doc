---
title: "Triple Exponential Moving Average (TEMA)"
date: 2021-07-05T17:41:48-05:00
draft: false
ShowToc: true
categories: ["pine scripts", "tradingview"]
tags: ["moving-averages"]
---

### Summary
The triple exponential moving average (TEMA) was designed to smooth price fluctuations, thereby making it easier to identify trends without the lag associated with traditional moving averages (MA). 

It does this by taking multiple exponential moving averages (EMA) of the original EMA and subtracting out some of the lag. The TEMA is used like other MAs. It can help identify trend direction, signal potential short-term trend changes or pullbacks, and provide support or resistance.

---

### Key Points
- Coming soon

---

### Preview
![TEMA](/pine/tema/tema.png)

---

### Pine Script
{{< highlight tv >}}
// © Pirate
//@version=4

study("[Pirate] Triple EMA", overlay=true)

//-------------------------------------//
//----------Default Variables----------//
//-------------------------------------//
fColorD=color.new(#1c4670, 5) // Fast EMA Color - Blue
mColorD=color.new(#4b2a62, 5) // Mid EMA Color - Soft Violet
sColorD=color.new(#1dc690, 5) // Slow EMA Color - Neon Green

//---------------------------------------------//
//----------Configurable Menu Options----------//
//---------------------------------------------//
oSource=input(title="Source", type=input.source, defval=close) // Source
dFast=input(title="Enable/Disable Fast EMA",type=input.bool, defval=true) // Enable/Disable Fast EMA
dMid=input(title="Enable/Disable Mid EMA",type=input.bool, defval=true) // Enable/Disable Mid EMA
dSlow=input(title="Enable/Disable Slow EMA", type=input.bool, defval=true) // Enable/Disable Slow EMA
fPeriod=input(title="Fast EMA Period", type=input.integer, defval=50) // Fast EMA Time
mPeriod=input(title="Mid EMA Period", type=input.integer, defval=100) // Slow EMA Time
sPeriod=input(title="Slow EMA Period", type=input.integer, defval=200) // Slow EMA Time
fColor=input(title="Fast EMA Color", type=input.color, defval=fColorD) // Fast EMA Color
mColor=input(title="Mid EMA Color", type=input.color, defval=mColorD) // Mid EMA Color
sColor=input(title="Slow EMA Color", type=input.color, defval=sColorD) // Slow EMA Color
fWidth=input(title="Fast EMA Line Width", type=input.integer, defval=2, minval=1, maxval=4) // Fast EMA LW
mWidth=input(title="Mid EMA Line Width", type=input.integer, defval=2, minval=1, maxval=4) // Mid EMA LW
sWidth=input(title="Slow EMA Line Width", type=input.integer, defval=2, minval=1, maxval=4) // Slow EMA LW


//---------------DO NOT CHANGE---------------//
//-----------------Functions-----------------//
//---------------DO NOT CHANGE---------------//
fEMA=ema(oSource, fPeriod) // Fast EMA Variable
mEMA=ema(oSource, mPeriod) // Mid EMA Variable
sEMA=ema(oSource, sPeriod) // Slow SEMA Variable
plot(dFast ? fEMA : na, linewidth=fWidth, color=fColor) // Plot Fast EMA
plot(dMid ? mEMA : na, linewidth=mWidth, color=mColor) // Plot Mid EMA
plot(dSlow ? sEMA : na, linewidth=sWidth, color=sColor) // Plot Slow EMA
{{< / highlight >}}

---

### More Information
> [More information about TEMAs](https://www.investopedia.com/terms/t/triple-exponential-moving-average.asp)
>
> [View this indicator on GitHub](https://github.com/PirateCrypto/TradingView/blob/main/Indicators/%5BPirate%5D%20Triple%20EMA.pine)

---