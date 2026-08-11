#  Notifications & Reminders

LuckyPick EuroMillions features smart local and remote push notifications to ensure users never miss a draw or a record jackpot.

---

##  1. Draw Cutoff Reminder (Local Push)

* **Trigger:** Scheduled every Tuesday and Friday evening (e.g. 19:00 CET, 1 hour before ticket sales close).
* **Payload:** *"Tonight's EuroMillions draw closes soon! Have you generated your Lucky Pick?"*
* **User Control:** Customizable reminder time or toggle off in Settings.

---

##  2. €100 Million+ High Jackpot Alert (Remote Push)

* **Trigger:** Dispatched via APNs / FCM when the advertised EuroMillions jackpot rolls over past **€100,000,000**.
* **Payload:** *" Mega Jackpot Alert! Tonight's EuroMillions jackpot has reached €130 Million. Generate your lucky numbers now!"*

---

##  3. Results Ready Alert (Remote Push)

* **Trigger:** Sent automatically when official Tue/Fri night draw results are ingested and verified by the backend scraper.
* **Payload:** *" Official EuroMillions results are in! Check your saved picks to see if you won."*
