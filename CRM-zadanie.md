# MOJEAUTO · interné CRM, vozidlá a kalendár

Stav: zadanie a klikateľný prototyp, 26. 9. 2026. Skutočná administrácia, import, dokumenty a Google synchronizácia ešte nie sú spustené. Tento súbor dopĺňa `MOJEAUTO-hlavne-zadanie.md`.

## Prístup a hlavné sekcie

- Po prihlásení dvoch individuálnych administrátorských účtov otvoriť interné CRM: Vozidlá, Záujemcovia z Auto Alarmu, Žiadosti o financovanie, Výkup vozidiel a Kalendár. Každý záznam má stav, čas vytvorenia/úpravy, zodpovedného pracovníka a históriu podstatných úkonov.
- Údaje zákazníkov a interné informácie sa nikdy nevkladajú do verejnej stránky ani do JavaScriptového balíka. Všetky čítania a zápisy v CRM kontrolovať na serveri podľa prihlaseného používateľa; verejná URL `#/admin` v prototypovej HTML stránke je len ukážka vzhľadu a nepredstavuje zabezpečenie.
- Vyhľadávanie a filtre kontaktov podľa značky, modelu, ceny, rozpočtu, stavu a dátumu. V kartách žiadostí priradenie k vozidlu a interná história komunikácie.

## Karta auta

- Verejná časť: značka, model, verzia, rok, km, cena, palivo, prevodovka, ďalšie dostupné parametre, samostatný popis, štruktúrovaná výbava, titulná fotografia a galéria. Štítok na fotografii podľa existujúceho zadania. Stavy koncept, zverejnené, rezervované, predané, archivované.
- Pre rozšírené vyhľadávanie doplniť štruktúrovaný výkon (kW), pohon, počet miest, typ karosérie, počet dverí, farbu, kraj a trojstavový údaj o možnom odpočte DPH (áno/nie/neoverené). Správa katalógu značiek/modelov, aliasov a nových modelov bude súčasťou zabezpečeného CRM; štartovací statický zoznam je len podklad pre demo.
- Interná časť: časovo označené poznámky s autorom (napr. telefonát, servis, rezervačná dohoda); pridanie, úprava a audit zmien. Interné poznámky sa nikdy neposielajú vo verejnej API odpovedi.
- Každé inzerované auto má samostatný interný kontakt na jeho majiteľa: meno, priezvisko, telefónne číslo, e-mail. K nemu patrí voľné textové pole **Poznámky k majiteľovi** a samostatné voľné textové pole **Servis** (servisná história, opravy a plánované práce). Ide o údaje viazané na konkrétny inzerát; pri opakovanom inzerovaní toho istého auta možno kontakt prepojiť s existujúcou osobou, pričom poznámky a servis zostanú priradené správnemu autu. Úpravy ukladajú čas a používateľa. Polia nie sú v inzeráte ani v e-mailoch Auto Alarmu.
- Interné súbory: nahrať a spravovať PDF zmluvy, veľký technický preukaz a iné dokumenty konkrétneho auta. Súkromné úložisko bez verejnej adresy; autorizácia pred každým načítaním, krátkodobé odkazy iba pre oprávneného admina, kontrola typu obsahu, veľkosti a bezpečnosti uploadu. Uchovať názov, kategóriu, autora a čas nahratia; možnosť vymazania podľa prevádzkových pravidiel. Nikdy ich nevkladať do verejnej fotogalérie ani odoslaných mailov.
- Pred zverejnením auta viditeľný kontrolný náhľad; zverejnenie spustí Auto Alarm podľa pravidiel bez duplicitných upozornení. Fotografie sa nahrávajú osobitne.

## Prenos údajov z Autobazar.EU

- V karte auta bude pole na odkaz na konkrétny inzerát (oficiálna stránka používa doménu `autobazar.eu`). Po oprávnenom napojení systém podľa odkazu identifikuje záznam v partnerom sprístupnenom exporte/feede a pripraví **koncept**, ktorý musí administrátor potvrdiť. Importujú sa iba dostupné textové a číselné údaje: značka, model, verzia, rok, km, cena, palivo, prevodovka, VIN len ak je právne a zmluvne povolený, popis a výbava. Žiadne cudzie fotografie. Chýbajúce polia zostanú na ručné doplnenie.
- Oficiálny cenník Autobazar.EU uvádza službu import/export inzercie na vlastný web v partnerských balíkoch. Ich podmienky zakazujú parsovanie dát z portálu bez predchádzajúceho písomného súhlasu prevádzkovateľa. Preto **neimplementovať scraper odkazu**. Overiť obchodný prístup, povolený rozsah dát, formát feedu a oprávnenie na opätovné publikovanie; potom implementovať mapovanie. Do dovtedy je k dispozícii ručné vypísanie údajov a uloženie zdrojového odkazu.
- Zachovať zdrojové ID a URL, odhaľovať duplicity podľa zdrojového ID a prípadne VIN, evidovať výsledok importu/chyby. Úprava na Autobazar.EU nesmie potichu prepísať ručne upravené údaje na MOJEAUTO.
- Zdroj: https://www.autobazar.eu/nase-sluzby a obchodné podmienky zverejnené prevádzkovateľom (časť o zákaze parsovania). Konkrétny typ partnerského rozhrania potvrdí prevádzkovateľ.

## Interný kalendár a Google

- Záznamy: skúšobná jazda, obhliadka pri výkupe, odovzdanie vozidla, servis a pripomienka. Časové pásmo `Europe/Bratislava`; začiatok/koniec, miesto, typ, stav, priradené auto, kontakt a interný pracovník. Pohľad mesiac/týždeň/agenda, vyhľadávanie a upozornenia.
- Kalendár CRM funguje samostatne. Voliteľné pripojenie firemného Google Kalendára cez OAuth jednotlivého administrátora alebo schváleného spoločného firemného účtu; najmenší nevyhnutný rozsah oprávnenia (napr. správa udalostí konkrétneho kalendára), šifrované tokeny len na serveri a možnosť odpojenia. Do Google udalosti prenášať len minimum (názov/čas/miesto), bez zmlúv, dokladov a citlivých údajov klienta.
- Pri implementácii dohodnúť smer synchronizácie. Odporúčaná prvá verzia: vytvorenie/úprava/zrušenie CRM termínu sa premietne do vybraného Google kalendára; uložiť Google event ID, ošetriť chyby a opakované pokusy. Čítanie cudzích udalostí späť do CRM zaviesť až po rozhodnutí o právach a konfliktoch pri súbežných úpravách.
- Google OAuth konfigurácia a prihlásenie budú potrebné pri vytvorení projektu. Zdroje: https://developers.google.com/workspace/calendar/api/auth a https://developers.google.com/workspace/calendar/api/v3/reference/events/insert.

## Čo obsahuje dnešný náhľad

- `#/admin`: vizuálny CRM prehľad, autá a fungujúca ukážka štítkov. `#/admin/vozidlo/x5` (resp. `octavia`, `a6`, `glc`): úprava verejného popisu a výbavy s okamžitým náhľadom v detaile auta; tieto neosobné údaje sa ukladajú iba lokálne v danom prehliadači. Zdrojový odkaz sa ukladá rovnako, no import nenačítava údaje.
- `#/admin/kontakty`, `#/admin/ziadosti`, `#/admin/kalendar`: klikateľné ukážky rozvrhnutia bez skutočných údajov. V karte každého auta je navyše zobrazená sekcia Majiteľ vozidla s poľami meno, priezvisko, telefón, e-mail, poznámky a servis. Zadávanie kontaktov, interných poznámok/PDF a prepojenie Google je zablokované, kým nebude existovať zabezpečený server. Do demo stránky nevkladať reálne osobné údaje.
