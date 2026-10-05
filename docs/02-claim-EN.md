# COMPLAINT — LACK OF CONFORMITY OF GOODS WITH THE CONTRACT

> English translation of `01-reklamacja-PL.md`, for reference. The Polish text is the operative document.

**Warsaw, 2 October 2026**

**Buyer (consumer):** [Buyer], [adres], Warszawa · [e-mail] · [tel.] · Allegro account: Client:48695146

**Seller (trader):** Grzegorz Pawlik, trading as Kintech, Mnichów 121a, 28-300 Jędrzejów · NIP 656-233-10-99, REGON 362036210 · Allegro account: **grzesiup255**

**Re:** Allegro order no. **6c1d38c0-…** of **17 March 2025**, offer no. 16733065275
**Item:** "Dysk SSD Samsung MZ-77E2T0 2TB 2,5" SATA III 870 EVO" — 4 units
**Price:** 4 × PLN 675.00 = **PLN 2,700.00** (paid 17.03.2025, payment ID 6c5316b5-…, Przelewy24 / Google Pay)
**Delivery:** Allegro Paczkomaty InPost

---

## I. Subject of the complaint

Under Articles 43b–43e of the Polish Consumer Rights Act of 30 May 2014 ("the Act") I file a complaint concerning all four SSD drives delivered under the above order.

The offer — as it stood on the day of purchase, preserved by Allegro — described the goods as follows: **Condition: New; Manufacturer: Samsung; Manufacturer code: MZ-77E2T0B/EU; EAN (GTIN): 8806090545900; Maximum write speed: 530 MB/s; Maximum read speed: 560 MB/s.** The contract was therefore for factory-new, genuine Samsung 870 EVO 2 TB drives, unambiguously identified by manufacturer code and EAN. The Seller also declared in the offer terms, which form an integral part of the contract: **"Warranty type: manufacturer's. Warranty period: 24 months"** (Annex 3). The offer contained no indication that the goods do not come from Samsung.

**The drives delivered are not genuine Samsung 870 EVO drives designated MZ-77E2T0.** They are devices built on another manufacturer's controller and merely labelled with the Samsung name and model. This applies to all four units, including the unit the Seller supplied as a replacement in April 2025.

The price of PLN 675.00 per unit was in line with the prices of a genuine Samsung 870 EVO 2 TB at the time; nothing suggested I would receive a non-genuine product.

Serial numbers reported by the drives: S5Y4R020A077805, S5Y4R020A077806, S5Y4R020A077808, S5Y4R020A077877 (the April 2025 replacement unit).

## II. Facts

### 1. Earlier complaint and replacement (April 2025)

On 14 April 2025 I reported, in the Allegro Discussion for this order, a defect in one of the drives (it disconnected by itself after a few minutes of operation; serial number given in the report: S5Y4R010A077819). The Seller accepted the report ("proszę go pilnie do nas odesłać – wymienimy go tak szybko, jak to tylko możliwe") and replaced that unit; I received the replacement on 17 April 2025 (Annex 3).

The power-on-hours and power-cycle counters (about 150 hours and 9–10 cycles fewer than the other three drives) indicate that the replacement is unit S5Y4R020A077877. It is not a genuine Samsung drive either: it is the only one reporting firmware `W0724A0` and a capacity of 2,048,408,248,320 bytes. **The Seller has therefore already made one attempt to bring the goods into conformity and delivered further non-conforming goods.**

### 2. Test results

Measurements were taken with `smartctl` 7.5 (smartmontools) on 1 October 2026, with the drives connected directly to the motherboard SATA (AHCI) ports. The data come from the drives' own responses to the ATA IDENTIFY DEVICE and SMART READ DATA commands, not from the label or packaging. Full documentation is Annex 1; raw output is Annex 2; label photos are Annex 5.

1. **Labels.** The labels of all four drives carry the same WWN (`5002538F2000CAB`) and the same PSID code (`YRR72JB0YU84…AJ1AWK`); only the serial number differs (Annex 5). WWN and PSID are by nature unique to each individual drive. This also applies to the April 2025 replacement unit — it bears the same date (2024.12), the same WWN and the same PSID as the other three. Moreover, none of the drives electronically reports the WWN printed on its label (point 5).
2. **Controller.** Each of the four drives itself reports, in its SMART data sector, the controller designation `SMI2259XT` (Silicon Motion). A genuine Samsung 870 EVO uses, per the manufacturer's data sheet, the Samsung MKX controller.
3. **Firmware.** The drives report `W0814A0` (3 units) and `W0724A0` (1 unit). Samsung publishes only `SVT01B6Q`–`SVT04B6Q` for the 870 EVO. The reported versions occur in drives of other brands built on Silicon Motion controllers (cf. smartmontools `drivedb.h` and the linuxhw/SMART database).
4. **SMART attribute table.** The drives report 30 attributes, including 160, 161, 163–169 and 245, matching the Silicon Motion firmware table. A genuine 870 EVO reports 14 or 15 attributes in a different layout; none of attributes 160–169 occurs in it.
5. **No WWN.** In IDENTIFY DEVICE (words 84 and 87, bit 8 = 0; words 108–111 = 0) the drives declare no World Wide Name; genuine Samsung drives report a WWN with the manufacturer prefix `5002538`.
6. **Declared standards and features.** The drives declare ACS-2 and SATA 3.2 and report neither deterministic TRIM nor encryption; a genuine 870 EVO declares ACS-4, SATA 3.3, TRIM "deterministic, zeroed" and AES 256-bit encryption with TCG/Opal 2.0.
7. **Capacity.** Unit S5Y4R020A077877 reports 2,048,408,248,320 bytes, whereas a genuine 870 EVO 2 TB has 2,000,398,934,016 bytes.

### 3. Media health

Three of the four drives already have damaged memory blocks ("reallocated sectors" attribute: 6, 3 and 4). According to my earlier readings the count rose between 27.04.2026 and 4.08.2026 from 3 to 6 in unit 077805 and from 2 to 4 in unit 077808; on 1.10.2026 the values were unchanged. The damage appeared after about 14 TB written per drive, i.e. about 1% of the 1,200 TB (TBW) endurance the manufacturer declares for the genuine model.

I describe the media condition as supporting information only: the basis of this complaint is the lack of identity of the goods, not their degree of wear.

### 4. Consequences for me and my family

I bought the drives for a home file server that stores **my whole family's data and the backups of our computers**. I chose genuine drives from a reputable manufacturer precisely for the safety of that data. Instead, for a year and a half that data has been sitting on devices of unknown origin, without manufacturer warranty, three of which already have damaged sectors, and one unit failed after only a few days of use.

Establishing the true state of affairs, diagnostics, measurements and safeguarding the data cost me many hours of work.

Moreover, SSD prices have more than tripled since the purchase: a genuine Samsung 870 EVO 2 TB now costs from about PLN 2,165 per unit (Allegro and Ceneo.pl, as of 1.10.2026) against PLN 675 on the day of purchase (Annex 4). **Even a refund of the entire price would not allow me to buy today the goods I paid for in March 2025** — buying four genuine drives now would cost about PLN 8,660.

## III. Legal basis

Under Art. 43b(1)(1) of the Act, goods conform to the contract if, in particular, their description, type, quantity, quality, completeness and functionality conform. Under Art. 43b(2)(1) and (2), goods must also be fit for the purposes for which goods of that kind are normally used and have the features, including durability, that are typical for such goods and that the consumer may reasonably expect, taking into account the trader's public statements. Delivering devices that are not genuine Samsung 870 EVO (MZ-77E2T0) drives but are merely labelled as such is a lack of conformity as to description, type and quality.

**Time limit.** Under Art. 43c(1), first sentence, the trader is liable for a lack of conformity existing at delivery and revealed within two years; under Art. 43c(1), second sentence, a lack of conformity revealed within two years of delivery is presumed to have existed at delivery. The goods were delivered in March 2025 (the replacement unit on 17 April 2025) and the lack of conformity was revealed in 2026 (I established it in August 2026 when analysing the drives' identity data). Irrespective of the presumption, the lack of conformity concerns the identity of the goods — a feature that cannot arise after delivery.

**Materiality.** The lack of conformity is material (presumption in Art. 43e(4), second sentence) because it: concerns the identity and origin of the goods, the feature that determined the purchase, and undermines trust in the Seller; deprives me of the manufacturer's warranty that the Seller declared in the offer and that Samsung grants only on its genuine products; deprives me of manufacturer support, including firmware updates intended for genuine drives; and exposes my whole family's data stored on these drives to loss.

**The right to a price reduction.** If replacement is refused or not carried out within a reasonable time, I will be entitled to a price reduction under Art. 43e(1)(1) or (2). Independently of that: (a) for the unit replaced in April 2025, the lack of conformity persists although the trader attempted to bring the goods into conformity (Art. 43e(1)(3)); (b) the lack of conformity concerns the identity and origin of all four drives and is serious enough to justify a price reduction without first using the remedies in Art. 43d (Art. 43e(1)(4)). By demanding replacement first I do not give up reliance on those grounds.

## IV. Demand

**1. Replacement.** Under Art. 43d(1) I demand replacement of all four drives with factory-new, genuine Samsung SSD 870 EVO 2 TB (MZ-77E2T0B) drives, in intact manufacturer packaging, sourced from authorised distribution. Please enclose a document confirming their origin; before handing over the current drives I will verify the serial numbers with the manufacturer.

I expect confirmation of the replacement within 14 days of receipt of this letter and its completion within a further 14 days. The costs are borne by the trader (Art. 43d(4), second sentence), who collects the replaced goods at his own expense (Art. 43d(5)); I owe nothing for normal use of the goods (Art. 43d(7)). Because the drives hold my family's data, I ask — in line with Art. 43d(4) — that the replacement drives be delivered first; I will make the current ones available for collection within 30 days of receiving them.

**2. Price reduction and damages — in case replacement is refused.** If you refuse replacement, in particular under Art. 43d(2), or do not confirm or carry it out within the above deadlines, I reserve the choice between continuing to pursue replacement and making a separate declaration of price reduction under Art. 43e(1)(1), (2) or (5) (and independently (3) and (4)), together with a demand for damages. I already state the amounts of those claims:

a) a price reduction of **PLN 2,160.00**, i.e. to PLN 540.00, repayable within 14 days of receipt of the declaration (Art. 43e(3)). The measurements in Annexes 1 and 2 show that the drives delivered are not products of Samsung although they bear its markings: they carry no manufacturer warranty, I cannot resell them as Samsung drives, they are built on a Silicon Motion controller instead of a Samsung controller, and three of the four already have damaged memory blocks. I value them at no more than 20% of the value of conforming goods (Art. 43e(2));

b) damages under Art. 471 in conjunction with Art. 361 and Art. 363 § 2 of the Civil Code of **PLN 4,767.33**. Buying four genuine Samsung 870 EVO 2 TB drives now costs at least PLN 8,659.16 (4 × PLN 2,164.79 — the lowest price of a new unit on Allegro and on the Ceneo.pl price comparison site on 1.10.2026, Annex 4). The loss is the difference between that amount and the value of the drives I keep (20%, i.e. PLN 1,731.83), less the price reduction (PLN 2,160.00): 8,659.16 − 1,731.83 − 2,160.00 = PLN 4,767.33. That loss is the normal consequence of delivering non-genuine goods instead of genuine ones, and its amount is set at prices as of the date damages are determined; I reserve the right to update it to prices at that date.

**Total: PLN 6,927.33.** I will state the bank account for payment in the price-reduction declaration.

**3. No consent to withdrawal.** I declare that **I do not withdraw from the contract** and do not agree to the complaint being settled by returning the goods against a refund. The choice between price reduction and withdrawal belongs to the consumer (Art. 43e(1)). Closing the Allegro Discussion in April 2025 was not a waiver of rights (Art. 7).

## V. Deadline and next steps

Under Art. 7a(1) of the Act I expect a reply **within 14 days** of receipt, on paper or another durable medium (Art. 7a(3)). Failure to reply in time means, under Art. 7a(2), that **the complaint is deemed accepted**.

This letter is an attempt to resolve the dispute out of court (Art. 187 § 1(3) of the Code of Civil Procedure). If the complaint is not accepted, I will use Allegro Buyer Protection and the assistance of the Municipal Consumer Ombudsman in Warsaw, and then **take the case to court with professional legal representation**. I will then claim the amounts due together with statutory interest for delay and the costs of proceedings, including the cost of a court expert opinion and of legal representation.

---

**Annexes:** 1. Technical annex — test results · 2. Raw `smartctl -x`, ATA IDENTIFY DEVICE and SMART READ DATA output for the four drives (1.10.2026) · 3. Offer from the day of purchase, the Seller's complaint and warranty terms, and the record of the Allegro Discussion of 14–17 April 2025 · 4. Current prices of the genuine Samsung 870 EVO 2 TB (screenshots of 1.10.2026) · 5. Photos of the drive labels (2.10.2026)

Yours faithfully,
[Buyer]
