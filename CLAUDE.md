# CLAUDE.md – zasady pracy w repo boppard-news

## Cel
Statyczny serwis lokalnych wiadomości i prostej rozrywki dla Boppard (Niemcy). Ten sam kod co `grodzisk-news`;
różni się konfiguracja (`site.yaml`, `sources.yaml`, `admin/config.yml`, `i18n/de.yaml`).
Etap: demo na darmowej infrastrukturze (GitHub Actions + Pages). Docelowo możliwa migracja na VPS.

## Zasady
- Dokumentacja i komunikaty po polsku; identyfikatory w kodzie po angielsku.
- Najpierw aktualizacja `docs/`, potem kod.
- Brak backendu: stan trzymamy w repo (`data/*.json`, `content/articles/*.md`).
- Wpisy zewnętrzne: tylko tytuł, krótki lead (≤220 znaków), data i link do źródła.
  Nie kopiujemy pełnych treści ani zdjęć. Mediów komercyjnych nie pobieramy.
- Każde źródło = wpis w `sources.yaml`. Nowy adapter tylko wtedy, gdy istniejące nie wystarczą.
- Paczki z poprawkami nie zawierają `data/`, `content/articles/` ani `static/img/uploads/` – to treść
  tworzona przez bota i redakcję w repo; paczka nadpisałaby ją starszą wersją.
- Adapter ma funkcję `parse(content, source) -> list[Item]` (testowalna offline) i `fetch(source)`.
- Błąd jednego źródła nie może przerwać przebiegu; wynik trafia do `data/status.json`.
- Linki w szablonach zawsze przez zmienną `root` (serwis działa w podkatalogu repo) i ścieżki z `p.*` (i18n).
- Żadnych tekstów interfejsu w szablonach ani JS – wszystko w `i18n/<lang>.yaml`.
- Strony dla czytelników nie ładują niczego z serwerów trzecich (RODO); wyjątkiem jest panel `/admin/`.
- Wygląd: wariant „Zielony Grodzisk” (zmienne w `:root` w `static/style.css`). Główny blok: zdjęcie artykułu
  z zielonym przyciemnieniem albo – bez zdjęcia – rysowana panorama `static/img/panorama.svg`.
  Kafelki bez zdjęć: pastel w kolorze kategorii. Zdjęcia podpisujemy polem `image_credit` („Fot. …”).
- Front bez frameworków i bez zewnętrznych bibliotek; JS w `static/app.js`.
- Przed commitem: `python -m unittest discover -s tests && python -m gn.build`.

## Mapa
| Ścieżka | Rola |
|---|---|
| `sources.yaml` | katalog źródeł |
| `site.yaml` | nazwa, kategorie, slot reklamowy, e-mail kontaktowy |
| `gn/fetch.py` | pobieranie + scalanie z `data/items.json` |
| `gn/fetchers/` | adaptery `rss`, `html_links`, `tribe_events`, klient HTTP |
| `gn/sudoku.py`, `static/sudoku.js` | generator i gra „Sudoku dnia” |
| `gn/build.py` | generator `dist/` |
| `templates/`, `static/` | szablony Jinja2, CSS, JS |
| `content/articles/` | własne artykuły (Markdown + YAML) |
| `content/krzyzowki/` | gotowe krzyżówki jako samodzielne pliki HTML |
| `admin/` | panel redakcji: Sveltia CMS (wersja przypięta w `index.html`), pola w `config.yml` |
| `.github/workflows/build.yml` | cron, commit danych, deploy Pages |

## Otwarte
- Uzupełnić `operator` w `site.yaml` (adres, e-mail) – Impressum i Datenschutz.
- Po pierwszym przebiegu sprawdzić `/quellen/` i poprawić wzorce `html_links`.
- Etap 2: kalendarze (Museum, Stadthalle, VHS, kino) → włączyć `events_nav`.
- Zmiany w kodzie wspólnym przenosić także do `grodzisk-news`.
