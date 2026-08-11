#  Backend, Scraper & Admin Control Panel

The LuckyPick backend automates EuroMillions draw data collection, stores subscription logs, and handles remote push dispatches.

---

##  1. Automated EuroMillions Scraper Engine

```
Every Tue / Fri 20:45 CET  Scraper Cron Job  Parse Official Results
                                                           
                                                           
Push Alert Sent  Store In Database (PostgreSQL/Firestore)
```

* **Schedule:** Runs every Tuesday and Friday night starting at **20:45 CET**.
* **Failover & Validation:** Scrapes from two independent official sources. If data differs or is incomplete, alerts system admin via email/Slack webhook before publishing.

---

##  2. Owner Admin Control Panel

A lightweight admin panel (`https://admin.luckypick.eu` or internal dashboard) allowing the app owner to:

1. **Monitor Scraper Health:** View status of Tue/Fri automated draw ingestion.
2. **Dispatch Custom Push Notifications:** Trigger manual broadcasts for record jackpots.
3. **Analytics Overview:** View active subscribers and daily generation metrics.
