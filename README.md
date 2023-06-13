# ASK
## Sposób zarządzania złożonością systemów cyfrowych
- Abstrakcja - ukazywanie szczegółów kiedy nie są istotne
- Dyscyplina - celowe ograniczenie	wyboru projektowania
np. cyfrowa dyscyplina, dyskretne napięcie zamiast stałych.
- Trzy wyrazy ść
	1. Niehierarchiczność - system podzielony na moduły i ...
	2. Modułowość - dobrze zdefiniowane funkcjonalności i interfejsy
	3. Regularność ...?

## Multiplekser
Układ kombinacyjny służący do wyboru jednego z kilku dostępnych sygnałów wejściowych i przekazanie go na wyjście
Mux ma:
- k wejść informacyjnych, jest ich 2^n (x0, x1)
- n wejść adresowych (a0, a1)
- Y wyjście

```
         ______
a0 ---- |      |
a1 ---- |      |
x0 ---- | AND  |-- Y
x1 ---- |      |
         ------
```
## Dekoder
Należy do klasy układów kombinacyjnych, układ posiadający n wejść oraz k = 2^n wyjść. Jego działanie polega na zamianie NKB o długości n na kod "1 z k". W zależności od ilości wyjść nazywa się go dekoderem 1 z N

```
      _______
D0 --|       |
D1 --|       |--- Y0 00
     |       |
     |       |--- Y1 01
     |       |
     |       |
     |       |
     |       |--- Y2 10
     |       |
     |       |--- Y3 11
     |_______|

```
## Opóźnienia propagacji i konkatenacji
Opóźnienia propagacji - czas pomiędzy zmianą stanu wejść, a chwilą ustalenia stanu wyjścia.
Przyczyny:
- prędkość światła
- obwody zwalniają gdy są gorące i przyśpieszają gdy są zimne
- wiele wejść i wyjść jest starszych, z których niektóre są szybsze niż inne
Suma propagacji to suma opóźnień każdej bramki na ścieżce krytycznej

Opóźnienie konkatenacji - czas minimalny od momentu wejścia do momentu zmiany sygnału w obwodzie, przyczyny są takie same.

Rozwiązaniem jest budowanie najbardziej jak to możliwe prostych obwodów.

## Glitch
Oznacza że pojedyncza zmiana wejścia może spowodować wiele zmian wyjścia. W obwodach, gdzie na bramce na jeden sygnał musi czekać na drugi..? Występuje w obwodach kombinacyjnych.
Rozwiązaniem jest rysowanie więcej obszarów w k mapach.

## Zatrzask D i przerzutnik D

Główna różnica między zatrzaskiem D a przerzutnikiem D polega na sposobie działania i synchronizacji. Zatrzask D jest asynchroniczny i reaguje na zmiany wejścia bezpośrednio (przesyła na wyjście gdy CLK = 1	a gdy CLK = 0 pozostaje ten sam stan), podczas gdy przerzutnik D jest synchroniczny i reaguje na zmiany wejścia tylko w określonym momencie, synchronizowanym przez zegar (gdy jego wartośc wzrasta z 0 do 1, dla pozostałych sytuacji przechowuje poprzednią wartość Q). Przerzutnik D jest bardziej powszechnie stosowany w układach cyfrowych, ponieważ jego synchroniczność pomaga w unikaniu błędów i zagwarantowaniu prawidłowego działania.

## Zatrzask SR

| S | R | Q | Q' |
|:-:|:-:|:-:|:-:|
| 0 | 0 | Qprev | Q'prev |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | -| - |

## Pół sumator i pełny sumator
Półsumator - ma dwa wejścia i wyjścia. Zmiennymi wyjściowymi są bity składników dodawania, które są sumowane, a zmienne wyjściowe tworzą bity sumy i przeniesienia.
| A | B | Cout | S |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 0 |

Pełny sumator - realizuje sumę trzech bitów (dwa bity znaczące i bit przeniesienia z poprzedniej pozycji).
Sumator posiada dwa wejścia A i B oraz Cin, który jest bitem przeniesienia z poprzedniej pozycji. Na wyjściu S otrzymujemy sumę, a Cout to przeniesienie do następnej pozycji
| Cin | A | B | Cout | S |
|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 |
| 0 | 1 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 | 1 |
| 1 | 0 | 1 | 1 | 0 |
| 1 | 1 | 0 | 1 | 0 |
| 1 | 1 | 1 | 1 | 1 |

## Rodzaje sumatorów
- Szeregowy - podczas każdej operacji dodają one dwa bity składników oraz bit przeniesienia
	Zalety: sumowanie liczb n-bitowych, gromadzenie wyników
	 Wady: wolne
- Równoległy - dodaje do siebie jednocześnie wszystkie bity ze wszystkich pozycji, a przeniesienie jest realizowane od w zależności od połączenia sumatorów jednobitowych
	Zalety: prosty, łatwa budowa
	Wady: sumowanie liczb k *4 bitowych
- Prefiksowy
Zalety: szybki, najkrótszy czas

## ALU
Alu - jednostka arytmetyczno-logiczna, która jest kluczowym elementem procesora
Realizuje:
- dodawanie i odejmowanie
- mnożenie i dzielenie
- operacje logiczne
- przesunięcia bitowe
- porównywanie i testowanie warunków

Elementy jednostki to:
- rejestry wejściowe i wynikowe
-  wybór operacji
- blok logiczny i arytmetyczny
- sygnały kontrolne

## Rejestry MIPS
 Nazwa | Numer rejestru | Opis 
 ------|-------------|------------------------------------------------ 
 `$0` | 0 | Zawsze równy zero 
 `$at` | 1 | Assembler tymczasowy 
 `$v0-$v1` | 2-3 | Zwraca wartość funkcji
 `$a0-$a3` | 4-7 | Argumenty funkcji
 `$t0-$t7` | 8-15 | Tymczasowe
 `$s0-$s7` | 16-23 | Zapisane zmienne 
 `$t8-$t9` | 24-25 | Tymczasowe
 `$k0-$k1` | 26-27 | Zarezerwowane dla OS
 `$gp` | 28 | Wskaźnik globalny 
 `$sp` | 29 | Wskaźnik stosu
  `$fp` | 30 | Wskaźnik ramki stosu 
  `$ra` | 31 | Adres powrotu funkcji

## Organizacja pamięci w MIPS
- Text - przechowuje program w języku maszynowym
- Global Data - segment danych globalnych przechowujący zmienne globalne, zmienne mogą być widoczne dla wszystkich procedur w programie
- Dynamic Data - segment danych dynamicznych zawiera stos i sterte. Dane są dynamiczne przydzielane podczas wykonywania programu.
- Reserved - zarezerwowane segmenty są używane przez OS i nie moga być używane podczas wykonywania programu

| Mapa pamięci|
| ----- |
| Reserved |
| Dynamic Data|
| Global Data| 
| Text |
| Reserved |

## R-Type (Rejestrowe)
- rs, rt (5 bit) rejestry źródłowe
- rd (5 bit) rejestr docelowy
- op (6 bit) op code (R-type = 0)
- funct (6 bit) - funkcje z opcode
- shamt (5 bit) - liczba przesunięcia dla instrukcji z przesunięciem

Przykład: add, sub

## I-Type (Bezpośredni)
- rs, rt (5 bit) rejestry operandów
- imm (6 bit) bezpośrednie 16 bitowe w kodzie u2
- op
Przykład: addi, lw

## Pseudoinstrukcje
Są to instrukcje, które nie mają bezpośredniej implementacji sprzętowej. Pełnią rolę udogodnienia. Assembler tłumaczy je na rzeczywiste instrukcje mips
np. clear, more

## Wyjątki
Są to nieplanowane wywołania procedury, który przeskakuje pod nowy adres. Wyjątki są spowodowane przez sprzęt lub oprogramowanie
- Przerwanie systemowe
- Wywołanie systemowe
- Dzielenie przez 0
-  Niezidentyfikowana instrukcja
- Arytmetyczne przepełnienie

## Rodzaje architektur
- Risc - duży zestaw rejestrów, rzadkie odwołanie do pamieci i szybka jednostka wykonawcza
	- Zalety:  duża szybkość ułatwionego rozkodowania rozkazów, ułatwienie zwiększenia częstotliwości zegara
	- Wady: duża liczba rozków w kodzie, konieczne szybkie przesyłanie rozkazów z pamięci

- Cisc - Czeste odwołanie do pamięci, mały zestaw rejestrów, złożone rozkazy
	- Zalety: zmniejszona liczba rozkazów w skomplikowanym kodzie
	- Wady: złożone dekodowanie rozkazów, utrudnione przetwarzanie potokowe

## Hazard
Krótkotrwałe zakłócenia stany logicznego na wyjściu układu. Powstanie hazardu spowodowane jest opóźnieniami na poszczególnych bramkach w układach logicznych
Typy:
- statyczny - zmiana w chwili gdy wejście powino zostać w stanie niezmienionym
- dynamiczny - kilkukrotna zmiana stanu wyjścia przez zmianę stanu wejścia
Likwidacji tego najlepiej dokonać przez wprowadzenie dodatkowych implikantów
