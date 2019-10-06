# **DNA 01-02**


## Lekcja 02.04. Big Picture Event Storming

### Cel

- Eksploracja przestrzeni problemu biznesowego

- Problem zrozumialy dla wszystkich

### Cechy

- Szybki

	- 2-4h na warsztat

- Stopniowy

	- Wiedze zdobywamy porcjami, zeby byla zrozumiala

	- Podzielony na fazy

		- Wiedze zdobywamy warstwami

	- Operujemy eventami

		- Mowia co sie stalo

		- A nie jak sie stalo

- Uwidaczniajacy braki

	- Zbyt obszerny opis ukrywa braki

		- wychodza pozniej

	- Dzieki nanoszeniu zdarzen na os czasu, latwiej wychwycic braki

- Synchronizujacy wiedze

	- Zdobywanie wiedzy od ekspertow domenowych

	- Ale takze ujednolicanie wiedzy miedzy interesariuszami

		- Chcemy mowic wspolnym jezykiem

	- Warsztat wizualizujacy flow, na stajaco

		- Wspolne „notatki” na scianie, zamiast kazdej osoby notujacej niezaleznie

			- To wszystko minimalizuje ryzyko, ze dwie osoby wyjda z inna wiedza na ten sam temat

- Prosty

	- Zwlaszcza dla interesariuszy

		- Musza wejsc w proces i chetnie dzielic sie wiedza

	- Niski prog wejscia

		- Przyklejanie karteczek

		- Podzielony na fazy

			- Brak intro

### Kogo zaprosić?

- Interesariuszy wewnetrzni

	- Pracownicy

	- Managerowie

	- Wlasciciele

- Interesariusze zewnetrzni maja reprezentacje wsrod wewnetrznych

	- Pracownik odpowiadajacy za...

		- ...doswiadczenia uzytkownikow

		- ...ogarnianie regulacji prawnych

- Stakeholder mapping

	- Przed warsztatem

	- Na podstawie rozmow, zapisujemy interesariuszy

	- Mapujemy ich

		- Zaangazowanie

			- Czy biora aktywny udzial w procesie developmentu

				- PO, QA, etc.

		- Zainteresowanie

			- Nie biora udzialu bezposrednio, ale sa mocno zainteresowani wynikiem

				- Wlasciciel

				- Inwestor

		- Zapraszamy kluczowych i istotnych

		- Przyklad

### Nie nadaje się

- Gdy nie ma procesu biznesowego

	- Np. caly sytem to algorytm

### Przebieg warsztatu

- Przygotowanie

	- Przestrzen

		- Duzo miejsca w srodku sali

		- Malo krzesel

	- Sciany

		- Idealnie, jesli jest tablica do pisania

		- Musi byc duzo przestrzeni

	- Karteczki i flamastry

		- Zapewniamy tyle zestawow, ilu jest uczestnikow, a najlepiej wiecej

	- Flipchart

		- Moderator zapisuje legende, kluczowe mysli

	- Minutnik

		- Time-boxing

- Faza 0: Rozpoczecie

	- Przedstaw cel

		- Rozpoznanie procesu biznesowego

		- Poprawienie codziennej pracy

- Faza 1: Chaotyczna eksploracja

	- Napisz na pomaranczowej karteczce

		- Zdarzenia biznesowe istotne z waszego punktu widzenia

		- W czas przeszlym

			- Tryb temporalny

			- Np. Wystawiono fakture

	- Kazdy pracuje osobno (lub w malych grupach)

		- Na poczatku warsztatu

		- Jest to opcja, ale warto

		- Dlaczego

			- Torowanie/priming

				- Pierwszy kto sie odezwie, narzuca kierunek grupie

			- Samiec alfa

				- Nie menager ma mowic, a wszyscy

			- Skupienie

	- Kiedy skonczyc?

		- Kiedy pierwsza osoba przestaje pisac zdarzenia

- Faza 2: Wprowadzanie osi czasu

	- Ulozenie chronologiczne

		- **Ukladanie eventow w kolejnosci chronologicznej**

		- Kluczowy jest wymiar czasu

	- Usuniecie duplikatow

		- Niektore osoby ten sam event nazwa inaczej

			- Ciekawe dyskusje i informacja dla nas

	- **Hot Spot**

		- Kiedy kilka osob nie moze dojsc do porozumienia

			- My nie rozwiazujemy konfliktu

			- Mowimy: ok, tu jest jakis problem, zajmiemy sie nim pozniej

				- Teraz wazne jest, żeby ulozyc eventy na osi czasu

				- Pozniej kogos poprosimy o pomoc

		- Nie wiemy, co się dzieje

			- Jesli duzo, to biznes nie jest gotowy, bo za duzo niewiadomych

	- Swimlanes

		- Duzo rownoleglych procesow

			- Porzadkowanie

	- Rozgalezienia/branche

		- Reprezentowane przez karteczki jedna pod druga

			- Jesli jednozdarzeniowe

		- Jesli wielozdarzeniowe

			- Nadajemy nazwy

			- https://github.com/ddd-by-examples/library/blob/master/docs/images/eventstorming-big-picture.jpg

- Faza 3: Opowieść od końca

	- Od tej pory facilitator wchodzi do gry

		- Prowadzi uczestnikow

			- Poprzez zadawanie pytan

				- Wczesniej

					- Co sie musialo stac, zeby X?

				- Pomiedzy

					- Czy miedzy X a Y dzieje sie cos jeszcze?

					- Intuicyjnie dobieramy eventy

				- Alternatywa

					- Co jesli X by sie nie powiodlo?

					- Czy zawsze dzieje sie X, jesli Y?

		- Wczesniej stal z boku

	- Celem jest zdebuggowanie procesu

		- Odkrycie, czego brakuje

		- Co zostalo przegapione

	- Dwa systemy myslenia

		- 1

			- Szybkie podejmowanie decyzji

			- Energooszczedny

			- Dziala najczesciej

			- Podatny na bledy kognitywne, pulapki myslenia

		- 2

			- Logiczny, dokladniejszy

			- Zuzywa wiecej energii

			- Aktywuje sie, gdy jestesmy skupieni

				- Chcemy, zeby uczestnicy weszli w ten tryb

				- Potrzebny cognitive workload - cos trudnego

					- Dlatego prosimy ich o odtwarzanie procesu od konca

	- Efekt

		- Nowe zdarzenia

		- Poprawki w procesie

		- Rozgalezienia

- Faza 4: Ludzie i systemy

	- Cel

		- Okreslenie, kto wchodzi w interakcje z systemem, korzysta z niego

			- Kto jest zrodlem eventow?

	- Dwie grupy

		- Czlowiek

			- Czasem rola, czasem nazwisko

		- Systemy

			- Nie tylko komputerowe

			- Moze byc zewnetrzny dzial, urzad, spolaczenstwo

- Faza 5: Problemy i okazje

	- Input

		- Proces biznesowy

			- Taki, jaki jest naprawde

			- Taki, jak go rozumieja wszyscy zebrani

	- Teraz dopiero mozemy dostrzec problemy i okazje do poprawy

		- Okazja

		- Problem

		- Jedni sa nastawieni na problem, drudzy na okazje

	- Priorytezujemy to, czym sie zajmiemy

		- Za pomoca strzelek

- Alternatywy

	- Raczej oparte na narracjach interesariuszy

	- Przyklady

		- Domain Story Telling

		- Design Thinking

		- User Journey Mapping

		- Story Mapping

- Dokumentacja

	- Efekt event stormingu mozna udokumentowac

		- UML Activity

		- BPMN

	- Mozna zrobic zdjecie sciany

	- Zwinac folie

	- https://miro.com

## Lekcja 01.05. Zwinna architektura

### Ograniczenia moga umozliwiac zwinnosc

- ruch prawostronny

	- podnioslo bezpieczenstwo i przewidywalnosc

- immutability

	- daje prostsze rozwiazanie

- podzial na autonomiczne podsystemy

	- umozliwia kazdemu podsystemowi niezalezny rozwoj

- automatyzacji CI/CD

	- robimy raz i kazdy zespol ma czas na rozwiazywanie problemow biznesowych

- spojny stos technologiczny

	- przenoszenie programistow miedzy projektami

- protokol komunikacji miedzy podsystemami

	- nie musimy rozwazac wszystkich mozliwosci

	- prostsza integracja

- szukamy takich decyzji, ktore otwieraja mozliwosci

### Zaniechanie architektury

- nie da sie tworzyc, nie podejmujac decyzji

	- ktos inny je podejmie

### Ostatni odpowiedzialny moment

- im pozniej podejmujemy decyzje, tym lepiej rozumiemy drivery i ich miary

	- im lepiej rozumiemy, tym lepsze decyzje podejmujemy

## Lekcja 01.01 Wstęp do architektury

### Wytyczne dobrej architektury

- Powinna odzwierciedlac cel systemu, a nie okolicznosci jego powstawania

- Zrownowazona architektura

	- Wystarczajoco duzo struktury, zeby wszyscy grali do jednej bramki

		- Dobre, gdy outsourcujemy do innego zespolu, bo musza wiedziec, co robic

	- Wystarczajaco duzo swobody, zeby mozna bylo podejmowac swobodne, szybkie decyzje

		- Dobre dla malego, zgranego zespolu

	- Nie ma zlotego srodka

### Architekt vs programista

- Analogia z budownictwa

	- Architekt to solution architect

	- Projektant to application architect

	- Wykonawca to programista

		- To problem, bo programisci robia wiecej

			- Sa tak naprawde projektantami

		- Wykonawca jest build pipeline

### Czym jest architektura?

- zestaw decyzji

	- ksztaltujacych projekt

- opis struktury

	- Programista optymalizuje pod implementację, architekt pod wszystkie elementy cyklu rozwoju: implementacja, testowanie, wdrazanie, etc.

- proces projektowania

	- OODA loop

		- Observation

			- zbieranie informacji z otoczenia

		- Orientation

			- dobieranie znanych technik do informacji

		- Decision

			- podjecie decyzji na podstawie powyzszego

		- Action

			- dzialanie

- Proces podejmowania decyzji, zaczynający się od driverów architektonicznych i skwantyfikowania ich przy pomocy metryk 

	- Dzięki temu budujemy spojne zrozumienie problemu wsrod interesariuszy

### Najwazniejsi sa LUDZIE

- umiejetnosci miekkie

	- bo lider techniczny

	- bo gada z biznesem

### Po co jest?

- zmniejsza ryzyko kosztownych pomylek

- ulatwia komunikacje

- umozliwia calosciowe postrzeganie

## Lekcja 01.02 Model C4

### Sposob wizualizacji architektury

- mapa nawigacyjna

- zapewnia wspolne zrozumienie systemu

- struktura systemu

### od dawna to UML

- wysoki prog wejscia

- powoli zapominamy?

	- jesli organizacja go rozumie, fajnie

### ArchiMate

- wszystko na jednej grafice, wiec ciezki do zrozumienia

### C4

https://c4model.com

- Składowe

	- Kod

		- Klasa

			- w j. obiektowym

		- Funkcja

			- w j. funkcyjnym

	- Komponent

		- Zestaw klas, ktore tworza kontrakt wyzszego poziomu

	- Kontener

		- srodowisko uruchomieniowe dla 1+ komponentow

			- baza danych

			- serwer aplikacyjny

		- powinny byc gotowe na osobne wdrozenie

		- komunikacja przez API

			- REST

			- SOAP

	- System

		- zestaw kontenerow tworzacych wartosc biznesowa

- Diagramy

	- Kontekstu, C1

		- kto uzywa systemu

		- z jakiego powodu on powstal

		- jakie sa integracje i jaki jest ich cel

		- wysokopoziomowy

			- rowniez dla nietechnicznych

	- Kontenerow, C2

		- Przyklady

			- Aplikacja mobilna, Xamarin

			- API, Java/Spring

			- Baza danych, RDBS

		- Opis konteneru

			- nazwa

			- odpowiedzialnosc

			- wybrana technologia

			- interakcja

				- jaki protokół

		- Admin moze zobaczyc: sa 3 jednostki wdrozeniowe

	- Komponentow, C3

		- Dla osoby technicznej, pracujacej z systemem

		- Rozklad odpowiedzialnosci

			- promowanie reuzywalnosci komponentow

			- strukturyzuje wiedze

				- moze za wiele komponentow i trzeba rozbic

		- Przyklady

			- Resetowanie hasla

			- Logowanie

			- Komponent bezpieczenstwa

			- Fasada do innego systemu

		- Opis komponentu

			- nazwa

			- odpowiedzialnosc

			- wybrana technologia

			- interakcja

				- jaki protokół

				- sync/async

	- Klas, C4

		- UML

		- bardzo niestabilny ze wzgl. na zmiennosc

			- opcjonalny

	- Możliwy C0 (C5?) i więcej

		- widoczne wszystkie systemy w organizacji

			- jesli jest ich bardzo wiele, mozna podzielic na domeny

- Ogolne warunki

	- malo notacji

	- najwazniejsze jest operowanie na jednym poziomie abstrakcji

	- nie wyklucza innych narzedzi

	- utrzymac aktualnosc

		- max. stopien integracji diagramow z kodem

		- generowanie z kodu

			- https://structurizr.com

	- jest to diagram logiczny

		- mozna mapowac na wdrozeniowy

- Ograniczenia

	- model statyczny

		- nie bierze pod uwage wymiaru czasu

	- nie wspiera modelu domenowego ani maszyn stanow

		- pozostaje UML

## Lekcja 02.01. Architektura a biznes

### Programista/architekt musi rozumiec problem space, dziedzine problemowa

- Mimo, ze czesto nie jest ciekawy

- Dostrzeganie wzorcow w problemie (zamiast w budowanym systemie)

	- Czesto prowadzi do prostszych rozwiazan

- Zrozumienie problemu to wlasnie Obserwacja z modelu OODA

- Niezbędne do odkrycia driverow architektonicznych

- Potrzebna do ewaluacji architektury

	- Postfactum chcemy stwierdzic, czy to, co stworzylismy jest dobre, czy zle

- Zadania architekta

	- Zrozumienie celu

		- Strategia (co osiagnac?)

		- Programiscie sa slabi w tym obszarze

			- Brakuje metodycznego podejscia

		- Rozwiazanie

			- Strategiczne DDD

				- Subdomains, domain model, bounded context, ubiquitous language

			- Taktyczne DDD

				- Pomaga w implementacji ladnego, testowalnego kodu

			- Mozna uzywac oddzielnie

	- Znalezienie rozwiazania

		- Taktyka (jak osiagnac?)

		- Frameworki, wzroce architektoniczne, biblioteki, wzorce projektowe

		- Programiscie sa mocni w tym obszarze

### Dlaczego analityk/PO nie wystarcza?

- Trzy perspektywy

	- Wartościowość

		- Analityk rozumie, co w biznesie idzie dobrze, a co zle, gdzie sa straty

			- To nie wystarcza

	- Wykonalnosc

		- Architekt, programista zna narzedzie, techniki, uslugi, ktore pomogloby rozwiazac czesc tych problemow

			- O ktorych analityk nie wie

	- Uzywalnosc

		- Dzieki UXom, unikamy rozwiazania, ktore jest nieuzywalne

	- Tylko rozpatrzenie trzech perspektyw lacznie, gwarantuje dobre rozwiazanie, idealny punkt

## Lekcja 02.06. Metryki dla biznesu

### Cel

- Usprawnienie komunikacji z biznesem

- Liczbowe wyrazenie sukcesu projektu

### Jak mysli biznes?

- Jezyk rozwiazan, nie problemow

	- Nie mowimy, ze jest taki i taki problem

	- Mowimy: chyba sie da, wrocimy do Was za tydzien z odpowiedzia, bo musimy zrobic to i to

		- Nie geneza problemu

		- Konkretne etapy, ktore trzeba zrealizowac, zeby dojsc do rozwiazania problemu

- Widzi

	- funkcje (featury)

	- bledy

	- liczby

- Planowanie

	- Dlugofalowo

		- IT

		- Zarzad

	- Krotkoterminowo

		- Kierownictwo sredniego szczebla

			- Mysla o biezacym projekcie, a nie tym za 3 lata

### Metryki SMART

- Smart sluzy z zalozenia do definicji celow

	- Ale dziala tez fajnie do metryk

- Cechy

	- Specific (Skonkretyzowany)

	- Measurable (Mierzalny)

	- Achievable (Osiagalny)

	- Relevant (Istotny)

	- Time-bound (Okreslony w czasie)

- Zblizony do metryki idealnej

	- Warto zastosowac, bo biznes to zna

- SMART+ER

	- Evaluated (Oceniony)

		- Retrospektywa

	- Readjusted (Dostrojony)

	- Tryb agileowy

		- Stale poprawiamy nasze zrozumienie problemu i sposoby implementacji rozwiazan

### Rodzaje metryk

- Techniczne

	- Zdrowie systemu w ujęciu technicznym

		- Opisuja stan procesow/zespolow technicznych

		- Przyklady

			- Czas potrzeby na wdrozenie poprawki

			- ...na onboarding pracownika

			- Liczba bledow na srodowisku produkcyjnym

			- Czas przetestowania krytycznych procesow/sciezek biznesowych

				- Jesli w ktoryms momencie pozwolisz, biznesie, wdrozyc testy automatyczne, to liczba bledow spadnie o X. Bedzie to kosztowalo Y.

					- Latwiej prosic o pieniadze na refaktoring

	- Zalety

		- Tlumacza technikalia na jezyk zrozumialy przez biznes - liczby

			- Najlepiej liczby w zlotowkach :)

			- Naszym celem jest ulatwienie biznesowi zrozumienie problemow

		- Wprowadzaja rozliczalnosc

			- Biznes moze zweryfikowac, czy refaktoring/projekt sie udal

		- Buduja zaufanie

			- Skoro cel zostal osiagniety, to latwiej o pieniadze na kolejny

- Biznesowe (procesowe)

	- Zdrowie systemu w ujeciu procesow biznesowych

		- Przyklady

			- Liczba zlozonych zamowien

			- Srednia wartosc koszyka

			- Czas spedzony na stronie

			- Liczba blednych platnosci

			- Liczba dodanych kursow

			- Liczba uzytkownikow systemu

	- Warto od nich zaczynac

		- Nie zarzucajmy ich technikaliami na poczatku

		- Niech naucza sie z tego korzystac, nie boja zajrzec do Grafany

		- Na poczatek cos prostego

		- Fajnie sie je pokazuje na spotkaniu zarzadu

	- Co daja?

		- Eliminuje potrzebe stosowania hurtowni danych

			- Odpowiedzi sa od razu, np. na dashboardzie

		- Mozliwosc analizy anomalii

			- Co wplynelo na to, ze w pt o 14 wartosc koszyka skoczyla dwkurotnie

			- Feedback na biezaco

		- Biznes jest podekscytowany rozliczalnoscia, wynikami

	- Jak znalezc?

		- Podczas Event Storming

			- Mamy dostep do waznych eventow biznesowych

			- Mozna zapytac, czy ich mierzenie mialoby wartosc dla biznesu

		- Kryteria sukcesu projektu

			- Co znaczy, ze projekt zakonczyl sie sukcesem?

			- Jakie sa kryteria sukcesu?

		- Po awarii/problemie

			- Przejdzmy przez metryki, ktore mamy i zastanowmy sie, czy cos zwiastowalo katastrofe

			- Moze w okolicy jest metryka, ktora warto monitorowac, alertowac

## Lekcja 02.02. Domena i subdomeny

### Nauka problemu biznesowego i analiza rozwiazan to clue inzynierii oprogramowania

- Kod jest efektem ubocznym

- Musimy zrozumiec biznes, zeby zdobyc dobre drivery architektoniczne

- Pozwala minimalizowac ryzyko kosztownych bledow

	- Od zmniejszenia potencjalu organizacji po zmiane jej zmiane jej modelu operacyjnego

### Strategiczne DDD

- Domena

	- to czym zajmuje sie firma, w ktorej pracujesz

		- Np. domena to prowadzenia ksiegarni online

- Subdomeny, szukanie subdomen

	- Wyróżnialne obszary biznesowe

	- Niezalenie od wielkosci firmy

	- Niektore sie przecinaja

		- Np. fakturowanie wie o dostawach i zamowieniach

	- Rodzaje

		- Core domain (główna domena)

			- Cechy

				- Wyroznik biznesowy

				- Stratego biznesowa

				- Nie da sie kupic

				- Nie musi byc oczywista

				- Tworzymy sami

					- Nie outsourcujemy

			- Odpowiada na pytania

				- Dlaczego powstal ten system?

				- Dlaczego go nie kupilismy?

			- Kladziemy na najwieksza jakosc

				- Spedzamy najwiecej czasu

				- Doradzamy biznesowi, ze tu musimy dac najlepszych ekspertow technicznych i domenowych

			- Przewaznie jedna

				- Ale moze byc wiecej

					- Szczegolnie, jesli organizacja odkrywa nowy potencjal

		- Supportive subdomain (wspierająca)

			- Wspieraja core

			- Nie maja same w sobie wartosci biznesowej

			- Ale sa na tyle specyficzne, ze nie mozemy kupic gotowego produktu

			- Troszke mniejszy nacisk na jakosc

		- Generic subdomain (generyczna)

			- Ważne dla biznesu...

			- ...ale nie unikalne dla naszej firmy

			- Mozemy kupic gotowe rozwiazanie

		- Przyklady dla księgarni

			- Core domain

				- Nie jest to katalog, bo kazda ksiegarnia moze taki miec

				- Moze byc modul prognozowania, ktory zamawia ksiazki upfront, dzieki czemu klient nie musi czekac

			- Supportive

				- Rekomendacje

				- Zwroty

				- Katalog

			- Generic

				- Magazyn

				- Dostawy

				- Fakturowanie

	- Dlaczego ważne?

		- Zrozumienie dzialania biznesu

			- Divide and conquere

	- Ewolucja

		- Zaproponowany podzial moze zmieniac sie w czasie

		- Moze nie byc core domain

			- Np. decydujemy sie na stworzenie wlasnego programu do fakturowania, bo jest taniej

		- Core domain moze ewoluowac

			- Ten system moze z czasem przeksztalcic sie w core domain

				- Zaczniemy go sprzedawac

- Kiedy nie robic, nie szukac subdomen? 

	- Zakres jest maly

		- nie ma zlozonosci

		- Wiecej niz 4 funkcje: CRUD

	- Zakres jest duzy, ale powtarzalny

		- nie ma zlozonosci biznesowej

		- np. transformacja danych

	- Co jesli kilkanasci funkcji biznesowych?

		- Sa dobrze wyspecifikowane? Czy ja je rozumiem?

			- Jesli nie, robimy strategic DDD

		- Sa przyszle pomysly?

			- Jesli tak, robimy strategic DDD

			- Pytac o to eksperta domenowego

	- Moze subdomeny sa juz wyspecifkiowane

		- Ktos to zrobil, a my dzialamy w ich zakresie

- Cynefin

	- Model badania i analizy zlozonosci

		- 5 kategorii

			- Prosty

				- natychmiast widac relacje skutku i przyczyny

				- Kroki

					- Odczuwanie problemu

					- Klasyfikacja

					- Reakcja

				- problem znany

					- przyklady

						- CRUD

						- Telefon nie reaguje, podlaczam do ladowarki

				- Bez DDD

			- Skomplikowany

				- Podlaczony telefon, dalej nie dziala

					- moze ladowarka, gniazdo, telefon

				- Kroki

					- Odczuwanie problemu

					- Analizowanie

					- Reakcja

			- Zlozony

				- znalezienie relacji miedzy skutkiem, a przyczyna dopiero po fakcie

					- eksperymenty, analizy, innowacyjnosc

				- miejsce na Core Domain

				- Debugguje system telefonu

				- Kroki

					- Badanie

					- Odczuwanie problemu

					- Reakcja

			- Chaos

				- Nie ma czasu na analize

				- Najpierw sprowadzam do problemu prostego, skomplikowanego, zlozonego

				- Telefon jest b. goracy

					- wyciagam baterie

				- Kroki

					- Dzialanie

					- Odczuwanie problemu

					- Reakcja

			- Nieporzadek

				- Nie mam danych, czy przyporzadkawac do pozostalych kategorii

- Alternatywa

	- Value Chain

		- podobny model podzialu domeny

## Lekcja 01.03 Drivery architektoniczne

### Czym sa?

- Odpowiadaja na pytania

	- Dlaczego system powstal w takim a nie innym ksztalcie?

	- Skad ta technologia?

	- Dlaczego jest tu obecna baza relacyjna?

### Piec klas

- Wymagania funkcjonalne

	- Lista funkcji okreslajacych system

- Atrybuty jakosciowe

	- Kluczowe dla sukcesu

	- Dodanie ich pozniej jest b. kosztowne

	- Przyklady

		- Skalowalnosc

		- Bezpieczenstwo

- Ograniczenia projektowe

	- Budzet

		- nie wybierzemy technologii, ktora jest droga, jesli inna jest za darmo

	- Czas

	- Wiedza

		- nie wybierzemy technologii, ktorej nie znamy, bo nauka zajmie za duzo czasu

- Konwencje

	- Szereg zasad, ktore stosujemy w organizacji, np. w celu promowania spojnych rozwiazan

	- Przyklady

		- Jedna biblioteka do logowania

		- Wybor takich technologii, ktore sa atrakcyjne dla potencjlanych specjalistow

- Cele projektowe

	- Inny stack do prototypu, inny do rozwiazania produkcyjnego

### Po co drivery?

- Oszczednosc czasu i pieniedzy

	- Zajmujemy sie tematami, co do ktorych wiemy, ze spelnia wymagania biznesowe

	- Np. system finansowy o slabym poziomie bezpieczenstwa jest bezuzyteczny

- Zawezenie przestrzeni mozliwego rozwiazania

	- Ograniczamy mnogosc rozwiazan

- Odkrycie prawdziwych potrzeb projektu

### Odkywanie driverow

- Zrodlem informacji sa interesariusze

	- Moge miec rozne poglady na wymagania

		- Nalezy rozmawiac z duzym i zroznicowanym gronem interesariuszy

		- Kazdy ma rozna decyzyjnosc i priorytety

			- Np. CTO powie o konwencjach, a odbiorca biznesowy o wymaganiach funkcjonalnych

	- Jak rozmawiac?

		- Czy driver X jest wazny?

			- Nie ma sensu, bo zawsze odpowiedz bedzie: tak, wazny

		- **Czy X jest wazniejszy od Y?**

			- daje informacje o priorytetach

		- **Ktore feature’y chcemy, jesli moglibysmy zrealizowac tylko 3?**

		- Co jesli zmniejszymy troche dostepnosc, ale znacznie obetniemy koszty?

	- Stakeholder mapping

		- Analizujemy priorytety i decyzyjnosc interesariuszy

- Kompromisy

	- Drivery moga byc zalezne

		- Dostepnosc (atrybut jakosciowy) daje wiekszy koszt (ograniczenie projektowe)

### Zmiennosc

- Lokalizacja w systemie

	- Nie musza dotyczyc calego systemu

		- skalowalnosci mozemy wymagac tylko w obrebie okreslonego procesu biznesowego

		- dostepnosc raportowania inna niz dostepnosc przyjmowania zamowien

- Czas

	- Organizacja ewoluuje, wiec moge zmieniac sie drivery

		- Na poczatku moze zalezec bardziej na rozwijalnosci i testowalnosci

		- Pozniej skalowalnosc i utrzymywalnosc moze byc wazniejsza

- Cykl zycia systemu

	- implementacja

		- reuzywalnosc

		- rozwijalnosc

		- testowalnosc

		- czytelnosc

	- wdrozenie

		- konfigurowalnosc

	- funkcjonowanie

		- bezpieczenstwo

		- skalowalnosc

		- wydajnosc

		- dostepnosc

	- serwis

		- niezawodnosc

		- obserwalnosc

- Zapisywanie zmian

	- Architecture Decision Record

		- Rekord opisuje dokladnie jedna decyzje

		- Zawiera czas podjecia decyzji

		- Wyjasnia obecna sytuacje organizacyjna i priorytety

		- Specyfikuje wplyw driverow na decyzje

		- Rekordu nie nadpisujemy

			- Dodajemy nowy

			- z odniesieniem do starego

		- Kod powinien linkowac do ADRa

	- Architecture Decision Log (ADL)

		- zbior ADRow

		- moze byc w repo z kodem

		- lub na innej platformie

			- Confluence

			- Google Drive

## Lekcja 01.04. Metryki

### Co to jest?

- Metryka jest kwantyfikacją drivera

	- Do zapisu drivera liczbami

		- Zapewnia jednoznaczne rozumienie drivera

			- Testowalnosc dla jednych moze byc liczba testow, dla drugich szybkoscia dzialania testow, a dla kolejnych latwoscia ich implementacji

		- Umozliwia sledzenie zmian

	- Przyklad

		- Chcemy miec fajne biuro

		- Chcemy miec biuro, do ktorego dojedziemy w max. 30 min i gdzie na pracownika przypada min. 10 m2

		- Nowe biuro jest fajniejsze o 10%, bo na pracownika przypada 11 m2

		- https://en.wikipedia.org/wiki/Software_metric

	- Proces kwantyfikacji jest trudny

		- Na poczatku przynosi wiecej pytan, niz odpowiedzi

### Przykłady

- Testowalnosc

	- Procent krytycznych procesów biznesowych możliwych do przetestowania z pominięciem UI

	- Czas w minutach potrzebny do wykonania testów integracyjnych w środowisku ciągłej integracji

- Low-hanging fruits

	- Czas kompilacji aplikacji

		- Dostepna na CI/CD

	- Czas potrzebny do wdrożenia

		- Ile czasu potrzeba od commitu do dzialajacej aplikacji na produkcji

		- Jesli wynosi 8h, to w razie bledu, tyle lezymy

			- Dobre do dyskusji z biznesem: chcecie, żeby tyle lezal system?

	- Procesy biznesowy pokryte testami

### Wartości

- aktualna

- limit

	- minimalna wartosc, ktora chcemy osiagnac

		- ponizej -> projekt sie nie udal

	- prog bolu

- cel (goal)

- ideał (wish)

### Rodzaje

- Metryki długu technicznego (dłużne)

	- Im niższa wartość, tym lepiej

	- Np. calkowity czas backupu

	- **Dopuszczasz, ze cel jest gorszy, niz stan obecny**

- Metryki jakościowe

	- Im więcej, tym lepiej

	- Np. szybkość kopiowania danych

	- https://en.wikipedia.org/wiki/List_of_system_quality_attributes

- Metryka łączona

	- Cześć jest dłużna, część jakościowa

		- Np. Czas wykonywania kopii to metryka dłużna, ale szybkość wykonywania kopii (Mb/s) to jakościowa

		- z jednej strony czas uruchomienia testów jest dłużny a z drugiej pokrycie ścieżek jest jakościowe

	- Jakis driver jest zawsze opisany jakimis metrykami

### Cechy

- Jednoznaczna

	- Kwantyfikacja to zapewnia, ale nie możemy pozwolić na pole do interpretacji

	- Czas wykonywania testow

		- Jakich testow?

		- Na jakim srodowisku?

		- Pod jakim obciazeniem?

- Mierzalna

- Łatwo dostępna

	- Najlepszy dashboard z metrykami, KPIs, i historia

### Tradeoffs

- Wiecej testow -> dluzszy czas kompilacji i wdrozenia

- Konieczne jest rozwazenie konsekwencji

	- Czy ja jestem na to gotowy?

	- Byc moze musze zmienic kwantyfikacje innej metryki

## Lekcja 02.05. Odkrywanie subdomen w praktyce

### Przyklad

- Platforma sprzedazy kursow on-line

### Notacja jest elastyczna

- Mozna dodac ikony np. Excel, Dropbox

- Wazne, zeby wszyscy rozumieli co to znaczy

### Zalezy nam na odkrywaniu subdomen

- Dzielenie procesu na autonomiczne komponenty

- Heurystyki

	- H1 - Struktura organizacji

		- Elementy, ktorymi zajmuje sie jeden dzial

		- W pelni autonomiczny

		- Nie interesuje ich zmiana procesu

		- Przyklady

			- Marketing

			- Ksiegowosc

	- H2 - eskperci domenowi

	- H3 - jezyk domenowy

		- Te same slowa uzywane przez rozne osoby

		- Przyklad

			- Subskrypcja

				- BOK

					- Definiuje

					- Globalna

				- Klienta

					- Oplaca

					- Swoja

				- Mozemy zmienic providera platnosci i to nie wplynie na definicje planow subskrypcji

					- Mozemy zmienic proces definiowania subskrypcji i to nie wplynie na platnosci

			- Reklamacja

				- Mimo dwoch aktorow, ta sama subdomena, bo to de facto jest ten sam obiekt reklamacji

			- Publikacja

				- Zmiana z liczby pojedynczej (odcinek) na mnoga (kurs)

		- Patrzymy na slownictwo domenowe i sprawdzamy, czy to samo slowo oznacza to samo

	- H4 - wartosc biznesowa

	- H5 - kroki procesu

		- Kroki procesu definiuja znaczenie slowa

		- Przyklad

			- Kurs

				- Ogladanie dot. konkretnego uzytkownika

				- Wyszukiwanie - wszystkich uzytkownikow

			- Recenzja

				- Subdomena generyczna

			- Rekomendacje

				- Subdomena generyczna

### Czasem warto zostawic wieksza subdomene, zeby podzielic ja na etapie prac nad konkretnym rozwiazaniem (przestrzenia rozwiazan)

### Rodzaje subdomen

- Core

	- Subskrybcji (?)

		- kupujesz, bo jest jakiś konkretny autor, ale autor umieszcza coś na naszej platformie, dlatego, że model subskrybcji jest taki, a nie inny

		- Być może nasz model domenowy polega na zdobywaniu autorów, a nie oglądających, bo wiemy, że oglądajacy i tak przyjdą jeśli mamy odpowiednich autorów

		- tam było najwięcej czerwonych karteczek (problemow/niedomówień)  i na tych chcemy sie skupić aby naprawić "najsłabsze ognowo". 

			- zmniejszenie kosztów obsługi subskrypcji przekłada się na mniejsze koszty operacyjne co umożliwi przeznaczenie tych środków na pozyskanie najlepszych treści (aktualnie jest to największy koszt operacyjny firmy: zwroty, błędy, problematyczna obsługa)

	- Katalog

	- Na tym etapie mozemy jeszcze nie wiedziec, gdzie jest core

- Supportive

	- Publikacja

- Generic

	- Recenzje

	- Rekomendacje

	- Ksiegowosc

## Lekcja 02.03. Odkrywanie subdomen

### Istnieja dobre praktyki

- Budowanie

	- Uczestnictwo w wielu projektach

	- Poznawanie wielu domen

	- Rozmawianie z wieloma ekspertami domenowymi

### Heurystyki

- Struktura organizacji

	- Granice działów stanowia subdomeny

	- Np. zwroty, dostawa, magazyn

	- Nie ma działów

		- W malych firmach

		- W startupach

	- W tym wypadku nie zauwazymy wspolpracy dzialow

		- Np. zamowienia i magazyn wspolnie opracowuje prognoze zamowien

		- **A zatem core domain**

	- Dobra na start

- Rozni eksperci domenowi

	- Niezaleznie od departamentow

	- Ekspert domenowy od fakturowania moze rozwiazywac dwa problemy

		- Kliencie zagraniczni

		- Klienci krajowi

		- Rozne regulacje prawne

		- Dwa problemy powinny byc dwoma subdomenami

			- Bo pozniej rozwiazania beda sobie wchodzic w droge

- Jezyk ekspertow domenowych

	- Jakiego slownictwa uzywaja?

	- Ksiazka znaczy...

		- Paczka o masie X

			- dla Dostaw

		- Liczba dostepnych egzemlarzy

			- dla Magazynu

		- Tytul, autor, cena,...

			- dla Katalogu

		- Konkretny egzemplarz

			- dla Zwrotow

		- Cena, podatek, ...

			- dla Fakturowania

	- Inny cykl zycia

		- Zwrot ksiazki, ktorej nie ma juz w Katalogu

	- Separacja zagadnien

		- Zamowienie ksiazki, ktorej nie ma w Magazynie

	- Jak zauwazyc inne znaczenie slowa?

		- Szukac czasownikow, ktore ida w parze z rzeczownikiem

			- Opis zachowan tego rzeczownika

			- Zamek

				- Zalozyc (w drzwiach)

	- Stabilny koncept biznesowy jest nazywany inaczej

		- Ta sama osoba, inna nazwa

			- Adresat

				- Dostawa

			- Kupujacy

				- Zamowienia

			- Platnik

				- Platnosci

		- Czy Kupujacy i Adresat moga byc inna osoba?

			- Tak, ksiazka na prezent

		- Czy Kupujacy i Platnik moga byc inna osoba?

			- Tak, system placi np. ze srodkow ze zwrotu

	- Badajac jezyk, dochodzimy do zlozonych wymagan biznesowych

- Wartosc biznesowa

	- Jesli cos ma duza wartosc biznesowa, to jest osobna subdomena

		- Zawsze Core domain

		- Zamowienia

			- 95% obrotow od klientow korporacyjnych

				- Wiec oddzielamy to, jako subdomene od klientow indywidualnych

					- Nie szukamy abstakcji. Biznesowo to moga byc inne procesy.

						- A jesli beda takie same przez dlugi czas, to polaczyc

- Kroki procesu biznesowego

	- Kupowanie ksiazki

		- Katalog -> Zamowienie -> Platnosc -> Wysylka

	- Szukajac krokow, patrzymy, czy zmieniaja sie zasady gry

		- Np. po dodaniu do zamowienia, cena ksiazki sie zmienia

			- W ten sposob doszlismy do konceptu koszyka, ktory rzadzi sie swoimi prawami

				- A zatem zmienia zasady gry

- Subdomeny sie zmieniaja

	- Kroki procesu biznesowego sie zmieniaja

	- Zasady rynkowe

	- Regulacje

	- Raz odkryty model mentalny nie musi nadazac za modelem operacyjnym

		- Trzeba go walidowac

