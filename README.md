# Team XX - Crypto Trading Strategy

## 👥 Members
- Lapko Daria Andreevna  
- Zaporozhets Anastasia Alexandrovna  
- Kuznetsov Vladimir Petrovich  
- Alektorov Gleb Konstantinovich 

## 🧠 Strategy Overview

Our strategy combines **news sentiment analysis with technical indicators (Trend Following + Risk Management).**

### Entry Condition (Buy)
- News Sentiment = POSITIVE and `sentiment_score > 0.5`  
- `RSI < 60`  
- Not currently in a position  

### Exit Condition (Sell)
- News Sentiment = NEGATIVE and `sentiment_score > 0.5`, **or**  
- `RSI > 65`, **or**  
- Downtrend (`MA20 < MA50` and `MACD < 0`), **or**  
- Current return ≤ -3% (stop-loss) or ≥ +6% (take-profit)  

### Decision Flowchart
```mermaid
graph TD
    Start[Market Data Input: Price, RSI, MA, MACD, Bollinger, Sentiment] --> CheckBuy{Not in Position & Sentiment POSITIVE?}
    CheckBuy -->|Yes| CheckRSI{RSI < 60?}
    CheckBuy -->|No| CheckSell[Check Exit Conditions]

    CheckRSI -->|Yes| Buy[Enter Position]
    CheckRSI -->|No| CheckSell

    CheckSell -->|Exit Condition Met| Sell[Exit Position]
    CheckSell -->|No| Hold[Stay in Position]

    Buy --> Monitor[Holding]
    Monitor --> CheckSell
