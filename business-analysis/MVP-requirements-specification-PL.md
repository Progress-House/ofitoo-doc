# Specyfikacja wymagań dla MVP - Ofitoo

![img.png](../ofitoo-logo.png)


| **Wersja dokumentu** | **Ostatnia aktualizacja** | **autor**     |
|----------------------|---------------------------|---------------|
| 0.3                  | 21 czerwca 2024           | mcblankenburg |

## 1. Wprowadzenie
**Cel dokumentu:**  
Dokument ma na celu zdefiniowanie wymagań funkcjonalnych i niefunkcjonalnych dla aplikacji Ofitoo.

**Zakres projektu:**  
Ofitoo-api (monorepo mikrousług dla backendu, java, spring-boot, spring jpa (hibernate), spring security, rabbit).
Ofitoo-mobile (aplikacja mobilna w typescript i react-native).
ofitoo-infra (pliki terraform, pliki dockerfile, kubernetes yaml i helm chart'y).
ofitoo-doc (dokumentacja techniczna, zbiór wymagań, dobre praktyki, ADR, proces biznesowy itp.).
ofitoo-frontend (aplikacja webowa w typescript i react).

**Kluczowi interesariusze:**
- wszyscy z zespołu ofitoo (developerzy, devopsi, QA, testerzy, product owner itd.)
- sponsorzy


## 2. Opis produktu
**Ogólny opis systemu:**  
Ofitoo to aplikacja mobilna do śledzenia spożycia kalorii, aktywności fizycznej, zdrowych nawyków i postępów fitness.

**Główne funkcje:**
- Rejestracja i logowanie użytkowników
- Dodawanie i zarządzanie posiłkami oraz produktami
- Śledzenie spożycia kalorii
- Śledzenie aktywności fizycznej
- Raportowanie i analizy
- Społeczność

## 3.2. Stos Technologiczny:
- **UI/UX Design:** Figma  
- **Mobile:** React Native, Typescript, TailwindCSS, Vite, Expo  
- **Frontend:** React, TailwindCSS, Vite
- **Backend:** Java 21, spring boot, hibernate, message-broker (rabbit or other)  
- **Baza danych:** MongoDB, PostgreSQL  
- **Autentykacja:** JWT, OAuth2 (facebook, google)  
- **Konteneryzacja, Orkiestracja i Intrastruktura:** Docker/Podman, Kubernetes (GCP), Terraform
- **CI/CD:** GitHub Action  
- **Monitoring:** Prometheus, Grafana  


## 4. Wymagania funkcjonalne
### Podstawowe funkcjonalności MVP

MVP (Minimum Viable Product) to nie jest gotowy produkt.   
Jest to wersja produktu z minimalnym zestawem funkcji, która pozwala na zdobycie pierwszych użytkowników i zebranie od nich opinii.   
Celem MVP jest przetestowanie pomysłu na produkt na rynku przy minimalnym nakładzie pracy i zasobów.   
Dopiero na podstawie feedbacku od użytkowników rozwija się pełny produkt.

**Rejestracja i logowanie użytkowników**
  - Rejestracja nowego konta po adresie email.
    - Weryfikacja adresu e-mail poprzez link aktywacyjny.
  - Resetowanie zapomnianego hasła.
  - Logowanie za pomocą loginu / email i hasła. (JWT token)
  - Rejestracja i logowanie za pomocą (oAuth2):
    - Integracja z Google.
  - Profil użytkownika:
    - Dane biometryczne (wiek, waga, wzrost, płeć)
    - Cel (redukcja, masa, utrzymanie formy)

**Baza danych produktów spożywczych**
  - Sortowania wyświetlanych produktów (opcje: public first, private first, low kcal first, the most used first).
  - Wyszukiwanie produktów publicznych, prywatnych, oraz znajomych za pomocą:
    - Kodu kreskowego.
    - Nazwy produktu.
    - Zdjęcia produktu (integracja z technologią AI, np. chatGPT).
    - (możliwość sortowania np po kaloriach rosnąco)
  - Dodanie, edycja, usuwanie produktów prywatnych:
    - Z opcjonalnym skanowaniem kodu kreskowego.
    - //TODO (GRUBSZA ROZKMINA) Edytowania produktów publicznych lub znajomych:
    - //TODO (GRUBSZA ROZKMINA) Dane edytowanego produktu (publicznego lub znajomego) zostają skopiowane i na jego podstawie tworzony jest nowy produkt prywatny który przed zapisem może zostać zmieniony.
    - //TODO (GRUBSZA ROZKMINA) Jeśli edytowany produkt został użyty w historii posiłków użytkownika, musi zdecydować czy zmiana ma dotyczyć również przeszłych wpisów.
      - jeśli nie, należy stworzyć nowy produkt o innym id, a stary produkt oznaczyć "old"
      - jeśli tak, należy

**Śledzenie spożycia kalorii**
  - Dodawanie, usuwanie i edycja posiłków w historii posiłków na podstawie produktów i ich gramatury (również znajomego z większymi uprawnieniami).
  - Automatyczne kalkulowanie spożytych kalorii i makroskładników.
  - Tworzenie templatów posiłków czyli listy produktów bez wpisanej gramatury.

**Śledzenie aktywności fizycznej**
  - Dodawanie, usuwanie, edycja ćwiczeń fizycznych (pływanie, bieganie itd) i spalonych kalorii (również znajomego z większymi uprawnieniami).
  - Integracja z urządzeniami IoT (jedna integracja)
  - Integracja z aplikacjami fitness (jedna integracja).

**Raportowanie i statystyki**
  - Tygodniowy, miesięczny, roczny przegląd aktywności, wagi, spożytych kalorii, mikroskładników.

**Społeczność**
  - Wysłanie zaproszenia do znajomych.
  - Dodawanie, usuwanie się ze znajomych.
  - Nadanie większych uprawnień (wgląd w kalorie, posiłki, statystyki edytowanie historii posiłków znajomego i aktywności).


## 5. Wymagania niefunkcjonalne
**Bezpieczeństwo:**
- Wszystkie dane przesyłane między aplikacją (mobile, frontend) a serwerem (backend) muszą być szyfrowane (SSL/TLS).
- Hasła użytkowników muszą być hashowane.
- Użytkownicy muszą być uwierzytelniani za pomocą JWT lub OAuth2.

**Skalowalność:**
- System powinien być łatwo skalowalny, aby obsłużyć rosnącą liczbę użytkowników.
- Architektura musi umożliwiać łatwe dodawanie nowych funkcjonalności w różnych wersjach bez wpływu na istniejące usługi.
- Czas odpowiedzi aplikacji nie powinien przekraczać 3 sekund dla większości operacji.
- Aplikacja powinna działać płynnie na urządzeniach z IOS i Android.

**Utrzymywalność**  
- System powinien być stworzony w technologiach popularnych i zalecanych na rynku pracy branży IT.
- System jako całość powinien być stworzony z podobnych, synergicznych technologii pozwalając na efektywne wykorzystanie zasobów ludzkich.
- System powinien w miare możliwości używać najnowszych wersji użytych technologii z wyłączeniem wersji canary/beta itd.