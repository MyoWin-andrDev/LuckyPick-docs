#  Architecture & System Structure

LuckyPick EuroMillions is architected for speed, modularity, and future expansion into other international lotteries (*EuroJackpot*, *Lotto Belgium*, *Powerball*, *Mega Millions*).

---

##  System Overview

```

                   Flutter Mobile Client                     
    
   UI Screens     State Mgmt     Local SQLite / Storage 
    

                                              
                                              

                 Lucky Pick Core Modules                     
    
  Generation     Frequency      Local Push             
  Algorithms     Statistics     Notifications          
    

                           (HTTPS REST API)
                          

                Cloud API & Scraper Engine                   
    
  Official Data  PostgreSQL /   APNs / FCM             
  Web Scraper   Cloud Firestore  Push Dispatcher        
    

```

---

##  Section & Navigation Flow

The mobile app follows a strict 5-tab navigation layout:

```
App Launch  Welcome / Onboarding  Main Dashboard (5 Tabs)
                                          
    
                                                                           
[1. Home & Gen] [2. Statistics]     [3. Results & Hist]   [4. My Picks]    [5. Settings]
 - Jackpot banner- Frequency chart  - Tue/Fri draw      - Saved tickets  - Subscriptions
 - Quick Pick    - Hot/Cold numbers - 13 Prize tiers    - Ticket checker - Language
 - Lucky Modes   - Odd/Even ratio   - 100-Draw DB       - Cost calc      - Support
```

---

##  Technology Stack

| Layer | Technology Choice | Rationale |
| :--- | :--- | :--- |
| **Mobile Client** | Flutter / Dart (or Native Swift & Kotlin) | Smooth 60fps UI, cross-platform iOS & Android deployment |
| **Database** | SQLite / Hive (Client) + PostgreSQL (Backend) | Offline-first ticket storage with fast historical draw querying |
| **Push Gateway** | Firebase FCM + Apple APNs | Reliable remote push notifications for jackpot milestones |
| **Payments** | StoreKit 2 (iOS) + Google Play Billing (Android) | Native, secure in-app subscription processing |
| **Documentation** | MkDocs + Material for MkDocs | Fast, search-indexed Markdown documentation |
