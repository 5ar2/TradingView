# 📊 TradingView — Pine Indikatori i Alati [by Domar Ćećo]

<div align="center">

![TradingView](https://img.shields.io/badge/TradingView-Platform-0E4C92?style=for-the-badge&logo=tradingview)
![Pine Script](https://img.shields.io/badge/Pine%20Script-v6-7B3FF2?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-28A745?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

**Kolekcija Pine indikatora, predložaka i prilagođenih boja za TradingView**

[Opis](#-opis) • [Značajke](#-značajke) • [Instalacija](#-instalacija) • [Korištenje](#-korištenje)

</div>

---

# ⚠️ VAŽNA UPOZORENJA I DISKLEJMER

SIGURNOST - KLJUČNO:
Kopirajte kod ISKLJUČIVO iz ovog repozitorija/izvora. 
Nikada ne preuzimajte ili koprirajte Pine kod s: 
❌ Nepoznatih web stranica
❌ Javnih foruma ili socijalnih mreža
❌ Neverificiranih autora
❌ Skraćenih URL-a ili linkova

Treće osobe mogu ubaciti zlonamjerni kod ili malware u tuđe kodove.
Jedino kod iz ovog repozitorija je provjeren i siguran.

SAMOODGOVORNOST:
Ovaj Pine kod je pružen u informativne svrhe. Vi ste u potpunosti odgovorni za 
provjeru, testiranje i razumijevanje ovog koda prije nego ga koristite.

OBAVEZE KORISNIKA:
- Pročitajte i razumijete svaki redak koda
- Testirajte kod na paper trading računu prvo
- Provjerite sve eksterne pozive i URL-e
- Ne koristite kod koji vam nije jasan

ISKLJUČENJE ODGOVORNOSTI:
Autor nije odgovoran za:
- Gubitke novca ili vremena
- Neuspješne signale ili greške u kodu
- Neplanirana ponašanja ili bugove
- Bilo kakvu štetu direktnu ili indirektnu
- Korištenje koda iz drugih izvora (čak i ako je kopiran s našim nazivom)

NEMA JAMSTVA:
Kod se pruža "KAKO JEST" bez jamstva bilo koje vrste, izričite ili implicitne.
---

## 📝 Opis

Ovaj repozitorij sadrži skup **Pine skripti**, **indikatora** i **predložaka alata** za TradingView platformu. Svi indikatori i alati su osmišljeni sa sustavom boja optimiziranim za **maksimalnu preglednost na tamnoj pozadini** grafikona.

Ako trebаš brže donositi odluke, lakše prepoznavati signale i imati konzistentan izgled svog grafikona — ova kolekcija je rješenje.

---

## ✨ Značajke


- 🎯 **Precizni Indikatori** — Tehnički alati za identificiranje trendova i signala
- 🎨 **Prilagođene Boje** — Koncizan sustav boja za maksimalnu čitljivost
- 🔧 **Fleksibilni Alati** — Prilagođeni drawing alati s konfiguracijama
- 📋 **Predlošci** — Spremi predlošci za brže postavljanje
- 🌙 **Dark Mode Optimiziran** — Savršen za duže sjedene faze analize

---

## 🚀 Instalacija

### Korak 1: Kloniranje Repozitorija
```bash
git clone https://github.com/5ar2/TradingView.git
cd TradingView
```

### Korak 2: Kopiranje Pine Koda
1. Otvori TradingView platformu
2. Idi na **Pine Editor** (Alati → Pine Editor)
3. Kopiraj kod iz relevantne datoteke iz ovog repozitorija
4. Kreiraj novi skript i zalijepi kod

### Korak 3: Primjena Indikatorske Konfiguracije
- Otvori indikator na grafikonu
- Idi na **Postavke** (gear ikona)
- Prilagodi boje prema preferiranju (preloženi su optimalni)

---

## 📁 Struktura Repozitorija

```
TradingView/
│
├── 📂 TradingView indikatori/
│   ├── Moving Averages.pine
│   ├── RSI Extended.pine
│   ├── MACD Custom.pine
│   ├── Bollinger Bands.pine
│   └── Volume Indicators.pine
│
├── 📂 TradingView predlošci alata/
│   ├── Color Scheme (Dark Mode).json
│   ├── Drawing Tools Config.json
│   ├── Trading Template Basic.json
│   ├── Trading Template Advanced.json
│   └── README (predlošci).txt
│
├── README.md (ovaj dokument)
└── .gitignore
```

### 📊 **TradingView Indikatori**
Folder sadrži Pine skripte različitih indikatora:

| # | Pine skripte ||
|---|------|----------|
| 1 | 01 Bull Market Support Band + 8W SMA
| 2 | 02 EMA Cloud | 
| 3 | 03 Fractals | 
| 4 | 04 Multitime VWAP | 
| 5 | 05 Medijan predhodnog dana |


### 🎨 **TradingView Predlošci Alata**
Folder sadrži konfiguracije za drawing alate i boje:

| # | Alat ||
|---|------|----------|
| 1 | Horizontal Ray
| 2 | Rectangle | 
| 3 | Fixed Range Volume Profile | 
| 4 | Fib Speed Resistance Fan | 
| 5 | Trend-Based Fib Extension |
| 6 | Fibonacci Retracement > | 

### ୭ **Fibonacci predlošci:**

| # | Naziv predloška |
|---|----------------|
| 01 | Golden Pocket Zone |
| 02 | Standard |
| 03 | Fib Expansion |
| 04 | GZ |
| 05 | Negative Fibonacci |
| 06 | Range Fib |
| 07 | EQ Equilibrium |
| 08 | Fib 0.25 |
| 09 | Fib 0.5 |
| 10 | Mini Fibs |
| 11 | Scalp |
| 12 | Gann Fib |


---

## 📖 Korištenje

### Korištenje Indikatora

1. **Otvori Pine Editor** — Alati → Pine Editor
2. **Nove skripte** — New Script ili Duplicate existing
3. **Kopiraj kod** — Iz `TradingView indikatori/` foldera
4. **Dodaj na grafikon** — Add to Chart
5. **Prilagodi postavke** — Po potrebi u Settings

---

## 🎨 Sustav Boja

Boje su osmišljene za **tamnu pozadinu** grafikona i **maksimalnu preglednost**:


Sve boje se lako mogu prilagoditi u postavkama indikatora:
```pine
plot(series, color=color.new(color.green, transp=0))
```
---

## ⚙️ Konfiguracija

### Prilagođene Postavke po Indikatoru

Većina indikatora ima fleksibilne parametre:

---

### Vremenska Razdoblja
Indikatori su optimizirani za:
- ✓ 1 min — 1 hour (Scalping & Day Trading)
- ✓ 4 hour — Daily (Swing Trading)
- ✓ Weekly — Monthly (Position Trading)

---

## 💡 Praktični Savjeti

1. **Kombiniraj više indikatora** — Ne oslanjaj se samo na jedan
2. **Testiraj na povijesnim podacima** — Koristi Strategy Tester
3. **Prilagodi periode** — Prema vremenskom Izboru i instrumentu
4. **Koristi alarme** — Postavi notifikacije za važne signale
5. **Čuva predloške** — Spremi konfiguracije za brži pristup

---

## ⚠️ Odricanje od Odgovornosti

Ovi indikatori su **alati za analizu**, ne investicijski savjet. Uvijek:
- 🔹 Testiraj indikatore prije korištenja s pravim novcem
- 🔹 Koristi stop-lose za zaštitu kapitala
- 🔹 Raditi sa razumnom pozicijom
- 🔹 Konzultiraj financijskog savjetnika ako je potrebno

**Prošla performansa ne garantira buduće rezultate.**


---

<div align="center">

### ⭐ Ako ti se sviđa projekt, ostavi zvjezdicu!

Made by **Domar Ćećo**

[GitHub](https://github.com/5ar2) • [TradingView](https://www.tradingview.com)

</div>

---

