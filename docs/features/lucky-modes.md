#  Lucky Modes & Number Generation Logic

EuroMillions requires selecting **5 Main Numbers (1 to 50)** and **2 Lucky Stars (1 to 12)**. LuckyPick features proprietary **Lucky Modes** that personalize and optimize this selection.

---

##  1. EuroMillions Rules & Constraints

```

               EuroMillions Combination Rules                
                                                             
    Main Numbers:  [ 5 ] numbers chosen from 1 to 50         
    Lucky Stars:   [ 2 ] numbers chosen from 1 to 12         

```

* **No duplicates within a line:** 5 main numbers must all be distinct; 2 lucky stars must be distinct.
* **Ascending order display:** All generated lines are displayed sorted in ascending numerical order.

---

##  2. Birthday Mode

Converts meaningful personal dates (birthdays, anniversaries, graduation years) into EuroMillions numbers.

### Algorithm Rules:
1. **Direct mapping:** Days (1–31) and Months (1–12) directly map to Main Numbers and Lucky Stars.
2. **Year mapping:** Digits of birth years (e.g. `1994` $\rightarrow$ `19`, `94` $\rightarrow$ `49`) are modulo-mapped to valid 1–50 and 1–12 ranges.
3. **Entropy filler:** If date inputs yield fewer than 5 unique main numbers, high-entropy pseudorandom numbers fill the remaining slots.

---

##  3. Horoscope / Zodiac Mode

Generates daily personalized combinations based on the user's astrological sign.

```
Zodiac Input (e.g. Leo)  Astrological Ruling Numbers + Ephemeris  5 Main + 2 Stars
```

* **12 Astrological Signs Supported:** Aries, Taurus, Gemini, Cancer, Leo, Virgo, Libra, Scorpio, Sagittarius, Capricorn, Aquarius, Pisces.
* **Daily Refresh:** Number combinations update daily based on planetary house positions and sign ruling numbers.

---

##  4. Pet & Family Modes

* **Pet Mode:** Uses pet name letter values, pet adoption/birth dates, and pet category (Dog, Cat, Bird, etc.) to derive a unique 5+2 combination.
* **Family Mode:** Combines multiple family members' ages, birth months, and lucky digits into a combined ticket set.

---

##  5. Frequency & Hot / Cold Mode

Leverages the rolling **100-draw EuroMillions database** to generate statistics-backed combinations.

### Selection Strategies:
1. **Hot Numbers:** Picks from the most frequently drawn numbers in the last 100 draws.
2. **Cold / Overdue Numbers:** Picks from numbers that have not appeared in the longest duration.
3. **Balanced Mix:** Combines 3 Hot numbers + 2 Overdue numbers with a 3:2 odd/even ratio.
