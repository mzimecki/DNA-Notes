# **Tydzień VII DDD taktyczne**


## Lekcja 7.01. Elementy konstrukcyjne

### Grupy

- zachowania modelu

	- Skladowe

		- zdarzenia

		- komendy

		- zapytania / widoki

		- reguły biznesowe / niezmienniki i agregaty, ktore je grupuja

		- polityki

	- Cele

		- definiowanie granic

			- kiedy sa zdefiniowane, mozemy myslec o tym, co jest w srodku

		- komunikacje z biznesem

			- dostawanie feedbacku

		- informowanie

			- kto wchodzi w interakcje z systemem

			- co ten system robi dla tych osob

			- w jaki sposob system dziala

		- pozwalaja projektowac system na wysokim poziomie

			- Design Level Event Storming

- struktura modelu

	- Skladowe

		- encja

			- Cechy

				- zmienia sie w czasie

				- posiada cykl zycia

				- posiada tozsamosc niezalezna od atrybutow

			- Przyklad

				- Samochod po przemalowaniu i stuningowaniu to ten sam samochod

					- Identyfikuje go VIN

					- Po wielu latach to ten sam samochod

		- wartosc (value object)

			- Cechy

				- nie zmieniaja sie w czasie

				- wartosc jest ich tozsamoscia

					- jesli wymienimy sie dwuzlotowkami, to bedziemy zadowoleni

				- opisuja, sa atrybutami encji

					- sa elementami skladajacymi sie na encje

			- Przyklad

				- liczba 5

				- 2 zlote

		- serwis domenowe

			- Cechy

				- operacje nie bedace czescia encji ani wartosci

					- nie mozemy ich przydzielic ani do encji ani do wartosci

				- bezstanowe

				- enkapsuluja wyliczenia, algorytmy

			- Przyklad

				- wygenerowanie identyfikatora uploadowanego odcinka

					- funkcja, ktora bedzie korzystala z aktualnej daty, generatora sekwencji

						- moze zawierac logike

					- nie jest to wartosc

						- bo jej efektem moze byc wartosc

					- nie jest to encja - odcinek

						- bo musi powstac zanim odcinek zostanie zainicjowany

			- To **NIE** sa

				- serwisy

					- aplikacyjne

						- koncepcja czysto techniczna

						- nie rozmawiamy o nich z biznesem

						- np. fasada

							- to jest ten element, ktory zbiera elementy konstrukcyjne domenowe, zeby mogly razem wspolgrac

							- jest odpowiedzialna za zlozenie pewnego use case’a

					- infrastrukturalne

						- Przyklady

							- wyslac notyfikacje

							- wyslac maila

							- komunikacja z innymi systemami zewnetrznymi

						- w portach i adapterach funkcjonuja na granicy pomiedzy domena a infrastruktura

	- Cechy

		- sa czescia wszechobecnego jezyka

			- elementy nazwane jezykiem biznesu

		- okreslaja strukture modelu

			- katygoryzujac na 3 elementy

		- wspieraja komunikacje w zespole

			- jesli mowimy encja, to kazdy wie, jakie ma cechy

- cykl zycia modelu

	- Skladowe

		- fabryki

			- Cel

				- tworzenie skomplikowanych struktur

					- jesli proces jest skomplikowany

					- np. elementow domenowych

			- czysto techniczy koncept

				- nie funkcjonuja w domenie

		- repozytoria

			- Cel

				- utrwalanie i odczyt

	- Cechy

		- nie sa czescia wszechobecnego jezyka

		- czysto techniczne znaczenie

			- bo np. musimy persystowac encje w bazie

### Dlaczego sa wazne?

- umozliwiaja otrzymanie feedbacku od biznesu juz na poziomie projektu

	- Elementy konstrukcyjne sa jak makieta, ktora architekt pokazuje inwestorowi

	- Do tej pory pokazywalismy biznesowi UML

		- Ktory nic mu nie mowil

			- Bo jest przeznaczony dla osob technicznych

		- w takiej sytuacji, pierwszy feedback jest dopiero po pierwszym demo

	- Teraz mozemy pokazywac elementy konstrukcyjne definiujace **zachowania** modelu

		- Tj. eventy, queries, komendy, itp.

		- Sa tym dla backednowcow, co mockupy dla frontendowcow

		- Szybszy feedback -> mniej bledow

- buduja wszechobecny jezyk

	- powoduja, ze koncepcje widocznie w domenie sa widoczne rowniez w kodzie

		- brak translacji pomiedzy domena a kodem

- pozwalaja odkladac decyzje techniczne na pozniej

	- niezaleznosc od technologii

		- ta sama abstrakcja moze miec rozna reprezentacje

		- np. agregat moze byc

			- grafem obiektow

			- struktura danych + serwisem

				- model anemiczny

			- funkcjami + typami

			- aktorami

		- np. dzialanie bazy danych

			- komenda -> DML / update

			- zdarzenie -> log append

				- write-ahead log

			- zapytanie -> select

			- polityka -> trigger

			- agregat -> constraints

	- Ostatni odpowiedzialny moment

		- dzieki temu, ze elementy konstrukcyjne mozemy zaimplementowac na wiele sposobow, w zaleznosci od tego jaki  rodzaj zlozonosci odkryjemy

			- to mozemy nie myslec o tym od poczatku

			- dopiero gdy zaprojektujemy caly modul i wiemy, co ma robic i z jakich elementow, to dobieramy styl implementacji i technologie

		- mozemy odlozyc decyzje na pozniej

			- technologie

			- framework

			- wzorce projektowe

### Podsumowanie

- elementy konstrukcyjne to makieta / model

	- pozwalja projektowac z biznesem

	- opisuja

		- zachowania

		- strukture

		- cykl zycia

	- sa oderwane od implementacji

		- mozna je dowolnie implementowac

	- pozwalaja na odsuniecie decyzji architektonicznej

## Lekcja 7.02. Implementacja Value Object

### Cechy implementacji sa agnostyczne technologicznie

- Szegoly specyficzne dla jezyka

### Cechy

- Niemutowalność

	- z natury niemutowalne

	- w j. obiektowych sami musimy ja zapewnic

		- konstruktor tworzy wszystko

		- brak setterow

		- ewentualne medoty zmieniajace stan zwracaja nowy obiekt

		- slowa kluczowe

			- final

			- nic nie da, jesli dotyczy np. mutowalnej kolekcji

				- caly graf musi byc niemutowalny

	- Zalety

		- bezpieczenstwo watkowe

- Komponowanie

	- mozemy je dodawac i odejmowac

	- tworzymy nowe obiekty

		- a nie mutujemy stare

- Porownywanie

	- na podstawie structural equality

		- tj. na podstawie wszystkich atrybutow, ktore maja

	- nie maja tozsamosci biznesowej, wiec...

		- skoro atrybuty sa takie same, to    to jest ten sam value object

	- sporo podobnego kodu

		- mozna wydzielic do klasy bazowej

		- lub uzyc jezyka, ktory wspiera takie struktury

			- np. w Kotlinie: data class

- Bardzo latwe do testowania

	- Zwiezle testy

		- Kilka linijek kodu

### Niezmienniki

- Dobrze implementuja sie jako Value Objecty

- wplywaja na reuzywalnosc

	- be reguly definiujemy raz

		- w value objecie

	- np. pojemnosc kursu

- moga byc kontekstowe

	- moga dostawac wiecej parametrow, niz tylko te ktore sa wymagane do stworzenia value objectu

		- np. kurs, gdzie w zaleznosci od faktu, czy odbywa sie online, czy nie, dodajemy kolejny warunek

- po co metody fabrykujace?

	- dlaczego nie sprawdzic tego w konstruktorze?

	- konstruktor powinien pozwolic na stworzenie value object z pominieciem walidacji

		- bo reguly mogly sie zmienic

		- a w bazie mamy wartosci, ktore teraz sa traktowane jako niepoprawne, ale wtedy byly poprawne

### Kolejnosc validacji

- od najmniej do najbardziej kosztownej walidacji

	- fail fast

	- przyklad

		- np. not null

		- potem dlugosc

		- na koniec format

			- bo jesli przekazemy 10 milionow znakow do wyrazenie regularnego, to proces nie bedzie zadowolony

				- wspieramy driver bezpieczenstwa

				- zapobiegamy DoS

### Zachowania

- moga miec zachowania

	- o ile nie zmieniaja stanu

		- nie maja efektow ubocznych

	- np. odpowiadaja na pytania

- daja wieksza czytelnosc i ekspresje w kodzie

	- np. mozeym zapytac pojemnosc, czy moze zaakceptowac nowych kursantow

## Lekcja 7.03. Implementacja Encji

### Zachowania

- Encje sa mutowalne

- Musimy zapewnic bezpieczna modyfikacje

	- Taka, ktora sprawdzi reguly biznesowe

	- Najpierw sprawdzamy niezmienniki

		- i wtedy mutujemy stan

		- Za pomoca ifow

	- Unikamy mozliwosci bezposredniej modyfikacji

		- getterow i setterow

- Reprezentuja jezyk domenowy

### Niezmienniki

- Kontekstowe

	- sprawdzane tylko przy danym przejsciu

		- w zaleznosci od kontektu, rozne ify

		- np. subskrypcja pauzowana ma inny zestaw zasad, niz wylaczona

- Stale

	- sprawdzane po kazdym przejsciu

		- prywatna metoda

		- wywolujemy na koniec kazdego sprawdzania, czy wszystko jest w porzadku

		- na koniec kazdego zachowania publicznego

		- np. czy subskrybent just ustawiony, czy data wygasniecia jest ustawiona

		- czesto nazywane deferred validation / odlozona walidacja

- Zalezne od cyklu zycia

	- Obsluguja maszyne stanow

	- Jesli zbytnio sie rozrasta, dzielimy na mniejsze klasy

		- Przyklad

			- PausedSubscription

			- ActiveSubscription

			- DisabledSubscription

		- Zyskujemy na czytelnosci

			- Duzy obiekt stal sie 3 obiektami o mniejszej odpowiedzialnosci

			- Zestaw danych zostal porgrupowany do klas, gdzie rzeczywiscie jest uzywany

		- Kompilator sprawdzi poprawnosc przejsc

			- Nie musze implementowac sprawdzenia

			- Mniej kodu, mniej bledow

			- Bliskie podejsciu funkcyjnemu

				- zawsze zwracamy nowy obiekt

	- Co jesli jest duzo stanow?

		- Jesli mamy wiele statusow i podstatusow i wszystko zalezy od ich kombinacji

			- God class

				- robi wszystko dla wszystkich

		- Mozemy znalezc mocne ciecia biznesowe, reprezentujace podklastry obiektow

			- Glowne klastry

				- w srodku nadal skomplikowane

				- ale i tak prostsze

					- bo jednoczesnie myslimy o mniejszej liczbie zaleznosci

			- Przyklady

				- dlugotrwajaca transakcja biznesowa

				- wniosek, ktory najpierw jest w stanie Szkic, potem Aktywny, a nastepnie Przedawniony

- Specyfikacje

	- Building blocki, ktore odpowiadaja na pytanie, czy encja spelnia jakies zalozenia

		- Implementujemy jako interfejs

	- Moga implementowac niezmienniki

		- Niezmiennik nie musi byc wewnatrz encji

		- Moze byc enkapsulowany w specyfikacji

			- Na zewnatrz encji

	- Mozemy wstrzykiwac rozne specyfikacje, w zaleznosci od tego, jakie warunki chcemy sprawdzic

		- Ma sens, gdy wdrazamy inne niezmienniki dla roznych subskrybentow

			- Inne dla subskrybentow premium

		- Lub gdy mamy multi-tenant

			- Wdrazamy dla innych klientow, z ktorych kazdy ma inne wymagania

				- Kod otwarty na rozszerzenia, zamkniety na modyfikacje

					- Open/Closed Principle

	- Komponowanie za pomoca logiki boolowskiej

		- Jezyk domenowy jest wzbogacony

		- Pozwala komponowac i reuzywac pytania, ktore zadajemy encjom

		- Ma sens, jesli potrzebujemy roznych warunkow, dla roznych przypadkow

### Polityka

- jako wzorzec strategii

	- z GoF

- Nie sprawdza regul

	- dostraja zmiany stanu

- Warstwa wyzszego poziomu wybiera/wstrzykuje polityki

	- Kod domenowy zmienia sie rzadko

	- On nie musi wiedziec o zmianie polityki

		- Dostanie ja z gory

- Przyklad

	- pauzowanie z plityka okreslajaca koniec pauzy

		- subskrybent premium moze pauzowac do konca zycia :)

		- mozemy pauzowac do konca wakacji

- Ma sens

	- gdy potrzebujemy innych regul w zaleznosci od przypadkow uzycia

### Memento

- Przydaje sie jesli

	- nie uzywamy ORM

	- chcemy przekazac encje do persystencji

	- jednoczesnie nie lamiac enkapsulacji

- Jest to mediator, kontrakt miedzy encja, a swiatem zewnetrznym

	- Mozemy zmieniac strukture obiektu, dopoki potrafimy ja przetlumaczyc na nasz kontrakt/snapshot

	- Kontrakt jest juz publiczny

		- obiekt nadal nie

- Czesto spotykany w architekturze hexagonalnej

### Kolekcje

- Tworzymy specjalne klasy opakowujace kolekcje

- Dzieki temu pozbywamy sie metod wlasciwych dla kolekcji

	- dodaj do list, filtruj liste

- A mozemy dodac metody opisujace zachowania biznesowe

	- zapisz na kurs, wypisz sie z kursu

	- wzbogacamy jezyk domenowy

	- dodajemy wyzszy poziom abstrakcji

		- jestesmy blizej wszechobecnego jezyka

### Porownywanie encji

- encje maja tozsamosc, wiec jej trzeba uzyc do porownania

- tozsamosc definiuje sie przez unikalny klucz

	- moze byc naturalny, z przestrzeni problemu

		- Przyklady

			- ISBN

			- numer ubezpieczenia

			- PESEL, jesli obracamy sie w granicach Polski

		- trzeba uwazac

			- w Polsce zdarzyly sie dwie osoby z tymi samymi PESELami

			- nalezy sie upewnic, czy istnieje jednostka certyfikujaca, ktora waliduje unikalnosc klucza

	- moze byc generowany

		- sekwencja z bazy danych

			- Wady

				- tozsamosc encji dostajemy dopiero po zapisie

				- sekwencja jest unikalna tylko lokalnie w jednej bazie danych

					- jesli mamy partycjonowanie, to mamy problem

		- UUID

			- dosc dlugie id

		- Twitter Snowflake

			- krotsze id

			- ale polegamy na zewnetrznym serwisie

## Lekcja 7.04. Łamanie reguł biznesowych

### Przypadek, gdzie niezmienniki blokuja wykonanie komendy

### Metody

- Wyjatki

	- podejscie klasyczne

	- Wady

		- wyjatek bedzie musial byc wylapany przez warstwe wyzej

			- jesli chcemy czytac taki negatywny przeplyw biznesowy, to musimy skakac pomiedzy plikami

				- slaba nawigacja i czytelnosc

		- testujac kod, z sygnatury metody nie wiemy, ze ona ma efekt uboczny

			- musimy testowac jej szczegoly implementacyjne

				- musimy wiedziec, ze czasem rzuca wyjatki

				- testowalnosc nie stoi na najwyzszym poziomie

		- obsluga wyjatkow moze byc kosztowna

		- jesli go nie obsluzymy, moze wyleciec az do klienta

			- zawierajac szczegoly implementacyjne i techniczne

				- spada driver bezpieczenstwa

					- ktos widziy jakich wersji uzywamy

						- exploity

	- Jesli uzywamy wyjatkow, to warto oddzielic wyjatki biznesowe od technicznych

		- np. nadtypem

			- biznesowe

			- techniczne

		- po to, zeby odrozniac to w narzedziu monitorujacym

			- nie wszystkie sa tak samo wazne

				- nie chcemy, zeby techniczne budzily nas w nocy

	- Maja sens w konstruktorze

		- Jesli tworzymy obiekt, a jego stan jest niepoprawny

			- to IllegalArgumentException

- Rezultat

	- Zamiast wyjatku, zwracamy rezultat

		- Ktos moze zarzucic, ze to jak w C: 1 lub -1

			- Tym razem jednak to bardzo deskryptywny rezultat

		- W sygnaturze metody widac rezultat

			- nie trzeba poznawac szczegolow implementacyjnych

				- lepsza testowalnosc

		- Przeplyw jest liniowy, wiec obsluga bledow jest zaraz po wyjsciu z metody

			- lepsza nawigacja i czytelnosc

	- Moze byc Either

		- Mozemy dopisac

		- Albo uzyc biblioteki

		- Konwencja

			- po lewej porazka

			- po prawej sukces

		- Daje to ogromna deskryptywnosc

	- Try

		- szybka migracja z kodu sterowanego wyjatkami

		- enkapsuluje wyjatek, ktory moglby poleciec w innej metodzie, ktora chcemy schowac

			- albo zwroci typ, ktory mial byc zwracany przez ta metode

		- zwraca albo to, co mialo byc zwrocone albo opakowany wyjatek

			- lepsza testowalnosc

	- Minusy Either i Try

		- jezyk domenowy zaczyna mowic typami, ktore nie sa zwiazane z domena

		- dodatkowa biblioteka - zaleznosc

### Co wybrac?

- patrz na drivery

	- Rezultaty dla

		- czytelnosc

		- testowalnosc

		- wydajnosc

	- Wyjatki ze wzgledu na

		- znajomosc rozwiazania

		- konwencje

## Lekcja 7.05. Implementacja zdarzen

### Modelowanie struktury zdarzen

### Zdarzenia zewnetrzne

- publiczne

	- integracyjne

- uzywane do komunikacji miedzy Bounded Contextami

- staja sie czescia publicznego kontraktu

- sa wersjonowane

	- poniewaz BC sa autonomiczne, to to, ze jeden zmieni strukture zdarzenia, nie znaczy, ze drugi musi od razu to zrobic

- prosta struktura

	- value objecty lub inne obiekty domenowe w BC, nie stana sie czescia tego publicznego kontraktu

		- bo chcemy je swobodnie modyfikowac, bez potrzeby myslenia o tym, ze to publiczny kontrakt

		- chcemy enakpsulowac takie koncepty

- czesto sa zapisywane w bazie danych

	- np. na potrzeby synchronizacji innych BC

### Zdarzenia wewnetrzne

- uzywane wewnatrz Bounded Contextu

	- np. zeby skomunikowac dwa agregaty w jednym BC

- kompilator pilnuje kontraktu

- moga zawierac koncepty domenowe

	- bo nie myslimy o publicznym kontrakcie

	- nie wychodzimy poza granice BC

- raczej nie zapisujemy w bazie

	- chyba, ze chcemy zaimplementowac lokalny Event Sourcing

### Grupy zdarzen

- Czesto grupujemy zdarzenia

	- z jednego BC lub agregatu

	- promowanie nawigacji

	- od razu widzimy, jakie zdarzenia emituje dany BC lub agregat

### Niemutowalnosc

- zdarzenia to fakty z przeszlosci

	- historii nie mozemy zmienic

### Ogolne uwagi

- proste i niemutowalne struktury

- maja unikalny identyfikator

	- chcemy wiedziec, co to za zdarzenie

	- konieczny przy ponawianiu zdarzen zewnetrznych

- moga miec identyfikator przyczyny

	- np. id komendy

	- correlation id

		- jesli kilka zdarzen jest efektem jednej komendy

- maja identyfikator obiektu, ktory wyemitowal zdarzenie

	- jesli SubskrybcjaZapauzowana, to warto wiedziec, ktora subskrybcja

## Lekcja 7.06. Implementacja – Serwisy

### Serwis domenowy

- Cechy

	- nalezy do warstwy domenowej

	- enkapsuluje logike biznesowa

		- skoro tak, to zalezy nam na testowalnosci

		- dostaje obiekty biznesowe na wejsciu

	- nie ma zaleznosci do innych warstw

	- testowalny w izolacji i jednostkowo

	- bezstanowy

		- latwo testowac, bo sprawdzamy wejscie i wyjscie

		- chyba ze obiekty domenowe sa trudne do testowania

- Przyklad

- pewnie mozna byloby enkapsulowac logike w jednym z obiektow domenowych

- ale jesli mamy watpliwosc, bo logika nie pasuje ani w jednym ani w drugim lub pasuje do obu

	- to jest to dobra heurystka, zeby wyniesc logike do osobnego serwisu domenowego

### Serwis aplikacyjny

- Cechy

	- nie zawiera logiki domenowej

		- zawiera logike aplikacyjna

			- czesciej zmienna logike

			- ktora steruje procesem biznesowym

				- koordynuje proces biznesowy

	- komunikuje sie z zewnetrznymi serwisami

	- zajmuje sie technikaliami

		- logowaniem

		- transakcjami

		- autoryzacja

		- tlumaczenie bledow z warstwy domenowej do warstw wyzszych

			- nie chcemy, zeby bledy przeciekaly w sposob bezposredni wyzej

		- zalezne od technologii

			- w Javie czesto aspektami

				- aspekty zmniejszaja testowalnosc

				- trzeba uwazac na kolejnosc nalozenie aspektow

					- jesli najpierwo nalozymy Cache, a potem Autoryzacje, to najpierw zapisujemy dane, a pozniej sprawdzamy czy mamy dostep do nich

			- mozemy tez robic to recznie

	- Oblsuga operacji bulk

	- obslugje komendy - niebieskie karteczki

- Przyklad

	- deleguje operacje do serwisu domenowego

- Zazwyczaj

	- 1. wyjmuje obiekt domenowy z bazy danych

		- moze ich byc kilka

	- 2.deleguje akcje na tym obiekcie

	- 3. zapisuje obiekt

		- tylko jeden

			- **regula zapisu jednego agregatu w transakcji**

			- lamiemey ja np. w przypadku operacji bulk

### Wzorzec Command

- Jesli liczba parametrow wejsciowych do serwisu aplikacyjnego rosnie...

	- to enkapsulujemy je w Command

		- niebieska karteczka

- nadaje intencyjnosci żądaniu, ktore chcemy wyslac do systemu

- nie obslugujemy serwisem aplikacyjnym, tylko Command Handlerem

	- Wzorzec Command Handler

		- wyspecyfikowana jednostka kodu, ktora obsluguje jedna komende

		- najczesciej interfejs

		- z natury obsluguje jedna komende

			- unikamy sytuacji dodawania kolejnych metod do serwisu aplikacyjnego

				- ok, jest pauzowanie w Pause Service, to dodam wznawianie

- Command Bus

	- mediator miedzy klientami, ktore rzucaja komendy, a naszym systemem, ktory posiada command handlery

- Zalety

	- generyczne handlery, ktora zapewniaja funkcjonalnosc dla wszystkich komend

		- Przyklady

			- transakcyjnosc

			- retry

				- 2-3 razy, potem blad

			- log wszytkich żądań/komend

		- to samo da sie zrobic generycznym bazowym serwisem aplikacyjnym

			- ale bazowy serwis nie zapewni specyficznego zachowania drugiego dla jednej wybranej komendy

			- z CommandHandlerem to proste

				- rejestrujemy nowy handler na jedna specyficzna komende

		- Przyklad

			- eksperymentalne pauzowanie dla jednego klienta

				- dodajemy nowy handler

				- kod jest otwarty na rozbudowe, zamkniety na modyfikacje

					- OCP

	- Wersjonowanie komend

		- dwie wersje komend

			- doklejamy je warstwa konfiguracyjna

		- rozni klienci: korzystaja z 1 lub 2 wersji komendy, bo sa na roznym etapie migracji

			- co ktorzy sa przed migracja, uzywaja v1

			- w trakcie - v1 i v2

			- po migracji - v2

	- Maja sens jesli drivery architektoniczne na to wskazuja

		- np. multi tenant

		- jesli nie, to serwis aplikacyjny jest prostszym rozwiazaniem

## Lekcja 7.07. Publikacja Zdarzeń

### Agregaty

- 1. Przyjmuja komendy

- 2. Sprawdzaja szereg zalozen biznesowych

- 3. Zmieniaja stan

	- Zmiana stanu moze byc reprezentowana przez wygenerowanie zdarzenia domenowego

- Maja pelna wiedze o tym, jak i kiedy generowac zdarzenia domenowe

	- I one to robia

	- A nie serwisy domenowe czy aplikacyjne

### Sposoby publikacji zdarzen

- Wewnetrzna kolekcja zdarzen

	- Klasa abstrakcyjna, po ktorej dziedicza wszystkie agregaty

		- Kolekcja zdarzen reprezentowana interfejsem

		- 3 metody

			- raise(DomainEvent)

				- dodawania eventu do kolekcji

				- protected

					- tylko dla agregatow

			- getChanges

				- daj kopie kolekcji

				- publiczna

					- dla komponentow poza agregatem

			- clearEvents

				- wyczysc kolekcje

				- publiczna

					- dla komponentow poza agregatem

		- Przyklad agregatu

			- metoda / komenda

				- niebieska karteczka

			- if / regula

				- zolta karteczka

			- rise(...) / zdarzenie

				- pomoranczowa karteczka

		- Serwis aplikacyjny publikuje zdarzenia

			- 1. Wywoluje operacje na agregacie

			- 2. Pobiera z niego zdarzenia

			- 3. Publikuje je przez wstrzykniety EventPublisher

				- Warto sie przygotowac na wymienialnosc takiej klasy

				- Interfejs

			- 4. Czysci zdarzenia z agregatu

			- Wnioski

				- Te kroki beda powtarzac sie w wielu serwisach aplikacyjnych

					- Kandydaci do wydzielnia do nadtypu

				- zapis agregatu i publikacja zdarzen odbywaja sie w jednej transakcji

					- zaniedbanie tego tematu moze prowadzic do powaznych skutkow

			- Czasem zdarza sie, ze dzieje sie to w repozytorium, a nie serwisie aplikacyjnym

- Zwracanie zdarzeń

	- agregat zwraca zdarzenia, jako efekt wykonywania komendy

		- bez wewnetrznej kolekcji

	- Moze byc typ Either

		- albo porazka

		- albo lista zdarzen domenowych reprezentujacych faktyczna zmiane stanu

			- zdarzenia mozemy opakowac w jedna klase pokazujaca wszystkie mozliwe kombinacje zdarzen

				- np. zapauzowano subskrypcje, ale tez - opcjonalnie - max liczba pauz zostala osiagnieta

	- Wady

		- mozna powiedziec, ze lamiemy CQS

			- bo zmieniamy stan i zwracamy jednoczesnie

			- ale robimy to swiadomie i pragmatycznie

	- Zalety

		- nie potrzebujemy wewnetrznej kolekcji

		- nie potrzebujemy klasy bazowej

		- zwracajac deskryptywna liste zdarzen z metody, kompilator podpowie nam, jesli czegos zapomnimy

			- a braku wywolania metody rise() kompilator nie wylapie

		- Troche zwiezlejszy kod

			- Semantyka i testowalnosc kodu taka sama

	- Publikowanie zwroconych zdarzen

		- Jest prostsze, bo nie robimy getChanges i clearChanges

		- Otrzymane zdarzenia po prostu publikujemy

			- eventPublisher.publish(events)

		- Nadal w jednej transakcji

- Statyczna klasa publikujaca

	- na przekroju publikacji i transportu

		- bo na moment przerywa dzialania agregatu i od razu informuje wszystkich subskrybentow o zdarzeniach

		- agregat cos robi, wysylamy event, wszystkie listenery zostaja poinformowani o zmianie i dalej przetwarzamy w agregacie

	- Wady

		- konsekwencje moga byc takie, ze byc moze rzucamy wyjatek w agregacie, a listenerzy sa juz poinformowani

		- testowalnosc jest trudniejsza

			- ze wzgledu na efekt uboczny

		- debuggowanie trudniejsze

			- bo skok do listenera

	- ta klasa nie jest produkcyjnie gotowa

		- lepsze rozwiazanie na http://udidahan.com/2009/06/14/domain-events-salvation/

- Ktory wybieramy?

	- Testowalnosc, czytelnosc i nawigacja sa latwiejsze w 2 pierwszych przypadkach

	- Ale nalezy miec na uwadze konwencje, przyzwyczajenie i wiedze zespolu

		- byc moze poradzilismy sobie z problemami statycznej klasy publikujacej i jestesmy do niej przyzwyczajeni

### Testowalnosc

- uzywajac sztucznego zegara, mozemy sprawdzic, czy zdarzenie wygenerowalo sie w odpowiednim czasie

## Lekcja 7.08. Transport Zdarzeń

### Implementacje

- Just Forward

	- Bierze zdarzenie i przekazuje po kolei do wszystkich mozliwych subskrybentow/listenerow

		- Tak samo, jak bysmy wywolali kilka razy publish w serwisie aplikacyjnym

		- ale nie chcemy, zeby serwis nam sie rozrastal, wiec odwracamy zaleznosci

	- wszystko synchronicznie i sekwencyjnie

	- wszystko w jednej transakcji

	- Pod wzgledem synchronicznosci i transakcyjnosci jest to podobne rozwiazanie do **statycznej klasy publikujacej**

		- Roznica jest taka, ze statyczna klasa publikujaca wysyla eventy **juz w trakcie dzialania** agregatu

			- dzialamy w agregacie, wysylamy eventy i wracamy do agregatu

		- w **Just Forward** mamy pewnosc, ze przetwarzanie agregatu jest skonczone

			- komenda zostala biznesowo zaakceptowana

	- Overview

		- serwis aplikacyjny zaczyna transakcje

		- w tej transakcji zapisuje sie agregat

		- oraz odbywaja sie wszystkie operacje wykonywane przez listenerow

			- w szczegolnosci moga sie podpiac bo te operacje bazodanowa

	- Zalety

		- latwe w implementacji

			- najprostsze wsrod opcji transportu zdarzen domenowych

	- Wady

		- niejawne efekty uboczne

			- potencjalna koniecznosc ponowienia komendy, bo nie udalo sie wykonac jakiegos efektu ubocznego

				- kiepski UX

		- niejawne wiazanie roznych czesci aplikacji

			- bezposrednio nie widac tego w kodzie

			- a jest to silne wiazanie

			- ktos moglby zapytac po co odchudzalismy agregat, zeby uniknac kolizji transakcji, skoro teraz wszystko robimy w transakcji

				- agregat jest wciaz odchudzony

					- sztucznie wiazemy rozne czesci systemu transakcja

					- i mozemy sie tego wiazania pozbyc

						- np. dzielac komende i efekty uboczne do innych transakcji

- Transport w nastepnych transakcjach

	- Jak to robic?

		- najpierw przetwarzamy komende i robimy commit

		- nastepnie publikujemy eventy

			- efekty uboczne nie maja wplywu na pierwsza transakcje

			- odwracamy kolejnosc w kodzie

				- jesli sami obslugujemy transakcje

			- lub rejestrujemy callback

				- ktory uruchomiony jest po sukcesie transakcji z commita

				- jesli framework to obsluguje

	- Overview

		- Przebieg

			- serwis aplikacyjny zaczyna transakcje

			- w niej zapisuje sie agregat

			- trasnakcja jest commitowana

			- listenery dzialaja w osobnych transakcjach

				- problemy zw. z niezawodnoscia

				- czasem trwania operacji

				- nie wplywaja na zapis agregatu

		- Problemy

			- jesli ktorys z efektow ubocznych sie nie wykona, to tracimy spojnosc danych

				- bo nie mozemy powtorzyc komendy

				- bo ona zakonczyla sie sukcesem

				- zeby ja usunac, trzeba zadzialac recznie

			- pytamy biznesu, czy to jest problem

				- jesli nie, to mamy to

	- Zalety

		- latwa implementacja

		- brak wiazania transakcyjnego

			- separacja zagadnien

	- Wady

		- problem zawodnosci

			- probujemy tylko raz

- Store and Forward

	- Jak to robic?

		- serwis aplikacyjny zapisuje atomowo

			- wydarzenia sa zaimplementowane w innej implementacji Domain Event Publishera

		- agregat oraz liste zdarzen do bazy

			- intencja tego, ze wszyscy sluchacze beda musieli byc poinformowani

		- w jednej transakcji

			- lekko rozszerzamy zakres oryginalnej transakcji

	- Overview

		- Zamiast transportowac od razu do listenerow, najpierw zapisuje event w bazie

			- w tej samej, w ktorej trzymamy agregat

				- dzieki temu zapisumey wszystko albo nic

				- wszystko, czyli agregat i zdarzenie domenowe

		- Raz na jakis czas Domain Event Publisher musi

			- 1. Pobrac wydarzenia jeszcze nie opublikowane

			- 2. Opublikowac/wyslac je

				- Np. za pomoca JustForward

			- 3. Oznaczyc jako wyslane

		- Kroki

			- 1. Lewa strona

				- 1. Zapisujemy agregat

				- 2. Zdarzenie

					- w tabelce zdarzen

				- w jednej transakcji

					- daje pewnosc, ze zapisalismy, ze cos sie jeszcze musi zadziac, jesli chodzi o efekty uboczne

			- 2. Prawa strona

				- 1. Fetch unpublished events

					- do limitu, zeby nie zapychac bufora

					- cyklicznie

				- 2. Sent to all subscribers

				- 3. Save as published

		- Efekt

			- jesli efekt uboczny sie nie powiedzie, to nie zapiszemy zdarzenia jako wyslane

				- wiec zostanie podjeta ponowna proba

			- potrzebujemy transakcji

				- wiec dochodzimy do tego samego problemu

					- w jednej transakcji zapisujemy efekty uboczne i fakt, ze zdarzenia zostaly wyslane

					- baza nie moze zapisac, ze sie wyslaly, a efekty sie udaly

						- w efekcie wykonamy je jeszcze raz

					- **ale przeniesonego w czasie**

						- on w ogole nie wplywa na agregat, UX

	- Inna nazwa

		- outbox pattern

	- Zalety

		- brak wiazania transakcyjnego

		- gwarancja dostarczenia

			- niezawodnosc

	- Wady

		- bardziej zlozona implementacja

			- zapis

			- ponawianie

			- deduplikacja

			- problem wielu instancji

				- kilka instancji obsluguje pauzowanie subskrypcji?

				- ktora ma byc odpowiedzialna za wyciaganie zdarzen z db?

					- jedna, dwie, wszystkie?

### Efekty uboczne

- moga byc tworzone przez listenerow

- Grupy

	- Wewnetrzne

		- zapisuja w bazie danych

		- podpinaja sie pod jedna transakcje

		- przyklad

			- odjecie subskrybentowi 3 pktow lojalnosciowych

				- to jest powrot do tygodnia 6, gdzie chcielismy to robic, ale nie chcielismy, zeby rosla nam komenda

		- Efekty

			- Rosnie transakcja

				- spada skalowalnosc

				- spada UX

			- implementacja gotowa na przetwarzanie asynchroniczne

				- wynika z implementacji DomainEventPublishera, ktora mozemy szybko zmienic

			- Rollback na bazie wycofuje skutki uboczne

				- sama baza to robi

	- Zewnetrzne

		- komunikacja z serwisami zewnetrznymi

		- przyklad

			- wyslanie maila: subskrypcja zapauzowana

			- az sie prosi podpiac pod zdarzenie

				- kod jest maly i testowalny

				- problem: wszystko w jednej transakcji

					- subskrybent czeka na koniec transakcji

						- tych efektow ubocznych moze byc duzo

					- jesli nie dziala, to sypie sie cala transakcja

						- nie dziala serwis mailowy, to nie dziala pauzowanie subskrypcji

		- Efekty

			- Nie dziala serwis zewnetrzny, wiec nie moge wykonac akcji biznesowej

				- nie powinny byc ze soba zwiazane

				- trzeba na to uwazac

			- Rollback na bazie NIE wycofuje skutkiow zewnetrznych

				- mail juz poszedl, nie da sie tego odwrocic

				- to moga byc istotne konsekwencje biznesowe

### Gwarancja dostarczania

- at most one delivey

	- 0 lub 1 raz

	- „Transport w nastepnych transakcjach”

- at least once delivery

	- od 1 do n razy

	- idempotentnosc

		- sluchac powinien wiedziec, czy juz kiedys obsluzyl taka wiadomosc

	- „Store and Forward”

### Zdarzenie wyslane w swiat zewnetrzny staje sie publicznym kontraktem

- ciezko bedzie je zmienic bez zmiany listenera

## Lekcja 7.09. Dobór wzorca

### Wzorce projektowe

- uzyte do implementacj elementow konstrukcyjnych

- strategia

	- inaczej polityka

- speyfikacja

	- niezmienniki

- dekorator

- lancuch odpowiedzialnosci

### Kiedy sa uzyteczna, a kiedy to przerost formy nad trescia?

- dlaczego wzorzec strategii do polityki pauzowania?

	- tu jest dodatkowo fabryka z ifem

- a moze lepiej dwa ify?

	- nie ma strategii, osobnych obiektow, fabryki

	- jest czytelny i testowalny

		- jeden test

		- brak zaleznosci

		- mniej kodu

	- rozszerzalnosc

		- dodanie kolejnego ifa

			- nie popsuje testow

- co zyskalismy?

	- konfigurowalnosc

		- bez ingerencji w kodzie mozemy konfigurowac nasza subskrypcje, zeby raz miala taka, a raz inna polityke

		- czy jest potrzebna? czy takie zmiany w kodzie beda zachodzic?

- metafora roweru

	- rama jest mocno konfigurowalna

		- mozemy zmieniac siodelko, kola, pedaly, etc.

	- ale przez to skomplikowana

		- mechanizm laczacy sie komplikuje

	- gdyby zespawac siodelko

		- byloby taniej i prosciel

		- ale nie byloby konfiguralnosci

### Wektor zmiany

- przewidywanie, jakie zmiany w kodzie beda nam potrzebne w przyszlosci

- kiedy projektujemy na poziomie modelu i zastanawiamy sie nad wzorcem

	- musimy przemyslec, w ktorym kierunku nasz model ma sie zmieniac, a w ktorym nie

- 4 pytania

	- co sie zmieni, a co nie?

	- kiedy sie zmieni?

		- za tydzien, czy za rok?

	- jaka jest szansa na zmiane?

		- biznes mowi

			- na 100% pojdziemy w tym kierunku

			- moze nie do konca...

	- jaki jest koszt refaktoryzacji?

		- czy oplaca mi sie od razu wprowadzac skomplikowany wzorzed od razu?

			- wiecej kodu

			- wiecej elemntow ruchomych

		- czy mniejszym kosztem zrobic to teraz na sztywno?

			- nie byle jak

			- nie nietestowalnie

			- mowimy o designie sztywnym vs. konfigurowalnym

				- nie poswiecamy testowalnosci, czytelnosci

				- dalej robimy clean code

				- po prostu czesto konfigurowalnosc nie jest potrzebna

					- albo jest przedwczesna optymalizacja

			- koszt refaktoryzacji dobrego kodu do wzorca moze nie byc duzy

				- moze byc mniejszy od kosztu utrzymania wzorca, gdy ten nie jest potrzebny

### Podsumowujac

- dwa razy sie zastanow zanim skomplikujesz projekt

	- czy skomplikowane rozwiazanie jest naprawde potrzebne?

- unikaj przedwczesnej konfigurowalnosci

	- moze sie okazac, ze nigdy jej nie uzyjesz

- opisz wektory zmian w ADL

	- zeby kolejni programisci wiedzieli, dlaczego ten wzorzec tu jest

	- jaki byl kontekst wyboru tego rozwiazania w chwili podejmowania decyzji

