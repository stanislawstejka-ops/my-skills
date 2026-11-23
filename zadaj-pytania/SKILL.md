---
name: zadaj-pytania
description: "Testuj wiedzę z PDF-owych notatek quizem, lukami, miksem lub formą wskazaną przez użytkownika."
argument-hint: "[ścieżka do PDF lub dołączony PDF]"
user-invocable: true
disable-model-invocation: true
---

# Zadaj pytania

## Cel

Przetestuj wiedzę użytkownika wyłącznie na podstawie informacji z podanego pliku PDF z notatkami. Prowadź sesję pytanie po pytaniu, sprawdzaj odpowiedzi i planuj późniejsze powtórki pytań, na które użytkownik odpowiedział błędnie.

## Przebieg

1. Najpierw ustal formę testu.
   - Jeśli użytkownik nie wskazał formy jawnie, wywołaj `ask_user` z jednym pytaniem i jednym polem pojedynczego wyboru:
     - tytuł: `Forma testu`;
     - pole: `Jaką formę testu wybierasz?`;
     - typ pola: `string`;
     - opcje w tej kolejności: `Quiz — 3-4 odpowiedzi, jedna poprawna`, `Tekst z lukami`, `Mix quizu i luk`, `Własna forma`;
     - nie ustawiaj wartości domyślnej, aby żadna opcja nie była wstępnie wybrana.
   - Po wywołaniu `ask_user` natychmiast zakończ turę i czekaj na wybór użytkownika.
   - Jeśli `ask_user` zwróci błąd „user is not available” lub wskaże, że narzędzie jest niedostępne:
     - nie wybieraj `pragmatic`, pierwszej opcji ani innej wartości;
     - nie kontynuuj testu;
     - wyświetl jeden blok z pytaniem i czterema numerowanymi opcjami, po czym zakończ turę:

       ```text
       Jaką formę testu wybierasz?

       1. Quiz — 3-4 odpowiedzi, jedna poprawna
       2. Tekst z lukami
       3. Mix quizu i luk
       4. Własna forma
       ```

   - W tej turze nie wykonuj żadnej innej akcji: nie czytaj PDF, nie przeglądaj plików, nie uruchamiaj testów, nie generuj pytań i nie pisz podsumowania.
   - Nie wywołuj narzędzia zakończenia zadania i nie dodawaj nagłówka, znacznika ani szablonu `Task completed`.
   - Nie powtarzaj listy w dodatkowych blokach, wyjaśnieniach ani komentarzach.
   - Nie wybieraj formy za użytkownika, nie używaj odpowiedzi `pragmatic` ani innej wartości domyślnej.
   - Jeśli forma została jawnie wskazana w tym samym komunikacie, przejdź dalej bez ponownego pytania.
2. Sprawdź, czy użytkownik podał plik PDF.
   - Jeśli nie, poproś o jego dołączenie albo podanie ścieżki.
   - Jeśli PDF jest niedostępny, nieczytelny albo składa się głównie z zeskanowanego obrazu, którego nie da się odczytać, jasno opisz problem i poproś o wersję tekstową lub czytelną.
3. Odczytaj notatki i wydobądź z nich fakty, definicje, zależności, sekwencje, przykłady oraz inne treści nadające się do sprawdzenia.
   - Nie korzystaj z wiedzy spoza materiału jako źródła poprawnych odpowiedzi.
   - Jeśli informacje w PDF są niejasne lub sprzeczne, zaznacz to zamiast zgadywać.
4. Przygotuj pulę pytań obejmującą różne ważne fragmenty notatek.
   - Jeśli użytkownik nie ustalił długości sesji, przyjmij 10 pytań.
   - Zwykle zadawaj jedno pytanie naraz.
   - Nie ujawniaj poprawnej odpowiedzi, wyjaśnienia ani podpowiedzi przed odpowiedzią użytkownika.
   - W trybie `quiz` losowo zmieniaj pozycję poprawnej odpowiedzi i stosuj wiarygodne dystraktory, oparte na treści notatek.
   - W trybie `luki` usuwaj tylko takie słowa lub wyrażenia, które można jednoznacznie ustalić z materiału.
5. Po odpowiedzi oceń ją od razu:
   - `Poprawna odpowiedź.` — krótko potwierdź, a gdy warto, dodaj jedno krótkie uzasadnienie.
   - `Błędna odpowiedź.` — podaj poprawną odpowiedź i krótkie wyjaśnienie oparte na notatkach.
6. Prowadź stan sesji:
   - oznacz odpowiedzi jako poprawne lub błędne;
   - dodawaj każde błędnie rozwiązane pytanie do kolejki powtórek;
   - błędnego pytania nie zadawaj ponownie bezpośrednio po pokazaniu poprawnej odpowiedzi;
   - przed powtórką zadaj co najmniej dwa inne pytania;
   - jeśli materiał nie zawiera dwóch innych pytań, oznacz powtórkę jako zadanie na następną sesję;
   - przy powtórce zmień sformułowanie pytania albo kolejność odpowiedzi, zachowując ten sam cel sprawdzania.
7. Zakończ sesję po zadaniu uzgodnionej liczby pytań głównych i jednej odroczonej powtórki każdego pytania, na które użytkownik odpowiedział błędnie. Pytania nadal błędne po powtórce zachowaj do kolejnej sesji, chyba że użytkownik jawnie poprosi o dalszą powtórkę teraz. Na koniec podaj:
   - liczbę odpowiedzi poprawnych, błędnych i powtórzonych;
   - tematy opanowane;
   - tematy wymagające dalszej nauki;
   - propozycję kolejnej krótkiej sesji.

## Obsługa własnej formy

Jeśli użytkownik wybierze własną formę, najpierw upewnij się, że rozumiesz jej zasady. Ustal co najmniej:

- jak ma wyglądać pytanie;
- jak użytkownik ma odpowiedzieć;
- kiedy odpowiedź uznać za poprawną;
- czy dopuszczalne są częściowe punkty.

Po doprecyzowaniu stosuj tę formę konsekwentnie przez całą sesję.

## Kryteria jakości

- Każde pytanie wynika z treści PDF.
- Każda poprawna odpowiedź da się potwierdzić w notatkach.
- W quizie występuje 3-4 odpowiedzi i dokładnie jedna jest poprawna.
- Informacja zwrotna jest jednoznaczna, uczciwa i krótka.
- Po błędnej odpowiedzi użytkownik poznaje poprawną odpowiedź oraz uzasadnienie.
- Błędne pytanie wraca dopiero po innych pytaniach.
- Nie ujawniaj zbiorczej listy pytań i odpowiedzi przed ich zadaniem.
- Nie twierdź, że odczytano PDF, jeśli plik nie jest dostępny lub treść jest nieczytelna.
