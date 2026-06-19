# Medijana Prethodnog Dana (PDM) — Upute za korištenje

> **Pine Script v5 indikator za TradingView**
> Iscrtava 50% razinu dnevnog raspona prethodnog dana kao horizontalnu liniju podrške/otpora.

---

## Sadržaj

1. [Što je PDM?](#što-je-pdm)
2. [Instalacija](#instalacija)
3. [Postavke indikatora](#postavke-indikatora)
4. [Vizualni elementi na grafikonu](#vizualni-elementi-na-grafikonu)
5. [PDM kao indikator — čitanje signala](#pdm-kao-indikator--čitanje-signala)
6. [PDM kao strategija — pravila ulaza i izlaza](#pdm-kao-strategija--pravila-ulaza-i-izlaza)
7. [Primjeri setupa](#primjeri-setupa)
8. [Kombiniranje s ostalim alatima](#kombiniranje-s-ostalim-alatima)
9. [Česte greške i savjeti](#česte-greške-i-savjeti)

---

## Što je PDM?

**PDM (Previous Day Median)** je horizontalna razina koja predstavlja **sredinu dnevnog raspona prethodnog dana**:

```
PDM = (High prethodnog dana + Low prethodnog dana) / 2
```

Ova razina je poznata i pod nazivima:
- **Mid-point** ili **50% retracement** dnevnog raspona
- **Dnevna ravnoteža** — cijena oko koje se nalazila "ravnoteža" kupaca i prodavača prethodnog dana
- **IB Midpoint** u kontekstu Inner Bar / Globex analize

### Zašto je ova razina važna?

Institucionalni igrači i algoritmi često **koriste prethodni mid-point kao referentnu razinu** jer:

- Predstavlja fer vrijednost prethodnog dana
- Dijeli dnevni raspon na dvije jednake polovice — gornju (bullish zona) i donju (bearish zona)
- Ako cijena **ostaje iznad PDM** → kupci kontroliraju tržište toga dana
- Ako cijena **padne ispod PDM** → prodavači preuzimaju kontrolu
- Reakcija na PDM (odbijanje ili proboj) daje jasan signal smjera

---

## Instalacija

1. Otvori **TradingView** u pregledniku
2. Na dnu ekrana klikni na **Pine Editor** tab
3. Kopiraj cijeli sadržaj fajla `PDM_Medijana_Prethodnog_Dana.pine`
4. Zalijepiti u Pine Editor (izbriši postojeći sadržaj)
5. Klikni **Save** (disketa ikona) → daj ime indikatoru (npr. `PDM`)
6. Klikni **Add to chart**

Indikator je sada aktivan na grafikonu.

> **Preporučeni timeframeovi:** `5m · 15m · 30m · 1H · 4H`
> Na dnevnom (1D) timeframeu linije su redundantne jer svaka svjećica = jedan dan.

---

## Postavke indikatora

### ⚙️ Opće postavke

| Postavka | Opis | Zadano |
|---|---|---|
| **Broj dana unazad** | Koliko prethodnih PDM linija se prikazuje | 5 |
| **Prikaži oznake** | Uključuje/isključuje tekstualne labele uz linije | Uključeno |
| **Prikaži cijenu u oznaci** | Dodaje numeričku vrijednost razine u labelu | Uključeno |

### 📅 Završeni dani

Ove postavke kontroliraju **linije završenih dana** — medijane dana koji su potpuno zatvoreni.

| Postavka | Opis | Zadano |
|---|---|---|
| **Boja** | Boja horizontalne linije | Crvena |
| **Debljina** | Debljina linije (1–5) | 2 |
| **Stil** | Solid / Dashed / Dotted | Solid |

### ⏳ Tekući dan (live)

Ove postavke kontroliraju **live liniju tekućeg dana** — mijenja se svake svjećice jer dan još traje.

| Postavka | Opis | Zadano |
|---|---|---|
| **Boja** | Boja live linije | Narančasta |
| **Debljina** | Debljina linije (1–5) | 2 |
| **Stil** | Solid / Dashed / Dotted | Dashed |

> 💡 **Savjet:** Drži live liniju u iscrtkanom stilu (Dashed) da je vizualno odmah razlikuješ od završenih dana.

---

## Vizualni elementi na grafikonu

```
00:00                          23:59
|─────────────── PDM  0.007235 ─────────────────|   ← Crvena linija (završeni dan)

00:00              ← sada →
|─ ─ ─ ─ ─ ─ ─ ⏳ 0.006689 ◄ Medijan tekućeg dana — nije finalan ─ ─|
                                                                        ↑ Narančasta, dashed
```

### Trajanje linija

- Svaka linija počinje u **00:00** i završava u **23:59** istog dana
- PDM prethodnog dana **iscrtava se na sljedećem danu** — tj. sutra vidimo gdje je bila ravnoteža juče
- Live linija tekućeg dana se **automatski pomiče** gore/dolje kako se mijenjaju dnevni max i min

---

## PDM kao indikator — čitanje signala

### Osnovno čitanje (Bias)

| Pozicija cijene | Značenje |
|---|---|
| Cijena **iznad PDM** i drži se iznad | Bullish bias za taj dan — kupci dominiraju |
| Cijena **ispod PDM** i drži se ispod | Bearish bias za taj dan — prodavači dominiraju |
| Cijena **oscilira oko PDM** | Nema jasnog smjera — sideways, izbjegavaj ulaz |

### Reakcija na PDM razinu

```
Scenarij A — Odbijanje od PDM (Rejection)
─────────────────────────────────────────
Cijena se spusti do PDM → formira se svjećica s dugom donjom sjenom
→ cijena se odbija gore  →  LONG signal (kratak)

Scenarij B — Proboj PDM (Breakout)
─────────────────────────────────────────
Cijena probi PDM s volumenom → retestira razinu odozgo
→ PDM postaje podrška  →  LONG na retest

Scenarij C — Pad kroz PDM (Breakdown)
─────────────────────────────────────────
Cijena probi PDM prema dolje → retestira razinu odozdo
→ PDM postaje otpor  →  SHORT na retest
```

---

## PDM kao strategija — pravila ulaza i izlaza

### Strategija 1 — PDM Bounce (Odbijanje)

Tražimo **reakciju** cijene kada dotakne PDM liniju završenog dana.

**Uvjeti za LONG:**
1. Cijena se tokom dana spušta prema PDM liniji prethodnog dana
2. Na PDM razini formira se **bullish svjećica** (pin bar, engulfing, hammer)
3. Cijena je prethodno bila **iznad PDM** veći dio dana (bullish bias potvrđen)
4. Volume porastao na bar koji dodiruje PDM

**Ulaz:** Odmah po zatvaranju potvrdirajuće svjećice na/iznad PDM

**Stop Loss:** Ispod PDM linije — 0.5–1× ATR ispod razine

**Take Profit:**
- TP1: Dnevni High prethodnog dana
- TP2: 1.5× dnevni raspon prethodnog dana iznad PDM

---

**Uvjeti za SHORT:**
1. Cijena se diže prema PDM liniji prethodnog dana odozdo
2. Na PDM razini formira se **bearish svjećica** (shooting star, bearish engulfing)
3. Cijena je prethodno bila **ispod PDM** veći dio dana (bearish bias)
4. Volume porastao na odbijanju

**Ulaz:** Odmah po zatvaranju potvrdirajuće svjećice na/ispod PDM

**Stop Loss:** Iznad PDM linije — 0.5–1× ATR iznad razine

**Take Profit:**
- TP1: Dnevni Low prethodnog dana
- TP2: Premješteni stop na breakeven kad TP1 dostignut

---

### Strategija 2 — PDM Breakout (Proboj s retestom)

Tražimo **proboj PDM** i zatim **retest** razine s druge strane.

**Uvjeti za LONG Breakout:**
1. Cijena je ispod PDM prethodnog dana — bearish otvori dana
2. Cijena snažno probija PDM prema gore (veliki bullish bar, volume spike)
3. Cijena se vraća na PDM razinu (retest)
4. Na retestiranoj razini nema zatvaranja **ispod PDM**

**Ulaz:** Na retestiranoj PDM razini, po potvrdi bullish svjećice

**Stop Loss:** Ispod PDM linije

**Take Profit:** High prethodnog dana ili 1.5–2× rizik (R:R = 1:1.5 minimum)

---

### Strategija 3 — Live PDM Fade

Koristi **tekuću (live) PDM liniju** — trguj kad cijena dosegne 50% tekućeg dana.

> ⚠️ Ova strategija je **mean-reversion** i funkcionira bolje na rangebound tržištu.

**Setup:**
1. Prati narančastu (live) PDM liniju koja se mijenja kroz dan
2. Ako cijena otišla daleko od live PDM (>1× ATR), tražimo povrat
3. Ulaz u smjeru prema live PDM kada se formira reversal signal

**Napomena:** Live PDM nije finalna razina — **ne koristiti kao strogi S/R** već kao dinamičnu ravnotežnu zonu.

---

## Primjeri setupa

### Primjer 1 — Jutarnji bounce na PDM (15m chart)

```
Kontekst:  BTC/USDT, 15m chart
PDM razina prethodnog dana: 65.200 $

08:30 — cijena se otvara iznad PDM (bullish bias)
10:15 — cijena pada na 65.210 $ (tik iznad PDM)
10:30 — formira se bullish pin bar, zatvaranje na 65.350 $

Ulaz:   65.360 $ (iznad zatvaranja pin bara)
SL:     65.050 $ (ispod PDM, ~150 $ rizika)
TP1:    65.900 $ (High prethodnog dana)  →  R:R = 1:3.6
TP2:    66.200 $
```

---

### Primjer 2 — Bearish breakdown kroz PDM (1H chart)

```
Kontekst:  ETH/USDT, 1H chart
PDM razina prethodnog dana: 3.250 $

09:00 — cijena se otvara ispod PDM (bearish bias potvrđen)
11:00 — rally prema PDM, dotakne 3.248 $
12:00 — formira se shooting star svjećica, zatvara na 3.230 $

Ulaz:   3.228 $ (kratko ispod zatvaranja)
SL:     3.270 $ (iznad PDM, ~40 $ rizika)
TP1:    3.180 $ (Low prethodnog dana)   →  R:R = 1:1.25
TP2:    3.150 $
```

---

## Kombiniranje s ostalim alatima

PDM funkcionira **najbolje u kombinaciji** s:

| Alat | Kako kombinirati |
|---|---|
| **Volume Profile** | Potvrdi PDM gdje je i HVN (High Volume Node) iz VP — ojačana razina |
| **VWAP** | Ako PDM i VWAP blizu — zona je jako relevantna, veća vjerovatnoća reakcije |
| **EMA 20/50** | PDM + EMA poklapanje = confluencna zona, jači setup |
| **Dnevni S/R nivoi** | Slaganje PDM s prethodnim pivotima pojačava signal |
| **RSI** | Ulaz na PDM + oversold/overbought RSI = dodatna potvrda |
| **Doji / Pin Bar** | Price action potvrda na PDM razini je obavezan filter |

> 💡 **Pravilo confluencne:** što više faktora se poklapa na istoj razini, to je signal jači. PDM **sam po sebi nije dovoljan** — uvijek tražiti najmanje 2 potvrde.

---

## Česte greške i savjeti

### ❌ Greške koje treba izbjegavati

**1. Ulaz bez potvrde svjećice**
Cijena dodirne PDM → odmah ulaz bez čekanja zatvaranja potvrdirajuće svjećice. Rezultira lažnim ulaskom u trendove koji proveravaju razinu.

**2. Ignoriranje live PDM linije**
Live medijana (narančasta) govori gdje je ravnoteža **tekućeg** dana. Ako se cijena jako odmakla od live PDM, tržište je u trendu — ne trguj bounce.

**3. Previše linija (lookback)**
Postavljanje previše dana unazad (npr. 20+) zatrpa grafikon i otežava čitanje. Preporučeno: **3–7 dana**.

**4. Korištenje PDM na dnevnom ili weekly timeframeu**
Na višim TF razina nije korisna jer svaka svjećica = jedan dan. Indikator je dizajniran za **intraday** korištenje.

**5. Zanemarivanje konteksta trenda**
PDM bounce strategija (mean reversion) ne funkcionira dobro u snažnim trendovima. U bull/bear trendu prednost daj breakout strategiji.

---

### ✅ Savjeti za bolje rezultate

- **Jutro je najvažnije** — prvih 1–2 sata nach otvaranja tržišta daje najčišće reakcije na PDM
- **Crypto tržišta** (24/7): gledaj PDM reakciju između **08:00–12:00 UTC** (London open) i **13:00–16:00 UTC** (NY open)
- Postavi **upozorenje (Alert)** na TradingView na razini PDM prethodnog dana za automatsku notifikaciju
- Vodi **trading journal**: bilježi svaki PDM setup — odbijanje, proboj, ili ništa — da identificiraš koji pattern radi na tvojim parovima
- Na **kriptu** PDM je posebno efikasan jer nema "overnight gap" — cijena kontinuirano trguje pa je PDM "čist"

---

## Brza referenca — Cheat Sheet

```
PDM = (H_jučer + L_jučer) / 2

Cijena iznad PDM  →  Bullish bias za danas
Cijena ispod PDM  →  Bearish bias za danas

Odbijanje od PDM + potvrda svjećice  →  Ulaz u smjeru biausa
Proboj PDM + retest                  →  Ulaz u smjeru proboja

SL: s druge strane PDM (0.5–1× ATR)
TP: prethodni High/Low, ili min. 1:1.5 R:R

🟥 Crvena linija  = PDM završenog dana (fiksna)
🟧 Narančasta     = PDM tekućeg dana   (mijenja se live, nije finalna)
```

---

*Indikator je napisan u Pine Script v5 i testiran na TradingView platformi.
PDM nije financijski savjet — svaki trade nosi rizik gubitka kapitala.*
