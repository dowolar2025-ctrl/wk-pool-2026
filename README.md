# WK Pool 2026 — Scoretabel

Deze app houdt bij hoeveel punten het ingevulde WK-formulier (van Daniella Doors)
verdient in de WK-pool, op basis van de puntenregels uit het invulbestand.

## De app bekijken

De app staat online en is voor iedereen met de link te bekijken:

**https://dowolar2025-ctrl.github.io/wk-pool-2026/**

Bij het openen haalt de app automatisch de laatste uitslagen op. Met de knop
**"Haal laatste uitslagen op"** doe je dat tussendoor nog een keer — handig
tijdens een speeldag. Wedstrijden die op dat moment bezig zijn, zijn zichtbaar
met een rood "Live"-label (die tellen pas mee als ze afgelopen zijn).

## Hoe de stand wordt bijgewerkt

1. **Automatisch bij het openen en via de knop**: de app haalt live uitslagen
   op bij ESPN en telt afgelopen wedstrijden direct mee.
2. **Elke ochtend om 7:00**: een automatische taak controleert de uitslagen
   van de vorige dag, slaat ze vast op in `docs/data/uitslagen.json` en werkt
   ook zaken bij die de app niet zelf kan ophalen (knock-outschema,
   doelpunten van de 4 gekozen spelers, kaartentellingen).
3. **Handmatig**: zeg tegen Claude "Werk de WK-stand bij".

## Bestanden

| Bestand | Wat het is |
|---|---|
| `docs/index.html` | De app zelf (puntentelling + weergave) |
| `docs/data/voorspellingen.json` | De voorspellingen, uitgelezen uit het Excel-bestand |
| `docs/data/uitslagen.json` | De vastgelegde uitslagen (dagelijks bijgewerkt) |
| `docs/data/puntenregels.json` | De puntenregels — aanpasbaar als de pool anders telt |
| `Invulbestand wk 2026(ingevuld).xlsm` | Het originele formulier (alleen lokaal, staat niet online) |
| `app/extract.py` | Eenmalig gebruikt om het Excel-bestand uit te lezen |
| `app/` (overig) | Eerste lokale versie van de app, niet meer in gebruik |

Testen van de puntentelling: open de app met `?test=1` achter de link.

## Aannames bij de puntentelling

De regels in het Excel-bestand laten een paar dingen open. De app gaat uit van:

1. De **zestiende finale** telt hetzelfde als de achtste finale
   (10 punten per land op de juiste plaats; geen halve punten).
2. De **troostfinale** (3e/4e plaats) telt hetzelfde als de halve finale (30/15).
3. "Land op de correcte plaats" = het land staat in de juiste wedstrijd,
   thuis of uit maakt niet uit.
4. De puntenschaal voor de telvragen (50/20/10) geldt ook voor rode kaarten.
5. Bij knock-outwedstrijden telt de stand ná verlenging, zónder strafschoppen.

Klopt een aanname niet? De getallen staan in `docs/data/puntenregels.json`;
na aanpassing en publicatie rekent de app alles automatisch opnieuw uit.
