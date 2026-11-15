# boppard-news

Statyczny serwis z lokalnymi wiadomościami z Boppard (Niemcy, nad Renem) – drugi serwis na tym samym kodzie co
`grodzisk-news`. Interfejs po niemiecku (`lang: de` w `site.yaml`, teksty w `i18n/de.yaml`).
GitHub Actions raz dziennie pobiera komunikaty ze źródeł publicznych i publikuje stronę na GitHub Pages.

## Pierwsze wdrożenie

1. Utwórz puste publiczne repo `maciejkfrankowski/boppard-news`.
2. Wypchnij kod:
   ```powershell
   git init -b main
   git add .
   git commit -m "init: Boppard lokal"
   git remote add origin https://github.com/maciejkfrankowski/boppard-news.git
   git push -u origin main
   ```
3. Settings → Pages → Source: **GitHub Actions**.
4. Actions → „Abrufen und veröffentlichen” → Run workflow.
5. Strona: `https://maciejkfrankowski.github.io/boppard-news/`; stan źródeł: `/quellen/`.

## Przed pokazaniem strony komukolwiek

W `site.yaml`, sekcja `operator`, uzupełnij adres pocztowy i e-mail – trafiają do Impressum i Datenschutzerklärung
(strony `/impressum/` i `/datenschutz/`). Teksty obu stron to szablony, nie porada prawna.

## Różnice względem grodzisk-news

- język: niemiecki; ścieżki: `/kategorie/`, `/artikel/`, `/raetsel/`, `/quellen/`;
- bez pogody i bez bloku kontaktowego (brak zapytań do serwerów trzecich na stronach dla czytelników);
- bez zdjęć i reklamy; link „Veranstaltungen” ukryty (`events_nav: false`) do czasu podpięcia kalendarzy;
- panel redakcji: `/admin/`, osobny token GitHuba z dostępem do tego repo (Contents: Read and write).

## Uruchomienie lokalne

```bash
pip install -r requirements.txt
python -m unittest discover -s tests
python -m gn.fetch && python -m gn.build
python -m http.server -d dist 8000
```

Dokumentacja: `CLAUDE.md`, `docs/01-architektura.md`, `docs/02-zrodla.md`.
