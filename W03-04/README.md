# **DNA 03-04**


## Lekcja 03.01. Bounded Context

### Z przestrzeni problemu (subdomena) przechodzimy do przestrzeni rozwiazan

- Potrzebujemy modelu

	- Przyklad: mapa kraju

		- Zawiera zarys granic, sasiadow, najwazniejsze miasta

	- Model nie odwzorowuje rzeczywistosci

		- Tylko wybrane, wazne aspekty rzeczywistosci

			- W sposob abstrakcyjny

		- Nie modelujemy sposobu dzialania przedsiebiorstwa, tylko istotne funkcje

### Model w oprogramowaniu

- Zestaw klas/funkcji

	- Modelujemy najpierw na tablicy, na kartce, a potem w kodzie

- Cel

	- Sprawdzanie poprawnosci dzialania niektorych funkcji biznesowych

### Przykladowe rozwiazania

- Wszystkie subdomeny, jako jeden model

	- To tak, jakby miec mape adresujacay problemy nawigatorow morskich, kierowcow, taternikow, uzytkownikow komunikacji miejskiej, itd.

		- Nieczytelna i bezuzyteczna

	- Nietestowalne, nierozwijalne

	- W Katalogu ksiazek nie myslimy o egzemplarzach

		- To domena Magazynu

		- Omijamy fakt, ze ksiazka w subdomenie katalogu znaczy cos innego, niz w domenie magazynu

	- Omijamy fakt, ze byt w jednej subdomenie znaczy cos innego, niz w innej

		- Zlozonosc przypadkowa

			- Instrukcje warunkowe, filtrujace

		- To nie jest zlozonosc esencjonalna problemu katalogu, tylko zlozonosc

			- Pojawia sie tylko dlatego, ze takie rozwiazanie wybralismy

	- Powod

		- Nie dzielimy problemu na subdomeny

			- Albo nie dzielimy zestawu danych, na ktorych operujemy

- Model domenowy

	- Dopasowany do problemu subdomeny

		- Separacja zagadnien

			- W Dostawie nie uwzgleniamy koloru ciezarowki

				- Jest to element rzeczywistosci, ale nieistotny dla nas

					- Wartosc biznesowa zero, a zajmuje czas na implementacje i komplikuje model

		- Ekspert Katalogu

			- Zainteresowany Cena

		- Ekspert Dostaw

			- Masa

		- Ekspert Magazynu

			- Liczba egzemplarzy

	- Model per subdomena

		- DRY

			- Kazda skladowa wiedzy powinna miec jedna reprezentacje w systemie

			- Nie lamiemy DRY, bo mamy inny podproblemy, rozne skladowe wiedzy

	- Gdzie sa osadzone subdomeny?

		- W Bounded Contextach

			- Konteksty nie nachodza na siebie

				- Rozwiazanie, oprogramowanie

					- Chce byc autonomiczne

				- Beda procesy przechodzace przez wiele podsystemow

					- Integrujemy sie przez jasno wystawiony API, kontrakt

			- Subdomeny nachodza na siebie

			- Niektore rozwiazania mozemy kupic

### Definicja

- Pod-system ma swoje jasne granice (ang. is bounded)

	- Zawiera swoj model/jezyk domenowy

		- Opisany problemami danej subdomeny

	- Nie wspoldzieli danych modelu z innym kontekstami

		- Jesli musi, to przez API

	- Komunikacja przez jasne API

- **Ubiquitous Language**

	- Wszechobecny jezyk

		- W danym podsystemie

			- **Nie w calym systemie**

				- „Ksiazka” dla kazdego interesariusza moze znaczyc cos innego

		- Istnieje w...

			- kodzie

			- dokumentacji

			- rozmowach ekspertow domenowych

	- Platforma komunikacji

		- Nie ma wartstwy translacji miedzy konceptem w umysle eksperta, a jego reprezentacja w kodzie

			- Unikamy nazewnictwa, ktore nie wyplyneloby z ust eksperta domenowego; nie jest czescia problemu

				- BookUtils, BookHelper, BookService, BookManager...

				- Czasem nie da sie uniknac slownictwa technicznego

					- Jesli jest, to ma byc nieskopoziomowy detal, a nie wysokopoziomowy kontrakt

	- Jezyk ewoluuje

		- To nie jest BDUF

			- Nie definiujemy na poczatku, tylko iteracyjnie

				- Odkrywamy jezyk, mapujemy go do modelu

				- Moze zmienily sie warunki rynkowe i pojawilo sie nowe slownictwo

- Dlaczego context?

	- **Granice pod-systemu są granicami lingwistycznymi**

		- Pojecia sa jasne i klarowne w kontekscie okreslonych granic

			- Slowo zamek w kontekscie budowlanym, cos znaczy

			- Bez kontekstu - nic

- Nie ma jednego modelu

	- Jest wiele, wybieramy najlepszy z naszej perspektywy

### Architektura wdrozeniowa

- Czy to jest mikroserwis? Modul w swiecie monolitow? Serwis w SOA?

- To pytanie ortogonalne do problemu

	- Mozna to zrobic w rozny sposob

	- Jak to wdrozymy, to inny temat

### Jak duzy moze byc?

- 100, 10k, 1kk LOC?

	- Zle zadane pytanie...

- Skoro opisuje problem subdomeny wszechobecnym jezykiem

	- Ma tyle klas, slow, zeby ten jezyk dokladnie opisac, a problem rozwiazac

	- Jest tak duzy, jak musi byc

	- Tak maly, jak moze byc

## Lekcja 03.02. Subdomena a Bounded Context

### Geneza nieporozoumien

- W swiecie idealnym, greenfieldowym, jedna subdomena to jeden bounded context

### Roznica

- Przyklad

	- Swiat idealny

		- W pokoju podloga (przestrzen problemu) jest ograniczona scianami

		- Mozemy kupic wykladzine, ktora idealnie przykrywa podloge (przestrzen rozwiazania)

	- Swiat rzeczywisty

		- Mozemy zakryc podloge dwoma starymi dywanami

		- a w miejscu, gdzie brakuje dywanow, postawic szafe

### Świat Legacy

- Bounded Contexty starajace sie rozwiazac rozne problemy

- Albo subdomeny rozwiazywane przez wiele bounded contextow

### Swiat idealny

- Nawet tutaj mozemy zaburzyc proporcje

	- Np. startujemy z subskrypcji miesiecznych i rocznych

	- ale firma ewoluuje i okazuje sie, ze wazniejszy jest podzial na firmowe i indywidualne

	- Szybciej zmienia sie struktura organizacji, niz oprogramowania

		- Dostajemy dwa rozne podproblemy, ktore moga miec wymagana wobec dwoch starych bounded contextow

## Lekcja 03.03. Walidowanie granic kontekstów

### Heurystyki subdomen

- Daly nam wstepny podzial w przestrzeni problemu

- Teraz mamy wiecej pytan i wiecej watpliwosci, bo jestesmy blizej rozwiazania

- Wiec moze podzielmi problem inaczej/bardziej szczegolowo

### Heurystki kontekstow

- #1 Autonomia kontekstu

	- Nadrzedna heurystyka

	- Kontekst musi byc mozliwie autonomiczny

		- Nie musi komunikowac sie z innymi

		- Czy moze sam podejmowac decyzje?

		- Czy musi pytac o zgode innych kontekstow?

	- Przyklad

		- Katalog ma pokazac cene w zaleznosci od klienta

			- Pobiera dane klienta i pobiera cene

				- Tzn. nic nie robi, tylko koordynuje

			- Byc moze rozwiazanie jest zbyt granularne

				- Wiedza o cenie dla kupujacego powinna byc w Katalogu

					- Enkapsulacja wiedzy

- #2 Liczba kontekstow w procesie biznesowym

	- Jesli widzimy proces biznesowy, ktory przechodzi przez mniej kontekstow, to najpewniej jest to lepsze rozwiazanie

		- Mniej integracji, komunikacji - mniej problemow

			- Wieksza autonomia

	- Uczucie dyskomfortu technicznego

		- Gdy np. proces fakturowania przechodzi przez wiele kontekstow

		- Nie maskujmy go rozwiazaniem technicznym

			- cache

			- powtarzanie

		- Zastanowmy sie, czy granice sa dobrze zdefiniowane

- #3 Szukaj informacji zmieniajacych sie razem

	- Jesli jakas dana musi zmienic sie atomowo w dwoch roznych kontekstach, to najprawdopodobniej mamy doczynienia z jednym kontekstem

		- Jesli nie moze byc nawet najmniejszej jednostki czasu pomiedzy aktualizacjami

- #4 Szukaj informacji uzywanych razem

	- Przyklad

		- Towarzystwo ubezpieczeniowe

			- Laczne

				- Kontekst sprzedazy polis

					- Pyta o historie szkod

				- Kontekst obslugi szkod

					- Pyta o warunki polisy

			- Rozlaczne

				- Moze trzeba podzielic inaczej

					- Ubezpieczenia komunikacyjne

					- Ubezpieczenia nieruchomosci

	- Walidowanie granic doprowadzilo do przegrupowania sposobu dzialania, jako przedsiebiorstwo

- #5 Zadaj sobie pytania

	- Jaka jest odpowiedzialnosc kontekstu?

		- Czy potrafie zwiezle ja opisac?

		- Czy opis to kilka zlozonych zdan?

			- Jesli tak, to najpewniej powinno to byc kilka kontekstow

	- Ile integracji ma kontekst? Dlaczego one tam sa?

		- Integracja zewnetrzna

			- Zmniejsza autonomie bardziej, niz wewnetrzna

		- Integracja wewnetrzna

			- Do innego systemu w organizacji

	- Jaka jest intencja integracji?

		- Jesli nie potrafimy jej jasno okreslic, to po co jest?

	- Czy jest jendo zrodlo prawdy kazdej waznej informacji biznesowej?

		- Jeden kontekst

		- Np. wlascicielem ceny ksiazki jest jeden kontekst, Katalog

	- Czy istnieje schizofreniczny kontekst?

		- Kontekst, ktory kazdy proces biznesowy musi spytac, czy np. ja dzialam z klientem indywidualnym czy korporacyjnym

			- Najpewniej mamy dwa konteksty: klientow indywidualnych i korporacyjnych

		- Instrukcja warunkowa w kazdym procesie rozbija sciezke na dwie podsciezki

- #6 Szukaj antywymagan

	- Antywymaganie to wymaganie, ktore nie ma sensu biznesowego

		- Pozwala walidowac, czy granice kontekstu sa ok

			- Szukamy takich wymagan, ktore lamia granice

	- Jak szukac?

		- Pozwalaja walidowac granice kontekstow

			- Czy widzisz wymaganie, ktore przecina konteksty?

				- Jesli nie, to konteksty sa prawidlowe

		- Przyklad: kontekst magazynu i zwrotow

			- Czy chcesz miec wymaganie, ktore nie pozwoli zwrocic ksiazki, jesli przed sprzedaza lezala w magazynie nr 6?

				- Biznes pewnie powie, ze to bez sensu

## Lekcja 03.04. Definiowanie Bounded Contextów w praktyce

### Best practices

- Zanim zaczniemy rozwiazywac problem, nalezy go skwantyfikowac, zeby wiedziec, czy sie zblizamy do rozwiazania, czy sie od niego oddalmy

	- **Metryki**

		- **Przyklady**

- Mozna wydzielic czesc wspolna uzywana przez rozne subdomeny

	- Np. wrapper platnosci

- Bounded contexty powinny pokrywac sie z subdomenami

### Process Level Event Storming

- Juz w przestrzeni rozwiazan

	- Nie problemow, jak w Big Picture ES

- Skupiamy sie na projektowaniu

	- Oprogramowanie do rozwiazania problemow

		- Ale nie musi to byc software

- Nie ma pieciu faz

- Nie odkrywamy, tylko projektujemy na nowo

- Mniej osob

	- Bo pracujemy nad poszczegolnymi subdomenami, a nie caloscia

		- Np. przygotowywanie kursu

- Moze ujawniac nowe mozliwosci biznesowe

	- Np. okazalo sie, ze przygotowanie strony kursu moze odbywac sie rownolegle do przygotowywania samego kursu, co pozwala na dodanie opcji „coming soon”

### Proces biznesowy moze miec miejsce, ale nie byc obslugiwany przez oprogramowanie

- Jest poza Bounded Contextem

- Ale jest na diagramie Process Level Event Stormingu

### Cos co bylo niedookreslone na poziomie BPES moze byc sprecyzowane w PLES

- Jedna subdomena podzielona na Bounded Contexty

### Heurystyki

- Jedno zrodlo prawdy

	- Czy zawsze kurs moze byc ogladany przez jednego uzytkownka?

		- Ma sie subskrypcje

		- Nie mozna, gdy jest sie zbanowanym

		- W katalogu moze go widziec kazdy

	- Efekt: Nowy BC Dostepnosc

		- Z ktorego korzystaja inne BC

		- Jest wiele powodow dostepnosci/niedostepnosci kursu, wiec osobny BC ma sens

- Autonomiczny BC

	- Po to szukamy autonomicznych granic, zeby zmiany w przyszlosci byly enkapsulowane w BC

		- A nie dotyczyly calego systemu

	- Antywymagania

		- Czy jesli dojdzie dodatkowa walidacja przygotowania video, to zmienia sie inne konteksty?

			- Nie, poki wyjscie sie nie zmienia

- Schizofreniczny kontekst

	- Subskrybcje biznesowe i indywidualne

		- If (biznes) ... else if (indywidualna)...

### Efekt

- Bounded Contexty

	- Mapowane w przyszlosci na komponenty

- Mozemy myslec jaka architekture dobrac dla calego systemu

## Lekcja 03.05. Lokalne drivery architektoniczne

### Drivery steruja decyzjami architektonicznymi

### Klasy

- Wymagania funkcjonalne

- Atrybuty jakosciowe

- Ograniczenia

	- Jesli mozemy uzyc tylko 3 baz, to wybieramy jedna dla BC

- Konwencje

- Cele projektowe

	- Prototyp vs finalna wersja

### Drivery moga byc rozne w roznych czesciach systemu

- Bounded Context jest ta granica

	- Moze miec inne drivery

- Przyklad

	- Ogladanie kursow

		- wysoka dostepnosc

	- Dodawanie kursow

		- nie musi byc tak dostepna

### Lokalne drivery tworza lokalna architekture

- Kazdy BC moze miec inna architekture aplikacyjna

## Lekcja 03.06. Prawo Conway’a

### Jak struktura organizacji wplywa na strukture systemu?

### Teoria

- Struktura kodu bedzie odzwierciedlala strukture organizacji, w ktorej powstal

- Raczej obserwacja, niz faktyczne prawo

	- Harvard Business Review

		- Porownali systemy open sourcowe i komercyjne

			- OS modularne

			- komercyjne - monolit

### Przyklady

- Przyklad 1

	- Kolokacja

		- Pracuja w jednym biurze, obok siebie

		- Stworza system bedacy jednym modulem

	- Zdalna praca

		- Kazdy ustala za co jest odpowiedzialny

		- Efekt: system skladajacy sie x modulow

- Przyklad 2

	- Zleceniodawca zatrudnia architektow, a programistom podzleca

		- Efekt: ESB, przez ktore komunikuja sie pojedyncze moduly

### Zastosowanie

- Zespol per Bounded Context

	- Prekursor: Amazon

		- Zespol, ktory jest w stanie sie wyzywic dwoma pizzami

	- Co jesli jeden zespol musi ogarniac wiecej BC? 

		- Pilnowanie granic

			- Musimy miec dodatkowe rozwiazanie pilnujace granic

			- W Javie np. moduly maven

## Lekcja 04.01. Monolit

### Czym jest?

- System zaimplementowany calosciowo, jako jedna aplikacja

	- Jednostka Wdrozeniowa

	- Deployment Unit (DU)

- Samowystarczalny w zdefiniowanym zakresie

	- Aplikacja zawiera wszystko: sprzedaz kursow, streaming, faktury, platnosci, etc. 

- Bardzo czesto pozbawiony modularnosci

	- Modularnosc to nie znaczy brak modulow

		- Czesto w monolicie sa moduly stricte techniczne

		- Warstwy

			- API

			- UI

			- DAO

			- logika aplikacyjna

			- logika biznesowa

### Zalety

- Szybka i niezawodna komunikacja

	- Jeden proces w OS

	- ta sama przestrzen pamieci

	- czesto w jednym watku

	- zawsze szybsze od (de)serializacji, wysylania po sieci

- transakcyjnosc

	- ACID

		- nie wystepuje w zadnym innym wzorcu systemow

	- idealne, gdy chcemy uzyskac gwarancja bardzo silnej spojnosci procesu biznesowego

- bezpieczna komunikacja

	- trudnosc wpiecia sie pomiedzy wywolania metod jest duzo wieksza, niz w przypadku systemow rozproszonych

	- zapewnienie bezpieczenstwa jest duzo latwiejsze, jesli odpowiednio zabezpieczylismy granice

- prosta infrastuktura

	- wdrozenie

		- jeden serwer

		- jeden artefakt aplikacji

	- prostsza automatyzacja i zarzadzanie infrastruktura

		- ograniczona liczba komponentow

- latwy development na starcie

	- bo latwa infrastruktura

	- bo szansa, ze do projektu dolaczy ktos, kto nie zna tej architektury, jest nikła

- Sa to zalety niemozliwe do osiagniecia w innych systemach

### Wady

- Kruchy i nieodporny (fragile)

	- zlozonosc esencjonalna

		- wynika z natury problemu

	- jakikolwiek blad wystapi, to z punktu widzenia systemu operacyjnego nie ma to znaczenia i jest traktowany jako blad calego systemu

		- Przyklady

			- czy to w krytycznym procesie biznesowym

			- czy w generowaniu raportu kwartalnego

			- i taka cala aplikacja pada

			- Jesli nastepuje wyciek pamieci, nadmierna utylizacja zasobow...

				- ...uderza to w cala aplikacje

				- a nie tylko w element systemu, ktory ma problem

- ograniczona skalowalnosc

	- wynika z natury problemu

	- wydajnosci i infrastruktury

		- Mozna zduplikowac monolit na blizniaczej insfrastukurze

			- Moga dzialac w klastrze

			- Skalowanie wszystko albo nic

		- Natomiast nie mozna wyodrebnic fragmentu, ktory ma problem ze skalowalnoscia

	- produktywnosci

		- Zaangazowanie kilkudziesieciu, moze kilkuset osob do pracy nad jednym codebase’m jest proszeniem sie o problemy

- trudnosci zachowania struktury

	- zmiana w jednym miejscu ma nieprzewidywalne konsekwencje dla calego systemu

	- Jak sie bronic?

		- Cover and Modify

			- zabezpieczamy fragment testami, a pozniej go modyfikujemy

			- czestszym podejsciem jest Modify and Pray

				- zmieniamy i modlimy sie, zeby dzialalo

- trudny w utrzymaniu

	- zlozonosc przypadkowa

		- wynika ze sposobu rozwiazania problemu

		- ze sposobu implementacji

		- a nie z natury problemu

	- wynika z braku zachowania struktury

### Modularny Monolit

- odpowiedz na zlozonosc przypadkowa monolitu

- Cechy

	- wciaz pojedyncza Deployment Unit

	- modularna struktura wewnetrzna

		- zlozony z modulow autonomicznych biznesowo

			- Nie

				- DAO

				- UI

				- Logika biznesowa

			- Tak

				- Uzytkownicy

				- Produkty

				- Katalog kursow

				- Oceny

				- Ksiegowosc

				- Faktury, etc.

- Zalety

	- lepsza testowalnosc

		- kazdy modul mozemy testowac w izolacji

		- w przypadku klasycznego monolitu

			- zeby przetestowac, czy cos sie zaksiegowalo

			- trzeba przetestowac e2e

				- logowanie uzytkownika

				- przeszukiwanie katalogu

				- kupowanie

				- ksiegowanie

		- w modularnym monolicie

			- wolamy operacje ksiegowania i zobaczyc, czy sie wykonala prawidlowo

	- latwa migracja do architektury rozproszonej

		- zawsze trzeba ja planowac

	- prostsze utrzymanie

		- koszt nie rosnie lawinowo, bo utrzymujemy kilka, niezaleznie rozwijanych aplikacji

- Wady

	- duplikacja danych

		- moduly sa niezalezne, a czasem zachodzi potrzeba korzystania z danych jednego modulu w innym module

			- Np. Kursy wyswietlaja srednia Ocene kursu

			- Nie chcemy odwolywac sie do obu modulow jednoczesnie, bo to narusza ich autonomie

			- wtedy modul Oceny musi powiadomic modul Kursy o zmianie sredniej oceny

				- Kursy musza tę zmiane zachowac po swojej stronie

					- Wiec bedzie to duplikat

	- ograniczone stosowanie kluczy obcych

		- Przyklad

			- Na fakturze (modul Faktury) wyswietlamy nazwe konta (modul Ksiegowosc)

			- nie mozemy stosowac kluczy obcych, bo to inny modul

				- zamiast tego uzywamy identyfikatora biznesowego, np. nr konta

	- trudniejsze zachowanie spojnosci

		- Brak kluczy obcych utrudnia zachowanie spojnosci

### Monolith first (najpierw monolit)

- skoro modularny monolit rozwiazuje sporo wad monolitu, to...

- nawet planujac system rozproszony, zaczynamy od modularnego monolitu

- Dlaczego?

	- monolit wybacza blednie wyznaczone granice

		- granice swiadcza o sukcesie systemu rozproszonego

			- zmiana granic jest bardzo kosztowna

				- np. musimy przepinac klientow z jednego systemu na drugi, bo dane zostaly zmigrowane

		- latwo je zmienic

	- start pracy jest zdecydowanie latwiejszy i szybszy, niz w przypadku systemu rozproszonego

		- szybciej dostarczamy wartosc biznesowa, bo mniejszy jest naklad na budowe i automatyzacje infrastruktury

			- wazne w Agile

			- duze koszty, zysk na poczatku niewspolmierny do czasu/kosztu

## Lekcja 4.02. Systemy rozproszone

### Definicja

- System zaimplementowany jako zestaw niezaleznych uslug produktu komunikujacych sie za posrednictwem sieci

### Powody rozpraszania systemu

- To wady monolitu

- Konkretnie

	- Skalowalnosc

		- Mozemy skalowac kazdy komponent niezaleznie

			- Kazdy moze miec inna infrastrukture

	- Odpornosc (resilience)

		- Problem z jednym komponentem nie przeklada sie na inne

			- O ile system jest prawidlowo zaprojektowany i zaimplementowany...

	- Heterogenicznosc technologii

		- W monolicie - homogenicznosc technologiczna

			- Nie napiszemy monolitu w Javie i Pythonie jednoczesnie

		- Mozliwe w systemie rozproszonym

			- Jedna usluga w Javie, druga w .NET, trzecia w PHP

	- Regulacje i bezpieczenstwo

		- Latwiej dostosowac do wymagan pojedynczy komponent, niz caly system

		- Przyklady

			- RODO

				- Latwiej wyizolowac modul objety wysumblimowanymi regulami bezpieczenstwa, niz zrobic to dla calego systemu

			- Normy regulartora platnosci

	- Produktywnosc

		- Skalowanie liczby osob pracujacych nad systemem

		- Juz od kiludziesieciu osob staje sie to trudne w wypadku monolitu

			- Nie mowiac o setkach, czy tysiacach

### Koszty rozpraszania systemu

- Wzrost zlozonosci infrastruktury

	- Skokowy, lawinowy

	- Siatka pipelinow, serwerow, artefaktow, w roznych

- Brak transakcyjnosci

	- Transakcje rozproszone sprawdzaja sie w ksiazkach

		- Glownie ze wzgledu na problemy ze skalowalnoscia...

		- deadlockami, powodowanymi wielofazowymi commitami

	- Musimy zapewnic kompensacje

		- Np. musimy wycofac fakture, gdy platnosc sie nie powiodla

			- Nie ma rollbacku

- Utrudnienia

	- lokalny development

		- uruchomienie lokalnie systemu rozproszonego jest trudne

			- dokladanie kolejnych komponentow

			- mockowanie, stubowanie

	- zmiany przecinajace komponenty w systemie

		- musimy je koordynowac

			- miedzy zespolami i systemami

			- czesto zmieniamy kilka komponentow jednoczesnie i w odpowiedniej kolejnosci

	- zapewnienie bezpieczenstwa

		- mamy duzo komunikacji sieciowej, ktora musi byc odpowiednio zabezpieczona

	- analiza i debuggowanie

		- przesledzenie komunikacji

		- wnioskowanie

			- przyklady

				- kto naliczyl ten rabat

				- dlaczego id uzytkownika jest pusty

		- wymaga odpowiedniego podejscia, doswiadczenia i zestawu narzedzi

### Bledne zalozenia w projektowaniu

- Siec jest niezawodna (reliable)

- brak opoznien (latency)

- siec jest bezpieczna

	- kazdy etap nalezy zabezpieczyc

		- moze dojsc do ataku ze srodka

- topologia jest niezmienna

	- dodawanie instancji

	- migracja instancji

		- nowe adresy IP

- brak kosztow transportu

	- zwlaszcza w chmurze, koszt moze nieprzyjemnie zaskoczyc

### Service-oriented architecture (SOA)

- styl architektoniczny

- przez wiele lat tozsama z ESB

	- Enterprise Service Bus

	- warto brac pod uwage, ze rozmowca moze to tak traktowac

	- mimo, ze SOA nie narzuca ESB

- Cechy

	- uslugi niezalezne od technologii i dostawcow

	- sa autonomiczne biznesowo

	- maja wyrazne granice

		- widizmy jasno, jak wspolpracuja

		- jasny zakres odpowiedzialnosci

	- wspoldziela kontrakt, nie implementacje

		- znamy API, ale nie implementacje

## Lekcja 4.03. Enterprise Service Bus (ESB)

### Czym jest?

- implementacja wzorca SOA

- szyna integracyjna

	- cala komunikacji pomiedzy serwisami odbywa sie za posrednictwem szyny

	- zapewnia komunikacje w calej organizacji, wiec musi dostarczac...

		- ...bogaty zestaw wtyczek (connectors)

			- soap

			- rest

			- db

			- ftp

			- mail

	- Czesto komercyjny produkt pudelkowy

		- IBM AppConnect

		- WebMethods

		- etc.

### Charakterstyka

- wysoka skalowalnosc

	- kazda z uslug moze byc wdrozona w dowolnej liczbie instancji

- kompleksowosc (governance)

	- bezpieczenstwo

		- autoryzacja

		- uwierzytelnianie

	- audytowalnosc

	- logowanie i sledzenie (tracing)

		- szyna zapewnia narzedzia, ktore pozwalaja stwierdzic kto, kiedy i dlaczego dokonal zmian

	- konfigurowalnosc

		- spora czesc procesu moze byc obsluzona za posrednictwem samej szyny

### Komunikacja

- nacisk na orkierstracje

	- szyna, jak dyrygent, kontroluje przeplyw calego procesu komunikacji

		- mnie, jako klienta nie interesuje, do kogo i za pomoca jakiego protokolu zostanie wyslana wiadomosc 

			- mowie: potrzebuje dodac kurs on-line

			- reszte wie szyna

- kanoniczny model danych

	- bogaty, ale mocno weryfikuje schemat

		- pozwala na zarzadzanie tak obszerna komunikacja w jednym punkcie

	- jest to konieczne, bo szyna mocno stabilizuje i hermetyzuje komunikacje

- współdzielenie bibliotek klienckich

	- szyna udostepnia gotowa biblioteke do komunikacji

		- nie ja decyduje, jak sie z nia komunikowac

		- z zagniezdzonym kanonicznym modelem danych

### Wady

- wysoka cena

	- narzedzia sa bardzo drogie

	- niepomijalna w budzecie

- waskie gardlo i single point of failure

	- uslugi dobrze sie skaluja, szyna nie

	- przyklad

		- padl dominujacy konsument; padl na 24h

		- szyna zaczela odkladac wiadomosci, ktore powinen pobierac konsument

		- po skolejkowaniu ich duzej liczby, infrastruktura pod szyna zutylizowala sie w 100%

		- do wstania potrzebowala 10x tyle zasobow, co do normalnego dzialania

		- awaria naprawiona po 8h

		- samo dzialanie uslug bylo ok, ale komunikacja nie dzialala, wiec caly system padl

- ograniczona produktywnosc rozwoju szyny

	- wdrozenia szyny

		- duze zespoly

			- opisujace komunikacje

				- za pomoca designerow UIowych

					- gdzie definiuje sie, jakie pole ma sie mapowac do jakiego pola

		- efekt

			- coraz wiecej logiki znajduje sie w szynie

				- staje sie ona gigantycznym monolitem

			- jako firma, mozemy zaimplementowac wszystkie zmiany, we wszystkich systemach, poza szyna

				- na koncu dostawalismy pozwolenie na komunikacje z pominieciem szyny

					- krok do mikroserwisow

## Lekcja 4.04. Mikroserwisy

### Geneza

- ESB

	- Gdzie scentralizowana komunikacja ograniczala skalowalnosc i odpornosc systemu

- Vendor Driven Standards -> Community Driven Solutions

	- nie centralny punkt mowi nam, jak funkcjonowac

	- tylko cala spolecznosc wypracowuje rozwiazenie

- Przechodzimy z...

	- ciezkiego jezyka komunikacji kanonicznej...

		- duze dokumenty SOAP

	- na 4 poziomy dojrzalosci RESTa

### Charakterystyka

- implementacja wzorca SOA

	- w ESB byl nacisk na orkiestracje

- nacisk na choreografie

	- nie ma dyrygenta, ktory mowi, jak zyc

	- same uslugi wiedza, jak sie komunikowac

- eliminacja punktow centralnych

	- klient zlecajacy operacje musi wiedziec, gdzie znajduje sie usluga odpowiedzialna za te operacje

		- w jaki sposob

		- jaki dokument

		- metoda http

	- wplywa pozytywnie na

		- poprawienie skalowalnosci

		- eliminacje Single Point of Failure

- luzne powiazania komponentow

	- bo skoro zmiana jednego kompontenu wplywa nie tylko na szyne, ale na wszystkie uslugi, z ktorymi wspolpracuje, to powiazania musza byc luzne

		- bo zmiana jednej uslugi nie moze pociagac za soba koniecznosci wdrozenia kilku innych w tym samym momencie

- cloud native

	- mikroserwisy sa projektowane pod katem wykorzystania ich w chmurze

		- m.in. wykorzystanie skalowania

### Wady

- duza dowolnosc technologiczna moze prowadzic do chaosu

	- ludzie wychodzacy z monolitu dostaja malpiego rozumu

		- wykorzystuja kazda technologie, „bo tak”

		- a nie bo determinuje to jakis driver architektoniczny

- bardzo wysoka zlozonosc technologiczna

	- najtrudniejsza architektura

	- liczba elementow do przewidzenia ogromna

	- liczba technologii ogromna

- skomplikowana infrastruktura

	- zlozonosc rosnie lawinowo

- utrudniona analiza komunikacji

	- ESB zapewnialo mechanizmy logowania, audytowalnosci, sledzenia

	- w mikroserwisach musimy zapewnic to sami

### Kryteria stosowalnosci

- potrzeba autonomii

	- z zalozenia nie ma relesow, ogolnych wdrozen

	- kazdy z komponentow moze wdrozyc sie niezaleznie

	- autonomia wdrozen instancji rozni mikroserwisy od klasycznych systemow rozproszonych

- kompetencje pozwalajace opanowac technologie i narzedzia

	- zespol musi byc bardzo kompetenty, zeby byc w stanie pracowac z ta trudna architektura

- potrzeba szybkiej/wysokiej skalowalnosci

	- dodanie nowej instancji jest operacja natywna

		- dynamiczna skalowalnosc

			- np. usluga streamowania video bedzie w 5 instancjach, za chwile w 12, a pozniej w 2

## Lekcja 4.05. Autonomia

### Jeden z podstawowych kryteriow stosowalnosci mikroserwisow

### Rodzaje

- Biznesowa

	- zapewnienie nam swietego spokoju

		- jeden biznes mowi, zeby cos robic, drugi, zeby tego nie robic

			- Biznes zw. ze sprzedaza B2B mowi, ze jesli wprowadzimy jakas zmiane, to pozyskamy gigantycznego klienta

			- Biznes B2C odpowiada, ze w codebasie jest ich projekt, ktory przetestuja dopiero za miesiac, wiec B2B niczego nie wdrozy

	- pozwala rozwijac produkty niezaleznie od siebie

		- system sprzedazy B2B

		- system sprzedazy B2C

	- rozny cykl zycia poszczegolnych produktow

	- mniejsza zlozonosc kodu

		- wieksza specjalizacja

		- mniej ifow w systemie

		- jeden ekspert domenowy

- Techniczna

	- wydzielanie komponentow z uwagi na...

		- rozna skalowalnosc

			- jeden komponent charakteryzuje sie zupelnie inna utylizacja zasobow

			- mimo ze jest zarzadzana przez tego samego eksperta domenowego i zawsze wdrazana razem, to oplaca sie wydzielic, aby zainstalowac na niezaleznej architekturze

		- wymagania bezpieczenstwa

			- np. systemy kartowe z PCI DSS

			- warto wydzielic do innego komponentu, np. zeby wyizolowac sieciowo

				- i uproscic procedury wdrozeniowe w reszcie systemu

- Technologiczna

	- dobieramy narzedzie do problemu

		- Ten Bounded Context mozna byloby napisac w Javie, ale lepiej w Go, bo jest duzo integracji z systemem operacyjnym

	- rozne jezyki programowania

	- rozne systemy operacyjne

- Swiadome i wlasciwie stosowanie driverow architektonicznych, pomaga swiadomie kontrolowac granice techniczne i technologiczne

### Autonomia a standardy

- to ze moge zastosowac rozne technologie, nie znaczy, ze musze

	- drivery technologiczne dadza odpowiedz, czy warto zmieniac

		- jedna z klas driverow sa konwencje

			- jesli baza relacyjna, to MySQL

			- jesli nierelacyjna, to Mongo

			- moge wybrac cos innego, ale...

				- musze udownic driverami, a najlepiej metrykami, ze to ma sens

	- np. nie musisz zmieniac Solr na ElasticSearch, bo Solr zapewnia to, czego potrzebujesz

- mozemy dopasowac siebie do technologii albo technologie do siebie

	- jesli Spring Session potrzebuje Redisa, a my go uzywamy

		- to moge wdrozyc Redisa albo...

			- co nie bedzie trywialne

		- napisac wsparcie do Spring Session dla swojej bazy

			- oddac utrzymanie do community lub dostawcy

			- mniejszy i krotkofalowy koszt

## Lekcja 4.06. Wybór architektury systemowej

### Projekt Kursik

- 1. Wybor driverow

	- Ograniczenia

		- projekt od zera

			- z jednej strony dobrze, bo mamy duza decyzyjnosc w zakresie technologii

			- z drugiej to zle, bo biznes nie do konca wie, czego chce

				- bedzie duzo feedbacku

		- zespol sklada sie z 5 developerow

		- za 4 miesiace MVP

	- Atrybuty jakosciowe

		- Obciazenie 50-150 req/s

		- SLA - dostepnosc 99,99%

- Decyzja

	- Modularny monolit

- Konsekwencje

	- Pozytywne

		- Wybaczanie bledow w wyznaczaniu granic

		- szybka i niezawodna komunikacja

		- prosta infrastruktura

			- bedzie wiele instancji

		- latwa implementacja i wdrazanie

		- mozliwosc wydzielania osobnych serwisow w przyszlosci

	- Negatywne

		- skalujemy zawsze cala aplikacje

		- walidacja wideo moze uzywac sporo zasobow

			- widzimy ryzyko, ale je akceptujemy

		- zadbanie o granice modulow

### Structurizer

- Decision log

	- Prefixy zakresu

		- SYS

			- caly system

		- APP

			- konkretna aplikacja

		- APP - XXX

			- modul XXX w aplikacji

	- Przyklady - SYS

		- wybrano polski jako jezyk dokumentacji dla biznesu, angielski dla reszty

		- uzycie modularnego monolitu

- Zapis BPES i PLES

- Diagramy

	- C1 System Context

	- C2 Kontenery

		- Jednym z nich jest nasz modularny monolit

	- C3 Komponenty

		- Wnetrze modularnego monolitu

		- To widac BC odkryte podczas PLES

