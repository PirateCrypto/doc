---
title: "T3 Moving Average"
date: 2021-07-05T17:41:48-05:00
draft: false
ShowToc: true
categories: ["pine scripts", "tradingview"]
tags: ["moving-averages"]
---

## T3 Moving Average
![T3 Moving Average](/posts/pine/t3ma/t3ma.png#center)

The T3 MA incorporates a smoothing technique which allows it to plot curves more gradual than ordinary moving averages and with a smaller lag. Its smoothness is derived from the fact that it is a weighted sum of a single EMA , double EMA , triple EMA and so on. When a trend is formed, the price action will stay above or below the trend during most of its progression and will hardly be touched by any swings. Thus, a confirmed penetration of the T3 MA and the lack of a following reversal often indicates the end of a trend.

The T3 MA generally produces entry signals similar to other moving averages and thus is traded largely in the same manner. Here are several assumptions:

If the price action is above the T3 MA and the indicator is headed upward, then we have a bullish trend and should only enter long trades (advisable for novice/intermediate traders). If the price is below the T3 MA and it is edging lower, then we have a bearish trend and should limit entries to short. Below you can see it visualized in a trading platform.

#### Key Points
- Coming Soon

#### Pine Script
{{< highlight tv >}}
// © Pirate
//@version=4
study(title="[Pirate] T3 Moving Average",shorttitle="T3 MA",overlay=true)

//-------------------------------------//
//----------Default Variables----------//
//-------------------------------------//
l=input(title="Length",type=input.integer,minval=1,defval=5) // Length
a=input(title="Alpha",type=input.float,minval=0,maxval=1,defval=0.7) // Alpha
s=input(title="Source",type=input.source,defval=close) // Source
tColorD=color.new(#4b2a62,5)

//---------------------------------------------//
//----------Configurable Menu Options----------//
//---------------------------------------------//
sColor=input(title="T3 Color",type=input.color,defval=tColorD) // T3 Color
fWidth=input(title="T3 Line Width", type=input.integer, defval=2, minval=1, maxval=4) // T3 LW

//---------------DO NOT CHANGE---------------//
//-----------------Functions-----------------//
//---------------DO NOT CHANGE---------------//
gd(series,seriesLength,v)=>
    ema(series,seriesLength)*(1+a)-ema(ema(series,seriesLength),seriesLength)*a
t3(s,l,a)=>
    gd(gd(gd(s,l,a),l,a),l,a)
plot(t3(s,l,a),color=sColor, linewidth=fWidth)
{{< / highlight >}}

#### More Information
> [More information about T3 Moving Averages](https://www.tradingpedia.com/forex-trading-indicators/t3-moving-average-indicator/)
>
> [View this indicator on GitHub](https://github.com/PirateCrypto/TradingView/blob/main/Indicators/%5BPirate%5D%20T3%20MA.pine)