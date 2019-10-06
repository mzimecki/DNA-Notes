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

