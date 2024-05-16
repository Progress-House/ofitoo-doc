# Specyfikacja wymagań dla Ofitoo

## 1. Wprowadzenie

**Cel dokumentu:**  
Dokument ma na celu zdefiniowanie wymagań funkcjonalnych i niefunkcjonalnych dla aplikacji Ofitoo.

**Zakres projektu:**  
Ofitoo-api (monorepo mikrousług dla backendu, java, spring-boot, spring jpa (hibernate), spring security, rabbit).
Ofitoo-mobile (aplikacja mobilna w typescript i react-native).
ofitoo-infra (pliki terraform, pliki dockerfile, kubernetes yaml i helm chart'y).
ofitoo-doc (dokumentacja techniczna, zbiór wymagań, dobre praktyki, ADR, proces biznesowy itp.).

**Kluczowi interesariusze:**
- wszyscy z zespołu ofitoo (developerzy, devopsi, QA, testerzy, product owner itd.)
- sponsorzy

## 2. Opis produktu

**Ogólny opis systemu:**  
Ofitoo to aplikacja mobilna do śledzenia spożycia kalorii, aktywności fizycznej, zdrowych nawyków i postępów fitness.

**Główne funkcje:**
- Rejestracja i logowanie użytkowników
- Dodawanie i zarządzanie posiłkami
- Śledzenie spożycia kalorii
- Śledzenie aktywności fizycznej
- Raportowanie i analizy

## 3. Wymagania funkcjonalne

### 3.1 Rejestracja i logowanie
- [ ] Użytkownik może się zarejestrować za pomocą adresu e-mail lub konta społecznościowego (np. Facebook, Google).
- [ ] Użytkownik może się zalogować za pomocą adresu e-mail i hasła.
- [ ] Użytkownik może się zalogować za pomocą adresu numeru telefonu

### 3.2 Dodawanie i zarządzanie posiłkami
- [ ] Użytkownik może dodawać posiłki poprzez wyszukiwanie w bazie danych za pomocą skanowania kodu kreskowego produktu,
    lub wpisując jego kod kreskowy ręcznie lub wpisując nazwe produktu lub tworząc swój własny produkt który będzie widoczny
tylko dla tej osoby i osób dodanych do "fit-friends", i również dla administratora który może opublikować produkt globalnie.
- [ ] Użytkownik może edytować i usuwać posiłki. W momencie kiedy zedytuje produkt publiczny stworzy się jego zedytowana kopia
z właścicielem jako osobą edytującą i oznaczone jako prywatne. W momencie edytowania produktu prywatnego gdzie właścicielem
jest ta sama osoba nie zostanie stworzona kopia produktu, tylko produkt zostanie nadpisany nowymi danymi.

### 3.3 Śledzenie spożycia kalorii
- [ ] Aplikacja automatycznie oblicza spożycie kalorii na podstawie dodanych posiłków.
- [ ] Użytkownik może ustawić cele kaloryczne.

### 3.4 Śledzenie aktywności fizycznej
- [ ] Użytkownik może dodawać aktywności fizyczne (np. bieganie, pływanie) i śledzić spalone kalorie.
- [ ] Aplikacja synchronizuje się z popularnymi trackerami fitness (np. Fitbit, Apple Health).

### 3.5 Raportowanie i analizy
- [ ] Aplikacja generuje codzienne, tygodniowe i miesięczne raporty dotyczące spożycia kalorii i aktywności.
- [ ] Użytkownik może przeglądać wykresy postępów.

## 4. Wymagania niefunkcjonalne

**Bezpieczeństwo:**
- [ ] Dane użytkowników muszą być przechowywane i przesyłane w sposób bezpieczny (szyfrowanie SSL/TLS).
- [ ] Hasła użytkowników muszą być hashowane.

**Skalowalność:**
- [ ] System powinien być łatwo skalowalny, aby obsłużyć rosnącą liczbę użytkowników.

## 5. Interfejsy użytkownika

**Makiety ekranów:**
- [ ] Ekran startowy - logo ofitoo
- [ ] Ekran rejestracji i logowania
- [ ] Ekran resetowania hasła
- [ ] Ekran tworzenia nowego konta - google
- [ ] Ekran tworzenia nowego konta - email / nr telefonu
- [ ] Ekran przeglądu (overview)
- [ ] Ekran dodawania / wyszukiwania posiłku
- [ ] Ekran śledzenia spożycia kalorii
- [ ] Ekran śledzenia aktywności fizycznej
- [ ] Ekran śledzenia zdrowych nawyków
- [ ] Ekran ustawień aplikacji

## 6. Kryteria akceptacji
- System musi przejść testy funkcjonalne i niefunkcjonalne.
- Aplikacja musi być zgodna z wymaganiami opisanymi w specyfikacji.
- Użytkownicy końcowi muszą zatwierdzić prototypy interfejsów użytkownika.

## 7. Załączniki
- scenariusze przypadków użycia
- Makiety ekranów

## Przykładowy przypadek użycia

**Nazwa:** Dodawanie posiłku

**Opis:** Użytkownik dodaje nowy posiłek do swojego dziennego dziennika.

**Aktorzy:** Użytkownik

**Scenariusz główny:**
1. Użytkownik otwiera aplikację i przechodzi do sekcji "Dodaj posiłek".
2. Użytkownik wyszukuje posiłek w bazie danych lub skanuje kod kreskowy.
3. Użytkownik wybiera posiłek i dodaje go do swojego dziennego dziennika.
4. Aplikacja aktualizuje dzienne spożycie kalorii.

**Alternatywne scenariusze:**
- Użytkownik nie znajduje posiłku w bazie danych i ręcznie wprowadza jego dane.
- Użytkownik anuluje dodawanie posiłku.