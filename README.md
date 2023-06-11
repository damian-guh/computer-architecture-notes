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
