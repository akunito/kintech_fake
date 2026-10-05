# REKLAMACJA Z TYTUŁU BRAKU ZGODNOŚCI TOWARU Z UMOWĄ

**Warszawa, 2 października 2026 r.**

**Kupujący (konsument):**
[Kupujący]
[adres], Warszawa
e-mail: [e-mail] · tel. [tel.]
Konto Allegro: Client:48695146

**Sprzedawca (przedsiębiorca):**
Grzegorz Pawlik, prowadzący działalność gospodarczą pod nazwą Kintech
Mnichów 121a, 28-300 Jędrzejów
NIP: 656-233-10-99, REGON: 362036210
konto Allegro: **grzesiup255**

**Dotyczy:** zamówienie Allegro nr **6c1d38c0-…** z dnia **17 marca 2025 r.**, oferta nr 16733065275
**Przedmiot:** „Dysk SSD Samsung MZ-77E2T0 2TB 2,5" SATA III 870 EVO” — 4 sztuki
**Cena:** 4 × 675,00 zł = **2 700,00 zł** (zapłacono 17.03.2025 r., ID płatności 6c5316b5-…, Przelewy24 / Google Pay)
**Dostawa:** Allegro Paczkomaty InPost

---

## I. Przedmiot reklamacji

Na podstawie art. 43b–43e ustawy z dnia 30 maja 2014 r. o prawach konsumenta (dalej: „u.p.k.”) składam reklamację wszystkich czterech dysków SSD dostarczonych w ramach powyższego zamówienia.

Oferta — w brzmieniu z dnia zakupu, zachowanym w serwisie Allegro — opisywała towar następująco: **Stan: Nowy; Producent: Samsung; Kod producenta: MZ-77E2T0B/EU; EAN (GTIN): 8806090545900; Maksymalna prędkość zapisu: 530 MB/s; Maksymalna prędkość odczytu: 560 MB/s.** Przedmiotem umowy były zatem fabrycznie nowe, oryginalne dyski Samsung 870 EVO 2 TB, jednoznacznie określone kodem producenta i kodem EAN. Sprzedawca zadeklarował ponadto w warunkach oferty, stanowiących integralną część umowy: **„Rodzaj gwarancji: producenta. Okres gwarancji: 24 miesiące”** (Załącznik nr 3). Oferta nie zawierała żadnej informacji, że towar nie pochodzi od producenta Samsung.

**Dostarczone dyski nie są oryginalnymi dyskami Samsung 870 EVO o oznaczeniu MZ-77E2T0.** Są to urządzenia zbudowane na kontrolerze innego producenta, jedynie oznaczone nazwą i modelem Samsung. Dotyczy to wszystkich czterech egzemplarzy, w tym egzemplarza dostarczonego przez Sprzedawcę w ramach wymiany w kwietniu 2025 r.

Cena 675,00 zł za sztukę nie odbiegała od ówczesnych cen oryginalnego dysku Samsung 870 EVO 2 TB; nic nie wskazywało, że otrzymam towar nieoryginalny.

Numery seryjne zgłaszane przez reklamowane dyski:
- S5Y4R020A077805
- S5Y4R020A077806
- S5Y4R020A077808
- S5Y4R020A077877 (egzemplarz zamienny z kwietnia 2025 r.)

## II. Stan faktyczny

### 1. Wcześniejsza reklamacja i wymiana (kwiecień 2025 r.)

W dniu 14 kwietnia 2025 r. zgłosiłem w Dyskusji Allegro dotyczącej tego zamówienia wadę jednego z dysków (samoczynne rozłączanie się po kilku minutach pracy; numer seryjny podany w zgłoszeniu: S5Y4R010A077819). Sprzedawca uznał zgłoszenie („proszę go pilnie do nas odesłać – wymienimy go tak szybko, jak to tylko możliwe”) i wymienił ten egzemplarz; dysk zamienny otrzymałem 17 kwietnia 2025 r. (Załącznik nr 3).

Liczniki godzin pracy i cykli zasilania (ok. 150 godzin i 9–10 cykli mniej niż w pozostałych trzech dyskach) wskazują, że dyskiem zamiennym jest egzemplarz S5Y4R020A077877. On również nie jest oryginalnym dyskiem Samsung: jako jedyny zgłasza firmware `W0724A0` i pojemność 2 048 408 248 320 bajtów. **Sprzedawca podjął zatem już jedną próbę doprowadzenia towaru do zgodności z umową i dostarczył kolejny towar niezgodny z umową.**

### 2. Wyniki badania dysków

Pomiary wykonano programem `smartctl` 7.5 (smartmontools) w dniu 1 października 2026 r., z dyskami podłączonymi bezpośrednio do portów SATA (AHCI) płyty głównej. Dane pochodzą z odpowiedzi samych dysków na polecenia ATA IDENTIFY DEVICE i SMART READ DATA, a nie z etykiety ani opakowania. Pełna dokumentacja stanowi Załącznik nr 1, surowe wyniki — Załącznik nr 2, a zdjęcia etykiet — Załącznik nr 5.

1. **Etykiety.** Na etykietach wszystkich czterech dysków wydrukowano ten sam identyfikator WWN (`5002538F2000CAB`) i ten sam kod PSID (`YRR72JB0YU84…AJ1AWK`); różnią się jedynie numerem seryjnym (Załącznik nr 5). WWN i PSID są z natury niepowtarzalne dla każdego egzemplarza dysku. Dotyczy to także egzemplarza zamiennego z kwietnia 2025 r. — nosi on tę samą datę (2024.12), ten sam WWN i ten sam PSID co trzy pozostałe. Żaden z dysków nie zgłasza przy tym elektronicznie identyfikatora WWN wydrukowanego na jego etykiecie (pkt 5).

2. **Kontroler.** Każdy z czterech dysków sam zgłasza w sektorze danych SMART oznaczenie kontrolera `SMI2259XT` (Silicon Motion). Oryginalny Samsung 870 EVO ma, według karty katalogowej producenta, kontroler Samsung MKX.

3. **Oprogramowanie układowe (firmware).** Dyski zgłaszają wersje `W0814A0` (3 szt.) i `W0724A0` (1 szt.). Samsung publikuje dla 870 EVO wyłącznie wersje `SVT01B6Q`–`SVT04B6Q`. Wersje zgłaszane przez badane dyski występują w dyskach innych marek zbudowanych na kontrolerach Silicon Motion (por. bazy `drivedb.h` projektu smartmontools oraz linuxhw/SMART).

4. **Tablica atrybutów SMART.** Dyski zgłaszają 30 atrybutów, w tym atrybuty 160, 161, 163–169 i 245, zgodne z tablicą firmware Silicon Motion. Oryginalny 870 EVO zgłasza 14 albo 15 atrybutów o innym układzie; żaden z atrybutów 160–169 w nim nie występuje.

5. **Brak identyfikatora WWN.** W danych IDENTIFY DEVICE (słowa 84 i 87, bit 8 = 0; słowa 108–111 = 0) dyski deklarują brak World Wide Name; oryginalne dyski Samsung zgłaszają WWN z prefiksem producenta `5002538`.

6. **Deklarowane standardy i funkcje.** Dyski deklarują ACS-2 i SATA 3.2, nie zgłaszają deterministycznego TRIM ani funkcji szyfrowania; oryginalny 870 EVO deklaruje ACS-4, SATA 3.3, TRIM „deterministic, zeroed” oraz szyfrowanie AES 256-bit z TCG/Opal 2.0.

7. **Pojemność.** Egzemplarz S5Y4R020A077877 zgłasza 2 048 408 248 320 bajtów, podczas gdy oryginalny 870 EVO 2 TB ma 2 000 398 934 016 bajtów.

### 3. Stan nośnika

Trzy z czterech dysków mają już uszkodzone bloki pamięci (atrybut „realokowane sektory”: 6, 3 i 4). Według moich wcześniejszych odczytów ich liczba wzrosła między 27.04.2026 r. a 4.08.2026 r. w egzemplarzu 077805 z 3 do 6, a w egzemplarzu 077808 z 2 do 4; w pomiarze z 1.10.2026 r. wartości te nie uległy dalszej zmianie. Uszkodzenia wystąpiły po zapisaniu ok. 14 TB danych na dysk, tj. ok. 1% wytrzymałości 1 200 TB (TBW) deklarowanej przez producenta dla oryginalnego modelu.

Stan nośnika opisuję pomocniczo: podstawą reklamacji jest brak tożsamości towaru, a nie stopień jego zużycia.

### 4. Skutki dla mnie i mojej rodziny

Dyski kupiłem na potrzeby domowego serwera plików, na którym przechowywane są **dane całej mojej rodziny oraz kopie zapasowe naszych komputerów**. Wybrałem oryginalne dyski renomowanego producenta właśnie ze względu na bezpieczeństwo tych danych. Tymczasem od półtora roku dane te znajdują się na urządzeniach nieznanego pochodzenia, bez gwarancji producenta, z których trzy mają już uszkodzone sektory, a jeden egzemplarz uległ awarii już po kilku dniach użytkowania.

Ustalenie rzeczywistego stanu rzeczy, diagnostyka, pomiary oraz zabezpieczanie danych kosztowały mnie wiele godzin pracy.

Co więcej, od chwili zakupu ceny dysków SSD wzrosły ponad trzykrotnie: oryginalny Samsung 870 EVO 2 TB kosztuje dziś od ok. 2 165 zł za sztukę (Allegro i Ceneo.pl, stan na 1.10.2026 r.), wobec 675 zł w dniu zakupu (Załącznik nr 4). **Nawet zwrot całej zapłaconej ceny nie pozwoliłby mi dziś nabyć towaru, za który zapłaciłem w marcu 2025 r.** — odtworzenie zakupu czterech oryginalnych dysków kosztowałoby obecnie ok. 8 660 zł.

## III. Podstawa prawna

Zgodnie z art. 43b ust. 1 pkt 1 u.p.k. towar jest zgodny z umową, jeżeli zgodne z umową pozostają w szczególności jego opis, rodzaj, ilość, jakość, kompletność i funkcjonalność. Ponadto, stosownie do art. 43b ust. 2 pkt 1 i 2 u.p.k., towar musi nadawać się do celów, do których zazwyczaj używa się towaru tego rodzaju, oraz mieć takie cechy, w tym trwałość, jakie są typowe dla towaru tego rodzaju i których konsument może rozsądnie oczekiwać, biorąc pod uwagę publiczne zapewnienie złożone przez przedsiębiorcę. Dostarczenie urządzeń, które nie są oryginalnymi dyskami Samsung 870 EVO (MZ-77E2T0), a jedynie zostały tak oznaczone, stanowi brak zgodności towaru z umową co do jego opisu, rodzaju i jakości.

**Zachowanie terminu.** Zgodnie z art. 43c ust. 1 zdanie pierwsze u.p.k. przedsiębiorca ponosi odpowiedzialność za brak zgodności towaru z umową istniejący w chwili jego dostarczenia i ujawniony w ciągu dwóch lat od tej chwili, a zgodnie z art. 43c ust. 1 zdanie drugie domniemywa się, że brak zgodności, który ujawnił się przed upływem dwóch lat od chwili dostarczenia towaru, istniał w chwili jego dostarczenia. Towar dostarczono w marcu 2025 r. (egzemplarz zamienny — 17 kwietnia 2025 r.), a brak zgodności ujawnił się w 2026 r. (stwierdziłem go w sierpniu 2026 r., analizując dane identyfikacyjne dysków). Niezależnie od domniemania brak zgodności dotyczy tożsamości towaru, a więc cechy, która nie mogła powstać po jego wydaniu.

**Istotność.** Brak zgodności jest istotny (domniemanie z art. 43e ust. 4 zdanie drugie u.p.k.), ponieważ:
- dotyczy tożsamości i pochodzenia towaru, czyli cechy przesądzającej o decyzji zakupu, i podważa zaufanie do Sprzedawcy;
- pozbawia mnie gwarancji producenta, którą Sprzedawca zadeklarował w ofercie, a której Samsung udziela wyłącznie na swoje oryginalne wyroby;
- pozbawia mnie wsparcia producenta, w tym aktualizacji oprogramowania układowego przeznaczonych dla oryginalnych dysków;
- naraża na utratę dane całej mojej rodziny przechowywane na tych dyskach.

**Uprawnienie do obniżenia ceny.** W razie odmowy wymiany albo niedokonania jej w rozsądnym czasie uprawnienie do obniżenia ceny będzie mi przysługiwać na podstawie art. 43e ust. 1 pkt 1 albo pkt 2 u.p.k. Niezależnie od tego wskazuję, że: (a) w odniesieniu do egzemplarza wymienionego w kwietniu 2025 r. brak zgodności występuje nadal, mimo że przedsiębiorca próbował doprowadzić towar do zgodności z umową (art. 43e ust. 1 pkt 3 u.p.k.); (b) brak zgodności dotyczy tożsamości i pochodzenia wszystkich czterech dysków i jest na tyle istotny, że uzasadnia obniżenie ceny bez uprzedniego skorzystania ze środków ochrony określonych w art. 43d (art. 43e ust. 1 pkt 4 u.p.k.). Żądając w pierwszej kolejności wymiany, nie rezygnuję z powołania się na te podstawy.

## IV. Żądanie

**1. Wymiana.** Na podstawie art. 43d ust. 1 u.p.k. żądam wymiany wszystkich czterech dysków na fabrycznie nowe, oryginalne dyski Samsung SSD 870 EVO 2 TB (MZ-77E2T0B), w nienaruszonym opakowaniu producenta, pochodzące z autoryzowanej dystrybucji. Proszę o dołączenie dokumentu potwierdzającego ich pochodzenie; przed wydaniem dotychczasowych dysków zweryfikuję numery seryjne u producenta.

Oczekuję potwierdzenia wymiany w terminie 14 dni od otrzymania niniejszego pisma i jej dokonania w terminie kolejnych 14 dni. Koszty wymiany ponosi przedsiębiorca (art. 43d ust. 4 zdanie drugie u.p.k.), który odbiera wymieniany towar na swój koszt (art. 43d ust. 5 u.p.k.); nie jestem zobowiązany do zapłaty za zwykłe korzystanie z towaru (art. 43d ust. 7 u.p.k.). Ponieważ dyski przechowują dane mojej rodziny, proszę — stosownie do art. 43d ust. 4 u.p.k. — o dostarczenie dysków zamiennych w pierwszej kolejności; dotychczasowe udostępnię do odbioru w terminie 30 dni od ich otrzymania.

**2. Obniżenie ceny i odszkodowanie — na wypadek odmowy wymiany.** Jeżeli odmówią Państwo wymiany, w szczególności na podstawie art. 43d ust. 2 u.p.k., albo nie potwierdzą jej lub nie dokonają we wskazanych wyżej terminach, zastrzegam sobie wybór między dalszym dochodzeniem wymiany a złożeniem odrębnego oświadczenia o obniżeniu ceny na podstawie art. 43e ust. 1 pkt 1, 2 lub 5 u.p.k. (a niezależnie od tego pkt 3 i 4) wraz z wezwaniem do zapłaty odszkodowania. Już teraz wskazuję wysokość tych roszczeń:

a) obniżenie ceny o **2 160,00 zł**, tj. do kwoty 540,00 zł, ze zwrotem tej kwoty w terminie 14 dni od otrzymania oświadczenia (art. 43e ust. 3 u.p.k.). Z pomiarów stanowiących Załączniki nr 1 i 2 wynika, że dostarczone dyski nie są wyrobami producenta Samsung, choć noszą jego oznaczenia: nie są objęte gwarancją producenta, nie mogę ich odsprzedać jako dysków Samsung, zbudowane są na kontrolerze Silicon Motion zamiast kontrolera Samsung, a trzy z czterech egzemplarzy mają już uszkodzone bloki pamięci. Ich wartość oceniam na nie więcej niż 20% wartości towaru zgodnego z umową (art. 43e ust. 2 u.p.k.);

b) odszkodowanie na podstawie art. 471 k.c. w związku z art. 361 i art. 363 § 2 k.c. w kwocie **4 767,33 zł**. Nabycie czterech oryginalnych dysków Samsung 870 EVO 2 TB kosztuje dziś co najmniej 8 659,16 zł (4 × 2 164,79 zł — najniższa cena nowego egzemplarza w serwisie Allegro i w porównywarce Ceneo.pl w dniu 1.10.2026 r., Załącznik nr 4). Szkodę stanowi różnica między tą kwotą a wartością dysków, które zatrzymuję (20%, tj. 1 731,83 zł), pomniejszona o kwotę obniżenia ceny (2 160,00 zł): 8 659,16 zł − 1 731,83 zł − 2 160,00 zł = 4 767,33 zł. Szkoda ta jest normalnym następstwem dostarczenia towaru nieoryginalnego zamiast oryginalnego, a jej wysokość ustala się według cen z daty ustalenia odszkodowania; zastrzegam jej aktualizację według cen z tej daty.

**Łącznie: 6 927,33 zł.** Numer rachunku bankowego do zapłaty wskażę w oświadczeniu o obniżeniu ceny.

**3. Brak zgody na odstąpienie.** Oświadczam, że **nie odstępuję od umowy** i nie wyrażam zgody na załatwienie reklamacji przez zwrot towaru za zwrotem ceny. Wybór pomiędzy obniżeniem ceny a odstąpieniem od umowy należy do konsumenta (art. 43e ust. 1 u.p.k.). Zamknięcie Dyskusji Allegro w kwietniu 2025 r. nie stanowi zrzeczenia się uprawnień (art. 7 u.p.k.).

## V. Termin odpowiedzi i dalsze kroki

Zgodnie z art. 7a ust. 1 u.p.k. oczekuję odpowiedzi na niniejszą reklamację **w terminie 14 dni** od dnia jej otrzymania, na papierze lub innym trwałym nośniku (art. 7a ust. 3 u.p.k.). Brak odpowiedzi w tym terminie oznacza, zgodnie z art. 7a ust. 2 u.p.k., **uznanie reklamacji**.

Niniejsze pismo stanowi próbę pozasądowego rozwiązania sporu (art. 187 § 1 pkt 3 k.p.c.). W razie nieuwzględnienia reklamacji skorzystam z Allegro Ochrony Kupujących i pomocy Miejskiego Rzecznika Konsumentów w Warszawie, a następnie **skieruję sprawę na drogę postępowania sądowego, korzystając z pomocy profesjonalnego pełnomocnika**. Będę wówczas dochodzić należnych kwot wraz z odsetkami ustawowymi za opóźnienie i kosztami procesu, w tym kosztami opinii biegłego i zastępstwa procesowego (art. 98 k.p.c.; por. art. 458¹⁶ k.p.c.).

---

**Załączniki:**
1. Załącznik techniczny — wyniki badania dysków
2. Surowe wyniki `smartctl -x`, ATA IDENTIFY DEVICE oraz SMART READ DATA dla czterech dysków (pomiar z 1.10.2026 r.)
3. Oferta z dnia zakupu, warunki reklamacji i gwarancji Sprzedawcy oraz zapis Dyskusji Allegro z 14–17 kwietnia 2025 r.
4. Aktualne ceny oryginalnego dysku Samsung 870 EVO 2 TB (zrzuty ekranu z 1.10.2026 r.)
5. Zdjęcia etykiet dysków (2.10.2026 r.)

Z poważaniem,

[Kupujący]
