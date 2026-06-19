# 📊 5ar EMA Cloud — Kompletan vodič

> **TradingView Pine Script indikator** | Verzija: Pine Script v1  
> Tri EMA linije + dinamični oblak (cloud) između EMA 21 i EMA 200

---

## 📌 Što je ovaj indikator?

**5ar EMA Cloud** je trend-prateći indikator koji se crta direktno na price chart (overlay=true). Koristi **tri eksponencijalne pomične sredine (EMA)** različitih perioda i puni prostor između najbrže i najsporije EMA u **boju koja ovisi o tržišnom trendu**.

### Tri EMA linije

| EMA | Period | Boja | Uloga |
|-----|--------|------|-------|
| EMA 21 | 21 svjećica | 🟢 Zelena | Kratkoročni trend — najbržа reakcija na cijenu |
| EMA 89 | 89 svjećica | ⚪ Bijela | Srednjoročni trend — filter šuma |
| EMA 200 | 200 svjećica | 🔴 Crvena | Dugoročni trend — "zlatna linija" institucija |

### Oblak (Cloud Fill)

Prostor između **EMA 21** i **EMA 200** se puni bojom:

- 🟢 **Zeleni oblak** → EMA 21 je **iznad** EMA 200 — bullish zona
- 🔴 **Crveni oblak** → EMA 21 je **ispod** EMA 200 — bearish zona

Prozirnost oblaka je postavljena na 90% (`transp=90`), što znači da je oblak lagano vidljiv i ne zaklanja price action.

---

## 🔧 Objašnjenje koda

```pine
//@version=1
study("5ar EMA Cloud", overlay=true)
```
- `@version=1` — Pine Script verzija 1 (starija sintaksa)
- `overlay=true` — indikator se crta na grafikonu cijene, ne u zasebnom panelu

```pine
M1 = ema(close, 21)    // EMA 21  — zelena, brza
M2 = ema(close, 200)   // EMA 200 — crvena, spora
M3 = ema(close, 89)    // EMA 89  — bijela, srednja
```
- `ema(close, period)` — računa eksponencijalnu pomičnu sredinu na osnovi **close (zatvarajuće) cijene**
- EMA daje **veću težinu novijim cijenama** od jednostavne SMA

```pine
cloudcolor = M1 > M2 ? green : red
```
- Ternary operator: ako je EMA 21 > EMA 200 → oblak je zelen, inače crven
- Ovo je **dinamično** — boja se mijenja svaki bar

```pine
P1 = plot(M1, color=green, linewidth=2, title='EMA 21',  transp=0)
P2 = plot(M2, color=red,   linewidth=2, title='EMA 200', transp=0)
P3 = plot(M3, color=white, linewidth=2, title='EMA 89',  transp=0)
```
- `linewidth=2` — debljina linije 2px za bolju vidljivost
- `transp=0` — linije su potpuno neprozirne (100% vidljive)

```pine
fill(P1, P2, color=cloudcolor, title="Cloud Fill", transp=90)
```
- `fill()` — puni prostor između dviju plotova
- Ispunjava se između P1 (EMA 21) i P2 (EMA 200)
- `transp=90` — oblak je 90% proziran (jedva vidljiv, ne smeta price action)

---

## 🚀 Kako dodati na TradingView

1. Otvori **TradingView** → odaberi chart
2. Klikni na **Pine Editor** (donji panel)
3. Kopiraj cijeli kod i zalijepiti ga u editor
4. Klikni **"Add to chart"** (ili Ctrl+Enter)
5. Indikator se pojavljuje direktno na grafikonu

> **Napomena:** Stariji Pine v1 sintaksa (`ema()` bez `ta.ema()`) može zahtijevati da klikneš **"Convert to v5"** ili zadržiš verziju 1 u editoru.

---

## 📖 Kako čitati signale

### 1. Boja oblaka — opći trend

```
Zeleni oblak  ──► Tržište je u UPTREND-u (bikovi kontroliraju)
Crveni oblak  ──► Tržište je u DOWNTREND-u (medvjedi kontroliraju)
```

Što je oblak **deblji** (veći razmak između EMA 21 i EMA 200), to je trend **jači**.  
Što je oblak **tanji**, trend slabi ili se priprema preokret.

---

### 2. Raspored triju linija

**Idealan bullish raspored (od gore prema dolje):**
```
💰 Cijena
🟢 EMA 21
⚪ EMA 89
🔴 EMA 200
```

**Idealan bearish raspored (od dolje prema gore):**
```
🔴 EMA 200
⚪ EMA 89
🟢 EMA 21
💰 Cijena
```

---

### 3. Crossover signali

| Signal | Opis | Značenje |
|--------|------|----------|
| EMA 21 križa **iznad** EMA 200 | Oblak mijenja boju u zelenu | **Bullish crossover** — potencijalni buy signal |
| EMA 21 križa **ispod** EMA 200 | Oblak mijenja boju u crvenu | **Bearish crossover** — potencijalni sell signal |
| Cijena vraća na EMA 21 u uptrend-u | Bounce od zelene linije | **Retracement buy** |
| Cijena vraća na EMA 89 | Bounce od bijele linije | **Dublji retracement buy** |

---

### 4. EMA 89 kao filter

EMA 89 (bijela linija) služi kao **srednji filter**:
- U uptrend-u: cijena i EMA 21 trebaju biti **iznad** EMA 89
- Pad ispod EMA 89 = upozorenje, trend slabi
- EMA 89 u zoni između EMA 21 i EMA 200 = konsolidacija/nesigurnost

---

## 📐 Strategije trgovanja

---

### ✅ Strategija 1: Trend Following — "Ride the Cloud"

**Filozofija:** Ulaziš u smjeru oblaka i ostajеš dok god oblak ne promijeni boju.

**BUY ulaz:**
1. Oblak je **zelen**
2. Cijena je **iznad** svih triju EMA
3. Cijena se povuče i dotakne EMA 21 (ili EMA 89) i odbije se gore (bullish candle)
4. **ENTER LONG** pri zatvaranju te svjećice

**SELL / EXIT:**
- Postavi **Stop Loss** ispod EMA 89 ili EMA 200 (ovisno o risk toleranciji)
- **Take Profit** na sljedećem ključnom otporu ili kad EMA 21 križa ispod EMA 89

**Primjer (dnevni chart, dionice/kripto):**
```
📈 BTC/USD dnevni
Oblak zelen, cijena pada na EMA 21 → tvori bullish engulfing → LONG
SL: ispod EMA 200 (veliki rizik) ili ispod EMA 89 (konzervativan)
TP: ATH zona ili 2:1 RRR
```

---

### ✅ Strategija 2: Cloud Crossover — "The Flip"

**Filozofija:** Trguješ trenutak kada oblak mijenja boju — potencijalni početak novog trenda.

**BUY ulaz:**
1. EMA 21 križa **iznad** EMA 200 → oblak postaje **zelen**
2. Pričekaj konfirmaciju: prva ili druga svjećica koja zatvori **iznad** EMA 21 nakon crossovera
3. **ENTER LONG**

**SELL ulaz:**
1. EMA 21 križa **ispod** EMA 200 → oblak postaje **crven**
2. Prva svjećica koja zatvori **ispod** EMA 21 → **ENTER SHORT** (ili zatvori long)

> ⚠️ **Upozorenje:** Crossoveri mogu biti kasni signal — cijena je već napravila velik dio poteza. Koristi na **višim timeframe-ovima** (dnevni, tjedni) gdje je signal pouzdaniji.

---

### ✅ Strategija 3: Multi-Timeframe (MTF) — "Top-Down pristup"

**Filozofija:** Koristiš viši timeframe za smjer, niži za ulaz.

**Koraci:**
1. **Dnevni (D1) chart:** Provjeri boju oblaka — samo traži buy signale u smjeru oblaka
   - Zelen oblak → tražiš samo LONG setupove
   - Crven oblak → tražiš samo SHORT setupove (ili sediš na rukama)

2. **4-satni (H4) chart:** Čekaj da cijena padne na EMA 21 ili EMA 89

3. **1-satni (H1) chart:** Traži entry svjećicu (pin bar, engulfing, inside bar) na EMA razini

4. **ENTER** s tijesnim SL ispod lokalne EMA razine

**Primjer:**
```
D1: Oblak zelen, bullish trend ✔
H4: Cijena vraća na EMA 89 (bijela) ✔
H1: Bullish pin bar na EMA 89 → LONG ENTRY ✔
SL: 1% ispod pin bar low
TP: Prethodni H4 high ili 1:2 RRR
```

---

### ✅ Strategija 4: Kontra-trend "Bounce at 200 EMA"

**Filozofija:** EMA 200 je magnet za cijenu. U jakim trendovima cijena se često vrati na EMA 200 i odbije.

**BUY setup (bullish rebound):**
1. Prethodni dugoročni trend je bio **bullish** (cijena dugo iznad EMA 200)
2. Cijena pada **do** ili **blizu** EMA 200 (crvena linija)
3. Oblak je crven → ali tražiš reversal/bounce, ne nastavak pada
4. Pojavi se jaka bullish svjećica (hammer, bullish engulfing) na ili iznad EMA 200
5. **ENTER LONG** s kratkim SL ispod EMA 200

> ⚠️ Ovo je kontra-trend strategija — viši rizik! Koristi **manje pozicije** i **striktne SL**.

---

## ⚙️ Preporučeni timeframe-ovi

| Timeframe | Prikladnost | Stil tradinga |
|-----------|-------------|---------------|
| 1min – 15min | ❌ Previše šuma | Izbjegavaj |
| 30min – 1h | ⚠️ Prihvatljivo | Day trading |
| 4h | ✅ Dobro | Swing trading |
| Dnevni (D1) | ✅✅ Odlično | Swing / Position |
| Tjedni (W1) | ✅✅ Odlično | Position trading |

---

## 💡 Savjeti i napomene

### ✔ Kombinacije s drugim indikatorima

Za bolje rezultate, kombiniraj **5ar EMA Cloud** s:

- **RSI (14)** — izbjegavaj buy kad je RSI > 70 (overbought), sell kad < 30 (oversold)
- **MACD** — potvrdi crossover MACD crossoverom u istom smjeru
- **Volume** — veći volumen na crossoveru = pouzdaniji signal
- **Support/Resistance** — zoni SL/TP dodaj ključne S/R razine

---

### ⚠️ Česte greške

1. **Ulaz na crossoveru bez potvrde** → čekaj zatvaranje svjećice iznad/ispod EMA
2. **Ignoriranje višeg timeframe-a** → uvijek provjeri D1 trend
3. **Preskakanje SL** → obavezan Stop Loss, uvijek
4. **Korištenje na 1min chartu** → EMA na niskim TF-ovima daje lažne signale
5. **Očekivanje savršenih signala u sideways tržištu** → indikator je dizajniran za trendove; u ranging tržištu (bočno kretanje) generira mnogo lažnih signala

---

### 📊 Upravljanje rizikom (Money Management)

```
Preporučeni rizik po trgovini: 1% – 2% kapitala
Stop Loss: ispod/iznad relevantne EMA razine
Risk:Reward ratio: minimum 1:2 (bolje 1:3)
Veličina pozicije: kapital × rizik% / (entry – SL u pipsima)
```

---

## 🔄 Moguće nadogradnje koda

Ako želiš modernizirati kod na **Pine Script v5**, promijeni:

```pine
//@version=5
indicator("5ar EMA Cloud", overlay=true)

M1 = ta.ema(close, 21)
M2 = ta.ema(close, 200)
M3 = ta.ema(close, 89)

cloudcolor = M1 > M2 ? color.new(color.green, 0) : color.new(color.red, 0)

P1 = plot(M1, color=color.green, linewidth=2, title="EMA 21")
P2 = plot(M2, color=color.red,   linewidth=2, title="EMA 200")
P3 = plot(M3, color=color.white, linewidth=2, title="EMA 89")

fill(P1, P2, color=color.new(cloudcolor, 90), title="Cloud Fill")
```

---

## 📝 Sažetak

| Element | Opis |
|---------|------|
| Tip | Trend-prateći (trend following) |
| Prikaz | Direktno na grafikonu (overlay) |
| Primjena | Dionice, forex, kripto, indeksi |
| Idealni TF | H4, D1, W1 |
| Signal za kupnju | Zelen oblak + bounce od EMA 21/89 |
| Signal za prodaju | Crven oblak + odbijanje od EMA 21/89 |
| Slabost | Loš u ranging/sideways tržištima |
| Snaga | Odličan za hvatanje dugih trendova |

---

*Dokument kreiran za: 5ar EMA Cloud Pine Script indikator*  
*Svi primjeri su edukativne prirode. Trgovanje nosi rizik gubitka kapitala.*
