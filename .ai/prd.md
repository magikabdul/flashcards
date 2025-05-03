# Dokument wymagań produktu (PRD) - FlashLearn

## 1. Przegląd produktu
FlashLearn to aplikacja webowa umożliwiająca szybkie tworzenie, przeglądanie i powtarzanie zestawów fiszek edukacyjnych. Użytkownicy mogą wklejać dowolny tekst do 20 000 znaków lub ręcznie tworzyć fiszki, a system generuje kandydatów fiszek za pomocą AI. Zaakceptowane fiszki są przechowywane w koncie użytkownika i wykorzystywane w sesjach powtórek z wykorzystaniem otwartoźródłowego algorytmu.

## 2. Problem użytkownika
Ręczne przygotowywanie fiszek jest czasochłonne i zniechęca do korzystania z efektywnej metody nauki opartej na powtórkach rozłożonych w czasie. Użytkownicy potrzebują narzędzia, które automatycznie przekształci notatki i fragmenty tekstu w gotowe fiszki, przy zachowaniu kontroli nad ich zawartością.

## 3. Wymagania funkcjonalne
1. wklejenie czystego tekstu (max 20 000 znaków) i wysłanie żądania generowania fiszek przez AI  
2. wyświetlenie listy kandydatów fiszek generowanych przez AI z dwoma polami: front (max 200 znaków) i back (max 500 znaków)  
3. modalne okno do edycji, akceptacji lub odrzucenia każdego kandydata fiszki  
4. ręczne tworzenie nowych fiszek korzystające z tego samego modelu danych  
5. lista zaakceptowanych fiszek z możliwością przeglądania, edycji i usuwania  
6. progress bar pokazujący postęp generowania całego zbioru fiszek  
7. prosty system kont użytkowników (rejestracja i logowanie e-mail + hasło)  
8. uruchamianie sesji powtórek z wykorzystaniem wybranej biblioteki open-source  
9. rejestrowanie zdarzeń generate_requested, card_accepted, card_rejected, card_edited  

## 4. Granice produktu
W zakres MVP wchodzą: generowanie kandydatów fiszek przez AI, manualne tworzenie i zarządzanie fiszkami, system kont użytkowników, progress bar, integracja z algorytmem powtórek. Do MVP nie wchodzą: własny algorytm powtórek, import wielu formatów plików, współdzielenie zestawów między użytkownikami, integracje z platformami zewnętrznymi, aplikacje mobilne.

## 5. Historyjki użytkowników

- ID: FLCDS-010  
  Tytuł: rejestracja konta  
  Opis: nowy użytkownik zakłada konto, podając e-mail i hasło  
  Kryteria akceptacji:  
  1. formularz rejestracji wyświetla pola e-mail i hasło  
  2. przy poprawnych danych konto jest tworzone, użytkownik zostaje zalogowany  
  3. przy niepoprawnym formacie e-mail lub za krótkim haśle wyświetlany jest błąd

- ID: FLCDS-011  
  Tytuł: logowanie użytkownika  
  Opis: zarejestrowany użytkownik loguje się za pomocą e-maila i hasła  
  Kryteria akceptacji:  
  1. formularz logowania wyświetla pola e-mail i hasło  
  2. przy poprawnych danych użytkownik zostaje zalogowany i przekierowany do pulpitu  
  3. przy niepoprawnych danych wyświetlany jest komunikat o błędnych danych

- ID: FLCDS-012  
  Tytuł: wprowadzenie tekstu i żądanie generowania fiszek  
  Opis: zalogowany użytkownik wkleja czysty tekst <= 20 000 znaków i wysyła prośbę o wygenerowanie fiszek  
  Kryteria akceptacji:  
  1. pole tekstowe przyjmuje maksymalnie 20 000 znaków  
  2. kliknięcie przycisku „Generuj fiszki” inicjuje żądanie do serwisu AI  
  3. progress bar wskazuje postęp generowania

- ID: FLCDS-013  
  Tytuł: przegląd kandydatów fiszek AI  
  Opis: użytkownik widzi listę wygenerowanych kandydatów z polami front i back  
  Kryteria akceptacji:  
  1. lista pokazuje wszystkie wygenerowane kandydaty z ograniczeniem znaków  
  2. obok każdego kandydata dostępne są przyciski akceptuj, edytuj, odrzuć

- ID: FLCDS-014  
  Tytuł: akceptacja kandydata fiszki  
  Opis: użytkownik zatwierdza wygenerowaną fiszkę jako ostateczną  
  Kryteria akceptacji:  
  1. kliknięcie „akceptuj” przenosi fiszkę do listy zaakceptowanych  
  2. zdarzenie card_accepted jest wysyłane do systemu analitycznego

- ID: FLCDS-015  
  Tytuł: edycja kandydata fiszki  
  Opis: użytkownik modyfikuje front lub back fiszki w modalnym oknie przed akceptacją  
  Kryteria akceptacji:  
  1. modal otwiera się z polami front i back wypełnionymi istniejącą treścią  
  2. zapisanie zmian aktualizuje zawartość fiszki i wysyła zdarzenie card_edited

- ID: FLCDS-016  
  Tytuł: odrzucenie kandydata fiszki  
  Opis: użytkownik odrzuca niepożądaną fiszkę  
  Kryteria akceptacji:  
  1. kliknięcie „odrzuć” usuwa fiszkę z listy kandydatów  
  2. zdarzenie card_rejected jest wysyłane do systemu analitycznego

- ID: FLCDS-017  
  Tytuł: ręczne tworzenie fiszki  
  Opis: użytkownik tworzy nową fiszkę, wpisując front i back od podstaw  
  Kryteria akceptacji:  
  1. dostępne są pola do wpisania front (max 200 znaków) i back (max 500 znaków)  
  2. po zapisaniu fiszka pojawia się na liście zaakceptowanych

- ID: FLCDS-018  
  Tytuł: zarządzanie zaakceptowanymi fiszkami  
  Opis: użytkownik przegląda, edytuje lub usuwa fiszki ze swojej kolekcji  
  Kryteria akceptacji:  
  1. lista zaakceptowanych fiszek wyświetla front i back dla każdej  
  2. przy każdej fiszce dostępne są przyciski edycji i usunięcia  
  3. edycja otwiera modalne okno aktualizacji i wysyła card_edited, usunięcie usuwa rekord

- ID: FLCDS-019  
  Tytuł: wyświetlenie progress bar  
  Opis: użytkownik widzi pasek postępu przy generowaniu fiszek z AI  
  Kryteria akceptacji:  
  1. progress bar pojawia się po rozpoczęciu procesu generowania  
  2. pasek odpowiada procentowemu postępowi zwróconemu przez serwis AI  
  3. po zakończeniu generowania pasek znika lub wskazuje 100%

- ID: FLCDS-020  
  Tytuł: rozpoczęcie sesji powtórek  
  Opis: użytkownik rozpoczyna sesję powtórek według algorytmu open-source  
  Kryteria akceptacji:  
  1. przycisk „Rozpocznij powtórki” uruchamia sesję z zaakceptowanymi fiszkami  
  2. fiszki wyświetlane są sekwencyjnie zgodnie z harmonogramem  
  3. logika powtórek działa zgodnie z zintegrowaną biblioteką

## 6. Metryki sukcesu
- 75% wygenerowanych fiszek akceptowanych przez użytkowników  
- 75% wszystkich tworzonych fiszek pochodzi z generowania AI  
- uptime systemu ≥ 99% w skali miesiąca  
- monitorowanie czasów odpowiedzi usługi AI i liczby eventów w pipeline analitycznym  