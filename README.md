# Finanční dashboard k nákupu novostavby

Jednostránkový nástroj (čisté HTML + JavaScript, bez buildu a bez backendu) pro plánování cash flow při koupi bytu ve výstavbě: splátky developerovi, úschova z prodeje stávajícího bytu, termínované vklady a spořicí účty s limity a odhad potřebného úvěru.

> 🤖 **Vibecoding projekt.** Vzniklo jako experiment ve spolupráci s AI (Gemini, Claude, DeepSeek) a bylo upraveno hlavně „podle citu“, ne jako produkční software. Vzorce jsem zkontroloval, ale žádné automatické testy nejsou. Používejte na vlastní riziko a výsledky si ověřte.
>
> **Všechna data v repozitáři jsou fiktivní.** Nástroj není finanční ani daňové poradenství, termíny a pravidla v checklistu ověřte u banky nebo daňového poradce.

## Co umí

- **Denní simulace likvidity** od července 2027 do května 2029 včetně čistého úroku po 15% srážkové dani.
- **Spořicí účty podle priority:** hotovost se plní odshora dolů do účtů s limity a platností od–do, prázdný limit funguje jako záchytný účet.
- **Pevné termínované vklady** s uzamčením částky a výnosem při splatnosti.
- **Platby a příjmy:** platby developerovi se vykreslují jako kumulativní křivka.
- **Odhad potřebného úvěru** a kalkulačka splátek, s rozpadem na doplatek bytu a vybavení domácnosti.
- **Stress-test sazeb:** plošný posun všech sazeb o −1,5 až +1,0 p. b.
- **Časová osa a administrativní/daňový checklist.**
- **Export a import do JSON**, automatické ukládání do `localStorage`, tisková verze, responzivní layout pro mobil.

## Spuštění

Stačí otevřít `index.html` v prohlížeči nebo nasadit repozitář na GitHub Pages. Soubor načítá z internetu pouze Chart.js (jsDelivr) a písma Google Fonts. Bez připojení fungují výpočty i tabulky, grafy se nezobrazí a ukáže se hláška.

## Soukromí

Všechna data zůstávají v prohlížeči (`localStorage`), nic se neodesílá na server. **Neukládejte do repozitáře exportované JSON soubory se skutečnými údaji.**

## Jak model počítá (zjednodušeně)

1. Každý den se aplikují platby a příjmy dané dnem.
2. Od hotovosti se odečte uzamčená částka v termínovaných vkladech, zbytek se rozdělí do účtů podle priority a limitů.
3. Denní úrok se počítá jako `částka × sazba × 0,85 / 365` a připisuje se na konci měsíce (volitelně denně).
4. Odhad úvěru je největší záporná volná likvidita za celé období.

Upravit lze všechna vstupní data v tabulkách v aplikaci; výchozí hodnoty jsou v konstantách `DEFAULT_BUCKETS`, `DEFAULT_EVENTS` a `DEFAULT_DEPOSITS` v `index.html`.

## Známá omezení

- Model nepočítá s inflací, poplatky bank ani s předčasným výběrem vkladů.
- Datum „dnes“ se bere z prohlížeče, takže ukázková data (začínající v roce 2027) ukazují zaplaceno 0 Kč.
- Pojištění vkladů (100 000 EUR na banku) model nehlídá.

## Nasazení na GitHub Pages

Settings → Pages → Source: *Deploy from a branch* → `main` / `(root)`. Aplikace pak poběží na `https://<uživatel>.github.io/<repozitář>/`.

## Příspěvky

Kdokoli může projekt volně použít, upravit a poslat pull request nebo issue. Hodí se zejména přidání testů, další jazyky nebo úprava modelu pro jiné daňové prostředí než české.

## Licence

[MIT](LICENSE) © 2026 Libor Adamcik ([@Entes1](https://github.com/Entes1)): použití, úpravy i další šíření (včetně komerčního) jsou zdarma, bez jakékoli záruky.

---

## English summary

A single-file, zero-dependency (except Chart.js via CDN) dashboard for planning cash flow when buying an off-plan apartment: developer instalments, escrow from selling an existing property, term deposits, tiered savings accounts and the loan you may need. UI is in Czech; all data are fictional. Open `index.html` in a browser, no build required. Everything is stored locally in your browser.

**Vibe-coded with AI assistance, provided as is, with no warranty. Not financial or tax advice.** MIT licensed, contributions welcome.
