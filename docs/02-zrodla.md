# 02 – Katalog źródeł: Boppard (stan: 2026-11-15)

Wdrożone w `sources.yaml` (12): stadt, kreis, wasser, vrm, tv-bad-salzig, ruderclub, vfr-bad-salzig, dlrg,
regionalrat, jobcenter, welterbe, buga29. Kanały RSS potwierdzone odczytem: Stadt Boppard, RheinHunsrück Wasser,
TV Bad Salzig, Ruderclub, BUGA 2029, Jobcenter. Wzorce `html_links` (kreis, vrm, dlrg, regionalrat, welterbe)
oraz kanał VfR Bad Salzig – niesprawdzone na żywo; weryfikacja na stronie `/quellen/` po pierwszym przebiegu.

## Etap 2 – kalendarze i źródła wymagające dopasowania
| Źródło | Adres | Uwagi |
|---|---|---|
| Museum Boppard | https://museum-boppard.de/veranstaltungsarchiv/ | `/event/<slug>/`, daty DD/MM/RRRR; REST kalendarza niedostępny |
| Stadthalle Boppard | https://www.boppard-stadthalle.de/events/upcomingevents | Joomla, daty „28. November 2026” |
| VHS Boppard | https://vhs-boppard.de | `/Veranstaltung/cmx….html`, daty DD.MM.RR (rok dwucyfrowy – do obsłużenia) |
| Cinema Boppard | https://www.cinema-boppard.de/index.php/kinoprogramm | Joomla JEvents |
| KV Rhein-Hunsrück – kalendarz | https://www.kv-rhk.de/aktuelles/veranstaltungen/veranstaltungskalender/ | |
| MJBO | https://www.mjbo.de/index.php/aktuelles.html | Joomla |
| TG Boppard | https://tg-boppard.de/index.php/blog/ | wpisy bez dat |
| RH Entsorgung | https://www.rh-entsorgung.de/de/Hauptnavigation/Service/Aktuelles-News/ | `…_113450.html`, rzadkie |
| Hunsrückbahn | https://www.hunsrueckbahn.de/de/neuigkeiten | struktura do sprawdzenia |
| Gemeinschaftsklinikum | https://www.gk.de/news-veranstaltungen/uebersicht/veranstaltungen/ | filtr „Boppard” |
| VRM – utrudnienia | https://www.vrminfo.de/fahrplan/fahrplaene/aktuelle-verkehrsmeldungen/ | |

## Tylko jako skróty („Nützliches”)
Sesselbahn, Tourist-Information, Museum, Stadthalle, VHS, Kino – już w `site.yaml`. Kandydaci: Burgtheater,
FamilienOrt, JBS, Mittelrhein-Klinik, Stiftung Bethesda, Geoportal, Ratsinfosystem.

## Nie pobieramy
Media komercyjne i agregatory (Rhein-Zeitung, Wochenspiegel, aktuell4u, Rhein-Hunsrück-Anzeiger, Rund um Boppard,
meinort, stadtm, meinestadt) – m.in. ze względu na niemieckie prawo pokrewne wydawców prasy. Facebook.
