#  **Style architektury aplikacyjnej**


## Lekcja 5.01. Architektura warstwowa

### Przyklad

- 3-warstwowa

	- Prezentacja

		- Kontrolery

	- Logika

		- Interfejs (fasada) + implementacja, ktora moze sie skladac z wielu klas

	- Persystencja

		- Interfejs/repozytorium i implementacja w dowolnej technologii

### Cechy

- warstwy zaleza od siebie

	- wyzsza od nizszej

		- powod: warstwa wyzsza moze sie dostac do **kazdego** modulu warstwy nizszej

- stosowana w **calym** systemie

	- kazdy kontroler moze skorzystac z kazdego serwisu, a kazdy serwis z kazdego repozytorium

		- efekt: big ball of mud

### Rozwiazanie problemow

- stosowanie warstw nie do calego systemu, a do pojedynczych modulow

	- autonomiczny modul biznesowy

		- grupuje „male” moduly w pojedyncza funkcjonalnosc biznesowa

		- system powinien sie kladac z wielu takich modulow

### Rodzaje

- rozluźniona

	- dana warstwa moze komunikowac sie rowniez z warstwa **nie** bezposrednio pod nia

	- niektore warstwy moga byc otwarte

		- warstwa nad warstwa otwarta moze sie komunikowac bezposrednio z warstwa pod nia

		- raczej nie nalezy ich stosowac

			- symptom, ze warto wydzielic fragement nie korzystajacy z warstwy srodkowej do osobnego modulu

				- wtedy jeden modul ma architekture dwuwarstwowa, a drugi trzywarstwowa

				- wszystkie warstwy zamkniete

- sztywna

	- dana warstwa moze komunikowac sie wylacznie z warstwa bezposrednio pod nia

		- czyli z ta, od ktorej ona zalezy

	- moze prowadzic do warstw, ktore niczego nie robia

	- **dazymy zawsze do sztywnego podejscia, wydzielajac fragmenty omijajace warstwy do osobnego modulu**

### Spojnosc?

- Eklektyzm vs homogenicznosc

	- Eklektyzm

		- kazdy modul jest z innej bajki

			- nawet w innym jezyku

		- trudne do utrzymania

	- Homogenicznosc

		- kazdy modul ma identyczna technologie i styl architektoniczny

		- zbyt sztywne

			- obchodzimy ograniczenia modulow, ktore maja inne potrzeby

	- Znajdujemy zloty srodek

		- Korzystanie z jednego z 4 styli architektonicznych

			- warstwowego

			- hexagonalnego

			- pipe ’n’ filters

			- mikrojadro

		- odpowiedni styl ulatwia rozwiazanie problemu, implementacje, a nie utrudnia

### Moduly wspoldzielone

- logowanie, wspolne klasy bazowe

- ktora warstwa?

	- zwykle mamy shared, utils, lib, itp.

		- wstydzimy sie, ze nie powinno ich tam byc, a powinno

		- w jakiej warstwie jest String lub List?

			- w zadnej, to narzedzie

- Podzial modulow

	- capability (zdolnosci)

		- realizuja zdolnosc biznesowa

		- to je dzielimy pomiedzy warstwy

	- utility (narzedzia)

		- moduly biblioteczne

			- naturalne jest to, ze sa wspoldzielone

		- wazne jest to, zeby byl to kod generyczny, narzedziowy, a nie biznesowy

### Warstwy logiczne i fizyczne

- Tier (fizyczne)

	- odnosza sie do architektury wdrozeniowej

	- kontenery z C4

	- Przyklady

		- prezentacja

			- aplikacja webowa

			- aplikacja mobilna

			- SPA

		- logika biznesowa

			- serwery aplikacyjne

		- persystencja

			- baza danych

- Layer (logiczne)

	- architektura aplikacyjna dotyczy logicznych

### Ile warstw?

- „Kazdy problem moze byc rozwiazany przez dodanie kolejnego poziomu abstrakcji/posrednosci”

	- Poza problemem zbyt duzej ilosci warstw abstrakcji ;)

- Co daja nam warstwy?

	- Zmniejszenie zlozonosci

		- warstwa po warstwie zmniejszamy zlozonosc, dodajac latwiejsze API

		- Sterowanie robotem

			- Dostajemy bardzo niskopoziomowe API, ktore opakowujemy w kolejna warstwe

				- przyjazniejsze w uzyciu API

					- zmniejszamy zlozonosc

	- Separacja odpowiedzialnosci

		- CRUD

			- nie ma zmniejszenia zlozonosci

			- kazda warstwa ma tyle samo metod

		- Single Responsibility Principle

			- rozne powody do zmiany

				- wyswietlajmy nie HTML, a JSON

					- warstwa prezentacji

				- zmienmy baze

					- warstwa persystencji

			- rozne narzedzia

				- inne narzedzia (framework, biblioteka) do persystencji, a inne do prezentacji

### Zalety

- ogolnie znana

	- jest prosta

- zmniejsza zlozonosc

	- dobrze rozwiazuje zlozone problemy

- separacja odpowiedzialnosci

	- wymiana warstwy

		- zdarza sie rzadko

### Wady

- zmiany w wielu warstwach na raz

	- jesli chcemy cos zmienic w jednej warstwie, czesto zmieniamy wszystkie warstwy

- utrudniona testowalnosc

### Wnioski

- wszystkie style architektury aplikacyjnej aplikuje sie per autonomiczny modul, a nie caly system

	- metafora miasta

		- miasto sklada sie z wielu autonomicznych budynkow, ktore komunikuja sie ze soba za pomoca komunikacji miejskiej, samochodow, etc.

		- kazdy budynek posiada wlasna architekture

			- o tym mowi architektura aplikacyjna

## Lekcja 5.02. Architektura Hexagonalna

### Core Domain w architekturze warstwowej

- potrzebujemy

	- testowalnosci

	- rozwijalnosc

		- dodawanie nowych regul biznesowych i funkcji

- problem

	- logika biznesowa zalezy od persystencji

		- normalnie - stubujemy

			- stubowanie bazy byloby zmudne

				- w praktyce uzywamy bazy w pamieci lub stawiamy baze lokalnie, na Dockerze

					- to nie jest unit test, tylko integracyjny

					- musi zmieniac stan bazy

					- moze zwrocic negatywny wynik z wielu powodow

						- **test powinien padac z jednego powodu**

						- logika biznesowa jest niepoprawna

						- logika zapisu danych jest niepoprawna

						- blad w komunikacji z Dockerem

						- blad w ORM

		- jest wywolywana przez UI

			- do testu musimy dolozyc kolejna warstwe, prezentacji

				- z unit testu zrobil sie test e2e

			- a w praktyce mamy jeszcze wiecej zaleznosci

				- bezpieczenstwo

					- Oauth

				- konfiguracja

					- property files

					- git

				- klienci zewnetrznych systemow

				- kolejka

					- JMS

					- RabbitMQ

				- to tak, jakby producent laptopow musial przetestowac wszystki akcesoria podlaczane pod USB swojego laptopa

					- **my tez powinnismy wystawic interfejs - port**

### Porty i adaptery

- Port (interfejs)

	- Wejsciowe / drivers / primary

		- przypadki uzycia

			- brama wejsciowa do logiki biznesowej

			- nazewnictwo nie mowi nic o sposobie komunikacji, tylko o intencyjnosci

			- per funkcjonalnosc

				- np. pauzowanie subskrybcji

		- dla logiki biznesowej nie jest istotne, kto ja wywoluje

		- ile moze ich byc?

			- tyle, co funkcji biznesowych

			- nie musimy miec tyle samo serwisow

				- mozemy je grupowac

					- np. wszystkie porty zw. z subskrybcja indywidualna

		- moze miec implementacje HTTP

			- adaptacja przez controller

			- adaptacja do testow

		- rysujemy po lewej stronie

	- Wyjsciowe / driven / secondary

		- Port do persystencji

		- port do kolejkowania

		- do bezpieczenstwa

		- rysujemy po prawej stronie

	- w ten sposob warstwy o nizszym poziomie abstrakcji musza sie dostosowac do nas

		- do naszej logiki biznesowej

		- dependency inversion

			- odwrocenie zaleznosci

			- groty strzalek wskazuja od warstwy nizszej do wyzszej

			- nie tylko techniczne odwrocenie zaleznosci, ale tez koncepcyjne

				- warstwy niskopoziomowe musza rozumiec koncepty warstw wyzszych

		- czym sie rozni od architektury 3-warstwowej, ktora ma wyspecyfikowane interfejsy na poziomach technicznych?

			- w 3-warstwowej wlascicielem interfejsu jest nizsza warstwa

			- w hexagonalnej - wyzsza - logiki biznesowej

			- Konsekwencje

				- interfejs mowi konceptami warstwy, do ktorej nalezy

					- dla konfiguracji

						- getProperty(String key);

							- wiemy, jaki jest jezyk nizszej warstwy

						- getOperationSystemType() lub isDemo()

							- nie wiemy, czy logika biznesowa rozmawia z DB, plikami konfiguracyjnymi, itp.

	- Przyklad

		- Logika biznesowa

			- dla logiki biznesowej nie ma znaczenia, kto wykonuje persystencje

			- lezy tam, gdzie port persystencji

			- jest wlascicielem portu

		- Konfigurowanie zaleznosci

			- rozna konfiguracja portow 

				- na potrzeby roznych srodowisk

					- np. testowanie i produkcja

					- Testowanie

						- adapter do testowania

							- HashMapa w pamieci

								- jeden powod bledu

									- blad logiki biznesowej

									- nie bedzie bledu komunikacji z mapa

								- szybki unit

						- adapter produkcyjny

							- repozytorium PostgreSQL

							- mozemy go przetestowac integracyjnie z baza w pamieci, w Dockerze, etc.

						- mamy dwa rozne, niezalezne testy

- Adapter

	- Implementacja portu

- wizualizacja hexagonu

	- bo rzadko potrzebne jest wiecej, niz 6 portow

### Logika biznesowa rozbita

- dalsza separacja odpowiedzialnosci

- warstwa przypadkow uzycia

	- mowi co robic

- warstwa domenowa

	- mowi jak to zrobic

	- nie musi wiedziec nic o portach i adapterach

- wariacja architektury warstwowej

	- klasycznie zaleznosci szly od gory do dolu

	- tutaj - od zewnatrz do wewnatrz

### Zalety

- testowalnosc

- rozwijalnosc i utrzymanie

	- mozemy prototypowac nie myslac o bazie danych, etc.

- wymiana technologii

	- np. baze

	- podbijanie wersji ORM

- I/O na krancach hexagonu

	- serce hexagonu jest czyste

	- mozliwosc unit testow

	- obiekty immutable

- pozwala na podjecie decyzji pozniej

	- gdy wiemy wiecej

	- najpierw tworzymy logike biznesowa, a potem myslimy o bazie, kolejce, bezpieczenstwie...

### Wady

- wiele adapterow = wiele testow integracyjnych

	- jesli dostajemy adapter z zewnatrz, to nie mamy kontroli nad atrybutami jakosciowymi

- trudniejsza nawigacja po kodzie zrodlowym

	- potrzeba konfiguracji

	- musimy wiedziec, kiedy jaki adapter stosujemy

### Kryteria stosowalnosci

- dla projektow o zmiennej i zlozonej logice biznesowej

	- gdzie chcemy eksperymentowac

- w Core Domain

- nie w CRUDach

### Podobne architektury

- Onion Architecture

- Screaming Architecture

## Lekcja 5.03. Architektura Pipes and Filters

### Kontekst

- Pipes and Filters moze byc w kontekscie

	- architektury systemowej

		- wzorzec integracji systemow ze soba

	- architektury aplikacyjnej

		- tym sie zajmujemy

		- w obrebie modulu

- wymyslony w 1972 na potrzeby Unixa

	- przetwarzanie strumienia danych za pomoca kilku malych programow

	- command1 | command2 | ... | command_N

### Cel

- przetwarzanie strumienia danych za pomoca kilku komponentow

	- komponent -> filtr

	- rurka -> polaczenie miedzy komponentami

### Cześci skladowe

- Pierwszy filtr

	- Zrodlo

	- Producent

		- uzywane raczej w even driven

	- Pompa

		- rzadko uzywane

- Pomiedzy

	- filtry i rurki

- Ostatni filtr

	- Zlew

	- Konsument

		- uzywane raczej w even driven

### Rodzaje filtrow

- Zrodlo

	- Przyklady

		- listener

		- job w tle

		- metoda, ktora nasluchuje na request

- Transformer

	- odpowiadaja za transformacje danych

		- dane wchodza, sa przetwarzane i sa wypychane dalej

	- nie musi byc przetwarzanie tylko danych wejsciowych

		- enrichment

			- wzbogacanie

			- filtr wola o dane z systemow zewnetrznych, ktorymi wzbogaca dane wejsciowe

- Tester

	- odsiewaja ziarno od plew

		- te dane przechodza dalej, a tych nie bedziemy przetwarzac

			- rzucaja blad

			- albo /dev/null

- Zlew

	- przewaznie persystencja

### Zastosowanie

- przetwarzanie danych

	- filtrowanie req/res

		- pierwszy komponent przetwarza requesty za pomoca filtrow

			- mozemy dodawac kolejne

	- kompilator

		- kolejne fazy przejscia

	- przetwrzanie tekstu

### Przyklad

- 1. Pobieramy z Dropbox

- 2. Konwertujemy do wspolnego formatu

- 3. Walidujemy audio

	- zerojedynkowo

- 4. Walidujemy wideo

	- zerojedynkowo

- 5. Zapisujemy na Dropbox

- 6. Generujemy miniaturki

	- 7. Zapisujemy je na S3

### Zalety

- Elastycznosc

	- Konfigurowalnosc

		- mozemy zmienia kolejnosc filtrow i laczyc je ze soba

			- np. rozna konfigurowalnosc dla roznych klientow

	- Rozszerzalnosc

		- mozemy latwo dokladac elementy i rozszerzac funkcjonalnosc nie zmieniajac istniejacego pipelinu

			- generowanie miniaturek

		- **Zasada Open-Cloded Principle**

	- Mozliwosc zrownoleglenia

		- np. kilka faz walidacji rownolegle

			- performance

	- Mozliwosc rozproszenia

		- kazdy z filtrow moze byc osobnym serwisem

- Testowalnosc

	- kazdy z filtrow jest osobnym modulem

		- testowalnym w izolacji

		- testami jednostkowymi

### Wady

- Obluga bledow

	- Bo kazdy modul jest mocno odseparowany

		- Kod obslugi bledow duplikujemy pomiedzy filtry

		- albo globalny interceptor obslugujacy bledy

			- ktos nad filtrem, kto przechwyci wyjatek

		- albo bledy uczynic rezultatami, ktore wychodza z kazdego filtra

			- podejscie funkcyjne

## Lekcja 5.04. Architektura typu mikrojądro

### Inaczej - architektura pluginowa

### Geneza nazwy

- z systemow Unixowych

	- mamy tam jadro monolityczne, kernel

	- plus procesy w okol niego

	- dzialaja w jednej przestrzeni

- w kontrze do jader monolitycznych

	- kernel jest minimalny

	- wszstko z czym sie komunikuje jest definiowane w przestrzeni uzytkownika

### Cechy

- Nacisk na rozszerzalnosc

	- Nawet przez inny zespol

	- Nawet juz po wdrozeniu u klienta

- Elementy skladowe

	- Mikrojadro

		- Definiuje podstawowy proces

		- Jest minimalne

			- Zawiera minimalna ilosc kodu potrzebna do ustrukturyzowania procesu biznesowego, ktory sie dzieje

			- Czasem zawiera domyslna implementacje

		- Jest rozszerzane przez pluginy

		- **Mowi, co ma sie dziac**

	- Pluginy

		- **Mowi w jaki sposob ma sie dziac**

### Elementy

- Rejestr

	- odpowiada za zarejestrowanie uzywanych pluginow

	- musi byc skonfigurowany

		- hardcoded

		- pliki konfiguracyjne

		- zewnetrzny serwis

		- baza

- Kontrakt

	- Zewnerzni programisci musza wiedziec, kiedy i jak ich kod zostanie wykonany

		- Dostarczamy im zestaw klas i interfejsow - SDK

### Przyklady

- Microkernel definiuje kroki procesu

	- kompilacja

	- testy

	- raporty

- Przetwarzanie wideo

	- Fazy

		- 1. Pobieranie

		- 2. Konwersja

		- 3. Walidacja

		- 4. Zapis

	- Wdrazamy Kursik w roznych redakcjach

		- Kazda ma inny proces walidowania, konwersji, etc.

### Zalety

- testowalnosc

	- pluginy to male, latwotestowalne komponenty

		- podobnie, jak filtry

		- testowane w izolacji

	- jadro jest minimalne, wiec powinno sie dobrze testowac

- elastycznosc

	- po to uzywamy tego stylu

	- konfigurowalnosc

		- mozna na rozne sposoby skonfigurowac ten sam proces

	- rozszerzalnosc

		- dodawanie nowych pluginow

### Wady

- skalowalnosc

	- mozemy dokladac pluginy, ale jadro funkcjonuje w jednym module

		- bardzo trudno go rozdzielic

- zlozonosc

	- najwieksza wada

	- duzo elementow, trudnosc z konfiguracja

## Lekcja 5.05. Dobór architektury do modułu

### Podzial modulow

- Plytkie

	- Patrzysz na dno rzeki i od razu widzisz dno

	- Pomiedzy UI a DB nic sie nie dzieje

		- Nie ma redukcji zlozonosci

			- Na kazdym poziomie jest taka sama zlozonosc

	- CRUD

		- Patrze na UI i widze tabelke w bazie

	- Fasady

		- na zewnetrzny system lub baze

		- np. wyswietlanie raportow

			- nic sie nie dzieje, jesli chodzi o zmiane stanu

			- wrapper na baze danych

		- np. ograniczenie API lub prosty Anti-corruption Layer

	- **Styl warstwowy**

		- najczesciej 1-2 warstwy

- Glebokie

	- Przyklad

		- Google

			- jeden input i button -> lista wynikow

			- ale pod spodem dzieje sie bardzo duzo

		- Bramki platnosci

			- jeden formularz, kilka redirectow

			- pod spodem duzo skomplikowanej logiki

				- ktora umozliwia tak prosty UI

- Nie caly system jest gleboki

	- Czesc modulow plytka, czesc gleboka

		- Naszym zadaniem jest rozpoznac, ktore sa ktore

		- Widac na Process Level Event Stormingu

			- ktore Bounded Contexty przeloza sie na moduly bardziej zlozone, a ktore na mniej

		- Na Design Level ES widac jeszcze wiecej

	- Uzykownikowi koncowemu trudno odroznic fragmenty systemu glebokie od plytkich

		- Uzytkownik patrzy tylko z perspektywy UI

			- Amazon i sklepik pani Basi to dla niego to samo

		- Dlatego w DDD odrozniamy uzytkownika od eksperta domenowego

			- Ekspert odrozna, bo rozumie zlozonosc, ktora tam sie dzieje

				- Dlatego kluczowe jest, zeby wymagania i opis systemu brac od eksperta

### Rodzaje zlozonosci

- Charakteryzuja moduly glebokie

- W zaleznosci od rodzaju, wybieramy styl

- Konfiguracja

	- nie maja skomplikowanych regul biznesowych

	- ale wysoka konfigurowalnosc jest zlozonoscia

- Reguly

	- skomplikowane reguly biznesowe

		- w tej sytuacji moge, a w innej nie moge czegos zrobic

- Przetwarzanie danych

- Algorytmika

	- skomplikowany, matematyczny algorytm

- Koordynacja

	- modul koordynujacy prace innych modulow

		- process manager

### Perspektywa czasu

- Jedno to wiedziec, jaka mamy zlozonosc teraz

	- Drugie - jak sie to bedzie zmienialo w czasie

- W zaleznosci od perspektywy, wybieramy styl

- Co sie bedzie zmienialo?

	- Czy sa potencjalne fragmenty systemu, ktore beda sie zmienialy?

	- Moze nic nie bedzie sie zmienialo

		- Implementujemy i zostawiamy

		- Malowazna subdomena supportowa

- Jakie zmiany sa prawdopodobne?

	- Przedyskutowac z biznesem, co chcieliby w niedalekiej przyszlosci zrobic

		- Podpowiada, jaki moze byc kierunek zmian

- Jakie zmiany sa nieprawdopodobne?

	- Antywymagania

	- Ograniczaja kierunek zmian w aplikacji

- Pre-mature optimisation

	- Nie chcemy przygotowywac sie na wszystko

	- Musimy ocenic, jak bardzo zmiana jest prawdopodobna

		- Czy oplaca sie ja wprowadzac

		- Zeby nie przygotowywac sie na zmiane, ktora nie nadejdzie

			- To komplikuje system

### Mieszanie styli

- Czesto jeden modul ma konkretny styl, ale stye mozna mieszac

	- Najczesciej 2 style

- Heksagonalny + warstwowy

	- Na gorze i na dole adaptery

		- Z odwroconymi zaleznosciami

	- Pomiedzy nimi kilka warstw

		- Moga sluzyc redukcji zlozonosci

			- Piramida zlozonosci

- Heksagonalny + Pipe and Filters

	- Jesli filtry sa skomplikowane

		- Duzo enrichmentu

		- Integracja z serwisami zewnetrznymi

			- Zaciaganie danych

	- To kazdy moze byc malym hexagonem

- Mikrojadro + Pipe and Filters

	- Struktura mikrojadra to zestaw filtrow

	- Kazdy filtr moze byc rozszerzany przez pluginy

### Kroki doboru stylu

- 1. plytki vs gleboki

	- Daje grupe stylow

- 2. zlozonosc

- 3. perspektywa czasu

- 4. separacja odpowiedzialnosci

	- Pozwalaja na wprowadzenie zmian technicznych

		- Wymiana BD :)

		- Podbicie wersji biblioteki, drivera, frameworka

	- To moze nam podpowiedziec na ile komponentow/modulow/warstw podzielic system

- 5. ADR

	- wybor stylu dokumentujemy w ADR

### Regula kciuka

- CRUD

	- 3 warstwy

- Heavy Read

	- 1-2 warstwy

- Heavy Write

	- Heksagonalna

- Data Processing

	- Pipe and Filters

## Lekcja 5.06. Strategia testowania a styl architektoniczny

### Piramida testow

- Zasady

	- Malo testow E2E

	- Wiecej integracyjnych

	- Najwiecej jednostkowych

- **Czy zawsze sie ja aplikuje?**

	- Nie zawsze

		- Determinowana przez...

			- Styl architektoniczny

			- Zlozonosc

				- Jakie testy najlepiej ja testuja

### Rodzaje testow

- mowimy teraz o pojedynczym module, nie w kontekscie systemu

- e2e

	- testuja modul przez interfejs uzytkownika

	- w polaczeniu z systemami zewnetrznymi, z ktorymi sie integruje

		- lub z fake’ami tych systemow

- integracyjny

	- sprawdzaja, czy dwie jednostki (unity) poprawnie sie ze soba integruja

		- moga byc w obrebie naszego modulu biznesowego

			- dwa male moduly

		- moze byc test integracji repozytorium z baza danych

		- test integracji modulu integracyjnego z systemem zewnetrznym

- jednostkowy

	- spojny kawalek kodu

		- w rozumieniu Single Responsible Principle

	- nie musi byc pojedyncza klasa lub metoda

### Plytkie moduly

- nie ma redukcji zlozonosci

	- na kazdej wrstwie sa te same elementy

- CRUD

	- na warstwie UI, serwisow, persystencji - po 4 metody

	- na kazdej warstwie tyle samo testow

		- po 4 testy

- Strategia

	- Na kazdym poziomie mniej wiecej ta sama liczba testow

### Moduly glebokie

- **Pirmadia aplikuje sie wylacznie do modulow glebokich**

- Tam, gdzie mamy redukcje zlozonosci

- Tam, gdzie UI nie reprezentuje wprost tego, co jest pod spodem

- Gdzie duza zlozonosc sklada sie z wielu malych elementow

	- Kazdy z nich moze byc przetestowany w izolacji

		- Pojedynczy filtr w P&F

		- Zestaw regul w heksagonalnej

		- Plugin w architekturze mikrojadra

	- Do sprawdzania polaczen miedzy elementami - testy integracyjne

- Najmniej testow E2E, bo UI jest najczesciej duzo prostszy, niz to co jest wewnatrz

### Moduly integrujace

- Modul, ktory integruje ze soba wiele modulow zewnetrznych

	- Np. sciaga z nich dane i tworzy model kanoniczny

	- Duzo testow integracyjnych

	- To jest zlozonosc

- Nie ma tam skomplikowanej logiki

	- Pobieramy, przetwarzamy i wysylamy dalej

	- Niewiele testow jednostkowych

- Jedna funkcjonalnosc

	- wiec niewiele testow E2E

### Fasady

- Modul czysto odczytowy

	- Np. wyszukiwanie

- Nie jestesmy w stanie przetestowac w naszym module

	- Zeby przetestowac, czy dziala, potrzebujemy bazy danych

		- Tam siedzi ciezar operacji

	- On tylko zaweza akcje, ktore sa dostepne w bazie, a ktore my chcemy wystawic

- Duzo testow E2E

	- Sprawdzaja, czy nasze zapytania dzialaja poprawnie

- Malo testow jednostkowych

	- Bo nie ma logiki

		- Jedynie np. serializacja

