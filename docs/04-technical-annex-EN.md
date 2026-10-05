# Annex 1 — drive test results

> English translation of `03-zalacznik-techniczny-PL.md`, for reference.

**Re:** Allegro order 6c1d38c0-… of 17.03.2025 — 4 × "Dysk SSD Samsung MZ-77E2T0 2TB 2,5" SATA III 870 EVO"
**Serial numbers reported by the drives:** S5Y4R020A077805, S5Y4R020A077806, S5Y4R020A077808, S5Y4R020A077877
**Measured:** 1 October 2026
**Method:** `smartctl` 7.5 (smartmontools): `smartctl -x`, `smartctl --identify=wb` and `smartctl -r ataioctl,2 -A`; drives connected directly to the motherboard SATA (AHCI) ports.

All values come from the drives' own responses (ATA IDENTIFY DEVICE and SMART READ DATA), not from the label or packaging. Raw, unmodified output is Annex 2.

The buyer's earlier readings (27.04.2026 and 4.08.2026, LSI SAS3008 controller) are not part of Annex 2; the buyer will provide them on request.

## 1. Identity data reported by the drives

| Serial | Firmware | Capacity (bytes) | ATA version | SATA | WWN |
|---|---|---|---|---|---|
| S5Y4R020A077805 | **W0814A0** | 2,000,398,934,016 | ACS-2 | 3.2 | **none** |
| S5Y4R020A077806 | **W0814A0** | 2,000,398,934,016 | ACS-2 | 3.2 | **none** |
| S5Y4R020A077808 | **W0814A0** | 2,000,398,934,016 | ACS-2 | 3.2 | **none** |
| S5Y4R020A077877 | **W0724A0** | **2,048,408,248,320** | ACS-2 | 3.2 | **none** |

All four report the model name `Samsung SSD 870 EVO 2TB`.

## 2. Comparison with a genuine Samsung 870 EVO

| Feature | Tested drives | Genuine Samsung 870 EVO |
|---|---|---|
| Label (Annex 5) | the same WWN `5002538F2000CAB` and the same PSID on all four drives | WWN and PSID unique to each unit |
| Controller | the drive itself reports `SMI2259XT` (Silicon Motion) in its SMART data sector | Samsung MKX (manufacturer data sheet) |
| Firmware | `W0814A0`, `W0724A0` | `SVT01B6Q`–`SVT04B6Q` |
| Number of SMART attributes | **30** (incl. 160, 161, 163–169, 245) | **14** (firmware SVT01B6Q) or **15** (later versions): 5, 9, 12, 177, 179, 181, 182, 183, 187, 190, 195, 199, 235, 241, 252 |
| World Wide Name | none (IDENTIFY words 84 and 87, bit 8 = 0; words 108–111 = 0) | present, manufacturer prefix `5002538` |
| ATA / SATA version | ACS-2 / SATA 3.2 | ACS-4 / SATA 3.3 |
| TRIM | available, no DRAT/RZAT (word 69 = 0x0d00) | "Available, deterministic, zeroed" |
| Encryption / TCG Opal | none (word 48 bit 0 = 0; word 69 bit 4 = 0) | AES 256-bit, TCG/Opal V2.0 (data sheet) |
| 2 TB capacity | one unit: 4,000,797,360 sectors (2,048,408,248,320 B) | 3,907,029,168 sectors (2,000,398,934,016 B) |

- **2.1 Controller.** In the SMART data sector (SMART READ DATA, bytes 386–439) each of the four drives stores, in plain text, the firmware version and the controller designation: `W0814A0 00`, `SMI2259XT`, `N3800` (unit …877: `W0724A0 00`, `SMI2259XT`, `N2800`). A genuine 870 EVO uses the Samsung MKX controller.
- **2.2 Firmware.** `W0814A0` and `W0724A0` are not among the versions Samsung publishes for the 870 EVO (`SVT01B6Q`–`SVT04B6Q`). The identical versions are reported by drives of other brands built on Silicon Motion controllers (e.g. Intenso, Team Group, Verbatim, AGI, PNY — public linuxhw/SMART database); smartmontools' `drivedb.h` lists versions of this format (`W0413A0`, `W0714A0`, `W0825A0`) under "Silicon Motion based OEM SSDs".
- **2.3 SMART table.** Each drive reports the same 30 attributes: 1, 5, 9, 12, 160, 161, 163–169, 175, 176, 177, 178, 181, 182, 192, 194–199, 232, 241, 242, 245. The set matches the Silicon Motion firmware table described in `drivedb.h` and is identical to that of other-brand drives with firmware `W0814A0`. A genuine 870 EVO reports 14 or 15 attributes; none of 160–169 occurs in it.
- **2.4 No WWN.** IDENTIFY words 84 and 87 have bit 8 = 0 and words 108–111 are 0. `smartctl` prints no `LU WWN Device Id` line and the operating system creates no `wwn-…` identifier for any of the four drives (measured on AHCI ports). The manufacturer lists World Wide Name support among the 870 EVO's features.
- **2.5 Standards and features.** ACS-2 and SATA 3.2. IDENTIFY word 69 = 0x0d00: bit 14 (DRAT) = 0, bit 5 (RZAT) = 0, bit 4 (data encryption) = 0. Word 48 bit 0 = 0 (no Trusted Computing feature set, required for TCG Opal). Samsung's data sheet states for the 870 EVO: "AES 256-bit Full Disk Encryption, TCG/Opal V2.0, Encrypted Drive (IEEE1667)".
- **2.6 Capacity.** Unit S5Y4R020A077877 — most probably the April 2025 replacement (section 4) — reports 4,000,797,360 sectors (2,048,408,248,320 B), the IDEMA value for 2048 GB; genuine: 3,907,029,168 sectors (IDEMA, 2000 GB).
- **2.7 Serial numbers.** Serial numbers of genuine 870 EVO drives in public measurement databases have a different structure (e.g. `S6PNNJ0W303102W`, `S620NJ0R902825F`: a plant letter in fifth position, a check letter at the end). The numbers reported by the tested drives (`S5Y4R020A0778xx`) do not. Given as supporting information.

- **2.8 Labels (photos of 2.10.2026, Annex 5).** The labels of all four drives read: `PN MZ7L32T0HBLT`, `MODEL MZ-77E2T0 2024.12`, `WWN 5002538F2000CAB`, `PSID YRR72JB0YU84ENPZP05K1AVSR2AJ1AWK`, `PRODUCT OF KOREA`. Only the serial number differs. A WWN (World Wide Name) and a PSID (Physical Security ID) are by definition unique to each unit; their repetition on four drives, including the unit supplied a month later as a replacement, means the labels do not come from the manufacturer's production process. In addition, none of the drives electronically reports the WWN printed on its label (2.4), and the drives do not support TCG Opal, which the PSID relates to (2.5).

> Note: the `Model Family: Samsung based SSDs` line in `smartctl` output does not confirm authenticity; the tool derives it by pattern-matching the model name the drive itself reports.

## 3. Media health (1.10.2026)

| Serial | Reallocated (05) | Pending (197) | Uncorrectable (198) | Spare blocks (161/232, raw value) | Power-on hours (09) | Written (241) | CRC errors (199) |
|---|---|---|---|---|---|---|---|
| S5Y4R020A077805 | **6** | **6** | **1** | **60** | 9,969 | ~13.8 TB | 0 |
| S5Y4R020A077806 | **3** | **3** | 0 | **80** | 9,984 | ~14.2 TB | 0 |
| S5Y4R020A077808 | **4** | **4** | **1** | **73** | 10,006 | ~13.8 TB | 0 |
| S5Y4R020A077877 | 0 | 0 | 0 | 100 | 9,829 | ~13.0 TB | 0 |

- Three of four drives have damaged (reallocated) memory blocks. Attributes 161 and 232 (available spare blocks) have raw values 60, 80 and 73; the unit with no reallocations reports 100.
- According to the buyer's earlier readings (outside Annex 2) the reallocation counts were: 27.04.2026 — 3 / 3 / 2 / 0; 4.08.2026 — 6 / 3 / 4 / 0. On 1.10.2026 the values were unchanged.
- The damage appeared after about 13–14 TB written per drive. The manufacturer declares 1,200 TB (TBW) for a genuine 870 EVO 2 TB — this is about 1% of that. This concerns the condition of the media, not their authenticity.
- Data written is read from attribute 241, which on these drives counts in 32 MiB units (the smartmontools convention for Silicon Motion controllers). The "Logical Sectors Written" Device Statistics counter is 32-bit on these drives and has overflowed several times, so it shows apparently lower values; its value equals attribute 241 × 65,536 sectors modulo 2³² on all four drives (difference < 65,536 sectors), which confirms the 32 MiB unit.
- `199 CRC_Error_Count` = 0 on all drives, which does not indicate transmission errors (cabling, connectors); the SATA physical-layer error counters (log 0x11: ICRC, R_ERR) are also 0.

## 4. Power-on hours vs. order history

The drives were installed around 11 April 2025 (Allegro Discussion report of 14.04.2025: "three days ago"). Three units have 9,969–10,006 power-on hours and 283–284 power cycles. Unit S5Y4R020A077877 has 9,829 hours and 274 cycles — 140–177 hours and 9–10 cycles fewer, consistent with the roughly six days between installing the original drives and receiving the replacement (17 April 2025). It is also the only unit with firmware `W0724A0` and 2,048,408,248,320 bytes. This indicates that it is the drive the Seller supplied as the replacement.

## 5. Data integrity

The ZFS scrub of 1.10.2026 completed with 0 errors. No data has been lost so far.

## 6. Reference sources

- Samsung SSD 870 EVO data sheet (Samsung MKX controller, 1,200 TB TBW for 2 TB, TCG/Opal): https://download.semiconductor.samsung.com/resources/data-sheet/Samsung_SSD_870_EVO_Data_Sheet_Rev1.1_230509_10129500053000.pdf
- Samsung's official firmware list for the 870 EVO (SVT04B6Q, April 2026): https://semiconductor.samsung.com/consumer-storage/support/tools/
- Public `smartctl` database linuxhw/SMART — 371 readings of genuine 870 EVO 2 TB drives: https://github.com/linuxhw/SMART/tree/master/SSD/Samsung/SSD%20870/SSD%20870%20EVO%202TB
- `smartctl` output of a genuine 870 EVO 4 TB (firmware SVT02B6Q): https://www.smartmontools.org/raw-attachment/ticket/1734/smartctl-Samsung-SSD_870_EVO_4TB-SVT02B6Q.txt
- smartmontools `drivedb.h`: https://raw.githubusercontent.com/smartmontools/smartmontools/master/smartmontools/drivedb.h
- smarthdd.com — "Fake" entry for a drive reporting as Samsung SSD 870 EVO with firmware W0814A0 (Silicon Motion controller, ACS-2, SATA 3.2): https://smarthdd.com/database/Fake/Samsung-SSD-870-EVO-250GB/W0814A0/
