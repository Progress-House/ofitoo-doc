### Podstawowe funkcjonalności MVP

MVP (Minimum Viable Product) to nie jest gotowy produkt.   
Jest to wersja produktu z minimalnym zestawem funkcji, która pozwala na zdobycie pierwszych użytkowników i zebranie od nich opinii.   
Celem MVP jest przetestowanie pomysłu na produkt na rynku przy minimalnym nakładzie pracy i zasobów.   
Dopiero na podstawie feedbacku od użytkowników rozwija się pełny produkt.  

1. **Rejestracja i logowanie użytkowników**
    - Rejestracja nowego konta po adresie email.
      - Weryfikacja adresu e-mail poprzez link aktywacyjny.
    - Resetowanie zapomnianego hasła.
    - Logowanie za pomocą loginu / email i hasła. (JWT token)
    - Rejestracja i logowanie za pomocą (oAuth2):
      - Integracja z Google.
    - Profil użytkownika: 
      - Dane biometryczne (wiek, waga, wzrost, płeć) 
      - Cel (redukcja, masa, utrzymanie formy) 

2. **Baza danych produktów spożywczych**
    - Wyszukiwanie produktów publicznych, prywatnych, oraz znajomych za pomocą:
        - Kodu kreskowego.
        - Nazwy produktu.
        - Zdjęcia produktu (integracja z technologią AI, np. chatGPT).
        - (możliwość sortowania np po kaloriach rosnąco)
    - Możliwość dodania, edycji, usuwania produktów prywatnych:
        - Z opcjonalnym skanowaniem kodu kreskowego.

3. **Śledzenie spożycia kalorii**
    - Dodawanie, usuwanie i edycja posiłków w historii posiłków na podstawie produktów i ich gramatury (również znajomego z większymi uprawnieniami).
    - Automatyczne kalkulowanie spożytych kalorii i makroskładników.
    - Tworzenie templatów posiłków czyli listy produktów bez wpisanej gramatury.

4. **Śledzenie aktywności fizycznej**
    - Dodawanie, usuwanie, edycja ćwiczeń fizycznych i spalonych kalorii (również znajomego z większymi uprawnieniami).
    - Integracja z urządzeniami IoT (jedna integracja) 
    - Integracja z aplikacjami fitness (jedna integracja).

5. **Raporty i statystyki**
    - Tygodniowy, miesięczny, roczny przegląd aktywności, wagi, spożytych kalorii, mikroskładników.

6. **Społeczność**
    - Wysłanie zaproszenia do znajomych.
    - Dodawanie, usuwanie się ze znajomych.
    - Nadanie większych uprawnień (wgląd w kalorie, posiłki, statystyki edytowanie historii posiłków znajomego i aktywności).