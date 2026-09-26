# MOJEAUTO · prvá klikateľná verzia

Statický prototyp pripravený na Git a Vercel. Otvorte `index.html` v prehliadači alebo spustite `python3 -m http.server 8000` v tomto priečinku.

Funguje navigácia, základné aj rozšírené filtrovanie ukážkových vozidiel, detail, kroky formulára splátok, výber značky/modelu, podobné modely, ukážka výkupu a CRM ukážka správy vozidiel. Štartovací `catalog.js` obsahuje 79 značiek a 702 modelov, vrátane starších jazdených áut. Nie je to oficiálny úplný register všetkých historických modelov; v ostrej verzii bude redakčne dopĺňateľný. Štyri ukážkové vozidlá a fotografie sú ilustračné; nahradia sa skutočnými inzerátmi. Štítky a verejný popis/výbava sa ukladajú iba v danom prehliadači (`localStorage`). Interné poznámky, PDF, kontakty a kalendár sa v deme neukladajú.

Rozšírené hľadanie pod hlavnými filtrami: voľný výraz, rozsah ceny, ročníka, nájazdu a výkonu, výber viacerých palív, prevodoviek, pohonov, miest, karosérií, dverí, farieb a krajov a prepínač možného odpočtu DPH. Parametre sa kombinujú; viacero zaškrtnutí v jednej skupine znamená alternatívy. Výber značky zobrazí modely vybranej značky. Demo má len štyri autá, preto väčšina volieb správne vráti nulový výsledok. Ak udržiavate katalóg, upravte `catalog.js` (štruktúra `značka: [modely]`); v budúcom CRM sa to bude upravovať bez zmeny kódu.

Na úvodnej stránke sú tri rovnako veľké dlaždice v poradí **Financovanie – Auto Alarm – Výkup vozidla** (na úzkych obrazovkách pod sebou). Fotografia volantu pri financovaní je skutočná snímka od Sofíe Nuñez z Pexels: https://www.pexels.com/photo/black-car-interior-with-steering-wheel-18389234/; použitá ako ilustračný podklad podľa licencie Pexels. Vedie na ukážkový formulár `#/auto-alarm` na nastavenie upozornenia, keď pribudne auto podľa zadaných predstáv. Automatické e-maily začnú fungovať až po napojení backendu.

**Dôležité:** formuláre nič neodosielajú a žiadne osobné údaje neukladajú. Administrácia je iba verejná vizuálna ukážka bez prihlásenia. PDF, poznámky a osobné údaje do ukážky nevkladajte. Import z Autobazar.EU vyžaduje oficiálny export/súhlas; Google kalendár vyžaduje prihlásenie a OAuth. Pred verejným používaním treba zapojiť databázu, prihlásenie dvoch adminov, zabezpečené dokumenty, e-maily, ochranu osobných údajov a reálny obsah. Podrobnosti v `MOJEAUTO-CRM-integracie-zadanie.md`. Verejný prototyp nepublikovať ako hotový zber údajov.

Pri každom aute je v demo CRM zobrazená neverejná karta majiteľa s poľami meno, priezvisko, telefón, e-mail, poznámky a servis. Polia sú v ukážke vypnuté, pretože toto HTML ešte nemá bezpečné prihlásenie ani databázu. Skutočné kontakty a servisné záznamy sa nesmú ukladať do miestneho úložiska verejnej stránky.

Schválený smer loga: oceľový nápis MOJEAUTO na tmavomodrom pozadí. Súbor `assets/logo-steel.png` je náhľadový podklad hlavičky a pätičky. V `brand/` je verzia pre profilovú fotku Instagramu a návrh prednej strany vizitky. Sú to rastrové vizuály; na finálnu profesionálnu tlač treba čistú vektorovú predlohu, spadávku a potvrdené kontaktné údaje.

Písmo webu: Exo 2 (nadpisy, menu, karty, formuláre aj text), aby nadväzovalo na hranatý automobilový tvar oceľového loga. Samotný kovový nápis je obrazovo vytvorený znak, nemá dostupný súbor presného písma; Exo 2 je najbližší použiteľný webový typografický smer.

Farebná paleta: biela `#FFFFFF`, námornícka `#071D35`, azúrová `#00B8F0`. Obrázok v `assets/hero.jpg` je ilustračný generovaný podklad, nie fotografia konkrétneho predávaného auta.

## Nasadenie večer

1. Rozbaľte ZIP a vložte **obsah priečinka `mojeauto-v1`** do koreňa nového Git repozitára (súbory `index.html`, `styles.css`, `app.js`, `assets/`). Nahratie samotného ZIPu do repozitára web nespustí.
2. Vo Verceli pripojte Git repozitár ako statický projekt. Framework: `Other`; build command a output directory nechajte prázdne, pretože `index.html` je v koreňovom priečinku.
3. Najskôr skontrolujte testovaciu adresu Vercelu. Doménu mojeauto.sk z Websupportu pripojte po overení stránky a údajov DNS.
4. Pred zberom skutočných kontaktov odstráňte demo režim až po napojení bezpečného backendu, administrátorského prihlásenia a schválených textov ochrany údajov.

## Náhľad v aplikácii

Úvod je vložený priamo do `index.html`, takže sa zobrazí aj v prehliadačoch súborov, ktoré blokujú JavaScript. Tieto prehliadače nemusia umožniť preklikávanie aplikácie. Na skúšanie filtrov, formulárov a administrácie použite testovaciu adresu po nasadení na Vercel alebo otvorte HTML v bežnom prehliadači, ktorý spúšťa lokálne skripty.
