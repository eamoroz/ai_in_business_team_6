# Team 6 - Crypto Trading Strategy

## 👥 Members
- Милицына Полина
- Мороз Екатерина
- Соболева Татьяна

## 🧠 Strategy Overview

### Core Logic
Our strategy follows a conservative trend-following approach with news confirmation.
1. **Entry Condition (Buy):** When all of the following conditions are met:
   - Short-term moving average is above medium-term moving average: ma7 > ma20
   - RSI is in a neutral zone: 40 <= RSI <= 60
   - News sentiment is strongly positive: POSITIVE and sentiment_score > 0.8
2. **Exit Condition (Sell):** When any of the following risk signals appears:
   - Stop-loss: price drops more than 4%: change ≥ +7%
   - Take-profit: price increases more than 7%: change ≥ +7%
   - Trend reversal: ma7 < ma20
   - RSI becomes overbought: RSI > 70
   - Strong negative news: NEGATIVE and sentiment_score > 0.75

### Decision Flowchart (Mermaid)
```mermaid
graph TD
    Start[Market Data Input] --> InPosition{Currently Holding?}

    InPosition -->|No| EntryCheck{Uptrend AND RSI 40-60 AND Positive News?}
    EntryCheck -->|Yes| Buy[BUY] 
    EntryCheck -->|No| Sell1[SELL (Stay in Cash)]

    InPosition -->|Yes| ExitCheck{StopLoss OR TakeProfit OR TrendReversal OR RSI>70 OR Negative News?}
    ExitCheck -->|Yes| Sell2[SELL]
    ExitCheck -->|No| BuyHold[BUY (Keep Position)]
```

### Performance Analysis
*   **Sharpe Ratio:** **3.13**
*   Total Return: 2.31%
*   Max Drawdown: 0.00%

**Strengths:**
*   Strong risk management through several exit conditions
*   Consistent equity growth without large volatility

**Limitations & Learnings:**
*   Low trade frequency due to strict entry filters
*   Performance depends heavily on trend presence
*   Strategy may underperform in sideways markets
