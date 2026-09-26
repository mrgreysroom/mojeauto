# MOJEAUTO · prvé nahratie na GitHub a Vercel

Pripravené 26. 9. 2026. Tento balík je **verejná ukážka**, nie hotový zber osobných údajov. Vozidlá a fotografie sú ilustračné; formuláre nič neodosielajú, CRM nemá prihlásenie a interné polia majiteľa/PDF sú vypnuté.

## 1. GitHub

1. Repozitár už existuje: [github.com/mrgreysroom/mojeauto](https://github.com/mrgreysroom/mojeauto). V čase prípravy je prázdny a verejný. Ďalší repozitár nevytvárajte.
2. Na počítači stiahnite `MOJEAUTO-v1-GIT-VERCEL.zip` a rozbaľte ho.
3. V repozitári kliknite **uploading an existing file** (prípadne **Add file → Upload files**). Otvorte rozbalený priečinok `mojeauto-v1` a pretiahnite **jeho obsah** na stránku. `index.html`, `app.js`, `catalog.js`, `styles.css`, `advanced.css` a priečinky `assets`, `brand` musia byť v koreňovom priečinku repozitára. Nepretiahnite samotný ZIP ako jediný súbor.
4. Po nahraní skontrolujte v zozname `index.html` a oba priečinky. Do poľa Commit message napíšte `Prvá ukážková verzia MOJEAUTO` a kliknite **Commit changes**.

## 2. Vercel

1. Prihláste sa na [vercel.com/new](https://vercel.com/new). V časti **Import Git Repository** vyberte `mrgreysroom/mojeauto`. Ak nie je viditeľný, Vercel môže vyžadovať pridanie tohto repozitára medzi povolené GitHub repozitáre; povoľte iba repozitár MOJEAUTO.
2. Project Name: `mojeauto`. Framework Preset: **Other**. Root Directory: `./` (ak sú súbory v koreni). Build Command aj Output Directory nechajte predvolené/prázdne. Žiadne environment variables prvá ukážka nepotrebuje.
3. Kliknite **Deploy** a počkajte na stav **Ready**. Otvorte pridelenú adresu `*.vercel.app`. Preklikajte úvod, rozšírené hľadanie, detaily áut, Auto Alarm, výkup a `#/admin`.
4. Doménu `mojeauto.sk` z Websupportu pripojíme až po kontrole testovacej adresy. DNS hodnoty zadáme presne podľa pokynov Vercelu pre konkrétny projekt.

## Ak sa nahrávanie zasekne

- Ak Vercel hlási 404, skontrolujte, či je `index.html` priamo v koreňovom priečinku GitHub repozitára.
- Ak chýbajú obrázky alebo filtre, skontrolujte prítomnosť `assets/`, `catalog.js`, `advanced.css` a `app.js` pri `index.html`.
- Formuláre v tejto ukážke neposielajú e-maily a interný CRM bez prihlásenia neprijíma kontakty. Na test používajte vymyslené údaje.

Aktuálne oficiálne postupy: [GitHub – vytvorenie repozitára](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository), [GitHub – nahratie súborov](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository), [Vercel – nasadenie Git repozitára](https://vercel.com/docs/git).
