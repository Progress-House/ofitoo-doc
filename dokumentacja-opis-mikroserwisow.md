# Dokumentacja Projektu

oFitoo to innowacyjna aplikacja mobilna, stworzona z myślą o dbaniu o zdrowie, 
monitorowaniu żywienia i osiąganiu celów związanych z dietą i aktywnością fizyczną. 
Aplikacja łączy w sobie najlepsze cechy popularnych rozwiązań takich jak MyFitnessPal i Fitatu, jednocześnie oferując prostote i możliwość odłączenia zbędnych dla nas modułów.

**Główne funkcje oFitoo to:**
* **Śledzenie Spożytych Kalorii:** 
_Monitoruj codziennie spożyte kalorie, makroskładniki i mikroskładniki, aby utrzymywać kontrolę nad swoją dietą._
* **Planowanie Posiłków:** 
_Twórz spersonalizowane plany żywieniowe dostosowane do Twoich celów i preferencji._
* **Skanowanie Kodów Kreskowych:** 
_Dodawaj produkty spożywcze do swojego dziennika żywieniowego szybko i łatwo, skanując ich kody kreskowe._
* **Statystyki i Wykresy:** 
_Otrzymuj wykresy i statystyki, które pomagają Ci monitorować postępy i osiągać cele._
* **Społeczność i Motywacja:** 
_Pozwól swojemu partnerowi na edycje twoich posiłków ułatwiając sledzenie posiłków oraz sledzenie osiągów._

## Ogólne zalecenie architektoniczne
* **Izolacja**
Każdy mikroserwis powinien być w stanie funkcjonować niezależnie, z własną bazą danych, co ułatwia zarządzanie, rozwój i skalowanie serwisu.
* **Bezpieczeństwo**
Zapewnienie bezpieczeństwa na poziomie każdej bazy danych, w tym szyfrowanie danych w spoczynku i w transmisji, regularne backupy.
* **Migracje i Wersjonowanie**
Utrzymywanie skryptów migracji dla każdej bazy danych, aby łatwo zarządzać zmianami schematu i ułatwić deployment nowych wersji serwisów.

## Architektura Microserwisów
## 1. user-service
- Autentykacja i zarządzanie profilami użytkowników.
- Aktualizacja danych biometrycznych: data-urodzin, wzrost, waga, płeć.
- Generowanie tokenów JWT (o ile nie będzie tego robił Keycloak).
- Zarządzanie sesjami (o ile nie będzie tego robił Keycloak).
* **Baza Danych**
  PostgreSQL lub inna relacyjna baza danych dla zarządzania danymi użytkowników, które mogą wymagać transakcyjności i spójności, takich jak informacje o koncie, historii logowań.
* **Cel**
  Bezpieczne przechowywanie danych użytkowników, wsparcie dla złożonych zapytań związanych z autentykacją i zarządzaniem profilami.

## 2. product-service
- Wyszukiwanie produktów na podstawie kodów kreskowych lub nazwy produktu.
- Dodawanie nowych produktów.
- Aktualizacja informacji o produktach (nie wymagane pola takie jak kaloryczność na produkt oraz na 100 gram, tłuszcze, węglowodany, białko, błonnik).
- Możliwość zgłaszania nieprawidłowości w produktach.
* **Baza Danych**
Może używać NoSQL takiego jak MongoDB dla elastyczności schematu, co ułatwi przechowywanie różnorodnych danych o produktach, w tym kodów kreskowych, składników, wartości odżywczych.
* **Cel**
Szybkie wyszukiwanie produktów, łatwa aktualizacja i dodawanie nowych produktów.

## 3. calorie-tracking-service
- Śledzenie spożywanych posiłków.
- Obliczanie spożytych kalorii i składników odżywczych.
- Monitorowanie postępów.
* **Baza Danych**
Może korzystać z relacyjnej bazy danych jak PostgreSQL dla przechowywania informacji o posiłkach i spożyciu, ponieważ dane te często są strukturalne i zależne od relacji.
* **Cel**
Efektywne zarządzanie dziennikami spożycia, obsługa zapytań agregujących dla raportowania i analiz.

## 4. habits-tracker-service
- Umożliwienie użytkownikom ustawianie własnych nawyków w formie listy do zrobienia.
- Monitorowanie realizacji celów, powiadamianie przypominkami.
* **Baza Danych**
Relacyjna baza danych tak jak MySQL, idealna do przechowywania rzeczy do zrobienia i postępów użytkowników, które są ściśle powiązane z danymi użytkownika i posiłkami.
* **Cel**
Monitorowanie osiągnięć użytkowników, zarządzanie celami.

# 4. notification-service
- Umożliwienie wysyłanie smsów i emaili. 
- Nasłuchuje na kolejce rabbitMQ i asynchronicznie wysyła wiadomości.

## 7. Gateway API
- Agregacja żądań do mikroserwisów.
- Zarządzanie endpointami, autoryzacja żądań.
* **Baza Danych**
Redis lub inna baza danych typu klucz-wartość do szybkiego cache'owania danych sesji, tokenów JWT, limitów zapytań oraz tymczasowych danych o błędach.
* **Cel**
Zwiększenie wydajności przez redukcję czasu dostępu do często używanych danych, zarządzanie rate limit.

## 8. Frontend Mobilny
- Komunikacja z mikroserwisami przez API.
- Skanowanie kodów kreskowych.
- Dodawanie posiłków, ustawianie celów, przeglądanie wykresów.

## Dodatkowe Elementy do Wdrożenia
- Kolejka Komunikatów: RabbitMQ do asynchronicznej komunikacji między mikroserwisami, przetwarzanie zadań w tle.
- Logowanie i Monitorowanie: Prometheus + Grafana/Kibana dla logowania i monitorowania działania mikroserwisów.
- Zarządzanie Błędami i Zabezpieczenia: Implementacja zabezpieczeń przed atakami, takimi jak SQL Injection, XSS, zapewnienie odporności na błędy. NeuVector.
- Dokumentacja API: Stworzenie dokumentacji API z wykorzystaniem Swagger lub OpenAPI dla łatwiejszego zarządzania i integracji.
- Projektowanie Schematów Bazy Danych: Określenie modeli danych dla produktów, użytkowników, posiłków, celów.
- Konfiguracja Środowiska Deweloperskiego: Ustawienie lokalnego środowiska dla rozwoju mikroserwisów, w tym bazy danych, kolejki komunikatów.
- Konfiguracja Kubernetesa:
    - Utworzenie środowisk
        - developerskich (Dev
