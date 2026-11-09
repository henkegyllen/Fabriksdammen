# Fabriksdammen AR – förslag till ny åfåra

Webbaserad AR för förslaget att behålla Fabriksdammen i Bodafors och leda vattnet i en ny åfåra ner till Emån. Besökaren skannar en QR-kod på skylten vid dammen, passar in fisken på skylten i kamerarutan och ser sedan förslagets sträckning i mobilen, på plats. Ingen app behövs.

**Live:** https:// henkegyllen.github.io/Fabriksdammen/
*(Mellanslaget efter `https://` är avsiktligt, så att adressen inte blir en länk.)*

## Så fungerar det

1. Skylten har en QR-kod för förslag 1 och en för förslag 2.
2. Besökaren står på markeringen framför skylten och passar in hela fisken i rutan, med den orange mittlinjen mitt på fisken. Då är position och riktning kända utan GPS eller kompass.
3. "Starta AR" låser kalibreringen.
   - **Android** (Chrome med ARCore/WebXR): man kan gå längs fåran.
   - **iPhone** (Safari, ingen WebXR): stå kvar och vrid dig.

I AR-läget visas:
- **Orange linje:** förslagets sträckning, 1,5 m över dagens mark. Knappen *Linjen* lägger den på marken i stället.
- **Stolpar var 25:e m:** avstånd från intaget, planerad vattenyta och hur djupt den ligger under dagens mark. Intag och anslutning till ån har samma texter som kartorna.
- **Vattenytan** (knapp): en blå linje där vattenytan i den nya fåran hamnar, i verklig höjd. Den ligger mest under marken och syns "genom" den.
- **Vita stolpar:** hushörn och småhus. Står de vid de riktiga husen stämmer riktningen; annars vrider man med ◀ ▶.
- **Visa förslag 1/2:** byter förslag utan ny kalibrering.

## Adress och parametrar

| Parameter | Betydelse |
|---|---|
| `s=1` / `s=2` | Skylt 1 (vid intaget) eller skylt 2 (vid ån) |
| `f=1` / `f=2` | Förslag 1 (via bäckfåran) eller förslag 2 (direkt till nuvarande fåra) |
| `test=1` | Visar scenen utan kamera, för granskning på dator. `hojd=40` lyfter kameran 40 m. |

## Filer

| Fil | Roll |
|---|---|
| `index.html` | Hela appen (kalibrering, scen, knappar). Enda externa beroendet är A-Frame 1.5.0. |
| `assets/fabriksdammen.json` | Förslagen (punkter med markhöjd och planerad vattenyta), skyltarnas lägen och riktning, kontrollmärken |
| `version.json` | Versionsstämpel för cache-handskakningen |

Koordinaterna är SWEREF 99 TM och höjderna RH 2000. Skyltens riktning (ståpunkt → skylt) räknas i samma rutnät, så skillnaden mellan rutnätsnorr och geografiskt norr tar ut sig själv.

`assets/fabriksdammen.json` skapas av ett skript i GIS-projektet ur förslagsberäkningen. Riktningen kan rättas per skylt med `offset` (grader, + medurs) i JSON-filen eller gemensamt med `HEADING_OFFSET` i `index.html`.

## Deploy och cache

Statisk sajt på GitHub Pages, inget byggsteg. GitHub Pages och iOS Safari cachar hårt, därför jämförs `APP_VERSION` i `index.html` med `version.json` och sidan laddas om vid skillnad.

> **Vid varje ändring i `index.html`: höj både `APP_VERSION` och `version.json`.**

## Källor

Höjddata © Lantmäteriet (Markhöjdmodell, laserskannad). Förslagen är preliminära skisser, inte projektering.
