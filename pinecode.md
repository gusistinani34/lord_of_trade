// lord_of_trade

// bear


indicator("Harami - Bearish", shorttitle = "Harami - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_HaramiBearishNumberOfCandles = 2
C_HaramiBearish = C_LongBody[1] and C_WhiteBody[1] and C_UpTrend[1] and C_BlackBody and C_SmallBody and high <= C_BodyHi[1] and low >= C_BodyLo[1]
alertcondition(C_HaramiBearish, title = "New pattern detected", message = "New Harami – Bearish pattern detected")
if C_HaramiBearish
    var ttBearishHarami = "Harami\nThis is a two-day candlestick pattern with a small, red-bodied candle that is entirely encompassed within the body that was once a green-bodied candle."
    label.new(bar_index, patternLabelPosHigh, text="BH", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishHarami)
bgcolor(ta.highest(C_HaramiBearish?1:0, C_HaramiBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_HaramiBearishNumberOfCandles-1))




indicator("On Neck - Bearish", shorttitle = "On Neck - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_OnNeckBearishNumberOfCandles = 2
C_OnNeckBearish = false
if C_DownTrend and C_BlackBody[1] and C_LongBody[1] and C_WhiteBody and open < close[1] and C_SmallBody and C_Range!=0 and math.abs(close-low[1])<=C_BodyAvg*0.05
	C_OnNeckBearish := true
alertcondition(C_OnNeckBearish, title = "New pattern detected", message = "New On Neck – Bearish pattern detected")
if C_OnNeckBearish
    var ttBearishOnNeck = "On Neck\nOn Neck is a two-line continuation pattern found in a downtrend. The first candle is long and red, the second candle is short and has a green body. The closing price of the second candle is close or equal to the first candle's low price. The pattern hints at a continuation of a downtrend, and penetrating the low of the green candlestick is sometimes considered a confirmation. "
    label.new(bar_index, patternLabelPosHigh, text="ON", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishOnNeck)
bgcolor(ta.highest(C_OnNeckBearish?1:0, C_OnNeckBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_OnNeckBearishNumberOfCandles-1))


indicator("Kicking - Bearish", shorttitle = "Kicking - Bear", overlay=true)
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_KickingBearishNumberOfCandles = 2
C_MarubozuBullishShadowPercent = 5.0
C_MarubozuBearishKicking = C_LongBody and C_UpShadow <= C_MarubozuBullishShadowPercent/100*C_Body and C_DnShadow <= C_MarubozuBullishShadowPercent/100*C_Body
C_MarubozuWhiteBearish = C_MarubozuBearishKicking and C_WhiteBody
C_MarubozuBlackBearishKicking = C_MarubozuBearishKicking and C_BlackBody
C_KickingBearish = C_MarubozuWhiteBearish[1] and C_MarubozuBlackBearishKicking and low[1] > high
alertcondition(C_KickingBearish, title = "New pattern detected", message = "New Kicking – Bearish pattern detected")
if C_KickingBearish
    var ttBearishKicking = "Kicking\nA bearish kicking pattern will occur, subsequently signaling a reversal for a new downtrend. The first day candlestick is a bullish marubozu. The second day gaps down extensively and opens below the opening price of the day before. There is a gap between day one and two’s bearish candlesticks."
    label.new(bar_index, patternLabelPosHigh, text="K", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishKicking)
bgcolor(ta.highest(C_KickingBearish?1:0, C_KickingBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_KickingBearishNumberOfCandles-1))



indicator("Tri-Star - Bearish", shorttitle = "Tri-Star - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_TriStarBearishNumberOfCandles = 3
C_3Dojis = C_Doji[2] and C_Doji[1] and C_Doji
C_BodyGapUp = C_BodyHi[1] < C_BodyLo
C_BodyGapDn = C_BodyLo[1] > C_BodyHi
C_TriStarBearish = C_3Dojis and C_UpTrend[2] and C_BodyGapUp[1] and C_BodyGapDn
alertcondition(C_TriStarBearish, title = "New pattern detected", message = "New Tri-Star – Bearish pattern detected")
if C_TriStarBearish
    var ttBearishTriStar = "Tri-Star\nThis particular pattern can form when three doji candlesticks appear in immediate succession at the end of an extended uptrend. The first doji candle marks indecision between bull and bear. The second doji gaps in the direction of the leading trend. The third changes the attitude of the market once the candlestick opens in the direction opposite to the trend. Each doji candle has a shadow, all comparatively shallow, which signify an interim cutback in volatility."
    label.new(bar_index, patternLabelPosHigh, text="3S", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishTriStar)
bgcolor(ta.highest(C_TriStarBearish?1:0, C_TriStarBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_TriStarBearishNumberOfCandles-1))



indicator("Doji Star - Bearish", shorttitle = "Doji Star - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_DojiStarBearishNumberOfCandles = 2
C_DojiStarBearish = false
if C_UpTrend and C_WhiteBody[1] and C_LongBody[1] and C_IsDojiBody and C_BodyLo > C_BodyHi[1]
	C_DojiStarBearish := true
alertcondition(C_DojiStarBearish, title = "New pattern detected", message = "New Doji Star – Bearish pattern detected")
if C_DojiStarBearish
    var ttBearishDojiStar = "Doji Star\nThis is a bearish reversal candlestick pattern that is found in an uptrend and consists of two candles. First comes a long green candle, followed by a Doji candle (except 4-Price Doji) that opens above the body of the first one, creating a gap. It is considered a reversal signal with confirmation during the next trading day."
    label.new(bar_index, patternLabelPosHigh, text="DS", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishDojiStar)
bgcolor(ta.highest(C_DojiStarBearish?1:0, C_DojiStarBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_DojiStarBearishNumberOfCandles-1))



indicator("Engulfing - Bearish", shorttitle = "Engulfing - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_EngulfingBearishNumberOfCandles = 2
C_EngulfingBearish = C_UpTrend and C_BlackBody and C_LongBody and C_WhiteBody[1] and C_SmallBody[1] and close <= open[1] and open >= close[1] and ( close < open[1] or open > close[1] )
alertcondition(C_EngulfingBearish, title = "New pattern detected", message = "New Engulfing – Bearish pattern detected")
if C_EngulfingBearish
    var ttBearishEngulfing = "Engulfing\nAt the end of a given uptrend, a reversal pattern will most likely appear. During the first day, this candlestick pattern uses a small body. It is then followed by a day where the candle body fully overtakes the body from the day before it and closes in the trend’s opposite direction. Although similar to the outside reversal chart pattern, it is not essential for this pattern to fully overtake the range (high to low), rather only the open and the close."
    label.new(bar_index, patternLabelPosHigh, text="BE", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishEngulfing)
bgcolor(ta.highest(C_EngulfingBearish?1:0, C_EngulfingBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_EngulfingBearishNumberOfCandles-1))


indicator("Hanging Man - Bearish", shorttitle = "Hanging Man - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_HangingManBearishNumberOfCandles = 1
C_HangingManBearish = false
if C_SmallBody and C_Body > 0 and C_BodyLo > hl2 and C_DnShadow >= C_Factor * C_Body and not C_HasUpShadow
	if C_UpTrend
	    C_HangingManBearish := true
alertcondition(C_HangingManBearish, title = "New pattern detected", message = "New Hanging Man – Bearish pattern detected")
if C_HangingManBearish
    var ttBearishHangingMan = "Hanging Man\nWhen a specified security notably moves lower after the open, but continues to rally to close above the intraday low, a Hanging Man candlestick will form. The candlestick will resemble a square, attached to a long stick-like figure. It is referred to as a Hanging Man if the candlestick forms during an advance."
    label.new(bar_index, patternLabelPosHigh, text="HM", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishHangingMan)
bgcolor(ta.highest(C_HangingManBearish?1:0, C_HangingManBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_HangingManBearishNumberOfCandles-1))



indicator("Tweezer Top - Bearish", shorttitle = "Tweezer Top - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_TweezerTopBearishNumberOfCandles = 2
C_TweezerTopBearish = false
if C_UpTrend[1] and (not C_IsDojiBody or (C_HasUpShadow and C_HasDnShadow)) and math.abs(high-high[1]) <= C_BodyAvg*0.05 and C_WhiteBody[1] and C_BlackBody and C_LongBody[1]
	C_TweezerTopBearish := true
alertcondition(C_TweezerTopBearish, title = "New pattern detected", message = "New Tweezer Top – Bearish pattern detected")
if C_TweezerTopBearish
    var ttBearishTweezerTop = "Tweezer Top\nTweezer Top is a two-candle pattern that signifies a potential bearish reversal. The pattern is found during an uptrend. The first candle is long and green, the second candle is red, and its high is nearly identical to the high of the previous candle. The virtually identical highs, together with the inverted directions, hint that bears might be taking over the market."
    label.new(bar_index, patternLabelPosHigh, text="TT", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishTweezerTop)
bgcolor(ta.highest(C_TweezerTopBearish?1:0, C_TweezerTopBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_TweezerTopBearishNumberOfCandles-1))



indicator("Evening Star - Bearish", shorttitle = "Evening Star - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_EveningStarBearishNumberOfCandles = 3
C_EveningStarBearish = false
if C_LongBody[2] and C_SmallBody[1] and C_LongBody
    if C_UpTrend and C_WhiteBody[2] and C_BodyLo[1] > C_BodyHi[2] and C_BlackBody and C_BodyLo <= C_BodyMiddle[2] and C_BodyLo > C_BodyLo[2] and C_BodyLo[1] > C_BodyHi
        C_EveningStarBearish := true
alertcondition(C_EveningStarBearish, title = "New pattern detected", message = "New Evening Star – Bearish pattern detected")
if C_EveningStarBearish
    var ttBearishEveningStar = "Evening Star\nThis candlestick pattern is bearish and continues an uptrend with a long-bodied, green candle day. It is then followed by a gapped and small-bodied candle day, and concludes with a downward close. The close would be below the first day’s midpoint."
    label.new(bar_index, patternLabelPosHigh, text="ES", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishEveningStar)
bgcolor(ta.highest(C_EveningStarBearish?1:0, C_EveningStarBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_EveningStarBearishNumberOfCandles-1))


indicator("Harami Cross - Bearish", shorttitle = "Harami Cross - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_HaramiCrossBearishNumberOfCandles = 2
C_HaramiCrossBearish = C_LongBody[1] and C_WhiteBody[1] and C_UpTrend[1] and C_IsDojiBody and high <= C_BodyHi[1] and low >= C_BodyLo[1]
alertcondition(C_HaramiCrossBearish, title = "New pattern detected", message = "New Harami Cross – Bearish pattern detected")
if C_HaramiCrossBearish
    var ttBearishHaramiCross = "Harami Cross\nThis candlestick pattern is a variation of the Harami Bearish pattern. It is found during an uptrend. This is a two-day candlestick pattern with a Doji candle that is entirely encompassed within the body that was once a green-bodied candle. The Doji shows that some indecision has entered the minds of sellers, and the pattern hints that the trend might reverse."
    label.new(bar_index, patternLabelPosHigh, text="HC", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishHaramiCross)
bgcolor(ta.highest(C_HaramiCrossBearish?1:0, C_HaramiCrossBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_HaramiCrossBearishNumberOfCandles-1))


indicator("Shooting Star - Bearish", shorttitle = "Shooting Star - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_ShootingStarBearishNumberOfCandles = 1
C_ShootingStarBearish = false
if C_SmallBody and C_Body > 0 and C_BodyHi < hl2 and C_UpShadow >= C_Factor * C_Body and not C_HasDnShadow
	if C_UpTrend
	    C_ShootingStarBearish := true
alertcondition(C_ShootingStarBearish, title = "New pattern detected", message = "New Shooting Star – Bearish pattern detected")
if C_ShootingStarBearish
    var ttBearishShootingStar = "Shooting Star\nThis single day pattern can appear during an uptrend and opens high, while it closes near its open. It trades much higher as well. It is bearish in nature, but looks like an Inverted Hammer."
    label.new(bar_index, patternLabelPosHigh, text="SS", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishShootingStar)
bgcolor(ta.highest(C_ShootingStarBearish?1:0, C_ShootingStarBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_ShootingStarBearishNumberOfCandles-1))



indicator("Falling Window - Bearish", shorttitle = "Falling Window - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_FallingWindowBearishNumberOfCandles = 2
C_FallingWindowBearish = false
if C_DownTrend[1] and (C_Range!=0 and C_Range[1]!=0) and high < low[1]
	C_FallingWindowBearish := true
alertcondition(C_FallingWindowBearish, title = "New pattern detected", message = "New Falling Window – Bearish pattern detected")
if C_FallingWindowBearish
    var ttBearishFallingWindow = "Falling Window\nFalling Window is a two-candle bearish continuation pattern that forms during a downtrend. Both candles in the pattern can be of any type, with the exception of the Four-Price Doji. The most important characteristic of the pattern is a price gap between the first candle's low and the second candle's high. The existence of this gap (window) means that the bearish trend is expected to continue."
    label.new(bar_index, patternLabelPosHigh, text="FW", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishFallingWindow)
bgcolor(ta.highest(C_FallingWindowBearish?1:0, C_FallingWindowBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_FallingWindowBearishNumberOfCandles-1))



indicator("Marubozu Black - Bearish", shorttitle = "Marubozu Black - Bear", overlay=true)
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_MarubozuBlackBearishNumberOfCandles = 1
C_MarubozuShadowPercentBearish = 5.0
C_MarubozuBlackBearish = C_BlackBody and C_LongBody and C_UpShadow <= C_MarubozuShadowPercentBearish/100*C_Body and C_DnShadow <= C_MarubozuShadowPercentBearish/100*C_Body and C_BlackBody
alertcondition(C_MarubozuBlackBearish, title = "New pattern detected", message = "New Marubozu Black – Bearish pattern detected")
if C_MarubozuBlackBearish
    var ttBearishMarubozuBlack = "Marubozu Black\nThis is a candlestick that has no shadow, which extends from the red-bodied candle at the open, the close, or even at both. In Japanese, the name means “close-cropped” or “close-cut.” The candlestick can also be referred to as Bald or Shaven Head."
    label.new(bar_index, patternLabelPosHigh, text="MB", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishMarubozuBlack)
bgcolor(ta.highest(C_MarubozuBlackBearish?1:0, C_MarubozuBlackBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_MarubozuBlackBearishNumberOfCandles-1))


indicator("Abandoned Baby - Bearish", shorttitle = "Abandoned Baby - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_AbandonedBabyBearishNumberOfCandles = 3
C_AbandonedBabyBearish = C_UpTrend[2] and C_WhiteBody[2] and C_IsDojiBody[1] and high[2] < low[1] and C_BlackBody and low[1] > high
alertcondition(C_AbandonedBabyBearish, title = "New pattern detected", message = "New Abandoned Baby – Bearish pattern detected")
if C_AbandonedBabyBearish
    var ttBearishAbandonedBaby = "Abandoned Baby\nA bearish abandoned baby is a specific candlestick pattern that often signals a downward reversal trend in terms of security price. It is formed when a gap appears between the lowest price of a doji-like candle and the candlestick of the day before. The earlier candlestick is green, tall, and has small shadows. The doji candle is also tailed by a gap between its lowest price point and the highest price point of the candle that comes next, which is red, tall and also has small shadows. The doji candle shadows must completely gap either below or above the shadows of the first and third day in order to have the abandoned baby pattern effect."
    label.new(bar_index, patternLabelPosHigh, text="AB", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishAbandonedBaby)
bgcolor(ta.highest(C_AbandonedBabyBearish?1:0, C_AbandonedBabyBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_AbandonedBabyBearishNumberOfCandles-1))

indicator("Gravestone Doji - Bearish", shorttitle = "Gravestone Doji - Bear", overlay=true)
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_GravestoneDojiBearishNumberOfCandles = 1
C_GravestoneDojiBearish = C_IsDojiBody and C_DnShadow <= C_Body
alertcondition(C_GravestoneDojiBearish, title = "New pattern detected", message = "New Gravestone Doji – Bearish pattern detected")
if C_GravestoneDojiBearish
    var ttBearishGravestoneDoji = "Gravestone Doji\nWhen a doji is at or is close to the day’s low point, a doji line will develop."
    label.new(bar_index, patternLabelPosHigh, text="GD", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishGravestoneDoji)
bgcolor(ta.highest(C_GravestoneDojiBearish?1:0, C_GravestoneDojiBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_GravestoneDojiBearishNumberOfCandles-1))


indicator("Dark Cloud Cover - Bearish", shorttitle = "Dark Cloud Cover - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_DarkCloudCoverBearishNumberOfCandles = 2
C_DarkCloudCoverBearish = false
if (C_UpTrend[1] and C_WhiteBody[1] and C_LongBody[1]) and (C_BlackBody and open >= high[1] and  close < C_BodyMiddle[1] and close > open[1])
	C_DarkCloudCoverBearish := true
alertcondition(C_DarkCloudCoverBearish, title = "New pattern detected", message = "New Dark Cloud Cover – Bearish pattern detected")
if C_DarkCloudCoverBearish
    var ttBearishDarkCloudCover = "Dark Cloud Cover\nDark Cloud Cover is a two-candle bearish reversal candlestick pattern found in an uptrend. The first candle is green and has a larger than average body. The second candle is red and opens above the high of the prior candle, creating a gap, and then closes below the midpoint of the first candle. The pattern shows a possible shift in the momentum from the upside to the downside, indicating that a reversal might happen soon."
    label.new(bar_index, patternLabelPosHigh, text="DCC", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishDarkCloudCover)
bgcolor(ta.highest(C_DarkCloudCoverBearish?1:0, C_DarkCloudCoverBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_DarkCloudCoverBearishNumberOfCandles-1))

indicator("Evening Doji Star - Bearish", shorttitle = "Evening Doji Star - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_EveningDojiStarBearishNumberOfCandles = 3
C_EveningDojiStarBearish = false
if C_LongBody[2] and C_IsDojiBody[1] and C_LongBody and C_UpTrend and C_WhiteBody[2] and C_BodyLo[1] > C_BodyHi[2] and C_BlackBody and C_BodyLo <= C_BodyMiddle[2] and C_BodyLo > C_BodyLo[2] and C_BodyLo[1] > C_BodyHi
	C_EveningDojiStarBearish := true
alertcondition(C_EveningDojiStarBearish, title = "New pattern detected", message = "New Evening Doji Star – Bearish pattern detected")
if C_EveningDojiStarBearish
    var ttBearishEveningDojiStar = "Evening Doji Star\nThis candlestick pattern is a variation of the Evening Star pattern. It is bearish and continues an uptrend with a long-bodied, green candle day. It is then followed by a gap and a Doji candle and concludes with a downward close. The close would be below the first day’s midpoint. It is more bearish than the regular evening star pattern because of the existence of the Doji."
    label.new(bar_index, patternLabelPosHigh, text="EDS", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishEveningDojiStar)
bgcolor(ta.highest(C_EveningDojiStarBearish?1:0, C_EveningDojiStarBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_EveningDojiStarBearishNumberOfCandles-1))
indicator("Long Upper Shadow - Bearish", shorttitle = "Long Upper Shadow - Bear", overlay=true)
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_LongUpperShadowBearishNumberOfCandles = 1
C_LongShadowPercent = 75.0
C_LongUpperShadowBearish = C_UpShadow > C_Range/100*C_LongShadowPercent
alertcondition(C_LongUpperShadowBearish, title = "New pattern detected", message = "New Long Upper Shadow – Bearish pattern detected")
if C_LongUpperShadowBearish
    var ttBearishLongUpperShadow = "Long Upper Shadow\nTo indicate buyer domination of the first part of a session, candlesticks will present with long upper shadows, as well as short lower shadows, consequently raising bidding prices."
    label.new(bar_index, patternLabelPosHigh, text="LUS", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishLongUpperShadow)
bgcolor(ta.highest(C_LongUpperShadowBearish?1:0, C_LongUpperShadowBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_LongUpperShadowBearishNumberOfCandles-1))

indicator("Three Black Crows - Bearish", shorttitle = "Three Black Crows - Bear", overlay=true)
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_ThreeBlackCrowsBearishNumberOfCandles = 3
C_3BCrw_ShadowPercent = 5.0
C_3BCrw_HaveNotDnShadow = C_Range * C_3BCrw_ShadowPercent / 100 > C_DnShadow
C_ThreeBlackCrowsBearish = false
if C_LongBody and C_LongBody[1] and C_LongBody[2]
    if C_BlackBody and C_BlackBody[1] and C_BlackBody[2]
        C_ThreeBlackCrowsBearish := close < close[1] and close[1] < close[2] and open > close[1] and open < open[1] and open[1] > close[2] and open[1] < open[2] and C_3BCrw_HaveNotDnShadow and C_3BCrw_HaveNotDnShadow[1] and C_3BCrw_HaveNotDnShadow[2]
alertcondition(C_ThreeBlackCrowsBearish, title = "New pattern detected", message = "New Three Black Crows – Bearish pattern detected")
if C_ThreeBlackCrowsBearish
    var ttBearishThreeBlackCrows = "Three Black Crows\nThis is a bearish reversal pattern that consists of three long, red-bodied candles in immediate succession. For each of these candles, each day opens within the body of the day before and closes either at or near its low."
    label.new(bar_index, patternLabelPosHigh, text="3BC", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishThreeBlackCrows)
bgcolor(ta.highest(C_ThreeBlackCrowsBearish?1:0, C_ThreeBlackCrowsBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_ThreeBlackCrowsBearishNumberOfCandles-1))

indicator("Downside Tasuki Gap - Bearish", shorttitle = "Downside Tasuki Gap - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_DownsideTasukiGapBearishNumberOfCandles = 3
C_DownsideTasukiGapBearish = false
if C_LongBody[2] and C_SmallBody[1] and C_DownTrend and C_BlackBody[2] and C_BodyHi[1] < C_BodyLo[2] and C_BlackBody[1] and C_WhiteBody and C_BodyHi <= C_BodyLo[2] and C_BodyHi >= C_BodyHi[1]
	C_DownsideTasukiGapBearish := true
alertcondition(C_DownsideTasukiGapBearish, title = "New pattern detected", message = "New Downside Tasuki Gap – Bearish pattern detected")
if C_DownsideTasukiGapBearish
    var ttBearishDownsideTasukiGap = "Downside Tasuki Gap\nDownside Tasuki Gap is a three-candle pattern found in a downtrend that usually hints at the continuation of the downtrend. The first candle is long and red, followed by a smaller red candle with its opening price that gaps below the body of the previous candle. The third candle is green and it closes inside the gap created by the first two candles, unable to close it fully. The bull’s inability to close that gap hints that the downtrend might continue."
    label.new(bar_index, patternLabelPosHigh, text="DTG", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishDownsideTasukiGap)
bgcolor(ta.highest(C_DownsideTasukiGapBearish?1:0, C_DownsideTasukiGapBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_DownsideTasukiGapBearishNumberOfCandles-1))

indicator("Downside Tasuki Gap - Bearish", shorttitle = "Downside Tasuki Gap - Bear", overlay=true)

C_DownTrend = true
C_UpTrend = true
var trendRule1 = "SMA50"
var trendRule2 = "SMA50, SMA200"
var trendRule = input.string(trendRule1, "Detect Trend Based On", options=[trendRule1, trendRule2, "No detection"])

if trendRule == trendRule1
	priceAvg = ta.sma(close, 50)
	C_DownTrend := close < priceAvg
	C_UpTrend := close > priceAvg

if trendRule == trendRule2
	sma200 = ta.sma(close, 200)
	sma50 = ta.sma(close, 50)
	C_DownTrend := close < sma50 and sma50 < sma200
	C_UpTrend := close > sma50 and sma50 > sma200
C_Len = 14 // ta.ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = math.max(close, open)
C_BodyLo = math.min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ta.ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (math.abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (math.abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (ta.atr(30) * 0.6)
patternLabelPosHigh = high + (ta.atr(30) * 0.6)

label_color_bearish = input(color.red, "Label Color Bearish")
C_DownsideTasukiGapBearishNumberOfCandles = 3
C_DownsideTasukiGapBearish = false
if C_LongBody[2] and C_SmallBody[1] and C_DownTrend and C_BlackBody[2] and C_BodyHi[1] < C_BodyLo[2] and C_BlackBody[1] and C_WhiteBody and C_BodyHi <= C_BodyLo[2] and C_BodyHi >= C_BodyHi[1]
	C_DownsideTasukiGapBearish := true
alertcondition(C_DownsideTasukiGapBearish, title = "New pattern detected", message = "New Downside Tasuki Gap – Bearish pattern detected")
if C_DownsideTasukiGapBearish
    var ttBearishDownsideTasukiGap = "Downside Tasuki Gap\nDownside Tasuki Gap is a three-candle pattern found in a downtrend that usually hints at the continuation of the downtrend. The first candle is long and red, followed by a smaller red candle with its opening price that gaps below the body of the previous candle. The third candle is green and it closes inside the gap created by the first two candles, unable to close it fully. The bull’s inability to close that gap hints that the downtrend might continue."
    label.new(bar_index, patternLabelPosHigh, text="DTG", style=label.style_label_down, color = label_color_bearish, textcolor=color.white, tooltip = ttBearishDownsideTasukiGap)
bgcolor(ta.highest(C_DownsideTasukiGapBearish?1:0, C_DownsideTasukiGapBearishNumberOfCandles)!=0 ? color.new(color.red, 90) : na, offset=-(C_DownsideTasukiGapBearishNumberOfCandles-1))
