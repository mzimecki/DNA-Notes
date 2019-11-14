# **Tydzień IX REST**


## Lekcja 09.01. Podstawy REST

### Co to jest REST?

- REpresentational State Transfer

	- Reprezentacyjny Transfer Stanu

- jest po prostu stylem architektonicznym

- nie ogranicza sie do API HTTP

	- chociaz jest to jedno z podstawowych zastosowan RESTa

- daje wskazowki i wtyczne

- przede wszystkim jest to zbior zasad, dobrych praktyk, kodeks

	- aby osiagnac wspolny jezyk z klientami

### REST Constraints

- separacja klient-serwer

	- klient inicjuje zadania

	- serwer je obsluguje

	- standardowa separacja w systemach rozproszonych

	- wyjatek

		- web hooki

		- to serwer inicjuje zadanie wysylane do klienta

- bezstanowość

	- budzi watpliowsci, bo stan systemow jest zawsze

	- tu chodzi o to, zeby stan przeniesc na zewnatrz

		- nie przechowywac w formie ulotnej po stronie serwera

		- do bazy danych lub rozproszonego cache

	- pozbycie sie stanu z aplikacji pozwala duzo lepiej klastrowac aplikacje

		- poniewaz przesylanie stanu, uzgadnianie go z innymi instancjami, robia za nas zewnetrzne zrodla danych

	- powodzenie kolejnego żądania nie moze zalezec od trafienia na ten sam serwer, co poprzednie

	- **nie wymusza rezygnacji z sesji HTTP**

		- sesja HTTP ma pozytywne skutki wydajnosciowe dla systemu

			- bo policzenie hasha hasła/tokena jest kosztowne

				- potrafi zajac kilkaset ms per request

		- nie trzeba rozpraszac sesji

			- rozpraszanie/klustrowanie sesji utrudnia nam architekture/infrastrukture

			- wystarczy obsluga statusu 401

				- brak uwierzytelnienia

				- zmuszamy uzytkownika do ponownego podania credentiali

			- ...oraz sticky-session

				- pozwala kierowac klienta na preferowane instancje

					- te, na ktorych jego dane juz sa

						- np. wczytane na lokalny file system lub do cache

						- obsluga bedzie szybsza na tych instancjach

				- gwarantuje, ze uzytkownik za kazdym razem trafia na tę sama instancje

				- Jak zapewniac sticky-session?

					- klasycznie: identyfikator sesji przekazywany

						- w cookie

						- w parametrze

					- obecnie dazymy do jak najwiekszej bezstanowosci systemu

						- nie chcemy tez uzytkownika obciazac stanem - id sesji

						- dlatego rozwijaja sie rozwiazania consistent hashing / spojne hashowanie

							- id sesji to unikalny hash jakiegos unikalnego identyfikatora klienta, np. IP

							- warto pamietac, ze w przypadku protokolu HTTP, to nie jest koniecznie jeden adres IP

								- uzytkownik przechodzac przez kolejne warstwy komunikacyjne - switche, firewalle, CDNy - ma doklejane kolejne adresy IP routingu do swojego adresu zrodlowego

								- w efekcie nasz system, otrzymujac adres klienta, otrzymuje liste adresow

								- aby hashowanie bylo spojne, powinnismy skupiac sie na wybranych elementach tej listy

									- nie hashowac calosci, tylko zrodlowy adres klienta IP

- cache’owalność

	- eliminuje czesc żądań, komunikacji

		- przyspieszajac komunikacje klienta z systemem

	- musimy zapewnic, zeby odpowiedzi, ktore wysylamy byly samoopisujace sie w kontekscie cache’owania

		- robimy to odpowiednimi naglowkami

		- jesli tego explicite nie zrobimy, to przegladarki zastosuja swoje domyslne strategie

			- czasem bardzo agresywne

			- niepowiedzenie, ze żądania nie wolno cache’owac, skutkowalo cache’owaniem

				- co moglo prowadzic do niespojnosci w systemie

- koniecznosć zastosowaniego spójnego (uniform) interfejsu

	- zobowiązuje do stosowania sie do specyfikacji HTTP

	- pozwala na reuzycie bibliotek klienckich pomiedzy roznymi serwerami

		- jedna biblioteka kliencka dogada sie z roznymi serwisami

		- oczywiscie dokumenty i urle beda inne, ale same mechanizmy beda takie same, np. wysylanie JSONa POSTem

			- to jest nasz standard

- warstwowość

	- poprawnosc komunikacji nie moze zalezec od liczby komponentow pomiedzy klientem a serwerem

		- czasem warstw jest bardzo wiele

	- dodanie CDN/cache/proxy/load-balancer nie powodouje niepojnosci ani bledow

		- to jest wlasnie wsparcie komunikacji warstwowej

- Za kazdym razem, gdy mowimy o tych 5 cechach, to mowimy o API RESTowym

### Poziomy dojrzalosci

- Model dojrzalosci / model Richardsona

- 4 kroki dojrzenia do RESTowej doskonalosci

	- Poziom 3

		- implementacja hypermediow

		- odkrywamy ponownie linki

			- wchodzac na wp.pl nie musze pamietac calego adresu url artykulu, tylko moge kliknac

			- podobnie, w odpowiedzi dostajemy kolejne linki

		- to jest wlaciwy REST

	- Poziom 2

		- eliminacja czasownikow z URL, czyli z jednoznacznego identyfikatora zasobu

		- zastapienie ich metodami HTTP

			- zamist POST /subscriptions/111/delete

			- wysylamy DELETE /subscriptions/111

		- przenosimy intencje do metody HTTP

	- Poziom 1

		- zasoby

			- users

			- subscriptions

			- courses

		- URL moga miec czasowniki

			- /subscriptions/111/cancel

	- Poziom 0

		- bagienko XMLa / SOAPa

		- zadnej struktury API

		- zadnych zasobow

		- zdalne wywolywanie procedur

			- JSON/XML RPC

## Lekcja 09.02. Zasoby w REST

### Zawsze maja unikalny identyfikator

- https://{adres-serwera}/{kolekcja}/{id}/{element-podrzedny}

- protokół i adres serwera

- ścieżka do zasobu

	- zaczyna się od kolekcji

		- users, books, orders

		- liczba mnoga

			- dzieki temu wiadomo, ze mozna wyszukiwac, iterowac

	- id - unikalny identyfikator

		- 123

		- konkretny element kolekcji

	- element podrzedny

		- orders, items

		- opisuje podkolekcje, podelementy

			- /orders/111/products

- Przyklad

### Cechy metod

- idempotentnosc / idempotent

	- wielokrotne wykonanie zadania ma taki sam efekt, jak jednokrotne

- bezpieczenstwo / safe

	- wywolanie nie powoduje efektow ubocznych w systemie

### Podstawowe metody

- przeniesienie czasownikow do metod HTTP

- GET

	- pobiera reprezentacje zasobu

	- idempotentna i bezpieczna

		- wywolanie 20x niczego nie zmienia

	- nigdy nie modyfikuje danych

	- standardowa odpowiedz

		- **200 OK + Body**

- POST

	- tworzy nowy zasob

	- nieidempotentna i niebezpieczna

		- wywolana za kazdym razem tworzy nowy zasob

		- ma efekt uboczny - nowy obiekt

	- standardowa odpowiedz

		- **201 Created + header Location**

		- warto dodac lokalizacje, zeby uzytkownik nie szukal nowoutworzonego zasobu

	- warto dodawac Body zawierajace stworzony obiekt

		- aby uniknac dodatkowego GETa do systemu

		- klient oszczedza czas, serwer moce przerobowe

- PUT

	- modyfikuje zasob

	- idempotentna i niebezpieczna

		- zmiana nazwiska usera na Kowalski 20x, nie sprawi, ze bedzie bardziej Kowalski :)

		- jest skutek uboczny

	- standardowe odpowiedzi

		- **202 Accepted lub 204 No content**

	- moze tworzyc zasob, jesli o identyfikatorze decyduje klient

		- jesli wiem, ze id to np. PESEL, ktory i tak mam w formularzu, to moge stworzyc nowego uzytkownika przez PUT

- DELETE

	- usuwa zasob

	- idempotentna i niebezpieczna

		- idempotenta, bo kilkukrotne usuniecie jest rownowazne jednokrotnemu

		- pelna idempotentnosc wymagalaby soft-delete

			- inaczej pierwszy request da odpowiedz „204 No content”, a kolejne 404

	- standardowa odpowiedz

		- **204 No content**

- OPTIONS

	- zwraca informacje o zasobie

		- np. liste dozwolonych operacji

		- OPTIONS /subscriptions/123

			- powie, czy np. moge anulowac te subskrypcje

			- albo czy jest na niej dostepna okreslona metoda

		- nie musze wykonac żądania i dowiedziec sie, ze sie nie udalo

			- moge zwalidowac przed wykonaniem żądania

	- idempotentna i bezpieczna

	- standardowa odpowiedz

		- **200 OK + Body**

### Grupy kodów odpowiedzi

- 20x

	- wszystko dobrze

	- 200 OK

		- zawartosc dokumentu

		- zawsze zaklada response body

			- sa biblioteki, ktore zawsze parsuja body

				- jesli sie nie uda, rzucaja wyjatek

	- 201 Created

		- zasob utworzony

	- 202 Accepted

		- przyjeto, ale nie zakonczono przetwarzania

		- np. przetwarzanie asynchroniczne

		- sprawa zalatwional, ale rezultatu nie ma

	- 204 No Content

		- zrealizowane i nie potrzeba dokumentu, body

		- często DELETE

		- czasem GET, zamiast pustej listy

- 30x

	- zapytaj gdzie indziej, kogos innego

	- 301 Moved Permanently

		- trwale przeniesiony

		- przegladarki czesto cachuja

			- np. FireFox

			- do czasu usuniecia historii

				- wczesniej nic nie dotrze do serwera

	- 304 Not Modified

		- nie zmieniono

		- np. cache odpowiada: to, co masz jest ok

	- 307 Temporary Redirect

		- tymczasowe przekierowanie

		- w danej chwili ten zasob jest gdzie indziej, ale wroci

- 40x

	- błąd klienta

	- 400 Bad Request

		- nieokreslony blad

		- cos sie nie udalo, ale nie wiem co

		- lepiej nie uzywac, bo niczego nie mowi klientowi

			- starajmy sie zwracac bardzo specyficzne kody bledow

	- 401 Unauthorized

		- brak uwierzytelniania

		- klient wie, ze musi ponownie wyslac dane uwierzytelniajace

	- 403 Forbidden

		- brak uprawnien do zasobu

		- pytanie, czy jako producent API chce jasno komunikowac, ze klient nie ma uprawnien do zasobu

			- wzgledy bezpieczenstwa

			- czasem sama informacja, ze zasob istnieje to duzo

				- np. fakt, ze ktos zlozyl wniosek o dofinansowanie moze byc istotny

			- moze warto zwrocic 404, udajac, ze nic takiego nie ma

				- mimo ze niezgodne ze specyfikacja, to zalecane ze wzgledu na security

	- 404 Not Found

		- zasob nie istnieje

		- warto dodac informacje, czy konkretny zasob nie istnieje, czy żądanie/URL jest błędne

	- 410 Gone

		- zasob nie jest juz dostepny

		- warto rozrozniac „nie istnieje” od „istnialo, ale juuz go nie ma”

	- 405 Method Not Allowed

		- metoda niedozwolona

		- na tej subskrypcji, w tym statusie, nie wolno wykonac metody GET

			- alternatywnie moge wyslac OPTIONS i dowiedziec sie, czy warto GETa wysylac

	- 409 Conflict

		- konflikt z obecnym stanem zasobu

		- inna wersja, bledny stan zasobu

		- ma zwiazek z optimistic locking i cache

	- 415 Unsupported Media Type

		- nieobslugiwana reprezentacja zasobu

		- przepraszam, jest rok 2019, nie uzywamy XML, uzyj JSON

		- albo: tej wersji API juz nie wspieram

- 50x

	- błąd serwera

	- 500 Internal Server Error

		- nieokreslony blad serwera

		- cos sie nie udalo, ale nie wiem co

		- warto dodac opis bledu w body

	- 503 Service Unavailable

		- serwer chwilowo niedostepny

		- moze sie zrestartuje, sprobuj za chwile, na pewno sie uda

	- 504 Gateway Timeout

		- przekroczony czas obslugi żądania

### Reprezentacje zasobow

- klient nie chce zgadywac, co to za format

	- probowac roznych marshallerow

	- obslugiwac wyjatki

	- chce wiedziec konkretnie, jak wyglada zwrotka z serwera

- Nagłówki

	- Accept

		- klient wysyla do serwera

		- „akceptuje taka i taka odpowiedz”

	- Content-Type

		- zarowno w żądaniu, jak i w odpowiedzi

		- mowi, jaki jest format danych

- Typy

	- Proste

		- application/xml

		- application/json;charset=UTF-8

	- Złożone

		- mozemy byc pewni, ze struktura jest okreslona, specyficzna

			- np. zawsze zawiera identyfikator

			- application/vnd.dna+json

			- application/json;entity=Payment

				- JSON zawierajacy encje Platnosc

		- wszystko po **+** albo przed **;** to informacja dla serializera, jak dana informacje parsowac

			- wszystko dalej to informacja dla naszych kontrolerow, jak routowac żądanie

### Daty

- preferowana serializacja

	- ISO 8601: 2019-08-23T19:37:25Z

		- jasno okresla format

	- epoch milliseconds: 1566593332014

- jasno okreslamy strefy czasowe

	- najlepiej zawsze w UTC

	- klient po swojej stronie zdecyduje, jak wyswietlic

## Lekcja 09.03. Domena w REST

### CRUD a domena

- REST ma nature CRUD

- implementacja złożonych domen biznesowych konczy sie klonach JSON-RPC

	- zdalne wywolywanie pewnych metod biznesowych

- REST mowi o przesylaniu dokumentow, a nie o wywolywaniu uslug

### Encje a zasoby

- encja jest reprezentacja domeny w kodzie, po stronie serwera

	- niekonieczne dostosowana do potrzeb uzytkownika, klienta

- zasob reprezentuje potrzeby klienta, uzytkownika

	- zasob jest projekcja modelu biznesowego na potrzeby uzytkownika

- dlatego mapowanie 1:1 encji na zasoby jest slabym pomyslem

	- bo domena biznesowa, sposob jej implementacji moze byc zbyt zlozona na potrzeby uzytkownika

		- przyklad: ubezpieczenie samochodu

			- dla uzytkownika jest proste: kosztuje x, obejmuje y, trwa od do

			- dla ubezpieczyciela: model moze byc bardzo zlozony; moze np. obejmowac kolor pojazdu, pojemnosci silnika, miejsce garazowania

		- nie chcemy calosci udostepniac uzytkownikowi

			- po 1, zeby nie przeziazac uzytkownika

			- po 2, zeby nie usztywniac sie na zmiany

				- bo jesli chce zmieniac szczegoly implementacyjne modelu domenowego, to niekoniecznie chce, zeby te zmiany byly widoczne dla uzytkownika

### Mapowanie

- stosujemy wydzielony bounded context dla interfejsu API

	- to bedzie strefa zgniotu; kontrolowana strefa separujaca nas od swiata zewnetrznego

- wykorzystujemy wzorzec adapter do przemapowania obiektow

	- wszystkie chwyty dozwolone

	- moge zrobic wszystko, zeby te dwa swiaty pogodzic

- Przyklad subskrypcji

	- 1. tworzenie to POST

	- 2. jesli zalozymy, ze prob anulowania subskrypcji moze byc wiele i wszystkie mnie interesuja, to przerzucajac domene na uzytkownika, zmusilbym go do zrobienia POST /subscriptions/111/cancellations

		- czyli uzytkownik nie anuluje subskrypcji, tylko sklada wniosek o jej anulowanie

			- byc moze uzytkownik potrzebuje takiej funkcjonalnosci - wtedy ok

			- ale musze swiadomie zrozumiec, czy rzeczywiscie tak jest

		- byc moze nie potrzebuje takiej zlozonosci

			- wtedy DELETE /subscriptions/111

			- i mapowanie w warstwie adapterow na zlozenie wniosku; sprawdzi czy mozna, jaki ma stan

				- zdejemuje ciezar z uzytkownika

	- 3. teraz GET /subscriptions/111 zwraca 410 Gone

### Zapytania

- Proste

	- /courses?rating=5

	- /courses?rating=5&sortAsc=author

- Złożone

	- zapisywanie warunkow w URL bywa trudne

		- ograniczona wielkosc URLa

		- ciezko zamodelowac zlozone logicznie ANDy i ORy w postaci plaskiego stringa

	- stosujemy cialo żądania

		- POST /courses/searches

			- tworzymy dokument zapytania

				- pozostajemy w zgodzie z REST

		- odpowiadamy identyfikatorem zapytania (gdzie je znalezc) w Location

		- dodaje informacje: liczba stron, liczba elementow, wielkosc strony, gdzie jest n-ta strona, etc.

		- czesto w ciele przekazujemy pierwsza strone wynikow

	- moge zapisac wyniki w rozporszonym cache

		- tak, zeby wolajac GET /courses/searches/123/pages/n, nie dotykac juz bazy, nie mapowac modelu na zasob, itp.

			- moge tak zrobic dla pierwszych 3 stron

			- reszte wyliczac w razie potrzeby

## Lekcja 09.04. Caching

### Po co cachowac?

- eliminujemy czesc żądań

	- poprawiamy wydajnosc

	- poprawiamy dostepnosc

		- jesli serwer nie dziala, to nie obchodzi nas to, o ile dane sa w cache

	- poprawiamy opoznienia (latency)

- przyspieszamy czesc zapytan

	- walidujemy aktualnosc zasobu

	- bez potrzeby jego pobierania, parsowania, przetwarzania

	- serwer odpowiada: tak, to co masz, to najnowsza wersja

### Kontrola cache

- brak zdefiniowania cache potrafi byc bardzo agresywnie potraktowany przez przegladarke

	- dlatego kazda odpowiedz i czesc żądań powinny jasne definiowac, jak powinien je obslugiwac cache

- Naglowki

	- Expires

		- okresla date waznosci zasoby

		- Expires: Sun, 08 Apr 2019 18:04:53 GMT

		- jesli jest pusty, dostaje domyslna wartosc, np. godzine

	- Cache-control

		- mowi o tym, w jaki sposob mozemy kontrolowac caly proces cache’owania

		- w teorii, jesli uzywamy Cache-control, to mozemy pominac Expires

			- w praktyce, wiele narzedzi go ignoruje

				- dlatego warto stosowac je jednoczesnie

		- zarowno dla żądania, jak i odpowiedzi

		- Determinuje dyrektywy cache’owania

			- cache’owalnosc

				- public

					- mozliwosc zapisu na cache publicznym

					- wszystkie mozliwe CDN, load balancery, firewalle po drodze

						- ...oraz przeglądarka

					- czesto mozna go wyczyscic

						- Cloudflare, Akamai

				- private

					- mozliwosc zapisu na cache prywatnym

					- tylko przegladarka uzytkownika

					- ma największe znaczenie przy żądaniu

						- mimo ze serwer zawsze cache’uje publicznie, to mozemy wymusic, zeby to żądanie nie bylo cache’owane

					- nie mamy nad nim kontroli

				- no-cache

					- wymusza walidacje po stronie serwera, czy to jest aktualna kopia

				- no-store

					- calkowicie wylacza mozliwosc przechowywania kopii

					- nie przechowuj, nie wolno ci tego zapisac

			- ważność

				- max-age=<sec>

					- jak dlugo moze byc wazny zasob po stronie cache prywatnego

				- s-maxage=<sec>

					- jak dlugo moze byc wazny zasob po stronie cache publicznego

					- „s” od shared

				- max-stale=<sec>

					- jak dlugo nawet nieaktualne dane moga byc wykorzystane

					- „s” od shared

			- walidacja

				- must-revalidate

					- po uplywie max-age nalezy sprawdzic aktualnosc zasobu po stronie serwera

				- proxy-revalidate

					- jw. ale do cache publicznego

		- Przyklady

			- Cache wylaczony

				- Cache-control: no-store,no-cache,max-age=0

			- Cache wlaczony

				- prywatny 1h

					- Cache-control: private, max-age=3600

				- prywatny 24h i publiczny 7 dni

					- Cache-control: public, max-age=86400, s-maxage=604800

### Dobor okresu waznosci

- jedna z dwoch, obok nazywania zmiennych, najtrudniejszych rzeczy w IT

- czesto inwalidujemy cache czesciej, niz musielibysmy, aby zapewnic aktualnosc

	- np. cennik, ktory zmienia sie raz do roku, ale jesli sie zmieni, to klienci musza dostac nowa kopie w max. 15 min

		- to znaczy, ze cache ma waznosc 15 min

			- przynajmniej ten prywatny

		- dlatego czesto robimy tzw. cache eternal / wieczny

			- dodajemy wersje do URL

				- /price.json?ver=129493

				- Przyklady wersji

					- timestamp

					- hash commita

					- numeru buildu

			- nowa wersja, nowy url, wiec pobieramy zasob od nowa

- Tagowanie zasobow

	- Jest rozwinieciem koncepcji sterowania cachem za pomoca URLa

	- Naglowek ETag

		- Entity Tag

	- Serwer

		- zwracajac zasob, dodaje ETag do odpowiedzi, np. timestamp

	- Klient

		- wysyla żądanie warunkowe z naglowkiem

			- If-None-Match: „123”

				- daj mi zasob, jesli jego wersja to nie jest 123, bo taka mam

				- moze zawierac liste zasobow

				- ale z reguly zawiera ostatnia posiadana wersje

			- If-Modified-Since: Sun, 08 Apr 2019 18:04:3 GMT

				- jesli zostal zmodyfikowany po tej dacie, to daj mi nowy egzemplarz

				- jesli nie, status 304

### Optymistyczne blokowanie

- W rozwiazaniach, gdzie UI generowany jest po stronie serwera, encje sa zwracane bezposrednio na widok i sa mapowane spowrotem, optymistyczne blokowanie jest wbudowane

- REST sam z siebie nie wspiera blokowania optymistycznego

	- nie przekazujemy encji do serwera, tylko jej reprezentacje w formie zasobu, DTO

	- pomiedzy wyswietleniem zasobu, a jego ponownym wyslaniem na serwer, na serwerze ten zasob mogl sie zmienic

		- REST tego nie weryfikuje

- Mozemy do tego uzyc naglowka ETag i zadan warunkowych If-Match

	- 1. dostaje encje z ETag = 6

	- 2. modyfikuje przez dluzsza chwile na UI

	- 3. wysylam PUT do serwera z If-Match = 6

		- zrob ta modyfikacje, ale wtedy i tylko wtedy, jesli encja po stronie serwera jest w tej samej wersji, ktora mam na UI

	- 4. Serwer odpowiada

		- 2xx, jesli ok

		- 412 Precondition Failed, jesli numer wersji encji sie nie zgadza

			- lub 409 Conflict

	- Przykład

## Lekcja 09.05. HATEOAS

### Czym jest?

- Hypermedia As The Engine Of Application State

	- hiperlacza sa motorem napedowym stanu aplikacji

- wg tworcy RESTa - prawdziwy, jedynie sluszny REST

- wprowadzamy linki, aby ulatwic nawigacje po zasobach

	- duzo wygodniejsze, niz sklejanie URLi

### Formaty

- application/json

	- Czasem nazywany formatem ATOM

	- zawiera id, status, kategorie, informacje o autorze, etc.

		- drugi poziom dojrzalosci RESTa

	- dodatkowo: linki do innych zasobow

		- trzeci poziom dojrzalosci

		- juz nie musimy pamietac, jaki jest url do autora

			- nie musimy budowac urla samodzielnie na podstawie zwroconych danych

			- uzywamy linka pod kluczem author

		- dodatkowo mamy klucz self

			- do samego siebie

- application/**hal**+json

	- roznice do json

		- wprowadza rozroznienie na...

			- obiekty zagniezdzone / embedded

				- dla encji, osobnych zasobow

				- obiekty embedded maja swoje linki

				- autor jest osobnym zasobem

			- proste skladowe

				- dla value objects

				- kategoria/metadane kursu nie sa osobnym zasobem, do ktorego moglibysmy sie odwolywac

		- inna struktura odnosnika

### Stronicowanie

- Hypermedia swietnie sie sprawdzaja przy stronicowaniu

	- linki do poprzedniej, nastepnej, ostatniej i bieżącej strony

		- nie musimy zastanawiac sie, jaki jest id kolejnej/poprzedniej strony, czy numerujemy od 0, itd.

	- w meta danych informacja o tym, ile jest wynikow

## Lekcja 09.06. Wersjonowanie REST

### Kiedy wersjonowac?

- przy zlamaniu kompatybilnosci wstecznej

	- zmieniamy format daty, nazwe pola, format wartosci

	- zeby nie zepsuc integracji dotychczasowym klientom

- przy zmianie modelu biznesowego

	- wyobrazmy sobie, ze zmieniamy model: ksiazke reprezentowalismy jako tytul, a od teraz jako konkretny egzemplarz

		- jesli stosujemy osobny BC do oddzielenia domeny od zasobu dla klienta, to dzieki temu adapterowi, ta zmiana nie wplynie na API

		- natomiast jesli ta zmiana jest pozadana z punktu widzenia naszego API - klient potrzebuje  o niej wiedziec, to podbicie wersji jest konieczne

### Zasób a jego reprezentacja

- Zasob to jest konkretny obiekt biznesowy, byt, encja, ktora zyje w bazie danych

	- URI jednoznacznie okresla zasob

	- /users/123

- Reprezentacja zasobu mowi w jakiej postaci zasob jest dostarczany do uzytkownika

	- JSON, XML, cos innego?

	- do okreslania reprezentacji sluza naglowki

		- Accept: application/json

		- Content-Type: application/json

	- a nie URI

- nigdy nie mieszamy reprezentacji i zasobu w URLu

	- /users/123.json

	- osoba ma jeden adres zameldowania i wiele reprezentacji: dres, marynarka

### Co wersjonujemy?

- z reguly encja sie nie zmienia

	- /users/123 to ta sama encja niezaleznie od wersji API

	- dlatego nie dodajemy wersji w URLu

- zmienia sie reprezentacja

	- dlatego wersjonujemy przez naglowki

		- Accept: application/v1+json  
		  Accept: application/v2+json

		- Content-type: application/vnd.dna.v1+json  
		  Content-type: application/vnd.dna.v2.hal+json

	- wysylamy naglowek i serwer wie, co zwrocic

### Co jest zlego w wersjonowaniu w URLu?

- co zlego jest w /v2/users/123?

	- powod jest pragmatyczny: klienci czesto przepinaja sie stopniowo

		- dostaja nowe pole, ktorego potrzebuja, w nowej wersji API

		- postuja do starego API

		- dostaja location w starym API

		- zmieniaja v2 na v3

		- i dopiero robia GET do nowej wersji, zeby dostac nowe pole

### Kiedy wersjonowac w URL?

- kiedy calkowicie wywracamy nasz model biznesowy do gory nogami

	- np. z ksiazka

		- wczesniej myslelismy o tytulach, katalogu

		- teraz o instancjach, egzemplarzach

		- ksiazka znaczy cos innego, niz wczesniej

- kiedy zmieniamy technologie

	- API bylo w PHP, teraz jest w Javie

	- routing na zupelnie inny serwer

		- mozemy parsowac naglowki i parsowac Content Type, ale...

		- latwiej jest robic routing po URL, niz po naglowku

- warto nie uzywac /v2/

	- bo pozniej ciezko klientowi przestawic sie na naglowki

		- /v2/ w URLu i v4 w naglowku jednoczesnie wydaja sie niespojne i rodza niescislosci

	- lepiej /new-api/, jesli bylo /rest/ to /api/

		- wszystko, co nie bedzie sie kojarzylo z wersja

## Lekcja 09.07. Dokumentacja REST

### Cechy dobrej dokumentacji

- aktualna

	- najważniejsza cecha

- czytelna

- dostępna

	- zeby uzytkownicy chcieli sie w niej poruszac

	- 1000 stronicowy PDF nie zacheca do integracji z API

- uruchamialna

	- uzytkownik klika i widzi, jak API funkcjonuje

	- swiety gral dokumentacji

### Jak zapewnić aktualność?

- dokumentacja musi być ściśle związana z kodem i wpięta w proces kompilacji

	- jesli powstaje z kodu, to musi byc aktualna, bo w przeciwnym razie przestanie sie kompilowac

- testy zgodności dokumentacji z przyjętą specyfikacją i kodem

### Co dokumentowac?

- wszystkie dostepne metody

	- ze mozna utowrzyc/usunac uzytkownika

	- mozna anulowac/zaktualizowac/oplacic subskrypcje

- strukture dokumentu

	- zarowno żądanie, jak i odpowiedz

	- opisy pol

		- co znaczy pole subscription status?

	- wartosci enum

		- jakie sa wartosci statusow?

	- formaty danych

		- i w jakiej strefie czasowej

	- wszystko, czego oczekiwalibysmy, jako klient API

- przykładowe żądanie i odpowiedź

	- zeby uzytkownik mogl zobaczyc, jak wyglada data w praktyce, jakiej dlugosci sa stringi, czy enumy rozpoczynamy wielka, czy mala litera, etc.

### Jak dokumentowac?

- dokumentacja generowana w runtime na podstawie definicji zasobow i endpointow

	- dodatkowy komponent, ktory wstaje razem z aplikacja i wyswietla dokumentacje

		- na podstawie adnotacji lub sledzenia żądan

	- wada: nie weryfikuje zgodnosci ze specyfikacja

		- jesli kod statusu zmieni sie z 200 na 204, to po prostu zmienimy dokumentacje

		- ale zepsujemy komunikacje klientom

- dokumentacja generowana podczas kompilacji na podstawie specyfikacji API

	- np. podczas testow

		- w ramach testowania API wykonujemy żądania, ktore chcemy udokumentowac i sprawdzamy asercjami, czy zwrocily dobre statusy, dokumenty

		- przy okazji zapisujemy żądanie, odpowiedz, naglowki

			- i generujemy z nich przyklady do dokumentacji

### Przyklady

- GitHub

	- Request

	- Prosty opis odpowiedzi

	- Przyklad odpowiedzi

- Swagger

	- popularne narzedzie

	- estetyczna strona

	- pozwala uzytkownikowi wykonywac zapytania z poziomu przegladarki

		- fajna opcja na eksploracje API

- Slate

	- strona podzielona na 3-kolumnowa strukture

		- po lewej struktura API

		- po srodku opis wybranej metody

		- po prawej przyklady dokumentow

			- zostaly wygnenrowane podczas testow

				- rezultat odpowiedzi od fizycznego serwera

	- po prawej curl - namiastka wykonywalnosci

## Lekcja 09.08. Testowalność REST

### Kto jest zainteresowany testowaniem API?

- producent (zespol developerski) testuje zgodnosc implementacji ze specyfikacja

- klient testuje poprawnosc integracji z API

### Rodzaje API z punktu widzenia testowania

- dedykowane, publiczne REST API

	- oficjalne API naszej firmy

- REST API na potrzeby aplikacji web/mobile

	- wewnetrzne

### Testy API dedykowanego/publicznego

- klient chce miec mozliwosc zweryfikowania, czy to, co zrobil dziala

	- szczegolnie istotne, gdy usluga jest platna

	- nie chcemy placic za testowanie integracji

		- czesto nie wiemy, czy spelni nasze oczekiwania

- dlatego warto wystawiac srodowiska testowe, piaskownice/sandbox

	- byc moze udostepnic testowy klucz API, ktory zawsze zwraca zastubowane odpowiedzi

### Testy API wewnetrznego

- wykorzystywane jako natamiastka testow E2E, z pominieciem UI

	- zeby nie bawic sie w selektory CSS i bieganie po HTMLu

	- uwaga: im wiecej logiki wypchniemy do klienta, tym mniej reprezentatywne beda testy

		- jesli cala logika jest po stronie klienta, to weryfikacja, ze takie żądanie skutkuje taka odpowiedzia, nie mowi nic o stabilnosci aplikacji

			- nalezy to uwzglednic, decydujac czy cos powinno sie dziac po stronie klienta, czy serwera

- w przypadku brakow w API publicznym, klienci czesto wykorzystuja API wewnetrzne

	- w celu automatyzacji swoich procesow biznesowych

		- Robotic Process Automation

	- w takiej sytuacji, czeste zmiany, zwlaszcza niekompatybilne wstecznie...

		- nam utrudniaja utrzymywanie testow

		- a klientom utrzymanie ich procesow

			- a to nie jest ich wina, ze my nie dostarczylismy istotnej operacji biznesowej w API publicznym

## Lekcja 09.09. CORS

### Cross-Origin Resource Sharing

- żądanie międzydomenowe

- odpowiedz na ataki CSRF / Cross-site Request Forgery

	- CSRF wykorzystuje specyficzna przypadlosc przegladarek internetowych

		- polega na tym, ze przegladarkę nie interesuje, w ktorej zakladce mamy otwary bank, a w ktorej komentarze do artykulu

			- jesli ktos wstrzyknie zlosliwy kod w komentarzu, ktory uderza do API banku, to przegladarka - majac ciasteczko sesji z drugiej zakladki - uwierzytelni ten request

- jesli jestesmy na stronie app.dna.pl, i probujemy wolac RESTowe API z api.dna.pl, to to jest żądanie CORS 

### Mechanizm CORS

- zapobiega atakom Cross-site request forgery (CSRF)

- przed wyslaniem docelowego żądania, przegladarka sprawdza mozliwosc jego wykonania...

	- za pomoca preflight request / przedzapytanie

		- na docelowy URL, ale metodą OPTIONS

		- Naglowki

			- Origin

				- z jakiej domeny robimy żądanie

			- Access-Control-Request-Method

				- jaką metodą HTTP

			- Access-Control-Request-Headers

				- jakie naglowki, chcemy dolaczyc

	- do okreslonego serwera, na konkretny adres i konkretna metoda

- i wykonuje je jedynie po otrzymaniu poprawnej odpowiedzi

	- preflight response

		- Kod z grupy 200

		- Nagłówki odpowiedzi

			- Access-Control-Allow-Origin

				- z jakich domen dopuszczamy żądania

				- moze byc lista

				- nie stosujemy tutaj gwiazdki

					- bo wylaczamy caly CORS

			- Access-Control-Allow-Methods

				- jakimi metodami dopuszczamy żądania

			- Access-Control-Allow-Headers

				- jakie naglowki dopuszczamy

			- Access-Control-Max-Age

				- po jakim czasie przegladarka musi zweryfikowac, czy dalej dopuszczamy żądania

- Przyklad CORS

### Co wymaga wykorzystania CORS?

- za kazdym razem, gdy rozmawiamy z API przy uzyciu XMLHttpRequest i Fetch API

	- asynchroniczne zapytania, AJAX

- import czcionek

	- @font-face z CSS

- tekstury WebGL

- generowanie grafik przy pomocy metody drawImage

- w kazdym z tych przypadkow poleci preflight request

### Eliminacja CORS

- CORS mocno wplywa na wydajnosc aplikacji

	- bo kazde zapytanie jest zdublowane

		- zanim GET /users/, to OPTIONS /users/

		- zanim GET /users/1, to OPTIONS /users/1

- zeby zapobiec dublowaniu, stosujemy proxy, ktore wprowadza mapowanie...

	- proxy ma rozne nazwy Edge Service, application gateway, API gateway

	- app.droga.dev

		- strona dostepna z przegladarki

		- każde żądanie przekierowuje do serwera ze statycznymi zasobami: HTMLe, JS, CSS

	- app.droga.dev/api

		- nie api.droga.dev

		- API REST wykorzystywane przez strone

		- to jest osobny komponent, ale z punktu widzenia przegladarki to ta sama domena

			- wiec nie sa wymagana żądania CORS

