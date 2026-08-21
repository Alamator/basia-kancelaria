# Strona kancelarii — Barbara Gradowska-Koprowska

Statyczna strona kancelarii adwokackiej (adwokat + stały mediator, Toruń).
Czysty HTML/CSS/JS, bez frameworków. Jedyna zależność zewnętrzna to Google Fonts
(Cormorant Garamond + Jost). Docelowa domena: **https://gradowska-koprowska.pl/**

Produkcja na `main` pozostaje wersją v1. Ta linia (preview / PR) to **wersja v2**:
pozycjonowanie na podział majątku wspólnego i mediacje majątkowe, osobna strona
`podzial-majatku.html`, poprawiony NAP (`33/2, 87-100`), bez obietnic wyniku (KEA).

## Struktura plików

```
index.html                  ← strona główna
podzial-majatku.html        ← podział majątku wspólnego (treść informacyjna)
polityka-prywatnosci.html   ← polityka prywatności (RODO) — DRAFT do akceptacji
styles.css                  ← wspólny system wizualny (gold/ink, te same fonty)
favicon.svg                 ← znak „§" w zieleni #2E6B3E
robots.txt                  ← allow all + wskazanie sitemap
sitemap.xml                 ← strona główna, podział majątku, polityka
assets/
  foto.jpg      ← zdjęcie hero/portret (B&W; nie kolorować)
  foto-about.jpg
  foto-og.jpg   ← obraz Open Graph 1200×630
  foto.png      ← oryginał (źródło; nie jest linkowany na stronie)
  adwokat_59716.pdf ← zaświadczenie wpisu na listę Izby Adwokackiej (link w stopce)
```

## Przed publikacją — checklist

1. **Klucz Web3Forms (formularz kontaktowy)** — patrz niżej. Bez tego formularz nie wyśle wiadomości.
2. **Akceptacja polityki prywatności** — plik `polityka-prywatnosci.html` ma na górze komentarz
   `<!-- DRAFT -->`. Basia musi przeczytać i zaakceptować treść; po akceptacji usunąć komentarz DRAFT
   oraz box „Projekt dokumentu" z sekcji nagłówka.
3. (Opcjonalnie) sprawdzić poprawność danych: adres, NIP 879-122-92-16, REGON 871710282,
   numer wpisu TOR/Adw/109.

## Formularz (Web3Forms)

Formularz używa darmowej usługi [web3forms.com](https://web3forms.com) (limit 250 zgłoszeń/mies.).
Klucz dostępu jest już wpisany w `index.html` (pole `access_key`) i powiązany na stałe
z adresem odbiorcy. Zmiana adresu odbiorcy = wygenerowanie nowego klucza na web3forms.com
i podmiana wartości `access_key`.

Temat maili ustawiony jest na „Nowe zapytanie ze strony kancelarii".
Jeśli maile nie dochodzą — sprawdź folder SPAM na skrzynce kancelarii.

## Deploy (GitHub → Vercel → domena home.pl)

1. **GitHub** — utwórz repozytorium i wgraj całą zawartość katalogu (`index.html`, `assets/`, itd.).
2. **Vercel** — zaloguj się na https://vercel.com, wybierz *Add New → Project → Import*
   i wskaż repozytorium z GitHuba. To strona statyczna, więc:
   - Framework Preset: **Other**
   - Build Command: *puste*
   - Output Directory: *puste* (root repozytorium)
   Kliknij **Deploy**. Vercel wystawi stronę pod adresem `*.vercel.app`.
3. **Domena** — w Vercel: *Project → Settings → Domains* dodaj `gradowska-koprowska.pl`
   oraz `www.gradowska-koprowska.pl`.
4. **DNS w panelu home.pl** (rekordy dla domeny):
   - **A** `@` → `76.76.21.21`
   - **CNAME** `www` → `cname.vercel-dns.com`
   - **MX** — **bez zmian** (poczta kancelarii zostaje na home.pl; nie ruszaj rekordów pocztowych).
5. Odczekaj na propagację DNS (do kilku–kilkunastu godzin) i sprawdź, czy strona
   otwiera się pod właściwą domeną z certyfikatem HTTPS (Vercel wystawia go automatycznie).

## Uwagi techniczne

- Brak analityki i cookies śledzących (świadomie — zgodne z polityką prywatności).
- Zdjęcie zoptymalizowane skryptem Pillow (900 px, quality 82, progressive) — z ~1,58 MB do ~110 KB.
- Formularz: honeypot antyspamowy + wymagana zgoda RODO + font inputów 16 px (brak zoomu na iOS).
- Dane merytoryczne o kancelarii pochodzą wprost od klientki (treści kanoniczne) — przy edycji
  nie dopisywać własnych obietnic wyniku ani statystyk (zakaz etyczny KEA).
