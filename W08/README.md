# **Tydzień VIII Modularyzacja**


## Lekcja 8.01. Wstęp do modularyzacji

### Ogolnie

- Modulowy i modularny to synonimy

- Moduly to spojne segmenty, na ktore chcemy podzielic system

- W srodku modulow mamy wiele zaleznosci, a na zewnatrz modulow, jak najmniej

### Zmiany

- zmieniamy wymagania

	- czesto priorytety odwracaja sie o 180 stopni, bo reagujemy na zmiany rynkowe

- zmieniamy technologie

	- wynika to z driverow architektonicznych

	- przede wszystkim atrybutow jakosciowych

		- np. bezpieczenstwo

		- skalowalnosc

		- testowalnosc

- zmieniamy zespoly

	- ludzie przychodza i odchodza

	- mamy ograniczenia projektowe zw. z dostepnoscia ludzi i ich wiedza

- sa nieuniknione

	- bazowa idea Agile jest mozliwosc dokonywania szybkich, czestych zmian niskim kosztem

	- wiec musza byc latwe

		- jasny zakres zmiany

			- sprecyzowane miejsce do zmiany

			- gdy dodajemy feature, to chcemy miec jedno miejsce w systemie, ktore ulegnie zmianie

		- zmiana nie wymusza kaskadowych zmian

			- wplywa na koszt wprowadzania zmian

		- niska „lepkosc” (viscosity)

			- cecha systemu, ktorego design/struktura wspiera dodawanie nowych funkcjonalnosci przy zachowaniu tego designu

			- system, ktory wymaga dodawania hackow i zmiany struktury/designu w celu dodania feature’ow, to system o wysokiej lepkosci

				- lepimy funkcje, a nie towrzymy je zgodnie ze struktura

### Ewolucyjnosc

- zachowanie/osiagniecie ewolucyjnosci to nasz cel

- meta driver opisujacy inne drivery

- mozliwosc ciaglego zapewnienia wybranych driverow

	- i dodawania nowych

- Przyklad

	- jesli nasze drivery to testowalnosc, utrzymywalnosc i czytelnosc i mozemy je zachowac dodajac kolejne drivery, np. wymagania funkcjonalne to mamy system ewolucyjny

- osiagamy za pomoca modularyzacji

### Modularyzacja

- podzial na moduly

- Modul

	- grupa logicznie zwiazanych funkcji

		- skoro grupuje zwiazane funkcje, to...

			- zaweza zakres zmian

			- powoduje, ze zmiany nie sa propagowane

			- bo rzeczy, ktore zmieniaja sie razem sa w jednym miejscu

- Modul vs Komponent

	- Modul

		- istnieje w swiecie statycznym

			- system wylaczony

			- nie na produkcji

		- nie wszyscy trzymaja sie tej definicji

			- w modelu C4, na poziomie C3 mowilismy o komponentach, chociaz zgodnie z ta definicja sa to moduly

	- Komponent

		- instancja modulu

	- Przyklad

		- mamy 4 klasy, ktore stanowia modul

		- w czasie wykonanie te klasy zamieniaja sie w instancje/obiekty, tworzace komponent

- Przyklad

	- Samochod

		- przechodzi przez rozne hale produkcyjne, gdzie na kazdej dodawane sa inne moduly: karoseria, zawieszenie, elektronika, itp.

		- pozniej mozemy wymienic wycieraczki, skrzynie biegow, etc.

		- mozemy kupic uzywana czesc, wiec reuzywalnosc

		- Gdyby to bylo IT...

			- wyobrazmy sobie, ze aby wymienic klocki, trzeba wymienic zawieszenie

			- zeby tankowac, trzeba wymieniac przednie swiatla

			- tak mysli biznes, gdy slyszy o rozwiazaniach w kodzie

				- bo nie rozumieja powiazan, ktore powstaly na etapie rozwiazania

				- dlatego warto te powiazania minimalizowac

	- Pociag

		- dostawianie kolejnych wagonow, zmiana lokomotywy

			- powiazania miedzy modulami sa trwale, ale latwo wymienialne

		- wagony sypialne, restauracyjne

	- Komputer

		- wymiana matrycy nie pociaga wymiany karty graficznej

- Modularnosc jako rozwiazanie

	- sama w sobie nie jest celem

		- nie wszystko musi byc modularne

	- jest rozwiazaniem problemu

		- zapewnia ewolucyjnosc

		- jesli nie potrzebujemy ewolucyjnosci, to modularyzacja nie musi byc potrzebna

			- np. system, ktory ma wejsc na produkcje za 2 tygodnie i obsluzyc black friday

				- driverem jest ograniczenie projektowe: czas

				- dziala jeden dzien, wiec nie obchodzi nas czytelnosc, czy utrzymalnosc

				- modularyzacja nas spowolni

### Moduly a Bounded Context

- BC ma granice lingwistyczne

	- podsystem o granicach lingwistycznych, w srodku ktorych jezyk jest spojny

	- przestrzen rozwiazania

- Modul ma granice logiczne

	- przestrzen implementacji

- Przyklad

	- BC Przygotowywanie video

	- Zawiera 2 moduly

		- validacja video

		- transkrypcje video

- czesto BC jest reprezentowany jako modul

	- chcemy uwidocznic BC, aby zwiekszyc czytelnosc struktury rozwiazania

	- bedzie mial kolejne podmoduly

### Zalety

- latwiejsze zrozumienie

	- divide and conquer

	- utrzymalnosc

- elastycznosc

	- moduly mozemy ze soba komponowac

- testowalnosc

	- osobno testowac

- wymienialnosc

	- mozemy wymienic modul nie dotykajac innych czesci systemu

- reuzywalnosc

- zrownoleglenie prac

### Wektor zmian

- ciezko wyobrazic sobie modularyzacje, ktora umozliwialaby ewolucyjnosc w kazdym mozliwym wektorze zmian

- jesli wektorem zmian jest czeste wymienianie technologii bazodanowej

	- to moduly techniczne - dostep do danych, logika biznesowa, UI - beda wspierac taka zmiane

	- bo zakres zmian jest w jednej warstwie

- w praktyce zmiany raczej dotycza kontekstow biznesowych

	- przyklady

		- wymiana uslugodawcy platnosci

		- zmiana metod platnosci

	- podzial techniczny spowoduje, ze taka zmiana rozpropaguje sie po kilku warstwach technicznych

	- wiec lepiej podzielic biznesowo

		- mozna modul biznesowy podzielic na podmoduly techniczne

- Zasada kciuka

	- Jesli widzimy rozne sposoby modularyzacji i kazdy kosztuje mniej wiecej tyle samo, to wybieramy taki, ktora wspiera wiecej wektorow zmian

		- Bo nie potrafimy przewidziec przyszlosci

		- A oprogramowanie, ktore mozemy zmienic w wiekszej liczbie kierunkow jest dla biznesu bardziej wartosciowe

## Lekcja 8.02. Enkapsulacja

### Modul to grupa logicznie zwiazanych funkcji/konceptow

- Reprezentacja zalezy od technologii

	- pakiet

	- przestrzen nazw

- Przyklad

	- Modul subskrypcji, katalogu i publikacji

	- przyjmuja liste video

	- zmieniamy na zbior video

	- i wszyscy kliencie naszych modulow musza taka zmiane wprowadzic

		- bo to byl publiczny kontrakt

	- i nagle prosta zmiana techniczna musi byc rozpropagowana po wszystkich modulach, ktore korzystaly z takiej informacji

		- zmiana nie jest ani prosta ani tania

	- potrzebujemy kontraktu

- Kontrakt

	- obiekt Kurs, a nie lista/zbior video

		- pozwala na zmiany techniczne

			- lista -> zbior

		- ale pozwala tez na zmiany biznesowe

			- Kurs nie reprezentuje juz listy video

			- moze byc to kurs odbywajacy sie na zywo online

		- za pomoca kontraktu spelniamy rozne wektory

### Moduly != Modularazycji

- modularyzacja wymaga kontraktu

- brak kontraktu skutkuje brakiem modularyzacji

	- zmiany beda sie propagowac po calym systemie

- Kontrakt nie musi skutkowac modularyzacja

	- nawet jesli mamy abstrakcje i kontrakt, to nie znaczy, ze ta abstrakcja jest na odpowiednim poziomie

	- przyklad

		- sprawdzamy, do jakich kursow ma dostep uzytkownik

			- potrzebujemy do tego katalogu, subskrypcji i publikacji

		- po chwili biznes mowi, ze jeszcze musimy sprawdzic, czy kurs jest ocenzurowany

			- wiec musimy odpytac modul Cenzura

		- ta zmiana dotknie wszystkich, ktorzy pokazywli dostepne kursy

			- mimo ze mamy abstracke Kursy

	- brakowalo abstrakcji na wyzszym poziomie

		- modul Dostepnosc

			- zmiana tylko w tym module

- Kontrakt jest warunkiem koniecznym, ale nie wystarczajacym

- Enkapsulacja

	- Kontrakt osiaga sie za pomoca enkapsulacji

		- ukrywanie szczegolow implementacyjnych obiektu

			- one nie sa dostepne na zewnatrz obiektu

			- na zewnatrz dostepne sa zachowania

	- Definicja

		- zaklada, ze mamy publiczna abstrakcje i prywatne szczegoly

		- ukrywanie szczegolow

			- jak vs. co

			- implementacja vs. abstrakcja

		- **ukrywanie tego, co zmienne, ulotne**

			- klucz modularyzacji

	- dotyczy obiektu, modulu, mikroserwisu...

		- takie samo myslenie dla kazdego z tych bytow

- Modularyzacja

	- wypisz wazne/trudne decyzje zwiazane z designem

	- takie, ktore maja duze szanse na zmiane

	- projektuj moduly tak, aby te decyzje enkapsulowac/ukrywac

		- tak, aby mozna ja bylo zmieniac

### Czeste „zapachy”

- niepelna abstrakcja

	- mimo, ze modul mowi o kursie, to gdzies i tak mozemy wyciagnac liste video

- brak abstrakcji

	- nie ma konceptu kursu, jest lista video

- cieknaca abstrakcja

	- poszczegolne moduly zapewniaja abstrakcje, ale kolejnosc ich wywolan jest istotna dla klienta

- niewykorzystana abstrakcja

	- klient musi sprawdzic, z jakim typem ma doczynienia

		- nie mowimy o pattern matchingu

### Klient naszego kodu

- Jak to dziala?

- Nie wiem i nie chce wiedziec!

	- Bo to, co wystawiamy na zewnatrz jest wystarczajace

	- Jak skrecam kierownice, to nie chce wiedziec, co sie dzieje pod spodem

## Lekcja 8.03. Coupling

### Wszyscy mowia: Low coupling, high cohesion.

### Definicja

- Jest miara tego, jak zdrowe sa polaczenia miedzy modulami

- Miara zaleznosci miedzy modulamie/obiektami/mikroserwisami

	- Myslimy o tych zaleznosciach w ten sam sposob na kazdym z tych poziomow

### Porownanie systemow

- Bardzo autonomiczne moduly

	- W ogole nie rozmawiaja ze soba

	- Bezuzyteczny system

		- Nie dowozi funkcji biznesowych

- Wszystko rozmawia ze wszystkim

	- omijajac warstwy abstrakcji

	- rozmawiajac ze szczegolami implementacyjnymi innych modulow

	- kazda zmiana bedzie propagowana do innych modulow

- Rozwiazanie posrednie

	- omijamy szczegoly implementacyjne

	- patrzymy tylko na abstrakcje

	- zdrowe polaczenia tworzace wartosc biznesowa

### Rodzaje

- Content Coupling

	- jeden modul rozmawia bezposrednio z wnetrznosciami drugiego

		- uzywa szczegolow implementacyjnych

	- najmniej akceptowalny coupling

- Common Coupling

	- dwa moduly polegaja na wspolnym, globalnym stanie

		- np. bazie danych

		- globalne zmienne

	- nie komunikuja sie bezposrednio, ale przez ten stan

- External Coupling

	- dwa moduly komunikuja sie przez zewnetrzny protokol, interfejs

		- jesli on sie zmieni, to komunikacja padnie

- Control Coupling

	- jeden modul mowi drugiemu, jak ma wykonywac swoja prace

		- np. ustawiajac/przekazujac flage

		- np. mowiaca, ze mamy wlaczyc lub wylaczyc walidacje w konkretnym przypadku

- Stamp Coupling

	- modul A przekazuje strukture danych do B, a B korzysta tylko z podzbioru pol tej struktury

		- mamy coupling do calej struktury, mimo ze potrzebujemy tylko jej fragmentu

- Data Coupling

	- przekazujemy wszystko, co potrzebne jest do komunikacji i nic wiecej

		- optymalna komunikacja

	- najbardziej akceptowalny coupling

### Tight vs. loose

- Tight / mocny

	- nasz modul wie bardzo duzo o szczegolach implementacyjnych drugiego

	- zwykle gdy nie mamy enkapsulacji

	- coupling do detali

	- zwieksza propagacje zmiany

	- np. pociag

		- gdyby wagony trzeba bylo spawac

- Loose / luźny

	- gdy polegamy na abstrakcjach

	- coupling do abstrakcji

	- jeden modul ma minimalna wiedze o drugim module

	- redukuje liczbe zalozen pomiedzy dwoma modulami, ktore sie komunikuja

	- np. pociag

		- latwo mozna wymieniac wagony, nie wiedza duzo o sobie, wiaza sie przez abstrakcje

### Explicit vs. implicit

- Explicit

	- mowilismy o nim do tej pory

	- syntaktyczny / składniowy

		- w kodzie widzimy zaleznosci

- Implicit

	- niejawny

		- nie widac go w kodzie

	- najgroźniejszy

	- np. jeden mikroserwis pisze do bazy, a drugi czyta oczekujac konkretnego formatu

		- pierwszy serwis moze zmienic format

			- komunikacja przestanie dzialac

### Coupling semantyczny

- Jeden modul polega na konceptach, wiedzy ktore zna drugi modul

- Np. wiedza, ze Kurs to lista video

	- jesli zmieni sie koncept i kurs bedzie onsite, to inne moduly korzystajce z tej wiedzy beda musialy zmienic implementacje

		- mimo ze jawni sie nie komunikuja

		- nie uzywaja swoich abstrakcji, czy nawet szczegolow implementacyjnych

- np. jedna strona szyfruje algorytmem X, to drua strona musi znac komplementarny algorytm deszyfrujacy

### Coupling Logiczny

- widzimy, ze zawsze, gdy zmieniamy jeden modul, to musimy zmienic drugi

- wychodzi w retrospektywie

- pokazuje, ze brakuje nam abstrakcji

	- albo ze mamy skopiowany kod

- wyjdzie przy analizie historii systemu kontroli wersji

	- commity zawsze dotykaja modulow, ktore nie sa bezposredniu zwiazane

### Metryki

- Dotycza couplingu strukturalnego, syntaktycznego

	- jawny w kodzie

- Liczba polaczen

	- wejsciowych

	- wyjsciowych

- Niestabilnosc

	- wyjsciowy / (wejsciowy + wyjsciowy)

		- od 0 do 1

		- 0 oznacza 0 wyjsciowych polaczen

			- duza stabilnosc

- Przyklad

	- plany-ui

		- zalezy od wielu modulow

		- malo modulow z niego korzysta / od niego zalezy

		- czesto

			- warstwa prezentacji

			- frameworki

	- platnosci

		- nie zalezy od niczego

		- od niego zalezy wiele modulow

		- czesto

			- warstwa persystencji

				- w architekturze warstwowej

			- biblioteki

				- to my wolamy biblioteke, nie odwrotnie

	- subskrypcje

		- zalezy od innych

		- inni zaleza od niego

		- czesto

			- logika biznesowa

		- niestabilnosc

	- marketing

		- nie zalezy od innych

		- inni nie zaleza od niego

		- cos nieuzywanego

			- cos do usuniecia

- Sama metryka niewiele mowi

	- trzeba podzielic na wejsciowy i wyjsciowy

	- limt liczbowy ma sens tylko w kontekscie warstwy, w ktorej jestesmy

		- nie mozemy ustalic buildu na „coupling 15”

		- to jest wstep do rozmowy

- Zmiennosc

	- nie zawsze liczba elementow, od ktorych zalezymy wystarcza

	- np. coupling do 5 stabilnych elementow vs. coupling do 2 czesto zmiennych elementow

		- lepszy ten do 5

		- mimo ze liczby wskazuja inaczej

	- trzeba sie zastanowic, kiedy byly ostatnie zmiany

		- czy logika sie zmienia

		- czy interfejsy sie zmieniaja

### Stabilnosc i zmiennosc

- Subskrypcja zalezy od zakupu, czy odwrotnie?

	- czy subskrypcja wie w ramach jakiego zakupu byla kupiona?

	- czy zakup wie jakiej subskrypcji dotyczyl?

	- a moze niebezposrednosc i trzeci modul?

- Musimy sie zastanowic, gdzie jest bardziej stabilny koncept biznesowy, a gdzie oczekujemy zmiennosci?

	- antycypujemy modularyzacje

	- byc moze subskrypcja jest stabilna, a zakup sie zmienia

		- bo kupujemy za bitcoiny albo punkty lojalnosciowe albo darmowe subskrypcje probne

		- wtedy lepiej, zeby zakup zalezal od czegos stabilnego - subskrypcji

	- warto chowac rzeczy zmienne

		- znow enakpsulacja

### Usuwalnosc / removability

- Projektowanie klas/modulow/mikroserwisow tak, zeby nastawic sie na mozliwosc ich usuniecia

- Jest to driver, ktory wspiera wymienialnosc

	- skoro mozemy modul usunac i napisac od zera, to latwo go wymienic

		- musi miec malo zaleznosci wejsciowych i wyjsciowych

- Na pewno promujemy stabilny interfejs

	- skoro inne moduly korzystaja, to nie chcemy, zeby byly dotkniete zmiana implementacji

- Podejscie wspierajace

	- minimalizacje couplingu

	- modularyzacje

	- minimalizacje czasu na przepisanie modulu

		- zamiast hackowac

		- jesli jest taka koniecznosc

### Law of Demeter

- prawo dobrego stylu

- Cechy

	- dobra praktyka projektowania

	- zaklada brak wiedzy o detalach innych modulow

	- wspiera loose coupling

	- „nie rozmawiaj z nienzajomymi”

- Przyklad

	- Mozemy wolac do

		- paremtru metody

		- pola klasy

		- lokalnej zmiennej

		- lokalnej metody

	- Nie mozemy wolac do

		- wnetrza obiektow

		- get().get().set(...)

- Lamiac zasade, nagle nasz obiekt ma wiedze o kilku kolejnych obiektach

	- mamy coupling wyjsciowy do kolejnych rzeczy

	- Rozwiazanie

		- nadal mamy coupling tylko do tej jednej rzeczy

		- mowimy obiektowi, co ma zrobic

		- zamiast go wybebeszac i robic to samemu

### Coupling systemowy

- temporal

	- zw. z czasem

	- dwie uslugi musza byc jednoczesnie dostepne, zeby sie komunikowac

		- synchroniczne HTTP

- spatial

	- zw. z przestrzenia

		- inaczej: z topologia

	- jedna usluga musi znac adres drugiej, zeby sie skomunikowac

- platform

	- np. komunikacja za pomoca serializacji klas danego jezyka

- zawsze cos za cos

	- coupling to funkcja wielowymiarowa

	- np. pozbywamy sie spatial couplingu uzywajac uslugi, ktora poinformuje nas o lokalizacji innych uslug

		- ale mamy coupling do uslugi

### Podsumowanie

- coupling powinien byc jawny

- coupling jest nieunikniony

	- ale unikamy przypadkowego i ukrytego

	- jesli nie wiemy dlaczego mamy powiazanie, to zapala sie czerwona lampka

- loose coupling to droga do modularyzacji

- loose coupling to subiektywne stwierdzenie

	- mamy wejsciowy, wyjsciowy, stabilnosc... ciezko stwierdzic jednoznacznie

	- raczej chodzi o przywiazanie do abstrakcji, a nie implementacji

- coupling w systemie ma rozna nature

## Lekcja 8.04. Narzędzia do mierzenia couplingu

### Syntaktyczny coupling

- Kroluje analiza statyczna

	- Narzedzia

		- SonarQube (25 jezykow)

		- NDepend, ReSharper

		- Cast

		- stan4j

	- Warto sprawdzic, jak taka metryka jest liczona w danym narzedziu

- Narzedzia do weryfikacji zaleznosci

	- ArchUnit

		- dla Javy

		- pozwala na napisanie testow jednostkowych walidujacych zaleznosci miedzy modulami

		- jesli jest zaleznosc, test failuje

### Logical coupling

- Nie ma az tylu narzedzi

- Mozna pobawic sie funkcjami Gita

	- Gita wspiera tez Code Maat

		- i jego nastepca - CodeScene

			- platny

	- Sporo o tym w ksiazce Software Design X-Rays

## Lekcja 8.05. Kohezja

### Definicja

- miara tego, jak poszczegolne funkcje, ktore wpadly w jeden modul, faktycznie tam przynaleza, sa ze soba logicznie zwiazane

- w fizyce

	- spojnosc osiagana za pomoca oddzialywan miedzyczasteczkowych

		- ciala stale maja wysoko kohezje

	- energia kohezji

		- energia potrzebna do rozbicia czasteczki na atomy

- w IT

	- trzeba duzo energii, aby rozbic modul o wysokiej kohezji na mniejsze czastki

	- to porzadana cecha, bo oznacza, ze klasa/modul/mikroserwis zawiera elementy, ktory faktycznie powinny byc razem

	- **miara dobrej modularyzacji, dobrego pogrupowania elementow w moduly**

### Cechy

- wysoka kohezja wspomaga modularyzacje

	- redukuje ryzyko propagacji zmiany

		- wysoka kohezja powoduje, ze rzeczy, ktore razem zmieniaja sie biznesowo w przestrzeni problemow, wpadaja w jedno miejsce w przestrzeni rozwiazan

			- zmiana jest zamknieta w jednym module

- redukuje coupling pomiedzy modulami

	- skoro rzeczy, ktore od siebie zaleza umiescimy w jednym module, to powiazania miedzy modulami beda mniejsze

### Typy

- Niewskazane

	- coincidental

		- wszystko, co wiaze elementy modulu, to to, ze sa w jednym module

			- przypadek

		- najmniej pożądana

		- np. klasy utils, gdzie wkladamy wszystko, co nie pasuje nam gdzie indziej

	- logical

		- wydaje sie, ze byty sa powiazane miedzy soba logicznie, ale to tylko pozory

		- np. subskrypcja indywidualna i firmowa, jako jedna klasa

			- rozne byty, ale wspolna nazwa

- Neutralne

	- temporal

		- w module mamy dwie funkcje, bo musza wykonywac sie w jednym czasie

		- np. modul, ktory przygotowuje procesy

	- procedural

		- jesli procedura wymaga szeregu operacji, to te operacje wpadly w jeden modul

		- np. sortowanie, ktore wymaga walidacji danych, a nastepnie ich transformacji

			- 3 operacje wpadaja w jeden modul

- Wskazane

	- communicational

		- w module ląduja funkcje, ktore korzystaja z tych samych struktur danych

	- sequential

		- w module ląduja funkcje, z ktorych wyjscie jednej jest wejsciem kolejnej

		- np. przygotowanie kursu

			- najpierw walidacja, potem transkrypcja, nastepnie recenzja

	- functional

		- funkcje wpadly w modul, bo razem tworza funkcje biznesowa wyzszego poziomu

		- np. modul kalkulatora zawiera funkcje dodawania, odejmowania, itd.

		- najbardziej pożądana kohezja

### Kohezja i coupling

- Moduly cechuja sie wysoka kohezja

	- Tam rzeczy zmieniaja sie razem

- Pomiedzy modulami jest niski coupling

	- Malo zaleznosci

	- Tam rzeczy zmieniaja sie osobno

- Przyklad

	- wagon to modul

		- zawiera przedzialy/siedzenia

		- jesli zmieniamy siedzenia, to modernizujemy caly wagon

			- zmiana jest rozpropagowana w jednym miejscu

### Wysoka kohezja

- IndividualSubscription

	- odpowiada jednej funkcji biznesowej

		- cykl zycia wlaczenia/wylaczenia subskrypcji

	- Podobnie z CompanySubscription

- Dwie klasy: wlaczanie i wylaczanie

	- konsekwencje

		- jesli chcemy zmienic sposob przechowywania informacji o aktywacji

			- to musimy to zrobic w dwoch miejscach

			- a moze to byc enum albo zapisany w kilku polach

		- za kazdym razem zmieniamy dwa miejsca

			- coupling logiczny

	- zbyt granularne moduly

		- dostalismy 2 moduly

		- rzeczy, ktore zmieniaja sie razem sa w dwoch miejscach

### Niska kohezja

- Nowe metody

	- nowe metody do odnawiania subskrypcji i platnosci

	- na pierwszy rzut oka

		- mowimy jezykiem domenowym

		- jest abstrakcja

		- ktos moglby powiedziec, ze jest ok

	- ale teraz zmiany zwiazane z platnosciami, odnowieniem i zapisaniem/wypisaniem sie z subskrypcji sa w jednej klasie

		- zmiany w jednym obszarze moga powodowac bledy w innym

	- **grupujemy koncepty, ktore zmieniaja sie osobno w jednym miejscu**

### Metryki

- LCOM (Lack of Cohesion of Methods)

	- mowi o tym, jak metody danej klasy tworza spojna jednostke

	- analizujemy klase CompanySubscription

		- metody enroll i withdrow

			- pole enrollment

		- metoda renew

			- pole expirationDate

		- metoda pay

			- pole payments

		- Algorytm

			- liczymy pary zbiorow **metod**, ktore sa rozlaczne

				- pay, renew

				- pay, enroll

				- pay, withdraw

				- renew, enroll

				- renew, withdraw

			- odejmujemy pary zbiorow **metod**, ktore maja czesci wspolne

				- enroll, withdraw

			- odejmujemy liczbe wspolnych - od liczby rozlacznych

				- 5 - 1 = 4

					- niska kohezja

	- analizujemy klase IndividualSubscription

		- 0 - 1 = -1

			- minimalna wartosc to 0, wiec normalizujemy do 0

	- rozne narzedzia roznie mierza taka metryke

		- warto sprawdzic w dokumentacji, co dokladnie tam liczymy

			- zeby nie bylo sytuacji, ze zmieniamy narzedzie i nie wiemy dlaczego dostajemy inne wartosci

	- metryka nie jest idealna

		- legenda

			- kropki to pola

			- elipsy to metody

		- intuicyjnie widac, ze w kazdym przypadku mamy dwie rozne klasy

		- metryka mowi cos innego

			- Przyklad 1

				- brak kohezji, wartosc 1

			- Przyklad 2

				- dodajemy metode, ktora pasuje do tej klasy

				- zwiekszamy kohezje, a metryka sie nie ruszyla

			- Przyklad 3

				- dodajemy kolejna metode, ktora pasuje do tej klasy

				- metryka 0, mimo ze ciagle ukrywaja sie tam dwie klasy

		- to tylko dobry wstep do rozmowy

## Lekcja 8.06. Single Responsibility Principle

### Definicja

- pierwsza z zasad SOLID

- mikroserwis/modul/klasa powinna miec jedna odpowiedzialnosc

	- co to znaczy?

		- ze ma jedna metode?

		- moze jedna metode publiczna?

		- robi dokladnie jedna rzecz?

- **Klasa/modul ma jeden powod do zmiany**

	- powodem do zmiany jest wymaganie biznesowe

		- dotyczace interesariusza lub grupy interesariuszy

	- jesli klasa spelnia wymagania plynace od roznych interesariuszy, to nie spelnia SRP

		- ma wiele odpowiedzialnosci

			- czyli wiele wymagan funkcjonalnych plynacych od kilku interesariuszy

- Grupuj razem rzeczy, ktore maja jeden powod do zmian. Oddzielaj rzeczy, ktore zmieniaja sie z roznych powodow.

	- Zwiekszaj kohezje pomiedzy elementami logicznie zwiazanymi ze soba

	- Zmniejszaj coupling pomiedzy elementami logicznie niezwiazanymi ze soba

### Rozni aktorzy

- CompanySubscription

	- 4 metody

	- 3 aktorow/interesariuszy

		- company manager

			- mowi, jak zapisujemy/wypisujemy sie z subskrypcji

		- sales manager

			- mowi o tym, jak odnawiac

		- accountant

			- mowi, jak splacamy

		- kazdy ma wplyw na to, jak wyglada „ich” funkcja

			- zmiany ksiegowego moga wplynac na zmiany managera sprzedazy

	- ma kilka powodow do zmiany

		- nie spelnia SRP

### Rozne poziomy abstrakcji

- Mimo, ze tylko jeden aktor

- Metody operuja na roznych poziomach abstrakcji

	- zmiana formatu danych w raporcie moze wplynac na zapisanie/wypisanie sie z subskrypcji

- Rozdzielamy na Command i Query

	- CQRS

	- kazda z klas ma pojedyncze odpowiedzialnosci

### Jest konsekwencją stosowania dobrych praktyk programistycznych

- stosowania enkapsulacji

	- nie mamy zaleznosci do szczegolow implementacyjnych innych modulow

	- zmiana tych szczegolow nie wplywa na nas

- szukania wysokiej kohezji

- szukania niskiego couplingu miedzy modulami

	- wtedy propagacja zmian bedzie odbywac sie w jendym miejscu

### Przyklad

- Agregat

	- klaster obiektow zapewniajacy granice spojnosci i transakcyjnosci

	- mozemy sie do niego odwolywac tylko przez aggregat root

		- daje abstrakcje

		- Jak pokazac tylko korzen, a ukryc szczegoly implementacyjne?

			- Widocznosc zalezy od technologi

	- Cechy

		- wysoka kohezja

			- szczegoly implementacyjne beda zmieniac sie razem

				- sa silnie zwiazane jedna transakcja bazodanowa

		- niski coupling

			- brak referencji do innych agregatow

			- odwolujemy sie tylko przez identyfikator

		- stosowanie Law of Demeter

		- enkapsulacja

			- tylko korzen moze udostepniac metody na zewnatrz

## Lekcja 8.07. Wybór modułów

### BC ma granice lingwistyczne, ale w srodku moze miec logicznie zwiazane moduly

### Po co dzielimy na moduly?

- Piramida potrzeb oprogramowania

	- wysoka utrzymywalnosc

		- ewolucyjnosc

		- pozwala na czeste zmiany niskim kosztem

	- wspiera mozliwe zmiany

		- nawet trudnym kosztem, ale jakos sie da

		- od tego poziomu musimy myslec o modularyzacji, wysokiej kohezji, niskim couplingu

	- da sie z tego korzystac

		- co z tego, ze spelnia wymagania, skoro nie zapewnia atrybutu jakosciowego dostepnosc i nie mozna niczego kliknac

	- spelnia wymagania biznesowe/funkcjonalne

	- po prostu istnieje na produkcji

### Dzielac na moduly warto pamietac o zlozonosci polaczen

- Jeden modul robi wszystko

	- Wysoka zlozonosc pojedynczego modulu

	- Za mala granularyzacja

- Bardzo duzo modulow

	- Wysoka zlozonosc polaczen

	- Za duza granularyzacja

- Zlozonosc calkowita

	- Musimy znalezc sie pomiedzy jednym, a drugim ekstremum

		- dlatego nie ma maksymalnej granularnosci

### Jak powstaly moduly jednego Bounded Contextu z projektu Kursik?

- BC Przygotowania Kursu

	- Diagram C3

	- Transkrypcja

		- Wektor zmian

			- zmiennosc API

			- inny dostawca

			- chcemy odgrodzic zmiany od innych modulow

			- modularyzacje osiaga sie przez ukrywanie niewiadomego

	- Recenzja

		- autonomia

			- niezalezne biznesowo od pozostalych

				- dlatego trafil do osobnego modulu

		- pod spodem dwa podmoduly

			- panel recenzenta

			- panel autora kursu

			- dlaczego jeszcze bardziej tego nie rozgraniczyc?

				- bo zmiana panelu autora wplywa na panel recenzenta i odwrotnie

				- silna kohezja

	- Walidacja

		- bardziej techniczne drivery

			- obawiamy sie duzych plikow

			- separujemy modul, liczac, ze w przyszlosci trzeba bedzie go wyciagnac do osobnego komponentu, zeby skalowac zasoby

				- zeby przetwarzanie duzych plikow nie wplywalo na inne funkcje BC przygotowania kursu

	- Alternatywa

		- dodanie modulu Przygotowanie

			- tak, jak caly BC

			- Odpowiedzialnosci

				- zarzadca calego procesu

				- definiuje kolejnosc

			- Zalety

				- zmiana kolejnosci krokow jest zamknieta w jednym miejscu

					- wektor zmiany zamkniety w jednym miejscu

					- przygotowujemy sie na wymagania, ze niektorzy recenzenci/autorzy maja inne kroki

						- moze sprawdzony autor moze pominac recenzje

## Lekcja 8.08. GRASP

### Wzorce GRASP mowia o tym

- jak dodawac nowa odpowiedzialnosc

- jak mapowac odpowiedzialnosc do obecnej struktury

	- gdzie ona powinna sie znalec

	- w ktorym obiekcie/module

		- moze w obecnym

		- mozew w nowym

### Sa agnostyczne od paradygmatu programowania

### General Responsibility Assignment Software Patterns

- Obiekt ma odpowiedzialnosc na temat

	- tego, co robi

		- wykonywanie / doing

		- akcji

		- tworzenia nowych obiektow

		- koordynacji, etc.

	- tego, co wie

		- wiedza / knowing

		- o swoich danych

		- o innych obiektach

		- o danych, ktore obiekt moze policzyc, etc.

### 9 wzorcow

- 1. Kontroler / Controller

	- start obslugi akcji biznesowej

	- wejscie do scenariusza biznesowego

	- np. serwis aplikacyjny

		- wyciaga z bazy i zapisuje

		- cala operacje biznesowa deleguje do warstwy domenowej

	- pierwszy obiekt pod warstwa UI

		- zatem inny niz kontroler z MVC, ktory nalezy do warstwy widoku

	- jest agnostyczny od tego, kto go wywoluje

- 2. Tworca / Creator

	- odpowiada na pytanie, kto ma odpowiedzialnosc tworzenia obiektow typu Y

		- moze to byc obiekt X, o ile

			- X agreguje/zawiera Y lub

			- X scisle uzywa Y lub

			- X ma wszystkie dane do stworzenia Y

	- np. IndividualSubscription

		- ma wszystkie dane do stworzenia pauzy

		- agreguje pauzy

		- fabryka pauz byłaby zbędna, bo subskrypcja ma wszystko, czego potrzebuje do tworzenia pauz i ich uzywa

- 3. Niebezposredniosc / Indirection

	- jesli mamy dwa obiekty, ktore maja sie komunikowac, to czasem nie wiemy, ktory z nich patrzy na ktory

		- w ktora strone jest strzalka zaleznosci

			- moze nie chcemy, zeby byla w zadna

				- bo chcemy ograniczyc coupling

	- np. przygotowanie kursu

		- nie chcemy, zeby Walidacja wiedziala o Transkrypcji

		- mozemy wprowadzic obiekt posredni, ktory bedzie nam delegowal komunikacje miedzy pierwszym obiektem a drugim

			- one nie beda o sobie nic wiedziec

				- mniejszy coupling miedzy obiektami/modulami

				- nie ma problemu, zeby powiedziec, ktory patrzy na ktory, bo zaden nie patrzy na zaden

		- to jest czwarty modul Przygotowywanie

			- zajmuje sie kolejnoscia przygotowywania wideo

			- on steruje procesem

			- skladowe niczego o sobie nie wiedza

	- Wzorce projektowe, ktore sa pochodna

		- adapter

		- mediator

		- fasada

		- bridge

- 4. Ekspert informacji / Information expert

	- mowi o tym, ze jesli dodajemy nowa odpowiedzialnosc do obecnej struktury oprogramowania, to powinnismy umiescic ja w miejscu, ktore ma najwiecej informacji o tym, jak ta odpowiedzialnosc zaimplementowac

		- **przydziel odpowiedzialnosc obiektowi/modulowi, ktory ma najwiecej danych potrzebnych do wypelnienienia zadania**

	- np. jesli mamy subskrypcje, ktora udostepnia funkcje zapisu

		- i chcemy dodac funkcje wypisania sie z subskrypcji

		- to ta klasa subskrypcji jest odpowiednim miejscem na dodanie funkcji

			- bo ma najwiecej informacj, jak takie zadanie wykonac

				- jest ekspertem nt. tego, jak to zrobic

	- czy taka klasa bedzie ciagle rosnac?

		- o te rzeczy, do ktorych rosci sobie prawa

			- o te, ktore zwiekszaja jej kohezje

		- nie do losowych rzeczy

			- tylko tych, ktore faktycznie powinny tutaj wpasc

		- nie bedzimy jej rozbijac, to to wplynie na coupling logiczny

- 5. High Cohesion

- 6. Low Coupling

- 7. Polimorfizm / Polymorphism

	- Jesli mamy byt roznie reprezentowany w zaleznosci od konkretnej sytuacji, to powinnismy te rozne zachowania reprezentowac za pomoca polimorfizmu

	- np. polityka pauzowania subskrypcji

		- jedna polityka pauzowania na zawsze

		- druga do konca sierpnia

	- klient abstrakcji nie powinen wiedziec, ze rozmawia z konkretna implementacja

		- nie powinno go to interesowac

		- nie sprawdza konkretnej implementacji

			- nie uzywa if-else

			- jesli uzywa, to producent abstrakcji popelnil blad

				- abstrakcja wycieka

- 8. Chroniona zmiennosc / Protected variations

	- powinnismy chronic zmiennosc, ktora znajduje sie w naszym oprogramowaniu, w naszym modelu

		- enkapsulacja

			- chronienie nie tylko szczegolow implementacyjnych

			- ale rzeczy, ktore maja sie zmienic

	- np. jesli mamy kursy reprezentowane, jako lista video, to blokujemy sie na mozliwosc przeprowadzania np. kursow off-line

		- nie chronimy zmiennosci

		- ulotna logika nie zostala ochroniona i wyciekla po systemie

			- zeby tego nie robic, reprezentujemy liste odcinkow, jako Kurs

- 9. Pure fabrications

	- Definicja

		- „sztuczny obiekt”

			- zwieksza kohezje

			- zmniejsza coupling

			- np. serwis domenowy

	- np. skoro klasa subskrypcji ma wszystkie informacje - jest ekspertem informacji - to moglaby sie zapisywac do bazy

		- czesto jednak nie chcemy, aby miala taka odpowiedzialnosc

			- aby przenikala do innej warstwy

		- wtedy tworzymy sztuczny obiekt Repozytorium / DAO

			- sztuczny, bo nie wystepuje w przestrzeni problemu

				- jest potrzebny tylko w przestrzeni rozwiazan

			- potrafi zapisac do bazy

	- innym przykladem jest serwis domenowy pauzowana subskrypcji

		- rozna polityka w zaleznosci od tego, ile subskrybent ma punktow lojalnosciowych

			- mozna byloby to wrzucic w subskrypcje lub subskrybenta

			- ale czasem chcemy odgrodzic sie od tego, ze te dwa obiekty cos o sobie wiedza

				- nie chcemy wiazan miedzy nimi

				- wtedy tworzymy sztuczny byt - serwis domenowy miedzy nimi

					- serwis ma wysoka kohezje

					- subskrypcja i subskrybent maja niski coupling

- 10. Pragamtyzm

	- nie nalezy do GRASP

	- to nie jest tak, ze zawsze musimy stosowac GRASP

		- trzeba byc pragmatycznym

			- swiadome lamanie

		- jesli nie widzimy przyszlych wymagan biznesowych, ktore uzasadnialyby takie decyzje, to nie robimy

		- jesli bedziemy potrzebowali to dodac, to w dobie dzisiejszych narzedzi to proste

## Lekcja 8.09. Testing Done Right

### Znane problemy testów

- wielolinijkowe testy

	- test zaczyna sie od 45 linijek mockowania

- dużo zależności typu mock

- mała zmiana wpływa na bardzo dużo testów

	- dlatego, ze testy patrza na szczegoly implementacyjne, chociaz nie powinny na nie patrzec, zamiast operowac na wyzszym poziomie abstrakcji

		- testujemy za nisko

	- testy podlegaja tym samym zasadom, co kod produkcyjny

		- np. dbamy o niski coupling

		- coupling do abstrakcji

- mamy siatke bezpieczenstwa, ktora niewiele daje

- czesto prowadza do konkluzji, ze testy nie dzialaja

	- te problemy wskazuja raczej, ze cos wczesniej poszlo nie tak

		- np. **dlaczego** mamy kilkanasie zaleznosci, ktore trzeba zamockowac?

		- dlatego, ze na etapie modularyzacji juz cos poszlo nie tak

			- wszystko patrzy na wszystko

			- omijamy warstwe abstrakcji

	- w takiej strukturze rzeczywiscie testy sa problematyczne

		- upewniamy sie za pomoca testow, ze nikt tej struktury nie zmieni

		- zabetonowanie zlej struktury kodu

### Coupling testów do implementacji

- Agregat subskrypcji firmowej

- mozemy go obtestowac z kazdej strony

	- nie tylko korzen

	- ale kazda z klas zaleznych od korzenia, ktora powinny byc niewidoczna dla innych

- zabetonowanie sposobu wykonania szczegolow implementacyjnych

	- jesli tak bedziemy robic, to kazda zmiana implementacji bedzie skutkowac padaniem testow

		- stracimy czas naprawiajac je, chociaz publiczny kontrakt mogl sie nawet nie zmienic

	- te klasy sa mocno powiazane, skoro sa w jednym module, wiec zmiana jednej wplynie na zmiane innych

		- a zatem ich testy beda padac

### Decoupling testow od implementacji

- testujemy przez publiczna abstrakcje

	- fasady modulu

	- korzen agregatu

- nie testujemy szczegolow implementacyjnych, tylko stabilna abstrakcje

	- wywolujemy **zachowanie** i sprawdzamy wynik

	- jesli zmienimy szczegoly implementacyjne, to test zostaje nienaruszony

	- mozemy zmieniac strukture wewnetrzna bez zmiany publicznych zachowan

		- co jest definicja refaktoringu

	- klucz do utrzymywalnosci testow

### Relacja testy -> kod produkcyjny

- powinna byc taka, jak miedzy modulami produkcyjnymi

- wiazania do abstrakcji, a nie do szczegolow implementacyjnych

	- podlega zasadom couplingu i enkapsulacji

- testujemy stabilna abstrakcje

	- nie testujemy niestabilnej implementacji

- testujemy kontrakt

	- a nie to, jak kontrakt zostal wypelniony

	- jesli kupujemy butelke wody, to interesuje nas jej pojemnosc, cena i smak wody

		- a nie z jakiej jest rozlewni, ani jaka ciezarowka zostala przywieziona

### Test-Driven Development

- Kroki

	- 1. przed pisaniem logiki biznesowej, najpierw napisac test do pierwszego scenariusza biznesowego

		- zobaczyc, jak ten test nie przechodzi

	- 2. piszemy minimalna liczbe linijek kodu produkcyjnego, ktora spowoduje, ze test bedzie zielony

		- nie myslimy tu o jakosci, utrzymywalnosci kodu

		- mamy gotowa abstrakcje

	- 3. refaktoryzujemy szczegoly implementacyjne

- Wspiera podejscie: najpierw abstrakcja, potem implementacja

- Test first

	- test jest pierwszym konsumentem tworzonej abstrakcji

	- czyni abstrakcje latwiejsza

### Kiedy napisac nowy test?

- nowa metoda czy klasa to nie powod do napisania testu

	- to jest szczegol implementacyjny

- nowe wymaganie to powod do napisania testu

- albo znajdujemy blad, ktory chcemy potwierdzic poprzez test

### Czym jest unit / jednostka?

- unit to niekoniecznie klasa czy metoda

- unit to moze byc zestaw logicznie powiazanych klas/funkcji, ktore tworza wartosc biznesowa

	- agregat

	- modul z fasada

### Kiedy mock?

- jesli mam spojna grupe obiektow, ktore stanowia kontrakt i nie wychodza na zewnatrz z zaleznosciami, to nie musimy nic mockowac

	- tworzymy nowe, prawdziwe obiekty

- mockujemy, gdy mamy kosztowny zasob, od ktorego chcemy sie odgrodzic

- mockujemy, gdy chcemy sprawdzic, czy zewnetrzna usluga zostala zawolana

	- zewnetrze api, ktorego nie chcemy wciagac do testu

- Przyklad

	- niskopoziomowy test

		- robi ze szczegolow implementacyjnych klasy, publiczna informacje dla testow

		- lacznie z mockowaniem Seta

			- zmienimy Set na List i wszystko padnie

		- testuje konkretne linijki algorytmu

			- licznosci wywolan metod

	- wysokopoziomwy test

		- sprawdzamy rezultat

		- jestesmy zwiazani z abstrakcja

### Testy a Law of Demeter

- jesli lamiemy prawo, to musimy mockowac kolejne wywolania

	- kazde z nich staje sie zaleznoscia testu

