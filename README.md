# ORM w pigułce
- Narzędzie mające na celu upraszczać modelowanie baz danych
- W założeniu przeznaczone dla osób nietechnicznych
- Bardziej skomplikowane od problemu który rozwiązuje
- Łatwe do zrozumienia po przeczytaniu przystępnie napisanej 200-stronicowej książki
- Zerowe wsparcie (brak narzędzi, materiałów, dokumentacji)
- Zerowa popularność
- Wszystko i wszyscy mylą to z `Object-Relational Mapping`

# ORM

- **Instancja**
    - Podobne do konceptu instacji w programowaniu obiektowym
    - np. ***Janek*** jest instancją encji ***Student***
    - np. ***12*** jest instancją encji ***Wiek***

- **Typy obiektów**
    - **Encja** 
        - np. `Person`, `Car`, `Country`
        - Podobna koncepcyjnie do klasy w programowaniu obiektowym

        ![](imgs/encja.png "")

    - **Wartość** 
        - np. `Name`, `Number`, `Date`
        - Może być przypisana do tylko jednej encji
    
        ![](imgs/wartosc.png "")

- **Rola**
    - Jest przedstawiana przez pojedyńczy prostokącik będący częścią `predyktatu`
    - np. `Predykat` ***Uczeń ma Wiek*** zawiera dwie `role`
        - `Rolę` **posiadacza** która jest pełniona przez `encję` **Uczeń**
        - `Rolę` **posiadanego** która jest pełniona przez `encję` **Wiek**
    - np. `Predykat` ***Osoba prowadzi Samochód*** zawiera dwie `role`
        - `Rolę` **kierującego pojazdem** która jest pełniona przez `encję` **Osoba**
        - `Rolę` **pojazdu** która jest pełniona przez `encję` **Samochód**

    - `Instancja roli` powstaje, dopiero gdy konkretna `instancja encji lub wartości` uczestniczy w konkretnej `instancji predykatu`
        - np. w fakcie: ***Adam prowadzi Toyotę Yaris***
            - **Adam** jest `instancją encji` **Osoba**
            - **Adam** jest `instancją roli` **kierowcy pojazdu**
            - **Toyota Yaris** jest `instancją encji` **Samochód**
            - **Toyota Yaris** jest `instancją roli` **pojazd**

- **Predyktat**
    - `Predykat` to wyrażenie opisujące relacje między encjami
    - np. ***Osoba jest_palaczem*** to `predyktat` z **jedną** `rolą`
    - np. ***Osoba posiada Samochód*** to `predyktat` z **dwiema** `rolami`
    - np. ***Student zapisany na Kurs w Semestrze*** to `predyktat` z **N**-ilością `ról`

    ![](imgs/predyktat1.png "")\
    *Reprezentacja graficzna predyktatu*

    ![](imgs/predyktat2.png "")\
    *Reprezentacja graficzna predyktatu z opisem relacji*\
    *Napis to część predyktatu, ***nie jest*** relacją*

- **Relacja**
    - Jest to **instancja** `predyktatu` zachodząca pomiędzy dwiema **instancjami** `obiektu` *(obiekt to encja lub wartość)*
    - np. jeśli **Jan posiada Forda**, to jest to `relacja` między **Janem** *(instancja np. Osoby)* a **Fordem** *(instancja np. Auta)*

- **Identyfikatory**
    - Specjalny rodzaj wartości
    - Służy do odróżniania jednej instancji od innych w ramach tego samego typu obiektu
    - Jednoznacznie identyfikuje daną instancję obiektu
    - np. ***Osoba*** *identyfikowana przez* ***PESEL***

- **Skrót notacji dla identyfikatorów**
    - Parę `wartość` i `encja`, połączoną predyktatem, można zastąpić samą `encją`\
        ![](imgs/identyfikatory.png "")

    - **Gdy typ identyfikatora nie jest specificzny dla danej encji:**
        - np. **nazwę** może mieć wiele różnych encji *(nazwa produktu, nazwa kursu, nazwa lokalizacji)*
        - Na symbolu encji skrótowej, nazwa identyfikatora jest poprzedzona kropką
        - Nazwa wartości powstaje przez złączenie nazwy encji i nazwy identyfikatora
            - np. gdy skrótowa encja ma postać: **Produkt (.Nazwa)** to nazwa wartości to **ProduktNazwa**
            - np. gdy skrótowa encja ma postać: **Kurs (.Nazwa)** to nazwa wartości to **KursNazwa**
            - np. gdy skrótowa encja ma postać: **Lokalizacja (.Nazwa)** to nazwa wartości to **LokalizacjaNazwa**

    - **Gdy wartość to jednostka**
        - np. jednostki układu SI, pieniężne, itp.
        - Na symbolu encji skrótowej, nazwa identyfikatora jest zakończona dwukropkiem
        - Nazwa wartości powstaje przez złączenie skrótu jednostki i nazwy
            - np. gdy skrótowa encja ma postać: **Produkt (kg:)** to nazwa wartości to **kgValue**
            - np. gdy skrótowa encja ma postać: **Kurs (PLN:)** to nazwa wartości to **PLNValue**
            - np. gdy skrótowa encja ma postać: **Lokalizacja (km:)** to nazwa wartości to **kmValue**
        - Można dodać informację o typie jednostki
            - np. `Produkt (kg:Masa)`, `Kurs (PLN:Pieniądze)`, `Lokalizacja (km:Długość)`, itp.

    - **Gdy typ identyfikatora jest specyficzny dla danej encji**
        - np. tylko **książki** mają **ISBN**
        - Nazwa wartości jest taka sama jak nazwa identyfikatora
            - np. gdy skrótowa encja ma postać: Książka (ISBN) to nazwa wartości to ISBN
            - np. gdy skrótowa encja ma postać: Student (NrIndexu) to nazwa wartości to NrIndexu

- **Ograniczenie unikatowości**
    - Jest przedstawione jako linią nad jedną lub wieloma rolami
    - Mówi że dana `instancja roli` lub kombinacja `instancji ról` może wystąpić jedynie raz
        - np. nie mogą istnieć dwa produkty o tej samej nazwie
        - np. nie może być dwóch studentów identyfikowanych tym samym numerem indexu na danym kursie

- **Ograniczenie obowiązkowości**:
    - Określa czy dana encja musi pełnić daną roli
        - np. każdy **Pracownik** ma **PracownikID**
    - Brak symbolu oznaczna brak wymogu udziału w danej roli
    - Wymóg udziału w danej roli oznaczany jest symbolem kropki ustawionej na lini łączącej encję z rolą

- **Ograniczenie ilości**:
    - Określa ile razy instancja danej encji może odegrać daną rolę
        - np. **Zamówienie** ma przynajmniej jeden **Produkt**
        - np. **Drużyna** ma dokładnie 5 **Graczy**

- **Ogranicznie wartości**:
    - Określa jakie wartości mogą przyjmować instancje obiektów typu wartość
        - np. **Wiek** musi być w zakresie od 0 do 120
        - np. **Płeć** to jedno z M, F, lub O

- **Ograniczenia zbiorów**:
    - Określa relację pomiędzy populacjami ról lub populacjami obiektów
        - np. Każdy **Kierowca** to **Pracownik**
        - np. **Osoba** nie może być jednocześnie **Uczniem** i **Nauczycielem**
        - np. **Uczeń** jest **Ubezpieczony**