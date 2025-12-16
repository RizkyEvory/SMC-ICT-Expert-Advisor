# 🚀 ICTnSMC_advance EA - Expert Advisor for MetaTrader 5

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Platform](https://img.shields.io/badge/platform-MetaTrader%205-orange.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Strategy](https://img.shields.io/badge/strategy-ICT%20%2F%20SMC-red.svg)

> 🏆 **Advanced Expert Advisor** berbasis konsep **Inner Circle Trader (ICT)** dan **Smart Money Concepts (SMC)** untuk trading XAUUSD dengan sistem otomatis yang intelligent dan powerful.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Smart Money Concepts](#-smart-money-concepts)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Strategy Logic](#-strategy-logic)
- [Risk Management](#-risk-management)
- [Visual Features](#-visual-features)
- [Parameters Guide](#-parameters-guide)
- [Performance Tips](#-performance-tips)
- [Troubleshooting](#-troubleshooting)
- [Disclaimer](#-disclaimer)
- [Support & Contact](#-support--contact)

---

## 🎯 Overview

**ICTnSMC_advance** adalah Expert Advisor canggih yang mengimplementasikan konsep-konsep trading institusional dari Inner Circle Trader (ICT) dan Smart Money Concepts (SMC). EA ini dirancang khusus untuk **XAUUSD (Gold)** dengan pendekatan multi-timeframe analysis dan money management yang robust.

### 🌟 Mengapa ICTnSMC_advance?

- ✅ **Konsep Institusional** - Menggunakan strategi yang sama dengan Smart Money
- ✅ **Multi-Timeframe Analysis** - Kombinasi Higher Timeframe trend + Lower Timeframe entry
- ✅ **Automatic Money Management** - Auto lot sizing berdasarkan risk percentage
- ✅ **Advanced Trade Management** - Trailing Stop, Break Even, Risk:Reward Ratio
- ✅ **Visual Dashboard** - Monitor performa real-time di chart
- ✅ **Clean & Optimized Code** - Ditulis dengan MQL5 best practices

---

## 🔥 Key Features

### 📊 Smart Money Analysis
- **Fair Value Gap (FVG)** Detection - Identifikasi gap yang akan diisi oleh market
- **Order Block (OB)** Identification - Mendeteksi zona supply/demand institusional
- **Break of Structure (BOS)** - Konfirmasi continuation trend
- **Change of Character (CHOCH)** - Deteksi reversal trend
- **Swing Points** - High/Low yang menjadi liquidity zones

### 💰 Money Management
- Auto Lot Sizing berdasarkan Risk Percentage
- Customizable Stop Loss & Take Profit
- Risk:Reward Ratio automation
- Trailing Stop dengan activation level
- Break Even protection
- Daily profit tracking

### 📈 Visual Tools
- Real-time Dashboard dengan informasi lengkap
- FVG Zones (Bullish/Bearish)
- Order Block Zones visualization
- BOS/CHOCH markers
- Swing High/Low lines
- Liquidity levels

### 🎮 Trade Execution
- Multi-timeframe confirmation
- Prevent over-trading dengan time filter
- One trade at a time (safety)
- Order retry mechanism
- Magic Number untuk multiple EA support

---

## 📚 Smart Money Concepts

### 1️⃣ Fair Value Gap (FVG)
**FVG** adalah gap/celah yang terbentuk ketika market bergerak terlalu cepat, meninggalkan area yang belum ter-trade dengan fair value. Market cenderung kembali untuk "mengisi" gap ini.

**Cara Kerja di EA:**
- Deteksi otomatis FVG bullish dan bearish
- Minimum gap size: `FVG_MinPoints` (default: 50 points)
- Visualisasi dengan rectangle hijau (bullish) / merah (bearish)
- Entry saat price "mitigate" FVG zone

### 2️⃣ Order Block (OB)
**Order Block** adalah candle terakhir sebelum impulsive move, di mana institusi menempatkan order besar mereka.

**Cara Kerja di EA:**
- Identifikasi last bearish candle sebelum bullish rally = Bullish OB
- Identifikasi last bullish candle sebelum bearish drop = Bearish OB
- Validasi dengan "strong move" criteria (3x candle size)
- Entry saat price return ke OB zone

### 3️⃣ Break of Structure (BOS)
**BOS** terjadi ketika price break melewati swing high/low terakhir, mengkonfirmasi continuation trend.

**Cara Kerja di EA:**
- Bullish BOS: Close candle > previous swing high
- Bearish BOS: Close candle < previous swing low
- Signal bahwa trend masih kuat dan valid untuk entry

### 4️⃣ Change of Character (CHOCH)
**CHOCH** adalah early signal reversal, di mana market gagal membuat higher high (uptrend) atau lower low (downtrend).

**Cara Kerja di EA:**
- Deteksi failure untuk continue trend
- Early warning untuk exit atau reverse position
- Lebih cepat dari traditional reversal patterns

---

## 🔧 Installation

### Step 1: Download Files
```bash
git clone https://github.com/RizkyEvory/SMC-ICT-Expert-Advisor.git
```

### Step 2: Copy to MetaTrader 5
1. Buka **MetaTrader 5**
2. Klik `File` → `Open Data Folder`
3. Masuk ke folder `MQL5` → `Experts`
4. Copy file `ICT_SMC_EA.mq5` ke folder tersebut

### Step 3: Compile
1. Buka **MetaEditor** (F4 di MT5)
2. Buka file `ICT_SMC_EA.mq5`
3. Klik `Compile` (F7)
4. Pastikan tidak ada error

### Step 4: Attach to Chart
1. Buka chart **XAUUSD**
2. Drag & Drop EA dari Navigator ke chart
3. Klik `OK` setelah setting parameter
4. Pastikan "AutoTrading" aktif (hijau)

---

## ⚙️ Configuration

### 🎯 Recommended Settings for XAUUSD

```
========== GENERAL SETTINGS ==========
MagicNumber          = 123456

========== STRATEGY SETTINGS ==========
LookbackBars         = 200
Trend_TF             = PERIOD_H1      // Higher timeframe untuk trend
Entry_TF             = PERIOD_M15     // Lower timeframe untuk entry
FVG_MinPoints        = 50             // Minimum 50 points gap
SwingStrength        = 5              // Sensitivity swing points

========== MONEY MANAGEMENT ==========
UseAutoLot           = true           // RECOMMENDED
FixedLot             = 0.01           
RiskPercent          = 1.0            // 1% per trade (Conservative)
SL_Points            = 1000           // 1000 points SL (~$10 untuk XAUUSD)
TP_Points            = 2000           
RiskRewardRatio      = 2.0            // 1:2 R:R
UseRRforTP           = true           
UseTrailingStop      = true           
TrailingActivate     = 1500           // Aktif setelah +$15
TrailingStop         = 500            
UseBreakEven         = true           
BreakEvenPoints      = 1000           

========== DASHBOARD & VISUAL ==========
ShowDashboard        = true
Show_FVG             = true
Show_OB              = true
Show_BOS_CHOCH       = true
Show_Liquidity       = true
```

### 📊 Timeframe Combinations

| Trend TF | Entry TF | Trading Style | Frequency |
|----------|----------|---------------|-----------|
| H4 | M15 | Swing Trading | 2-5 trades/week |
| H1 | M15 | Day Trading | 5-10 trades/week |
| H1 | M5 | Scalping | 10-20 trades/week |
| D1 | H1 | Position Trading | 1-3 trades/week |

---

## 🧠 Strategy Logic

### Entry Logic Flow

```
1. TREND IDENTIFICATION (Trend_TF)
   ├─ Identify Swing Highs & Lows
   ├─ Detect BOS (Break of Structure)
   └─ Confirm Trend Direction

2. ZONE MAPPING
   ├─ Mark FVG Zones
   ├─ Mark Order Block Zones
   └─ Mark Liquidity Levels

3. WAIT FOR RETRACEMENT
   ├─ Price returns to FVG/OB zone
   └─ Check if zone is still valid

4. ENTRY CONFIRMATION (Entry_TF)
   ├─ Momentum confirmation
   ├─ Candlestick pattern
   └─ No existing position

5. EXECUTE TRADE
   ├─ Calculate position size
   ├─ Set SL & TP
   └─ Place order
```

### Buy Signal Example
```
✅ Uptrend confirmed (BOS bullish)
✅ Price retraces to Bullish FVG/OB
✅ Price respects the zone (wick into zone)
✅ Bullish momentum on Entry_TF
➡️ BUY SIGNAL
```

### Sell Signal Example
```
✅ Downtrend confirmed (BOS bearish)
✅ Price retraces to Bearish FVG/OB
✅ Price respects the zone (wick into zone)
✅ Bearish momentum on Entry_TF
➡️ SELL SIGNAL
```

---

## 💼 Risk Management

### 🛡️ Protection Features

#### 1. Position Sizing
```cpp
Lot Size = (Account Balance × Risk%) / (SL in Points × Point Value)
```
- Auto-calculated berdasarkan account balance
- Disesuaikan dengan SL size
- Max lot limit protection

#### 2. Break Even
```
IF profit >= BreakEvenPoints (1000 points)
THEN move SL to entry price (0 risk)
```

#### 3. Trailing Stop
```
IF profit >= TrailingActivate (1500 points)
THEN trail SL at TrailingStop distance (500 points)
```

#### 4. Risk:Reward Enforcement
```
IF UseRRforTP = true
THEN TP = SL × RiskRewardRatio
EXAMPLE: SL=1000, RR=2.0 → TP=2000 points
```

### 📉 Risk Levels

| Risk % | Type | Description |
|--------|------|-------------|
| 0.5% | Ultra Conservative | Sangat aman, growth lambat |
| 1.0% | Conservative | **RECOMMENDED** untuk pemula |
| 2.0% | Moderate | Untuk trader berpengalaman |
| 3-5% | Aggressive | High risk, high reward |
| >5% | Very Aggressive | ⚠️ TIDAK DISARANKAN |

---

## 🎨 Visual Features

### Dashboard Display
```
═══════════════════════════════
      ICT SMC EA - XAUUSD
═══════════════════════════════
 Status: ON
 Signal: BUY SETUP
 Open Trades: 1
 Daily P/L: +125.50 USD
 Balance: 10000.00
 Equity: 10125.50
 Magic: 123456
 Trend: BULLISH
═══════════════════════════════
```

### Chart Elements
- 🟢 **Green Rectangles** = Bullish FVG
- 🔴 **Red Rectangles** = Bearish FVG
- 🔵 **Blue Rectangles** = Bullish Order Block
- 🟠 **Orange Rectangles** = Bearish Order Block
- ⬆️ **Gray Arrows** = BOS (Break of Structure)
- ⬆️ **Yellow Arrows** = CHOCH (Change of Character)
- 🔴 **Red Dotted Lines** = Swing High (Liquidity)
- 🟢 **Green Dotted Lines** = Swing Low (Liquidity)

---

## 📖 Parameters Guide

### GENERAL SETTINGS

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `Comment_` | string | "ICT SMC EA" | Komentar EA |
| `MagicNumber` | int | 123456 | Unique ID untuk EA |

### STRATEGY SETTINGS

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `LookbackBars` | int | 200 | Jumlah bar untuk analisis history |
| `Trend_TF` | ENUM | PERIOD_H1 | Timeframe untuk trend direction |
| `Entry_TF` | ENUM | PERIOD_M15 | Timeframe untuk entry confirmation |
| `FVG_MinPoints` | double | 50 | Minimum size FVG dalam points |
| `SwingStrength` | int | 5 | Bar kiri/kanan untuk swing validation |

### MONEY MANAGEMENT

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `UseAutoLot` | bool | true | Aktifkan auto position sizing |
| `FixedLot` | double | 0.01 | Lot size jika auto lot = false |
| `RiskPercent` | double | 1.0 | Persentase risk per trade |
| `SL_Points` | int | 1000 | Stop Loss dalam points |
| `TP_Points` | int | 2000 | Take Profit dalam points |
| `RiskRewardRatio` | double | 2.0 | Ratio R:R (1:2 = 2.0) |
| `UseRRforTP` | bool | true | Gunakan R:R untuk calculate TP |
| `UseTrailingStop` | bool | true | Aktifkan trailing stop |
| `TrailingActivate` | int | 1500 | Profit untuk aktifkan trailing |
| `TrailingStop` | int | 500 | Jarak trailing dari current price |
| `UseBreakEven` | bool | true | Aktifkan break even |
| `BreakEvenPoints` | int | 1000 | Profit untuk move SL ke BE |

### VISUAL SETTINGS

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `ShowDashboard` | bool | true | Tampilkan info dashboard |
| `DashboardBgColor` | color | clrBlack | Warna background |
| `DashboardTextColor` | color | clrLime | Warna text |
| `Show_FVG` | bool | true | Tampilkan Fair Value Gaps |
| `Show_OB` | bool | true | Tampilkan Order Blocks |
| `Show_BOS_CHOCH` | bool | true | Tampilkan BOS/CHOCH |
| `Show_Liquidity` | bool | true | Tampilkan liquidity levels |

---

## 💡 Performance Tips

### ✅ DO's

1. **Backtest First** - Test di Strategy Tester minimal 3-6 bulan data
2. **Start Small** - Mulai dengan risk 0.5-1% per trade
3. **Use VPS** - Untuk 24/7 operation dan low latency
4. **Monitor Daily** - Check performance setiap hari
5. **Proper Broker** - Pilih broker dengan low spread dan good execution
6. **Optimize Settings** - Sesuaikan dengan market condition

### ❌ DON'Ts

1. **Don't Overtrade** - Jangan ubah settings setiap hari
2. **Don't Increase Risk** - Setelah loss, jangan naikkan risk%
3. **Don't Use on Demo Forever** - Switch to small live account untuk real experience
4. **Don't Ignore Fundamentals** - Matikan EA saat high impact news
5. **Don't Mix Strategies** - Jangan run multiple EA dengan strategi berbeda di 1 account
6. **Don't Expect Miracles** - Trading is marathon, not sprint

### 📅 Optimal Trading Times (XAUUSD)

- **Best:** London Session (08:00-12:00 GMT) & NY Session (13:00-17:00 GMT)
- **Good:** Asian Session (00:00-08:00 GMT) - lower volatility
- **Avoid:** Friday after 18:00 GMT (weekend gap risk)
- **Avoid:** Major news events (NFP, FOMC, etc.)

---

## 🔍 Troubleshooting

### ❓ EA Tidak Membuka Position

**Kemungkinan Penyebab:**
- ✓ Check AutoTrading aktif (button hijau)
- ✓ Pastikan tidak ada position terbuka (EA = 1 trade at a time)
- ✓ Verifikasi trend belum confirmed (butuh BOS)
- ✓ Tidak ada FVG/OB zones yang valid
- ✓ Time filter - baru saja close trade

**Solusi:**
```
1. Check terminal → Experts tab untuk log messages
2. Refresh chart (F5)
3. Restart EA (remove & attach again)
4. Verify settings (terutama timeframe & points)
```

### ❓ Lot Size Terlalu Kecil/Besar

**Penyebab:**
- Auto lot calculation berdasarkan balance & risk%

**Solusi:**
```
Option 1: Adjust RiskPercent (naik/turun)
Option 2: Set UseAutoLot = false, gunakan FixedLot
Option 3: Sesuaikan SL_Points (smaller SL = bigger lot untuk same risk)
```

### ❓ Terlalu Banyak/Sedikit Zones di Chart

**Solusi:**
```
Terlalu banyak:
- Naikkan FVG_MinPoints (ex: 50 → 100)
- Naikkan SwingStrength (ex: 5 → 7)
- Ganti Trend_TF ke higher timeframe

Terlalu sedikit:
- Turunkan FVG_MinPoints (ex: 50 → 30)
- Turunkan SwingStrength (ex: 5 → 3)
- Ganti Trend_TF ke lower timeframe
```

### ❓ Dashboard Tidak Muncul

**Solusi:**
```
1. Set ShowDashboard = true
2. Adjust DashboardX & DashboardY position
3. Check chart space di kiri atas
4. Refresh chart (F5)
```

---

## ⚠️ Disclaimer

```
IMPORTANT DISCLAIMER:

Trading forex dan commodities (termasuk XAUUSD) melibatkan risiko tinggi 
dan mungkin tidak cocok untuk semua investor. Anda bisa kehilangan sebagian 
atau seluruh modal investasi Anda.

- Past performance TIDAK menjamin future results
- EA ini adalah TOOL, bukan "holy grail"
- Anda bertanggung jawab penuh atas keputusan trading Anda
- Selalu gunakan risk management yang proper
- Developer TIDAK bertanggung jawab atas loss yang terjadi

GUNAKAN DENGAN RISIKO ANDA SENDIRI!
```

### 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 📞 Support & Contact

### 🐛 Found a Bug?
- Open an [Issue](https://github.com/RizkyEvory/SMC-ICT-Expert-Advisor/issues)
- Provide detailed description & screenshots

### 💬 Questions?
- Check [Wiki](https://github.com/RizkyEvory/SMC-ICT-Expert-Advisor/wiki)
- Join our [Discussions](https://github.com/RizkyEvory/SMC-ICT-Expert-Advisor/discussions)

### 🤝 Contribute
Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) first.

### ⭐ Support This Project
If you find this EA useful, please give it a ⭐ star on GitHub!

---

## 📈 Changelog

### Version 1.0.0 (Current)
- ✅ Initial release
- ✅ FVG Detection & visualization
- ✅ Order Block identification
- ✅ BOS/CHOCH detection
- ✅ Multi-timeframe analysis
- ✅ Auto money management
- ✅ Trailing stop & break even
- ✅ Visual dashboard
- ✅ Liquidity levels

### Planned Features (v1.1.0)
- 🔜 Liquidity sweep detection
- 🔜 Fibonacci integration
- 🔜 News filter
- 🔜 Multiple TP levels
- 🔜 Telegram notifications
- 🔜 Advanced statistics panel

---

## 📚 Resources & Learning

### ICT/SMC Learning Materials
- [ICT YouTube Channel](https://www.youtube.com/@InnerCircleTrader)
- Smart Money Concepts Course
- Order Flow Trading Books

### MetaTrader 5 Resources
- [MQL5 Documentation](https://www.mql5.com/en/docs)
- [MQL5 Forum](https://www.mql5.com/en/forum)

---

<div align="center">

### 🚀 Happy Trading! 📈

**Made with ❤️ for the Trading Community**

[![GitHub Stars](https://img.shields.io/github/stars/RizkyEvory/SMC-ICT-Expert-Advisor?style=social)](https://github.com/RizkyEvory/SMC-ICT-Expert-Advisor/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/RizkyEvory/SMC-ICT-Expert-Advisor?style=social)](https://github.com/RizkyEvory/SMC-ICT-Expert-Advisor/network/members)

---

**⚡ Powered by Smart Money Concepts | Built with MQL5**

</div>

---

## 🙏 Acknowledgments

- Inner Circle Trader (ICT) - Untuk konsep trading
- Smart Money Concepts Community
- MetaTrader 5 Platform
- All contributors dan testers

---

**Last Updated:** 2025  
**Version:** 1.0.0  
**Status:** ✅ Active Development