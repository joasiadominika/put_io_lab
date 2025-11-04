# System aukcyjny

## Wprowadzenie

Specyfikacja wymagań funkcjonalnych w ramach informatyzacji procesu sprzedaży produktów w oparciu o mechanizm aukcyjny. 

## Procesy biznesowe

---
<a id="bc1"></a>
### BC1: Sprzedaż aukcyjna 

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Opis:** Proces biznesowy opisujący sprzedaż za pomocą mechanizmu aukcyjnego. |

**Scenariusz główny:**
1. [Sprzedający](#ac1) wystawia produkt na aukcję. ([UC1](#uc1))
2. [Kupujący](#ac2) oferuje kwotę za produkt wyższą od aktualnie najwyższej oferty. ([BR1](#br1)) ([UC2](#uc2))
3. [Kupujący](#ac2) wygrywa aukcję ([BR2](#br2))
4. [Kupujący](#ac2) przekazuje należność Sprzedającemu. ([UC4](#uc4))
5. [Sprzedający](#ac1) przekazuje produkt Kupującemu.

**Scenariusze alternatywne:** 

2.A. Oferta Kupującego została przebita, a [Kupujący](#ac2) pragnie przebić aktualnie najwyższą ofertę.
* 2.A.1. Przejdź do kroku 2.

3.A. Czas aukcji upłynął i [Kupujący](#ac2) przegrał aukcję. ([BR2](#br2))
* 3.A.1. Koniec przypadku użycia.

---

## Aktorzy

<a id="ac1"></a>
### AC1: Sprzedający

Osoba oferująca towar na aukcji.

<a id="ac2"></a>
### AC2: Kupujący

Osoba chcąca zakupić produkt na aukcji.


## Przypadki użycia poziomu użytkownika

### Aktorzy i ich cele

[Sprzedający](#ac1):
* [UC1](#uc1): Wystawienie produktu na aukcję
* [UC5](#uc5): Zakończenie aukcji przed czasem (jeśli brak ofert)

[Kupujący](#ac2)
* [UC2](#uc2): Złożenie oferty (licytacja)
* [UC3](#uc3): Przeglądanie wyników aukcji
* [UC4](#uc4): Opłacenie wygranego produktu

---
<a id="uc1"></a>
### UC1: Wystawienie produktu na aukcję

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu chęć wystawienia produktu na aukcję.
2. System prosi o podanie danych produktu i ceny wywoławczej.
3. [Sprzedający](#ac1) podaje dane produktu oraz cenę wywoławczą.
4. System weryfikuje poprawność danych.
5. System informuje o pomyślnym wystawieniu produktu na aukcję.

**Scenariusze alternatywne:** 

4.A. Podano niepoprawne lub niekompletne dane produktu.
* 4.A.1. System informuje o błędnie podanych danych.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc2"></a>
### UC2: Złożenie oferty (licytacja)

**Aktorzy:** [Kupujący](#ac2)

**Scenariusz główny:**
1. [Kupujący](#ac2) inicjuje złożenie oferty w wybranej aukcji.  
2. System udostępnia informacje o aktualnej najwyższej ofercie oraz czasie do zakończenia aukcji.  
3. [Kupujący](#ac2) podaje proponowaną kwotę.  
4. System weryfikuje, czy kwota jest wyższa od aktualnej najwyższej oferty o co najmniej 1,00 PLN. ([BR1](#br1))  
5. System zapisuje nową ofertę i aktualizuje dane aukcji.  
6. System informuje [Kupującego](#ac2) o pomyślnym złożeniu oferty.  

**Scenariusze alternatywne:**  
4.A. Podano kwotę niezgodną z regułą minimalnego przebicia.  
* 4.A.1. System informuje o błędnej ofercie.  
* 4.A.2. Przejdź do kroku 3.

---

<a id="uc3"></a>
### UC3: Przeglądanie wyników aukcji

**Aktorzy:** [Kupujący](#ac2)

**Scenariusz główny:**
1. [Kupujący](#ac2) inicjuje przeglądanie wyników zakończonych aukcji.  
2. System udostępnia listę aukcji, w których [Kupujący](#ac2) brał udział.  
3. [Kupujący](#ac2) wskazuje aukcję, której wynik chce poznać.  
4. System prezentuje wynik aukcji, w tym informację o zwycięzcy i kwocie końcowej.  
5. System umożliwia przejście do procesu płatności, jeśli [Kupujący](#ac2) wygrał aukcję.  

**Scenariusze alternatywne:**  
2.A. [Kupujący](#ac2) nie uczestniczył w żadnej zakończonej aukcji.  
* 2.A.1. System informuje, że brak zakończonych aukcji z udziałem użytkownika.

---

<a id="uc4"></a>
### UC4: Opłacenie wygranego produktu

**Aktorzy:** [Kupujący](#ac2) (główny), [Sprzedający](#ac1) (drugorzędny)

**Scenariusz główny:**
1. [Kupujący](#ac2) inicjuje opłacenie produktu wygranego w zakończonej aukcji.  
2. System udostępnia dane aukcji oraz kwotę należności.  
3. [Kupujący](#ac2) potwierdza chęć dokonania płatności.  
4. System przekazuje dane do zewnętrznego systemu płatności.  
5. Po potwierdzeniu płatności system rejestruje nową [Płatność](#bo4).  
6. System aktualizuje status [Aukcji](#bo1) na „opłacona”.  
7. System informuje [Kupującego](#ac2) oraz [Sprzedającego](#ac1) o pomyślnym opłaceniu produktu.  

**Scenariusze alternatywne:**  
4.A. Płatność nie została zrealizowana.  
* 4.A.1. System informuje o nieudanej płatności.  
* 4.A.2. Przejdź do kroku 3.  

---

<a id="uc5"></a>
### UC5: Zakończenie aukcji przed czasem

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) inicjuje zakończenie jednej z aktywnych aukcji.  
2. System udostępnia informacje o stanie aukcji, w tym o ewentualnych ofertach.  
3. [Sprzedający](#ac1) potwierdza chęć zakończenia aukcji przed czasem.  
4. System sprawdza, czy aukcja nie posiada jeszcze żadnych ofert.  
5. System oznacza aukcję jako zakończoną przed czasem.  
6. System informuje [Sprzedającego](#ac1) o pomyślnym zakończeniu aukcji.  

**Scenariusze alternatywne:**  
4.A. Aukcja posiada już złożone oferty.  
* 4.A.1. System informuje, że zakończenie aukcji jest niemożliwe, ponieważ rozpoczęła się licytacja.  
* 4.A.2. Przejdź do kroku 1.  


## Obiekty biznesowe (inaczej obiekty dziedzinowe lub informatyczne)

### BO1: Aukcja

Aukcja jest formą zawierania transakcji kupna-sprzedaży, w której Sprzedający określa cenę wywoławczą produktu, natomiast Kupujący mogą oferować własną ofertę zakupu każdorazowo proponując kwotę wyższą od aktualnie oferowanej kwoty. Aukcja kończy się po upływie określonego czasu. Jeśli złożona została co najmniej jedna oferta zakupy produkt nabywa ten Kupujący, który zaproponował najwyższą kwotę. 

### BO2: Produkt

Fizyczny lub cyfrowy obiekt, który ma zostać sprzedany w ramach aukcji.

### BO3: Oferta

Propozycja ceny złożona przez Kupującego w konkretnej aukcji. Każda kolejna oferta musi przebijać aktualnie najwyższą o co najmniej 1,00 PLN.

### BO4: Płatność

Rekord potwierdzający uregulowanie należności przez zwycięzcę aukcji (identyfikator transakcji, kwota, czas, status).

## Reguły biznesowe

<a id="br1"></a>
### BR1: Złożenie oferty

Złożenie oferty wymaga zaproponowania kwoty wyższej niż aktualnie oferowana o minimum 1,00 PLN.


<a id="br2"></a>
### BR2: Rozstrzygnięcie aukcji

Aukcję wygrywa ten z [Kupujący](#ac2)ch, który w momencie jej zakończenia (upłynięcia czasu) złożył najwyższą ofertę.

## Macierz CRUDL


| Przypadek użycia                                  | Aukcja | Produkt | Oferta | Płatność |
| ------------------------------------------------- | ------ | ------- | ------ | -------- |
| UC1: Wystawienia produktu na aukcję               |   C    |    C    |        |          |
| UC2: Złożenie oferty (licytacja)                  |  R,U   |    R    |    C   |          |
| UC3: Przeglądanie wyników aukcji                  |  R,L   |    R    |    R   |          |
| UC4: Opłacenie wygranego produktu                 |   U    |         |        |     C    |
| UC5: Zakończenie aukcji przed czasem              |   U    |         |        |          |
