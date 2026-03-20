# AITrader v2 — MT5 AI Trading Bot

Fully automated trading bot that analyzes **multiple instruments simultaneously** and executes trades without human intervention, 24/7.

---

## What the bot does

Once started, the bot:

- **Automatically scans** currency pairs, indices and crypto every 30 seconds
- **Sends market data** to an AI server that decides the direction for each instrument
- **Opens, manages and closes** trades automatically, without any click from the user
- **Avoids economic news** — automatically detects high-impact news and does not trade during their window
- **Adapts lot size** based on market volatility and account balance
- **Protects profit** via automatic trailing stop once the trade enters profit

---

## How the automation works

```
[MetaTrader 5]
     |
     |  Collects live data from instruments
     |  details, strategies, etc ...
     |
     v
[AI Server — Python]
     |
     |  Checks the economic calendar (Forex Factory)
     |  → Active news? Blocks all trades automatically.
     |
     |  Sends data to Groq AI
     |  → AI returns: BUY / SELL / HOLD / CLOSE per instrument
     |
     v
[MetaTrader 5 — Execution]
     |
     |  Calculates lot size automatically from account risk %
     |  Sets SL and TP dynamically based on volatility (ATR)
     |  Opens the trade
     |  Monitors and moves trailing stop automatically
     v
   TRADE EXECUTED AUTOMATICALLY
```

---

## In action

### AI Server — real-time response
The terminal shows the bot receiving data from all symbols and returning the AI decision (BUY/SELL) for each instrument:

![Server CMD](POZADINCMD.png)

---

### Bot automatically opens trades simultaneously
Immediately after launch, the bot analyzes the market and executes positions on all configured instruments:

![Bot start](POZACANDEEPUSINFUNCTIUNE.jpg)

---

### MT5 Journal — real-time execution
MT5 displays in real time every action of the bot: what signal it received, what lot it calculated, where it placed SL/TP:

![MT5 Journal](POZA1.jpg)

---

### Results after the market moved
Same positions opened automatically, after the trend confirmed — **+553.91 USD profit**:

![Profit](POZA2DUPACEEPUSINFUNCTIUNE.jpg)

---

## Project structure

```
mt5-ai-trader/
│
├── EA/
│   ├── AITrader.mq5        # Expert Advisor source code (MQL5)
│   └── AITrader.ex5        # Compiled EA — loaded directly in MT5
│
├── server/
│   ├── server.py           # Python Flask server + Groq AI integration
│   ├── config.json         # Groq API key configuration
│   └── requirements.txt    # Python dependencies
│
└── README.md               # This file
```

---

## Included automations

| Feature | How it works |
|---|---|
| Market scan | Every 30 seconds, automatically, on all instruments |
| AI decision | Groq LLaMA analyzes multi-timeframe data and decides direction |
| Order execution | Opens/closes trades without human intervention |
| Dynamic lot size | Calculated automatically from account risk % |
| Dynamic SL/TP | Set automatically based on volatility at entry moment |
| Trailing Stop | Automatically moves SL as the trade becomes profitable |
| News filter | Detects major news and blocks trades automatically |
| Daily reset | Trade counters reset automatically at midnight |
| Anti-martingale | Automatically increases lot after consecutive wins |
| Early exit | Closes automatically if loss exceeds configured threshold |

---

---

# AITrader v2 — MT5 AI Trading Bot

Bot de trading complet automat care analizeaza **instrumente simultan** si executa tranzactii fara interventie umana, 24/7.

---

## Ce face botul

Odata pornit, botul:

- **Scaneaza automat** perechi valutare, indici si crypto la fiecare 30 de secunde
- **Trimite datele** de piata la un server AI care decide directia pentru fiecare instrument
- **Deschide, gestioneaza si inchide** tranzactii automat, fara niciun click din partea utilizatorului
- **Evita stirile economice** — detecteaza automat stirile de impact ridicat si nu tranzactioneaza in fereastra lor
- **Adapteaza lot size-ul** in functie de volatilitatea pietei si balanta contului
- **Protejeaza profitul** prin trailing stop automat dupa ce tranzactia intra in profit

---

## Cum functioneaza automatizarea

```
[MetaTrader 5]
     |
     |  Colecteaza date live de la instrumente
     |  detalii, strategii, etc ...
     |
     v
[Server AI — Python]
     |
     |  Verifica calendarul economic (Forex Factory)
     |  → Stire activa? Blocheaza toate tranzactiile automat.
     |
     |  Trimite datele la Groq AI
     |  → AI returneaza: BUY / SELL / HOLD / CLOSE per instrument
     |
     v
[MetaTrader 5 — Executie]
     |
     |  Calculeaza lot size automat din % risc al contului
     |  Seteaza SL si TP dinamic bazat pe volatilitate (ATR)
     |  Deschide tranzactia
     |  Monitorizeaza si muta trailing stop-ul automat
     v
   TRADE EXECUTAT AUTOMAT
```

---

## In actiune

### Serverul AI — raspuns in timp real
Terminalul arata botul cum primeste date de pe toate simbolurile si returneaza decizia AI (BUY/SELL) pentru fiecare instrument in parte:

![Server CMD](POZADINCMD.png)

---

### Botul deschide automat tranzactii simultan
Imediat dupa pornire, botul analizeaza piata si executa pozitii pe toate instrumentele configurate:

![Pornire bot](POZACANDEEPUSINFUNCTIUNE.jpg)

---

### Jurnalul MT5 — executie in timp real
MT5 afiseaza in timp real fiecare actiune a botului: ce semnal a primit, ce lot a calculat, unde a pus SL/TP:

![Jurnal MT5](POZA1.jpg)

---

### Rezultate dupa ce piata s-a miscat
Aceleasi pozitii deschise automat, dupa ce trendul s-a confirmat — **+553.91 USD profit**:

![Profit](POZA2DUPACEEPUSINFUNCTIUNE.jpg)

---

## Structura proiectului

```
mt5-ai-trader/
│
├── EA/
│   ├── AITrader.mq5        # Codul sursa Expert Advisor (MQL5)
│   └── AITrader.ex5        # EA compilat — incarcat direct in MT5
│
├── server/
│   ├── server.py           # Server Python Flask + integrare Groq AI
│   ├── config.json         # Configurare API key Groq
│   └── requirements.txt    # Dependinte Python
│
└── README.md               # Acest fisier
```

---

## Automatizari incluse

| Functie | Cum functioneaza |
|---|---|
| Scanare piata | La fiecare 30 secunde, automat, pe toate instrumentele |
| Decizie AI | Groq LLaMA analizeaza date multi-timeframe si decide directia |
| Executie ordine | Deschide/inchide trades fara interventie umana |
| Lot size dinamic | Calculat automat din % risc al contului |
| SL/TP dinamic | Setat automat bazat pe volatilitatea din momentul intrarii |
| Trailing Stop | Muta automat SL-ul pe masura ce tranzactia devine profitabila |
| Filtru stiri | Detecteaza stirile majore si blocheaza tranzactiile automat |
| Reset zilnic | Contoarele de trades se reseteaza automat la miezul noptii |
| Anti-martingale | Creste lotul automat dupa win-uri consecutive |
| Early exit | Inchide automat daca pierderea depaseste pragul configurat |

---
