---
title: "Highs and Lows (In-Progress)"
date: 2021-07-05T17:41:48-05:00
draft: false
ShowToc: true
categories: ["pine scripts", "tradingview"]
tags: ["pivot-points"]
---
## Highs and Lows (In-Progress)
![HL](/posts/pine/hl/hl.png#center)

Right now, this script only labels highs and lows based on fibonacci pivot points because it's not yet complete. I will be adding on to this and continuing development soon.

#### Key Points
- Coming soon

#### Pine Script
{{< highlight tv >}}
//----------------------------------------------------------------------------//
// © Pirate
//@version=4
study('[Pirate] Highs and Lows',
      shorttitle='HL',
      overlay=true,
      max_labels_count=500)
//----------------------------------------------------------------------------//
//
//
//----------------------------------------------------------------------------//
//----Defaults
//----------------------------------------------------------------------------//
//----Highs Group
hGroup='Highs'

//----Lows Group
lGroup='Lows'

//----Highs Color
hColorD=color.new(#3faac0, 0)

//----Lows Color
lColorD=color.new(#c0553f, 0)
//----------------------------------------------------------------------------//
//
//
//----------------------------------------------------------------------------//
//----Configurable Menu Options
//----------------------------------------------------------------------------//
//----Highs Strength
hStrength=input(title='[Strength]:',
      type=input.integer,
      defval=10,
      minval=1,
      group=hGroup)

//----Lows Strength
lStrength=input(title='[Strength]:',
      type=input.integer,
      defval=10,
      minval=1,
      group=lGroup)

//----Highs Color
hColor=input(title='[Color]:',
      type=input.color,
      defval=hColorD,
      group=hGroup)

//----Lows Color
lColor=input(title='[Color]:',
      defval=lColorD,
      group=lGroup)
//----------------------------------------------------------------------------//
//
//
//----------------------------------------------------------------------------//
//  Functions
//----------------------------------------------------------------------------//
//----High Pivot
hPiv=pivothigh(hStrength, hStrength)

//----Low Pivot
lPiv=pivotlow(lStrength, lStrength)

//----Draw Labels
drawLabel(_offset, _pivot, _style, _yloc, _color) =>
    if not na(_pivot)
        label.new(bar_index[_offset], _pivot, tostring(_pivot, format.mintick),
             style=_style, yloc=_yloc, color=_color, textcolor=#131722)

//----High Labels
hLabel=drawLabel(hStrength, hPiv, label.style_label_down, yloc.abovebar, hColor) 

//----Low Labels
lLabel=drawLabel(lStrength, lPiv, label.style_label_up, yloc.belowbar, lColor)
//----------------------------------------------------------------------------//
{{< / highlight >}}

#### More Information
> [More information about Highs and Lows](https://www.investopedia.com/terms/p/pivotpoint.asp)
>
> [View this indicator on GitHub](https://github.com/PirateCrypto/TradingView/blob/main/Indicators/%5BPirate%5D%20Highs%20and%20Lows.pine)
