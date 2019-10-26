# **Tydzień VI Design level**


## Lekcja 6.01. Model domenowy

### Definicja

- Model domenowy to rozwiazanie jakiegos problemu

- Model nie odzwierciedla rzeczywistosci

	- Tylko wybrane aspekty

	- np. mapa

- Uzywa Ubiquitous Language

	- Bounded Context ma granice lingwistyczne

		- kazdy BC ma swoj jezyk

### Perspektywy

- Wzorzec

	- Obiektowy i Implementacyjny wzorzec

	- Martin Fowler

	- Obiektowy model domeny zawierajacy dane i zachowania

	- Reprezentacja

		- Implementcja modelu w kodzie

			- Dane (stan)

			- Zachowania

			- Zawiera

				- Obiekty

				- Funkcje

			- Usunelismy slowo „obiektowy”

				- Bo czasy sie zmienily i wiele osob uzywa jezykow wieloparadygmatowych

				- Ten sam model, reprezentowany funkcyjnie i obiektowo

					- Ten sam model, rozne interpretacje

- Rozwiazanie

	- Rozwiazanie problemu domenowego

	- Zbior konceptow, ktory sluzy wspolnemu zrozumieniu problemu domenowego

		- Przez ekspertow technicznych i nietechnicznych

	- Eric Evans

	- Reprezentacje

		- Diagram

		- lista zdan w j. angielskim

		- kod zrodlowy

		- Design Level Event Storming

	- Tej definicji bedziemy bliżsi w DNA

		- W jakims sensie obie sa komplementarne

### Implementacja modelu domenowego **nie zawiera**

- Koncepty

	- sposobu komunikacji z baza danych

	- zapisu/odczytu stanu

	- sposobu komunikacji ze swiatem zewnetrznym

- Te koncepty sa odseparowane

	- Dobra architektura do osadzenia modelu to hexagonalna

		- Nie jest jedyna sluszna architektura

			- Jesli model prosty

			- Malo zachowan

			- Wtedy 3-warstwy tez zadzialaja

### Projektowanie modelu

- Zanim pomowimy o architekturze modelu, to musimy go odkryc

- Eksploracja

	- Szukanie elementow konstrukcyjnych

		- Zachowania

		- Jezyk

		- Aktorzy

		- Np. za pomoca Design Level Event Stormingu

			- Artefakt: zbior karteczek w notacji DLES

	- Efektem jest model

		- Ktory bedziemy reprezentowac poprzez implementacje

## Lekcja 6.02. Design Level Event Storming

### Definicja

- Technika, która pozwala na eksploracje elementów konstrukcyjnych, z których tworzymy model domenowy

- Notacje mozna dowolnie modyfikowac

	- Na potrzeby wlasnego przedsiebiorstwa, problemu domenowego

### Zakres eksploracji

- Big Picture ES sluzy do horyzontalnej eksploracji domeny

	- Efekt: propozycje Bounded Contextow

- Design Level ES bada pojedynczy Bounded Context

	- Badamy system wertykalnie

	- Mozemy ograniczyc liczbe

		- ekspertow domenowych do danej subdomeny

		- programistow odpowiedzialnych za dane miejsce w systemie

### Notacja

- Zdarzenia (Events)

	- Czas przeszly

	- Wazne z biznesowego punktu widzenia

	- Reprezentuje zmiane stanu

	- Moze byc efektem Komendy lub przyjsc z zewnetrznego systemu

	- Zmusza do myslenia o zachowaniu, a nie strukturze systemu

- Komendy (Commands)

	- Przyczyna zdarzeń

	- Wyraża intencje

	- Wysylane przez uzytkownika lub zewnetrzny system

	- Nie kazdy event jest wyzwalany commandem

		- Event cykliczny

			- Co miesiac

			- Na poczatku okresu rozliczeniowego

		- Event jest przyczyna kolejnego eventu

	- Przyklad: Aktywuj subskrypcje -> Aktywowano subskrybcje

- Aktorzy (Actors)

	- Zolte kartkie, obok komend

		- Uzytkownicy lub systemy

		- Widac kto jest upowazniony do jakich komend

			- Widac dopuszczalne przeplywy

- Reguly biznesowe (Rules)

	- Warunek

		- Sprawdza, czy komenda ma sens biznesowy

		- Widzimy, czy komenda konczy sie zdarzeniem, czy nie

	- Pomiedzy komenda, a zdarzeniem

		- Aktywuj subskrybcje -> jesli nie jest juz aktywna -> aktywowano subskrybcje

- Polityki (Policies)

	- Jest reakcją na zdarzenie

	- Inaczej

		- Strategia

			- Wzorzec GoF strategii

	- Jesli mamy zdarzenie domenowe, to inna czesc systemu moze byc nim zainteresowana

		- Np. jesli aktywowano subskrypcje, to wyzwalamy Fakturowanie

		- Moze byc w innej czesci sytemu

		- Moze byc wiele podprocesow

	- To nie jest wzorzec Polityka z taktycznego DDD

	- Nie chcemy miec obslugi w ramach komendy, bo ona by rosla i rosla

		- Fakturowanie moze wygladac roznie, jesli klient byl indywidualny, korporacyjny

		- Dzieki polityce mamy separacje zagadnien

			- System bardziej rozszerzalny

				- Doklejamy polityki

- Widoki (Read Models)

	- Reprezentacja stanu systemu

		- Pytania, na ktore odpowiada nasz system

			- Np. wyswietlana strona

		- Odpowiedz dla innego systemu, jesli ten nas o cos pyta

	- Nie zmienia stanu

	- Pochodna wszystkich zdarzen, ktore zadzialy sie do momentu wygenrowania widoki

### Pętla Event Storming

- Cel

	- Opisuje przeplywy w systemie

	- Daje platforme komunikacji, ktora jest zrozumiala dla biznesu i programistow

- Kroki

	- 1. Aktor widzi Widok

	- 2. Na podstawie Widoku i swoich przemyslen, wola Komende

	- 3. Regula biznesowa sprawdza, czy Komenda moze byc wykonana

	- 4. Jesli Komenda jest wykonana, emitujemy Zdarzenie domenowe

	- 5. Zdarzenie zmienia Widok i uruchamia wiele Polityk

		- Polityka uruchamia kolejne Komendy

### Rozne poziomy zlozonosci

- Pelna symetria

	- Zdarzenie -> Komenda, Zdarzenie -> Komenda

	- W nazewnictwie

		- Zmodyfikuj -> Zmodyfikowano

		- Usun -> Usunieto

	- Bez regul biznesowych

	- Niska zlozonosc systemu w tym miejscu

		- Klasa zlozonosci CRUD

			- 3-warstwowa architektura

- Duza zlozonosc

	- Cechy

		- Wiele regul biznesowych

		- Wiele polityk

		- Biznes sam nie wie, jak to ma dzialac

		- Bedziemy eksperymentowac, tworzyc prototypy

	- Architektura hexagonalna

- Badamy trudnosc

	- Analizujac wielkosc przerwy miedzy Komenda, a Zdarzeniem

	- Na tej podstawie dobieramy odpowiednia architekture

### Zalety

- poznawanie domeny

	- rozmowy o domenie

	- szybkie odkrywanie jezyka

- wizualizacja

	- karteczki

		- widzialny artefakt

- eksploracja roznych modelow

	- przenoszenie komend, regul biznesowych

	- dodawanie i usuwac polityki

	- robimy to przesuwajac karteczki

		- jest to szybsze i tansze, niz gdyby robic to w kodzie

## Lekcja 6.03. BDD strategiczne

### W Design Level ES odkrylismy

- Komende, zdarzenie i widok

- Za pomoca tych trzech konstruktow mozemy zamodelowac kazda interakcje na linii Aktor - Model domenowy

	- Wynika to z lingwistyki, bo...

		- albo kogos pytamy

			- widok / query

		- albo kazemy mu cos zrobic

			- komenda

		- albo cos oznajmiamy

			- zdarzenie

	- Myslenie takimi zachowaniami, w oderwaniu od implementacji

		- jest bliskie BDD

- DLES nie jest konieczne do BDD, ale...

	- te techniki sa komplementarne

	- zyja w symbiozie

### Model to zwiazanie danych i zachowan

- Za pomoca ES tworzymy scenariusze zachowan

	- Pokazuja, jak mocno dane i zachowania sa ze soba zwiazane

- Dostajemy scenariusze BDD w notacji Event Stormingu

	- Moze ich byc wiele

		- Daja glebokie zrozumienie naszej domeny

		- Razem z ekspertami domenowymi

	- Z zycia wziete, faktyczne przypadki uzycia z naszej domeny

		- Minimalizujemy ryzyko, ze po jakims czasie biznes mowi: nie o to nam chodzilo

### Scenariusze BDD

- Przypadki uzycia z przestrzeni problemu zamodelowane w przestrzeni rozwiazania

- Mozemy je automatyzowac

	- Test mowi jezykiem domenowym, a nie technicznym

		- Ekspert domenowy powinien go zrozumiec

		- Nie mowimy, ze uderzamy po REST

	- Test nie dotyka modelu

		- Operuje na warstwie use-case’ów - zachowan

			- Dzieki temu mozemy eksperymentowac z roznymi modelami

				- Testy musza przejsc dla wszystkich

				- Nie przywiazujemy sie do pierwszych pomyslow

				- To umozliwia eksperymentowanie

- To jest moment, gdzie developerzy skupiaja sie na pisaniu testow, bez myslenia o implementacji

	- Nie myslimy o modelu, bo nie wiemy, jak on wyglada

		- Zero przestrzeni rozwiazan

		- Normalnie, gdy siadamy do implementacji i chcemy robic TDD, to myslenie o rozwiazaniu ksztaltuje test

### Czym jest?

- Dwie fazy

	- 1. Wspolne zrozumienie problemu biznesowego wraz z ekspertami domenowymi

		- Budujemy rozne scenariusze

			- Efekt Design Level Event Stormingu

	- 2. Zautomatyzowane use-case’ów

		- Sluza jako zywa dokumentacja

		- To nie sa testy regresji

			- Najpierw powstaja testy, pozniej model domenowy

			- Sluza regresji, ale to jest efekt uboczny

			- Ich zadaniem jest wysterowanie modelu

				- Zeby robil to, co musi i nic wiecej

		- Narzedzia

			- Cucumber, Spock, JBehave

			- Sprawa drugorzedna

			- To nie chodzi o given/when/then

			- Tylko o wspolne zrozumienie scenariuszy biznesowych

				- a potem przeniesienie ich do kodu

				- **Chodzi o sterowanie modelu zachowaniami**

### Co daje w zastanym systemie?

- Zwiekszenie zrozumienia

	- Jesli na dzialajacym sytemie wykonamy DLES, to lepiej zrozumiemy, jak dziala biznes

		- W oderwaniu od rozwiazania

		- DLES daje scenariusze, ktore mozemy mapowac do kodu

			- Automatyczne testy beda mowic jezykiem domenowym, problemu

				- a nie rozwiazania

				- ale... musimy je polaczyc z istniejacym rozwiazaniem, co daje...

- Mozliwosc refaktoringu

	- Jak juz mamy testy, to mozemy refaktoryzowac, bo nasza funkcjonalnosc jest zamrozona testami - przypadkami uzycia

		- Mozemy w srodku eksperymentowac

		- Zmieniac model

	- Parasol bezpieczenstwa

## Lekcja 6.04. Estymacja

### Dwie szkoly

- #NoEstimates

	- estymacje sa nieprecyzyjne

		- nie da sie precyzyjnie estymowac w IT

			- nieprzewidywalne zadania

	- dostarczona wartosc jest istotniejsza, niz koszt

		- skupienie na wartosci biznesowej

		- majac budzet na 3 miesiace pracy

			- priorytetyzujemy prace wg wartosci biznesowej

			- i dostarczamy, ile mozemy

				- to da najwiekszy zysk dla organizacji

		- czy wyestymujemy zadania, czy nie, to one zajma tyle samo czasu

	- estymacja prowadzi do dysfunkcyjnych zachowan

		- programisci maja tendencje do estymacji zbyt optymistycznej

			- efekt: nie wyrabiamy sie

				- nadgodziny

				- obcinamy na jakosci

				- czasem na funkcjonalnosci

				- pojawia sie bylejakosc

- #YesEstimates

	- estymacje moga byc precyzyjne

		- to, ze czasem nie wychodzi, nie znaczy, ze mamy sie poddac

		- czasem wychodzi, wiec zastanowmy sie co zrobic, zeby dzialo sie tak czesciej

			- zamiast wylewac dziecko z kapiela

	- szacowanie kosztu jest istotne

		- istotne dla biznesu

		- fajnie byloby wiedziec, ile dane feature’y beda kosztowac

			- w niektorych projektach nie mamy okreslonego czasu

			- tylko zestaw potrzebnych funkcjonalnosci

				- MVP

	- brak estymat alienuje biznes

		- biznes potrzebuje

			- wiedziec ile potrwa projekt

				- do szacunkow

				- predykcji

			- czegos, zeby wytlumaczyc sie przed swoimi szefami

			- iluzji kontroli

			- wiedziec, czy cos dziala, czy nie

				- czy musza reagowac

		- biznes jest przyzwyczajony do estymat i potrafi z nimi pracowac

### Bledy poznawcze / kognitywne

- Przyklady

	- myslenie zyczeniowe

	- torowanie / priming / anchoring / zakotwiczanie

	- zludzenie planowania

	- dysonans poznawczy

- Pozbycie sie ich?

	- Do niedawno myslano, ze niczego nie da sie z nimi zrobic

	- Najnowsze badania mowia, ze cwiczenia pozwalaja pozbyc sie niektorych

- Sama wiadomosc istnienia bledow

	- Pozwala na precyzyjniejsze estymowanie

### Kiedy estymacja dziala?

- gdy robiliśmy coś podobnego wcześniej

- gdy rozumiemy jak coś ma działać

	- gdy mamy pelna specyfikacje

	- i zakres wiedzy

- gdy zakres prac jest mały

- gdy w międzyczasie wymagania się nie zmieniają

- gdy nie musimy czekać na innych

### Estymacja a architektura

- Architekt, poprzez swoje decyzje, wplywa na tworzenie warunkow sprzyjajacych powstawanie dokladnych estymat

	- Wybrane narzedzia

	- Jak pracuje nasz zespol

	- Co zespol konkretnie robi

- Ryzyka

	- 1. Coś nowego

		- nowa technologia, framework, biblioteka

		- innowacyjne rozwiazanie

		- nowe atrybuty jakosciowe

			- Robilem taka funkcjonalnosc wiele razy, ale dla duzo mniejszych systemow

		- Mitygacja

			- Poziom wiedzy

				- **Pozwala stwierdzic, kiedy nie estymowac**

					- Na ostatnich dwoch poziomach, nie mozemy podac estymat

						- mozemy zrobic eksperyment

							- spikes, proof of concepts

							- w efekcie ktorego sprowadzimy problem do jednej z 3 pierwszych kategorii

								- nie zawsze sie udaje

						- mozemy timeboxowac

							- poswiece na to X czasu

							- nie jest to estymata, ale jakis czas jest

				- 1. wszyscy juz cos takiego zrobilismy

				- 2. ktos w naszym zespole to zrobil

				- 3. ktos w naszej firmie to zrobil

					- ryzyko jest wieksze, ale ciagle mozemy estymowac

				- 4. ktos to zrobil, ale w innym kontekscie

					- w innej firmie?

						- Moze konkurencja?

				- 5. nikt tego wczesniej nie zrobil

			- Powtarzalnosc

				- chcemy zwiekszyc podobienstwo funkcjonalnosci do siebie

					- probujemy sprowadzic funkcjonalnosc do kategorii, ktora mozemy porownac

						- wtedy estymacja jest realna i prostsza

						- Przyklad: CRUD dla ksiegowosci i CRUD dla szpitala

							- Niby rozne systemy, ale zblizona funkcjonalnosc i styl architektoniczny

								- Wtedy mozemy estymowac

				- Skladowe

					- elementy konstrukcyjne

						- komendy, eventy, read modele

						- jesli potrafimy sprowadzic do elementow konstrukcyjnych, to zyskujemy powtarzalnosc

							- duzo lepiej widzimy podobienstwa

					- wzorce projektowe

						- jesli potrafie dobrac wzorzec, ktory juz implementowalem, do biezacego problemu, to latwiej mi znalezc podobienstwo

					- style architektoniczne

				- Jak to zrobic?

					- 1. Zamodeluj problem przy pomocy znanych elementow konstrukcyjnych

					- 2. Znajdz wzorzec projektowy, przy pomocy ktorego zaimplementujesz model z (1)

					- 3. Dobierz styl architektoniczny do modulu, w ktorym ten model zenkapsuluje

					- 4. Estymuj korzystajac z faktu, ze juz wczesniej robiles te rzeczy

	- 2. Luki w wiedzy

		- Ogolne wymagania

			- precyzuja sie pozno

			- estymaty czegos ogolnego musza byc niedokladne

		- Braki w wymaganiach, ktorych nie widac

			- po spotkaniu z biznesem wydaje sie, ze znamy wymagania

			- ale so one zebrane w formie, ktora nie pokazuje luk

			- wychodza dopiero podczas implementacji

				- musze dopytac, cos sie nie zgadza

		- Niezrozumienie po stronie zespolu

			- mam precyzyjne wymagania bez luk, ale zrozumialem to inaczej, niz biznes sobie wyobrazal

				- feedback dociera po pierwszym demo

		- Mitygacja

			- Uwidacznianie wiedzy

			- Skracanie/zbieranie feedbacku

			- Wykrywanie luk wiedzy biznesowej

			- Narzedzia

				- Event Storming

				- Metryki

				- BDD

	- 3. Duzy zakres prac

		- zadania, ktore wydaja sie niepodzielne

		- rozwiazania, ktore mocno ingeruja w istniejacy kod

			- duzy coupling

			- robimy wszystko albo nic

		- Mitygacja

			- Bounded Context

				- dzieki nim mozemy podzielic nasze modele (encje) na wiele mniejszych modeli realizujacych konkretna funkcjonalnosc

					- dzielimy jeden duzy problem na wiele malych

			- Elementy konstrukcyjne

				- bardzo duza funkcjonalosc dzielimy bounded contextami na mniejsze

				- nastepnie w ramach jednego BC

					- skladamy modul z elementow konstrukcyjnych

						- kazdy element to podzadanie

							- ktore estymujemy osobno

								- a pozniej sumujemy, dodajac buffor

	- 4. Zmiana wymagań

		- Jedyna stala rzecza w zyciu jest zmiana

		- Mitygacja

			- Okreslic, ktore zmiany wymagan nas bola

				- Latwe do wprowadzenia zmiany nie bola

				- Bola te, ktore zajmuja duzo czasu

					- Psuja design

					- Wykraczaja poza zakres funkcjonalnosci, nad ktora pracuje

			- DDD

				- Subdomeny

					- Jesli moj system nasladuje strukture biznesu (subdomeny)

					- to zmniejszam szanse, ze wymagania wymagania wyjda poza subdomene

						- bo osoba, od ktorej je dostaje, rowniez pracuje w tej subdomenie

				- bounded contexty

					- dzieki podzielniu modelu na wiele malych modeli, wprowadzanie zmian jest zlokalizowane

						- zmniejszam ryzyko, ze zmiana bedzie kosztowna

							- maly model latwo sie zmienia

	- 5. Czekanie

		- Czas realizacji = Czas pracy + Czekanie

		- Estymujac bierzemy pod uwage czas pracy

			- pomijamy czekanie

		- Mitygacja

			- Autonomia

				- Bounded context

					- uzywajac BC, zmniejszamy ryzyko komunikacji z innymi modulami, komponentami w systemie

						- a zatem innymi osobami/teamami

					- zmniejszamy ryzyko, ze zmiany w innych komponentach beda wplywaly na nasz komponent

				- prawo Conwaya

					- jesli pokrywamy strukture

						- biznesu

						- zespolow

						- kodu

					- to mozemy budowac autonomie zespolow

						- zmniejszamy szanse, ze bedziemy musieli na kogos czekac

					- cross-functional teams

						- zespol musi miec wszystkie kompetencje do dostarczenia funkcjonalnosci

							- jesli musze pozyskac kompetencje z zewnatrz, to trace autonomie

							- decyzje techniczne powinny brac pod uwage kompetencje techniczne w zespole

				- automatyzacja

					- awarie, pozary odciagaja nas od pracy

					- im wiecej procesow mamy zautomatyzowanych, tym mniejsza szansa na pozar

						- pipeline CI/CD

						- pipeline budowania i testowania

						- skrypty dot. powtarzalnych prac

						- monitoring z automatycznymi alertami

### Konkluzja

- wiedzy kiedy nie estymowac

- uzywaj elementow konstrukcyjnych

	- szukaj powtarzalnosci

		- do porownywania fukcjonalnosci

		- estymacja historyczna

- szukaj autonomii

- skracaj cykl feedbacku

	- ES

	- metryki

	- BDD

## Lekcja 6.05. Implementacje modelu domenowego

### Przyklad

- Jak wyglada diagram rozwiazania, modelu domenowego?

	- Czesto odpowiedzia jest diagram encji / schemat bazy danych

		- On zawiera tylko dane

		- Brakuje zachowan

		- To jest model danych, nie domenowy

			- Model domenowy bedzie potrzebowal modelu danych

				- Do pamieci dlugotrwalej

				- Beda zyc w symbiozie, ale sa to rozne koncepty

### Modele

- Anemiczny

	- Mapowanie jeden do jednego

		- tabela do klasy

		- kolumna do pola

		- relacje bazodanowe przez referencje miedzy obiektami

		- To moze zrobic ORM

	- Getter i settery

		- Rozmawiamy z konkretnymi kolumnami tabeli

	- **Nie modeluje zachowan**

	- Zachowania sa w warstwie wyzej - serwisu

		- Operuja na danych poprzez DAO

			- 1. DAO wyciaga obiekt

			- 2. Operujemy na wnetrznosciach obiektu

			- 3. DAO zapisuje obiekt po zmianach

		- Zwykle dzieje sie w kontekscie ORM

			- Daje transakcyjnosc, przetwarzanie wspolbiezne - optimistic locking

	- Modernizacja Transaction Script

		- Bezposrednia rozmowa z baza danych

			- Get -> SELECT

			- Set -> INSERT, UPDATE

			- Sami musimy dostarczyc transakcyjnosc i optimistic locking

				- Ale koncepcyjnie dziala tak samo

				- Pozbylismy sie warstwy abstrakcji

		- Proceduralny kod, ktory rozmawia z baza, aby wykonac operacje biznesowa w jednej transakcji bazodanowej

		- Przewaga modelu anemicznego

			- wieksza czytelnosc

			- zarzadzanie transakcjami

			- blokowanie optymistyczne

			- nie piszemy SQL

			- statyczne typowanie

		- Przewaga Transaction Script

			- operacje BULK

			- operacje specyficzne dla bazy

			- abstrakcja ma koszt

				- wyciagamy wszystkie subskrypcje

					- ruch na sieci pomiedzy baza a aplikacja

					- zajmuje pamiec zalodowanymi danymi

					- iterujemy po danych, zajmujac czas procesora

- Bogaty

	- Enkapsuluje dane

		- Jedyna mozliwoscia dostepu do danych jest przejscie przez zachowania

			- ktore maja reguly

	- Obiekty, ktore maja i zachowania i dane

### Porownanie modeli

- Transaction script

	- Reguly

		- w warstwie aplikacyjnej

	- Dane

		- w bazie danych

	- Bezposrednio operujemy na danych

	- Zalety

		- prostota

		- latwy w zrozumieniu

		- wydajny

		- Dobry do problemow o niewielkiej logice

			- W dzisiejszych czasach pewnie uzyjemy abstrakcji - modelu anemicznego

- Anemic

	- Reguly

		- Nie sa ograniczaja dostepu do danych

	- Dane

		- Mapujemy do kodu

			- ale sa osobno od regul

	- **Dobre, gdy problem jest prosty**

		- Na DLES

			- Komenda -> zdarzenie, Komenda -> zdarzenie

		- Malo lub brak logiki biznesowej

- Rich

	- Reguly

		- Jedna mozliwosc dostepu do danych

	- Dane

		- Mapujemy do kodu

		- Dostepne tylko przez reguly

	- **Dobre, gdy mamy zlozona czesto zmieniajaca sie logike**

		- Na DLES

			- hotspoty

			- duzo regul

			- duzo watpliwosci

		- Pozwala duzo eksperymentowac

		- Model bedzie rozwijalny

- Nie zawsze musimy miec bogaty model

- Dobor rozwiazania

	- Transaction Script

		- Operacje bulk

		- operacje specyficzne dla bazy

		- zlozone odczyty

	- Model anemiczny

		- prosta logika

		- rzadko zmieniana logika

	- Bogaty model domenowy

		- bogata logika

		- czesto zmieniana

## Lekcja 6.06. Agregaty

### Stosowanie modelu anemicznego, gdy powinnismy zastosowac bogaty

- Pewna doza niepwnosci, niejasnosci, spodziewamy sie eksperymentow, nie jest proste

	- Mimo tych przeslanek, decydujemy sie na model anemiczny

		- Efekt: Niespojnosc

			- wszyscy maja dostep do wszystkich tabelek

			- design wspiera bezposrednia modyfikacje wybranych danych

			- wiedza o zachowaniu spojnosci lezy po stronie programisty

				- jesli zmienamy dana X, to musimy zmienic Y

				- przy wielu programistach i wymaganiach, jest to niemozliwe do spelnienia

- Przyklad: pauzowanie subskrybcji

	- 4 tabelki -> 4 klasy

	- gettery i settery

	- SubscriptionService

		- pauseSub

			- Atomowo wykonane trzy operacje w transakcji

				- dodanie pauzy

				- zmiane licznika pauz

				- update daty ostatniej pauzy

		- Nowe funkcje

			- Usuwanie pauzy

				- Bo subskrybenci omylkowo pauzuja

				- Mamy PauseService i PauseDao

					- Znajdujemy pauze przez DAO

					- I usuwamy przez DAO

					- W ten sposob nie aktualizujemy licznika pauz i daty ostatniej pauzy

						- wprowadzamy system w stan niespojnosci

							- przy wielu tabelach, dao i programistach - prawdopodobienstwo wprowadzenia systemu w stan niespojnosci jest bardzo duze

						- takie bledy ciezko sie naprawia, bo sa zauwazane, jak ktos juz podjal decyzje na podstawie niespojnego stanu

							- trzeba odkopac z czego wynikal problem

			- Odjecie punktow lojalnosciowych za kazdym razem, gdy pauzujemy subskrybcje

				- W systemie beda inne operacje dzialajace na subskrybencie

					- Potencjalnie niezalezne biznesowo transakcje

						- Zmiana numeru telefonu subskrybenta

						- Pauzowanie subskrybcji

						- Zostaja zablokowane w bazie, bo dotykamy tego samego rekordu subskrybenta

					- Prowadzi do konfliktu transakcji

						- Jesli doszlo do operacji wspolbieznych

						- A przy wielu uzytkownikach, to sie moze wydarzyc

					- W zaleznosci od bazy danych

						- jedna transakcja czeka na druga

							- MS SQL

						- Jesli pierwsza wykonala zmiane, to druga rzuci blad

							- Postgres

							- Musimy ja ponowic

					- UX sie pogarsza, bo subskrybent czeka

					- Skalowalnosc sie pogarsza, bo te transakcje moga sie kolejkowac

- Konflikt transakcji

	- Bazodanowych, nie biznesowych

		- dla biznesu jest dziwne, ze te operacje sa zalezne

	- Operacje niezwiazane biznesowo sa wzajemnie blokowane

	- Pogarsza sie skalowalnosc oraz UX

- Czytelnosc kodu

	- Po to odkrywalismy jezyk domenowy, zeby w miejscach o wysokiej zlozonosci go stosowac

		- W miejscach zlozonych sa czeste zmiany

			- Czeste zmiany, to duzo czytania tego kodu

			- Zatem powinien byc czytelny

		- **Uzycie jezyka domenowego zwieksza czytelnosc**

	- Istnieja operacje domenowe, ktore skutkuja taka sama zmiana stanu w bazie danych

		- Np. utworzenie subskrybcji i przyjecie platnosci

			- skutkuja zmiana flagi active na true

		- Znalezienie miejsca w kodzie, gdzie tworzymy subskrybcje jest bardzo trudne, bo wszedzie jest subscription.setActive(true)

			- Rozroznienie moze byc widoczne w warstwie serwisow

			- Albo nawet w warstwie prezentacji

				- Wysyla DTO do warstwy serwisow

- Powstale problemy

	- mozliwa niespojnosc

	- wzajemne blokowanie niezwiazanych biznesowo transakcji

		- mniejsza skalowalnosc

	- czytelnosc kodu

### Rozwiazania

- Niespojnosc

	- Enkapsulacja

	- Wprwadzamy bogaty model domenowy, ktory enkapsuluje dane i zachowania w jednym miejscu

		- Jedyny sposob na modyfikacje danych to przejscie przez reguly/zachowania

		- Wyjmujemy gettery i settery z serwisow i przekladamy to do klasy subskrybcji

			- Gettery i settery znikaja

			- Modyfikaca danych przez metode dostepowa

				- Dzieki temu nikt nie siegnie do wewnetrznego stanu

				- Potencjalnie powodujac niespojnosc systemu

				- Developer chcacy dodac usuwanie pauzy, bedzie musial zajrzec do tej klasy i zobaczyc dodawanie

			- Skoro nie mamy getterow i setterow, musimy miec nazwe metod

				- One sa w jezyku domenowym

					- To rozwiazuje od razu problem braku czytelnosci

		- Pauza staje sie szczegolem implementacyjnym Subskrybcji

			- wiec ma mniejsza dostepnosc, np. pakietowa

- Brak czytelnosci

	- Komplementarny do niespojnosci

		- Rozwiazany razem

			- Przez enkapsulacje

- Konflikty transakcji

	- Musimy zastanowic sie, co  w takiej obsludze transakcji/komendy jest nadmiarowe

		- Gdzie siegamy do zbyt wielu danych

		- Przez co stwarzamy ryzyko, ze inne transakcje modyfikuja te same dane

	- Intuicyja mowi, ze punkty lojalnosciowe tu nie pasuja

		- Ale nie mozemy polegac na intuicji

	- **Heurystka**

		- **Szukanie niezmiennikow**

			- Czy istnieje logika biznesowa, ktora mowilaby, ze jesli mam x punktow lojalnosciowych, to moge albo nie moge pauzowac?

				- Czy jest relacja miedzy punktami a pauza

				- Odpowiedz znajde na Design Level Event Stormingu

					- Szukamy regul biznesowych

						- Zolte karteczki

				- Nie ma, wiec mozemy rozbic na dwie transakcje

					- Uzywajac eventual consistency

					- Minimalna liczbe danych zmieniamy w pierwszej transakcji

						- subskrybent dostanie szybka odpowiedz

					- Minimalna jest szansa na blokowanie z innych transakcji

				- Gdyby regula byla

			- Reguly biznesowe

				- Niezmienniki

					- zawsze musza byc spelnione

					- inaczej jest katastrofa

					- nawet na kilka ms nie moze byc niespolnosci

					- Przyklad

						- nie moge zapauzowac subskrybcji past due

				- Zasady biznesowe

					- Reguly, ktore nie musza byc zawsze spojne

					- Raz na jakis czas dopuszczamy niespojnosc

				- Dzieki podzialowi mozemy odchudzic transakcje

					- I zmniejszyc ryzyko konfliktu miedzy transakcjami

					- Warto szukac prawdziwych niezmiennikow i odroniac je od zwyklych zasad

### Grupowanie komend

- 1. Biore niezmiennik

- 2. Szukam komend, ktore maja wplyw na dane, ktorymi zainteresowany jest niezmiennik

	- Operuja na tych samych danych

- 3. Stworz jeden obiekt z polaczonych komend/zachowan

	- Metody w jezyku domenowym

- 4. Majac zachowania, zaczynamy odkrywac pola

	- Odwracamy zachowanie, bo klasycznie najpierw tworzy sie pola

		- Mamy tyle pol, ile potrzebujemy

		- Klasa jest minimalistyczna

		- Obiekty sa granularne

		- Latwiej sie je testuje

- Przyklad

	- Komenda Oznacz jako past due oraz Pauzuj korzystaja z tych samych danych

		- Jedna zmienia, druga pyta

	- Podobnie: Pauzuj i wznow

		- Kiedy bylo ostatnie wznowienie?

	- Komendy wpadaja w jeden obiekt

		- I mamy API obiektu, nie wiedzac jak on to robi

		- Klasa nazywa sie Cos

			- Dobra praktyka jest nazywanie dopiero, gdy znamy wszystkie zachowania

	- Jesli subskrybcja jest zablokowana, to nie moge jej wznowic

		- Potrzebuja pola statusu / isDisabled

	- Moge pauzowac, jesli nie przekroczylem limitu pauz

		- Potrzebuje nowych pol

			- limit pauz

			- liczba uzytych pauz

- Efekt

	- Znalezlismy granice transakcji

	- Zapewnilismy spojnosc grafu obiektow

	- Jestesmy blizej programowania obiektowego

### Agregat

- Obiekt, ktory jest granica transakcji i spojnosci 

	- w nomenklaturze Taktycznego DDD - agregat

- Graf obiektow domenowych, ktory...

	- Zawsze jest spojny

		- Jesli usuwam pauze, to zmieniam licznik pauz i date ostatniej pauzy

	- Zapewnia granice transakcyjnosci

		- Dlatego nie maja referencji do innych agregatow

			- Bo istnieje szansa, ze zmienimy stan innego agregatu i dostaniemy blokowanie transakcji

	- Jest jednostka persystencji

		- Bedzie w calosci wyciagany z bazy i w calosci zapisany

			- po weryfikacji niezmiennikow

	- sprawdza niezmienniki systemu

	- komunikuje sie tylko przez obiekt, ktory jest korzeniem

		- **Aggregate Root**

		- bo chcemy miec spojnosc i przejscie przez reguly

		- Klienci beda zawsze rozmawac z Subskrypcja, a nigdy z Pauzowaniem

- Zasady

	- Modyfikujemy jeden agregat w transakcji

	- Zapisujemy w calosci (jednostka persystencji)

		- wiec mozemy partycjonowac

			- skalowalnosc

	- Nie ma referencji pomiedzy agregatami

		- Dlaczego nie mamy referencji do Planu Subskrypcji, tylko mamy kopie max liczby mozliwych pauz w naszym agregacie Subskrypcja?

			- Nie modyfikujemy stanu Planu Subskrybcji

		- Wynika to z granic kontekstow

			- Relacja jest niepotrzebna, bo plany subskrypcji zyja swoim zyciem, a subskrypcje swoim

				- Co jesli chcemy usunac plan, bo jest nierentowny?

					- Wiezy spojnosci referencyjnej by nam nie pozwolily

				- Dzieki temu, ze wyszlismy od metod/zachowan, to dostalismy odzwierciedlenie biznesu - kopie max. liczby pauz

	- Odpowiednie modelowanie Bounded Contextow i agregatow zmniejsza potrzeba relacji miedzy nimi

		- Relacje powinny byc minimalne

		- Jesli widzimy relacje, pytamy: czy granice sa ok?

	- Persystencja

		- Wzorzec repozytorium

		- Baza danych

			- Relacyjna

			- Dokumentowa

				- Najlepsza

					- Bo latwiejsza reprezentacja grafu obiektow

				- Zwalcza impedance mismatch

### Komedna a Pytanie (Query)

- W Subskrypcji mamy liste Pauz

	- Nie wynika ona z zachowan subskrypcji

	- Jest potrzebna do CQRS

### Krok po kroku

- 1. enkapsuluj zmiany stanu pod biznesowa komenda

	- ktora ma nazewnictwo zgodne z wszechobecnym jezykiem danego kontekstu

	- mamy intencje biznesowa i ona enkapsuluje zmiany stanu w agregacie

- 2. w komendzie obsluguj tylko prawdziwe niezmienniki

	- upewnij sie, ze nie ma zmian, ktore mozna przeniesc do innej transakcji

		- Eventual Consistency

- 3. grupuj wzajemnie wplywajace na siebie komendy w jeden obiekt

	- Znajdz niezmienniki, ktore korzystaja z danych, ktore moga byc modyfikowane przez inne komendy

		- Jesli Pauzuj nie moze byc wyonana, gdy Subskrypcja ma status PastDue, to komenda, ktora zmienia status na PastDue wpadnie do tego samego obiektu

- 4. nazwij agregat

	- Gdy mamy juz zachowania

- 5. Zapewnij komunikacje tylko przez korzen

	- Stan agregatu modyfikujemy tylko przez metody dostepowe

	- Zadnych getterow i setterow

- 6. Upewnij sie o braku referencji do innych agregatow

	- Po to zeby zminimalizowac ryzyko blokowania transakcji

- 7. Zapewnij optymistyczne blokowanie

	- Mimo, ze szansa na blokowanie transakcji jest mala, to jest

### Wnioski

- gdy logika jest zlozona, czest zmienna

	- buduj bogaty model domenowy

	- anemiczny model doprowadzi do problemow

- jesli system ma wielu wspolpracujacych uzytkownikow

	- szukaj malych agregatow

	- many writers vs. single writer, many readers

		- jesli malo writerow, to bardzo duza destylacja nie ma sensu

## Lekcja 6.07. CQRS (Command Query Responsibility Segregation)

### Agregat skupia sie na komendach

- Cel

	- Zachowanie spojnosci

	- Minimalizacja ryzyka konfliktu transakcji

	- Jest skrojony, odchudzony w celu optymalizacji zapisow

- Nie bierze pod uwage odczytow

	- A przeciez jest to istotny element

- Jak mozna by dodac funkcje odczytu do agregatu?

	- Dodac kolejne dane/pola do agregatu

		- Agregat znow rosnie, a specjalnie go odchudzalismy

		- Nie jest juz tak latwo testowalny i czysty

		- Latwo sie z niego dostac do innych obiektow i zlamac granice transakcyjnosci

		- Jesli ktos uzywa agregatu do przetwarzania komend, musi zaladowac wiele zbednych danych z bazy

			- To mozna by rozwiazac poprzez ladowanie danych zw. z widokiem leniwie

				- To jest jeszcze gorsze rozwiazanie, bo prowadzi do problemu N+1

	- Rozwiazanie

		- Zamiast dodawac dane po stronie klienta danych

		- Uzyjmy bazy danych

			- Jest stworzona do tego

			- Natywny SQL

				- Najszybszy sposob na rozmowe z baza danych

		- Mamy dwa obiekty

			- Agregat do zapisu/komend

			- Query do odczytu/widokow

			- Podstawowy CQRS

			- To ze uzywaja tych samych danych, nie znaczy, ze musi uzywac tych samych modeli

### CQRS

- Wzorzec zaproponowany przez Grega Younga

- Mamy dwa obiekty

	- Agregat do zapisu/komend

	- Query do odczytu/widokow

		- Nie ma szans zmienic stanu systemu

		- Nie ma szans na konflikt transakcji

	- To ze uzywaja tych samych danych, nie znaczy, ze musi uzywac tych samych modeli

		- Uzycie agregatu do odczytu wymagaloby tranformacji DB -> model domenowy -> DTO -> ViewModel

			- Za duzo pracy na prosta operacje

			- Przez DTO mogloby wyciekac szczegoly implementacyjne agregatu

				- **serializujac 1:1 szczegoly impelemntacyjne staja sie czescia published language**

		- Ale model bylby reuzywalny

			- Reuzywalnosc ma sens, gdy oba przypadki maja taka sama nature

			- Tutaj mamy komendy i query, czyli odmienne byty

	- Dwie klasy problemow -> dwie klasy rozwiazan

		- Roznice

			- Komend nie cachujemy, query tak

			- Komend nie mozemy bezpiecznie ponawiac, query tak

			- Zazwyczaj mamy wiecej query, niz komend

				- Wyjatek: np. IoT

		- Kazda klasa ma inne drivery architektoniczne

		- Zyskujemy na...

			- czytelnosci

			- testowalnosci

			- **wydajnosci**

- Stosujemy w obrebie lokalnych Bounded Contextow

- Co jesli faktycznie chce odczytac to, co zapisuje?

	- Do rozwazenia

		- Trzeba rozwazyc, czy serializujac taki obiekt do DTO nie lamiemy enkapsulacji

		- Czy zawsze bedziemy chcieli zapisywac/odczytywac to samo?

		- A moze to po prostu CRUD?

			- Wtedy cala rozkmina nie ma sensu

			- Wszystko rozwiazemy modelem anemicznym

### CQS

- Command Query Separation

- dobra praktyka programowania

- CQRS na niej bazuje

	- CQS poziomu systemowego

	- stosuje separacje i segregacje

		- segregowane dwa obiekty

- Zasady

	- Metoda...

		- albo zwraca wynik, ale nie zmienia stanu

		- albo zmienia stan i nie zwraca wyniku

	- Albo komenda albo query

- Czasem swiadomie lamiemy

	- Zwracamy z komendy wynik jej dzialania

	- operacje compare and swap

		- increment and get

### Synchronizacja modeli

- Problem

	- Komenda dokonuje malej zmiany

	- Query wyciaga efekt wielu takich malych zmian

		- W efekcie mozemy miec wiele joinow

		- To wplywa na wydajnosc

- Rozwiazanie

	- Zdenormalizowany stos danych obok starego

		- Synchronizacja

			- Widoki zmaterializowane w bazie

				- Czesto najszybsza technika w systemach legacy

				- Ale ciezka w testowaniu

				- I przeniesieniu do innej bazy

			- Synchronizacja bezposrednia

				- Obslgujac komende, w jednej transakcji zmieniamy stan rowniez stosu zdenormalizowanego

			- Synchronizacja zdarzeniami

				- Przygotowanie na przyszla asynchronicznosc

				- Pozbywamy sie obslugi dwoch modeli w jednej transakcji

					- Komenda nie czeka na drugi model

				- Przyjscie zdarzenia powoduje aktualizacje widokow

					- Potem mozemy wydajnie odpytac widok

### Jak to zrobic w legacy?

- wypisz logi SQL

	- generowane przez ORM

	- czesto to jest problem wydajnosci

- namierz problematyczne query

	- wypisz ich czas wykonania

		- narzedziem klasy Application Performance Monitoring

		- monitoruj przez 2 tyg

- zaimplementuj je jako natywne query

	- zazwyczaj skutkuje znaczacym wzrostem wydajnosci

- wyrzuc niepotrzebne mapowania z obiektow

	- te, ktore byly na potrzeby tego query

	- rzeczy, ktore nie sa potrzebne do walidacji regul I byly tam z pobudek odczytowych

- zastanow sie nad potrzeba cache, DTOs

- Efekt

	- odchudzilismy czesc systemu, jesli chodzi o stos do komend

	- i wprowadzilismy zwykle sapytanie

### Skalowalnosc odczyt vs zapis

- Osobne bazy danych

	- Baza do zapisu i odczytu

	- Mozemy horyzontalnie i asymetrycznie skalowac jedna ze stron

		- Stawiajac nowe instancje tej samej bazy

		- Nie ruszajac drugiej strony

	- Mozemy korzystac z roznych rodzajow baz

		- Relacyjna, grafowa, dokumentowa

		- W zaleznosci od specyfiki problemu

			- Relacja miedzy ludzmi

				- Social network

			- Wyszukiwanie full text

			- szukamy prawdziwych driverow architektonicznych

				- pamietajac, ze te wszystkie bazy trzeba utrzymywac

	- Musimy zapewni synchronizacje

		- Przez asynchroniczne eventy

			- Nie mamy spojnosci natychmiastowej

			- mamy koncowa

### Eventual consistency

- Potencjalne problemy

	- wyswietlanie danych

		- nawet majac jedna baze, mamy opoznienie/roznice miedzy tym, co widzi uzytkownik, a tym, co jest w bazie

			- bo sygnal sie propaguje

			- a przegladarka moze byc nieodświeżona

	- podejmowanie decyzji na podstawie wyswietlanych danych

		- rozmowa z biznesem wysteruje nas do decyzji, czy spojnosc koncowa w danym miejscu ma sens, czy nie

			- nie mowimy biznesowi, ze cos jest niespojne

				- to jest spojne, ale nie natychmiast

				- mowmy: aktualne na czas sprzed x czasu

			- przyklad

				- czy dane pogodowe sprzed 3 min na lotnisku sa ok?

					- my nie wiemy, biznes bedzie wiedzial

- jest charakterystyczna dla wielu biznesow

	- wiele bylo na swiecie przed komputerami

	- to programisci lubia spojnosc natychmiastowa i atomowosc

- Musimy podac czas sychronizacji

	- 3 min, a 3 dni to kolosalna roznica

		- mozemy zapisywac date ostatniej zmiany w trakcie aktualizacji widoku

			- i go wyswietlac

- Read Your Own Writes

	- Jesli postujemy cos na Twitterze, to nie ma znaczenia, czy wszyscy natychmiast to zobacza

		- z natury spojnosc koncowa

	- jesli ja jestem autorem, to chce go widziec od razu

		- inaczej klikne jeszcze raz

	- oszukuje po stronie frontendu

		- jesli serwer przyjal komende

		- to wyswietlam to, co napisalem

- To nie jest natura CQRS

	- CQRS to segregacja odpowiedzialnosci miedzy komendy, a query

	- W takim podejsciu, gdzie mowimy o mapowaniu odpowiedzialnosci

		- procesowanie komend to szczegol implementacyjny

			- nie ma znaczenia czy mamy

				- agregaty

				- anemiczny model domeny

				- command bus

				- serwisy aplikacyjne

	- moze byc katalizatorem rozmow

		- umozliwia, ale nie wymaga

### One-way command

- CQRS moze byc rozumiany jako podejscie analizy biznesowej

	- Moze nawet wplynac na wymagania funkcjonalne

- Mamy

	- UI

	- backend

	- szybki cache read-only

	- Command: zarejestruj usera

	- Niezmiennik: nick musi byc unikalny

		- rozpiety na duzym zbiorze danych

			- duze ryzyko blokowania

				- spada skalowalnosc i UX

- Mozemy czesc odpowiedzialnosci z komendy przeniesc na query

	- Cache ma informacje sprzed 3 min z lista nickow

	- UI pyta cache, czy nick istnieje

		- Jesli nie, wysylamy komende

			- Wysylamy asynchronicznie

				- Nie czekamy na odpowiedz z serwera, bo wg cache jest ok

				- superskalowalne rozwiazanie

			- Zminimalizowalismy szanse porazki, ale jej nie wykluczylismy

				- Dwie osoby moga wyslac komende z tym samym nickiem: joe

				- Wtedy drugi nick zmieniamy, np. joe1

				- I informujemy druga osobe mailowo, ze ma inny nick

					- UX i skalowalnosc wzrasta

					- ale zmienilismy proces biznesowy

						- analiza biznesowa musiala sie odbyc

			- Teoretycznie umozliwia to oszustwo

				- Od razu wysylamy komende, z pominieciem weryfikacji via UI

				- Na poczatku dostaniemy sukces

				- Ale potem mail, ze sie nie udalo

- W branzy czesto mowi sie, ze asynchroniczna komenda nie ma sensu

	- Bo idea komendy to potwierdzenie sukcesu

	- Taka komende mozemy traktowac, jako zdarzenie wysylane ze strony klienta bezposrednio do systemu

		- an event sent to our system

		- Semantyka jest taka sama

		- System zareaguja albo akceptacja albo informacja, ze zarejestrowano w inny sposob

		- Przyklad

			- Zamiast: zarejestruj z nickiem joe

			- Zarejestrowano z nickiem joe

## Lekcja 6.08. Długo działające procesy

### Rodzaje procesow

- Procesy lokalne

	- termin Lukasza Szydlo

		- inaczej proces „zwykly”

	- Cechy

		- sekwencja akcji

		- w obrebie jednego modelu

		- sa bezstanowe

		- czesto transakcyjne

		- czas jest modelowany implicite

			- przez sekwencje krokow

		- wiemy ile beda trwaly

			- monitorujemy ja

			- mamy metryki

	- Przyklad

		- Walidacja wideo

		- Mogloby to byc 4 metody w serwisie, wolane sekwencyjnie

- Procesy dlugo dzialajace (long-running processes)

	- Nie do konca fortunna nazwa, bo proces lokalny tez moze dzialac dlugo

		- Walidacja wideo moze trwac kilkanascie minut

	- Cechy

		- Posiada stan

			- pomiedzy swoimi krokami

		- Explicite modeluje czas

		- istnieja nieprzewidywalnie dlugo

	- Przyklad

		- Aktywacja konta

			- 4 warunki

				- 1. Admin zalozyl konto i wyslal zaproszenie

				- 2. Zaakceptowano zaproszenie

				- 3. Przydzielono uprawnienia

				- 4. Ustawiono 2FA

			- Moga wystapic w roznym czasie i kolejnosci

				- Dlatego potrzebujemy osobnego modulu, ktory zajmie sie koordynacja

			- Wszystkie musza byc spelnione, zeby aktywowac konto

				- **O to dba dlugo dzialacy proces**

			- Implementacja

				- Ma stan

				- Dostep do serwisu odpowiedzialnego za aktywacje

				- Dla kazdego zdarzenia mamy hadnler

					- Zmienia stan

					- I sprawdza, czy wszystkie warunki sa spelnione

				- Prostota jest mylaca

					- Skomplikowane jest to, co wokol

						- Infrastruktura

						- Zwlaszcza w systemach rozproszonych

					- Nie implementujemy samodzielnie

		- Najlepsza oferta

			- Integracja z innymi systemami

			- Kazdy z dostawcow moze odpowiedziec w innym czasie

				- Albo wcale

					- To jest moment, gdzie explcite modelujemy czas

						- Chcemy miec byt, ktory powie nam, ze minal czas oczekiwania na oferty

						- To jest po prostu kolejne zdarzenie

							- Czas minal

		- Aktywacja subskrypcji

			- Dwa zdarzenia niezbedne

				- Wybrano plan

				- Zakupiono subskrypcje

			- Jesli mamy zdarzenie: Anulowano Zakup

				- To od razu zamykamy LRP

	- Na Event Storming najczesciej oznaczane jako Polityki

		- Nie kazda Polityka bedzie dlugo dzialajacym zdarzeniem

			- Niektore moga nasluchiwac na zdarzenie i wykonywac akcje z tym zwiazana

		- Szukamy takiej, ktora...

			- Nasluchuje na kilka zdarzen

			- Albo zyje dluzej w czasie

				- Czyli wystepuje kilka razy na diagramie

### Saga vs Process Manager

- Rozne nazewnictwo LRP

	- Saga

		- bardziej zwiazana z zarzadzaniem dlugo trwajacymi transakcjami bazodanowymi

		- akcje kompensacyjne

		- obsluga bledow

	- Process Manager

		- w naszym rozumieniu to bardziej LRP

	- potencjalnie kolejne wzorce

		- kazdy moze byc zaimplementowany tak samo, korzystajac z tych samych narzedzi

		- maja rozne intencje i zakres ograniczen

### Narzedzia

- biblioteki

	- czasem zwykla maszyna stanow

- workflow engine

	- czesto dobre rozwiazanie

		- bo za darmo daja

			- monitorowanie

			- wersjonowanie

			- UI

	- moga byc embedded

- NServiceBus

	- tylko .NET

### Podsumowanie

- jesli czas jest istotny, modeluj go explicite

- polityki sa indykatorami

- implementacja jest nietrywialna

	- skorzystajmy z gotowych narzedzi

