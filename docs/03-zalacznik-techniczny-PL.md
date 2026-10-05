# Załącznik nr 1 — wyniki badania dysków

**Dotyczy:** zamówienie Allegro nr 6c1d38c0-… z 17.03.2025 r. — 4 × „Dysk SSD Samsung MZ-77E2T0 2TB 2,5" SATA III 870 EVO”
**Numery seryjne zgłaszane przez dyski:** S5Y4R020A077805, S5Y4R020A077806, S5Y4R020A077808, S5Y4R020A077877
**Data pomiaru:** 1 października 2026 r. (zdjęcia etykiet: 2 października 2026 r.)
**Metoda:** program `smartctl` 7.5 (smartmontools), polecenia `smartctl -x`, `smartctl --identify=wb` oraz `smartctl -r ataioctl,2 -A`; dyski podłączone bezpośrednio do portów SATA (AHCI) płyty głównej.

Wszystkie wartości pochodzą z odpowiedzi samych dysków (polecenia ATA IDENTIFY DEVICE i SMART READ DATA), a nie z etykiety ani opakowania. Surowe, niezmodyfikowane wyniki stanowią Załącznik nr 2.

Wcześniejsze odczyty kupującego (27.04.2026 r. i 4.08.2026 r., kontroler LSI SAS3008) nie są objęte Załącznikiem nr 2; kupujący przedstawi je na żądanie.

---

## 1. Dane identyfikacyjne zgłaszane przez dyski

| Numer seryjny | Firmware | Pojemność (bajty) | Wersja ATA | SATA | WWN |
|---|---|---|---|---|---|
| S5Y4R020A077805 | **W0814A0** | 2 000 398 934 016 | ACS-2 | 3.2 | **brak** |
| S5Y4R020A077806 | **W0814A0** | 2 000 398 934 016 | ACS-2 | 3.2 | **brak** |
| S5Y4R020A077808 | **W0814A0** | 2 000 398 934 016 | ACS-2 | 3.2 | **brak** |
| S5Y4R020A077877 | **W0724A0** | **2 048 408 248 320** | ACS-2 | 3.2 | **brak** |

Wszystkie cztery zgłaszają nazwę modelu `Samsung SSD 870 EVO 2TB`.

## 2. Porównanie z oryginalnym dyskiem Samsung 870 EVO

| Cecha | Badane dyski | Oryginalny Samsung 870 EVO |
|---|---|---|
| Etykieta (Załącznik nr 5) | ten sam WWN `5002538F2000CAB` i ten sam PSID na wszystkich czterech dyskach | WWN i PSID niepowtarzalne dla każdego egzemplarza |
| Kontroler | dysk sam zgłasza w sektorze danych SMART oznaczenie `SMI2259XT` (Silicon Motion) | Samsung MKX (karta katalogowa producenta) |
| Firmware | `W0814A0`, `W0724A0` | `SVT01B6Q`–`SVT04B6Q` |
| Liczba atrybutów SMART | **30** (w tym 160, 161, 163–169, 245) | **14** (firmware SVT01B6Q) albo **15** (nowsze wersje): 5, 9, 12, 177, 179, 181, 182, 183, 187, 190, 195, 199, 235, 241, 252 |
| World Wide Name | brak (IDENTIFY słowa 84 i 87, bit 8 = 0; słowa 108–111 = 0) | obecny, prefiks producenta `5002538` |
| Wersja ATA / SATA | ACS-2 / SATA 3.2 | ACS-4 / SATA 3.3 |
| TRIM | dostępny, bez DRAT i RZAT (słowo 69 = 0x0d00) | „Available, deterministic, zeroed” |
| Szyfrowanie / TCG Opal | brak (słowo 48 bit 0 = 0; słowo 69 bit 4 = 0) | AES 256-bit, TCG/Opal V2.0 (karta katalogowa) |
| Pojemność 2 TB | jeden egzemplarz: 4 000 797 360 sektorów (2 048 408 248 320 B) | 3 907 029 168 sektorów (2 000 398 934 016 B) |

**2.1. Kontroler.** W sektorze danych SMART (polecenie SMART READ DATA, bajty 386–439) każdy z czterech dysków zapisuje jawnym tekstem wersję firmware i oznaczenie kontrolera: `W0814A0 00`, `SMI2259XT`, `N3800` (egzemplarz …877: `W0724A0 00`, `SMI2259XT`, `N2800`). Oryginalny 870 EVO ma kontroler Samsung MKX (karta katalogowa producenta).

**2.2. Firmware.** Oznaczenia `W0814A0` i `W0724A0` nie występują wśród wersji publikowanych przez Samsung dla 870 EVO (`SVT01B6Q`–`SVT04B6Q`). Identyczne wersje `W0814A0` i `W0724A0` zgłaszają dyski innych marek zbudowane na kontrolerach Silicon Motion (m.in. Intenso, Team Group, Verbatim, AGI, PNY — publiczna baza linuxhw/SMART); baza `drivedb.h` projektu smartmontools wymienia wersje tego formatu (`W0413A0`, `W0714A0`, `W0825A0`) w grupie „Silicon Motion based OEM SSDs”.

**2.3. Tablica atrybutów SMART.** Każdy z czterech dysków zgłasza ten sam zestaw 30 atrybutów: 1, 5, 9, 12, 160, 161, 163, 164, 165, 166, 167, 168, 169, 175, 176, 177, 178, 181, 182, 192, 194, 195, 196, 197, 198, 199, 232, 241, 242, 245. Zestaw ten jest zgodny z tablicą atrybutów firmware Silicon Motion opisaną w `drivedb.h` (160, 161, 163–169, 178, 241, 242, 245) i identyczny z tablicą dysków innych marek z firmware `W0814A0`. Oryginalny 870 EVO zgłasza 14 albo 15 atrybutów; żaden z atrybutów 160–169 w nim nie występuje.

**2.4. Brak WWN.** W danych IDENTIFY DEVICE słowa 84 i 87 mają bit 8 („64-bit World Wide Name supported”) równy 0, a słowa 108–111 (WWN) mają wartość 0. Program `smartctl` nie wyświetla wiersza `LU WWN Device Id`, a system operacyjny nie tworzy identyfikatora `wwn-…` dla żadnego z czterech dysków (pomiar na portach AHCI). Producent wymienia obsługę World Wide Name wśród cech 870 EVO.

**2.5. Standardy i funkcje.** Dyski deklarują `ATA Version: ACS-2 T13/2015-D revision 3` i `SATA 3.2`. Słowo 69 IDENTIFY ma wartość 0x0d00: bit 14 (DRAT) = 0, bit 5 (RZAT) = 0, bit 4 (szyfrowanie danych) = 0. Słowo 48, bit 0 = 0 (brak funkcji Trusted Computing wymaganych przez TCG Opal). Karta katalogowa Samsung podaje dla 870 EVO: „AES 256-bit Full Disk Encryption, TCG/Opal V2.0, Encrypted Drive (IEEE1667)”.

**2.6. Pojemność.** Egzemplarz S5Y4R020A077877 — najprawdopodobniej egzemplarz zamienny z kwietnia 2025 r. (pkt 4) — zgłasza 4 000 797 360 sektorów (2 048 408 248 320 B), tj. wartość normy IDEMA dla 2048 GB; oryginał: 3 907 029 168 sektorów (IDEMA, 2000 GB).

**2.7. Numery seryjne.** Numery seryjne oryginalnych dysków 870 EVO w publicznych bazach pomiarów mają inną budowę (np. `S6PNNJ0W303102W`, `S620NJ0R902825F`: litera zakładu na piątej pozycji, litera kontrolna na końcu). Numery zgłaszane przez badane dyski (`S5Y4R020A0778xx`) tej budowy nie mają. Okoliczność tę podaję pomocniczo.

**2.8. Etykiety (zdjęcia z 2.10.2026 r., Załącznik nr 5).** Etykiety wszystkich czterech dysków zawierają: `PN MZ7L32T0HBLT`, `MODEL MZ-77E2T0 2024.12`, `WWN 5002538F2000CAB`, `PSID YRR72JB0YU84ENPZP05K1AVSR2AJ1AWK`, `PRODUCT OF KOREA`. Różni je wyłącznie numer seryjny (…077805, …077806, …077808, …077877). Identyfikator WWN (World Wide Name) i kod PSID (Physical Security ID) są z definicji niepowtarzalne dla każdego egzemplarza; ich powtórzenie na czterech dyskach, w tym na egzemplarzu dostarczonym miesiąc później w ramach wymiany, oznacza, że etykiety nie pochodzą z procesu produkcyjnego producenta. Ponadto żaden z dysków nie zgłasza elektronicznie WWN wydrukowanego na etykiecie (pkt 2.4), a dyski nie obsługują funkcji TCG Opal, której dotyczy kod PSID (pkt 2.5).

> **Uwaga:** wiersz `Model Family: Samsung based SSDs` w wynikach `smartctl` nie potwierdza autentyczności. Program wyprowadza go z dopasowania wzorca do nazwy modelu zgłaszanej przez sam dysk.

## 3. Stan nośnika (pomiar z 1.10.2026 r.)

| Numer seryjny | Realokowane (05) | Oczekujące (197) | Niekorygowalne (198) | Rezerwa bloków (161/232, wartość surowa) | Godziny pracy (09) | Zapisano (241) | Błędy CRC (199) |
|---|---|---|---|---|---|---|---|
| S5Y4R020A077805 | **6** | **6** | **1** | **60** | 9 969 | ok. 13,8 TB | 0 |
| S5Y4R020A077806 | **3** | **3** | 0 | **80** | 9 984 | ok. 14,2 TB | 0 |
| S5Y4R020A077808 | **4** | **4** | **1** | **73** | 10 006 | ok. 13,8 TB | 0 |
| S5Y4R020A077877 | 0 | 0 | 0 | 100 | 9 829 | ok. 13,0 TB | 0 |

- Trzy z czterech dysków mają uszkodzone (realokowane) bloki pamięci. Atrybuty 161 i 232 (dostępna rezerwa bloków) mają wartość surową 60, 80 i 73; egzemplarz bez realokacji zgłasza 100.
- Według wcześniejszych odczytów kupującego (spoza Załącznika nr 2) liczba realokacji wynosiła: 27.04.2026 r. — 3 / 3 / 2 / 0; 4.08.2026 r. — 6 / 3 / 4 / 0. W pomiarze z 1.10.2026 r. wartości nie uległy dalszej zmianie.
- Uszkodzenia wystąpiły po zapisaniu ok. 13–14 TB danych na dysk. Producent deklaruje dla oryginalnego 870 EVO 2 TB wytrzymałość 1 200 TB (TBW) — jest to ok. 1% tej wartości. Okoliczność ta dotyczy stanu nośników, a nie ich autentyczności.
- Ilość zapisanych danych odczytano z atrybutu 241, który na tych dyskach liczony jest w jednostkach 32 MiB (konwencja smartmontools dla kontrolerów Silicon Motion). Licznik „Logical Sectors Written” z Device Statistics jest na tych dyskach 32-bitowy i uległ wielokrotnemu przepełnieniu, dlatego pokazuje wartości pozornie niższe; jego wartość odpowiada atrybutowi 241 × 65 536 sektorów modulo 2³² na wszystkich czterech dyskach (różnica < 65 536 sektorów), co potwierdza jednostkę 32 MiB.
- `199 CRC_Error_Count` = 0 na wszystkich dyskach, co nie wskazuje na błędy transmisji (okablowanie, złącza); liczniki błędów warstwy fizycznej SATA (log 0x11: ICRC, R_ERR) również wynoszą 0.

## 4. Godziny pracy a historia zamówienia

Dyski zamontowano ok. 11 kwietnia 2025 r. (zgłoszenie w Dyskusji Allegro z 14.04.2025 r.: „three days ago”). Trzy egzemplarze mają 9 969–10 006 godzin pracy i 283–284 cykle zasilania. Egzemplarz S5Y4R020A077877 ma 9 829 godzin i 274 cykle, czyli o 140–177 godzin i 9–10 cykli zasilania mniej, co jest zgodne z ok. sześciodniową różnicą między montażem pierwotnych dysków a otrzymaniem dysku zamiennego (17 kwietnia 2025 r.). Jest to też jedyny egzemplarz o firmware `W0724A0` i pojemności 2 048 408 248 320 bajtów. Wskazuje to, że jest to dysk dostarczony przez Sprzedawcę w ramach wymiany.

## 5. Integralność danych

Kontrola spójności danych (ZFS scrub) z 1.10.2026 r. zakończyła się wynikiem 0 błędów. Dane nie zostały dotychczas utracone.

## 6. Źródła danych porównawczych

- Karta katalogowa Samsung SSD 870 EVO (kontroler Samsung MKX, 1 200 TB TBW dla 2 TB, TCG/Opal): https://download.semiconductor.samsung.com/resources/data-sheet/Samsung_SSD_870_EVO_Data_Sheet_Rev1.1_230509_10129500053000.pdf
- Lista oficjalnego firmware Samsung dla 870 EVO (SVT04B6Q, kwiecień 2026 r.): https://semiconductor.samsung.com/consumer-storage/support/tools/
- Publiczna baza pomiarów `smartctl` linuxhw/SMART — 371 odczytów oryginalnych 870 EVO 2 TB (WWN `5 002538…`, ACS-4, SATA 3.3, 14–15 atrybutów): https://github.com/linuxhw/SMART/tree/master/SSD/Samsung/SSD%20870/SSD%20870%20EVO%202TB
- Wynik `smartctl` oryginalnego 870 EVO 4 TB (firmware SVT02B6Q), baza zgłoszeń smartmontools: https://www.smartmontools.org/raw-attachment/ticket/1734/smartctl-Samsung-SSD_870_EVO_4TB-SVT02B6Q.txt
- Baza `drivedb.h` projektu smartmontools: https://raw.githubusercontent.com/smartmontools/smartmontools/master/smartmontools/drivedb.h
- Baza smarthdd.com — wpis „Fake” dla dysku zgłaszającego się jako Samsung SSD 870 EVO z firmware W0814A0 (kontroler Silicon Motion, ACS-2, SATA 3.2): https://smarthdd.com/database/Fake/Samsung-SSD-870-EVO-250GB/W0814A0/
