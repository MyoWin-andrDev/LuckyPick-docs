#  UML Diagrams

Structural and behavioural models for the LuckyPick EuroMillions system.

---

##  1. Domain Class Diagram

```mermaid
classDiagram
    direction TB

    class User {
        +String id
        +String preferredLanguage
        +UserTier tier
        +DateTime createdAt
        +List~LuckyModeInput~ savedInputs
        +NotificationPreferences notifPrefs
    }

    class UserTier {
        <<enumeration>>
        FREE
        PREMIUM_MONTHLY
        PREMIUM_YEARLY
        PREMIUM_LIFETIME
    }

    class MyPicksSet {
        +String id
        +String userId
        +DateTime createdAt
        +SetStatus status
        +List~Combination~ combinations
        +int maxSize = 12
        +addCombination(Combination) bool
        +startNewSet() MyPicksSet
    }

    class SetStatus {
        <<enumeration>>
        ACTIVE
        ARCHIVED
    }

    class Combination {
        +String id
        +List~int~ mainNumbers
        +List~int~ luckyStars
        +LuckyMode mode
        +LuckyModeInput modeSnapshot
        +DateTime generatedAt
        +validate() bool
        +isEqualTo(Combination) bool
    }

    class LuckyMode {
        <<enumeration>>
        QUICK_PICK
        BIRTHDAY
        HOROSCOPE
        PET
        FAMILY
        LUCKY_COLOR
        LUCKY_NUMBER
        HOT_NUMBERS
        COLD_NUMBERS
        TRENDING
        SMART_MIX
    }

    class LuckyModeInput {
        +LuckyMode mode
        +Map~String, dynamic~ params
    }

    class EuroMillionsDraw {
        +String id
        +DateTime drawDate
        +List~int~ mainNumbers
        +List~int~ luckyStars
        +BigDecimal jackpotAmount
        +bool jackpotWon
        +int jackpotWinners
        +List~PrizeTier~ prizeBreakdown
        +bool isValidated
    }

    class PrizeTier {
        +int tierNumber
        +String matchDescription
        +BigDecimal prizeAmount
        +int numberOfWinners
    }

    class DrawDatabase {
        +List~EuroMillionsDraw~ draws
        +int maxDraws = 100
        +addDraw(EuroMillionsDraw) bool
        +removeOldest() void
        +getLatest() EuroMillionsDraw
        +getHistory() List~EuroMillionsDraw~
        +getStatistics() DrawStatistics
    }

    class DrawStatistics {
        +Map~int, int~ mainNumberFrequency
        +Map~int, int~ luckyStarFrequency
        +List~int~ hotNumbers
        +List~int~ coldNumbers
        +List~int~ trendingNumbers
        +List~int~ hotStars
        +List~int~ coldStars
        +List~int~ trendingStars
        +DateTime calculatedAt
    }

    class NotificationPreferences {
        +bool drawReminders
        +bool resultsAvailable
        +bool jackpotWon
    }

    class Subscription {
        +String id
        +String userId
        +SubscriptionType type
        +DateTime startDate
        +DateTime expiryDate
        +bool isActive
        +String storeTransactionId
    }

    class SubscriptionType {
        <<enumeration>>
        MONTHLY
        YEARLY
        LIFETIME
    }

    class GenerationEngine {
        +generateQuickPick() Combination
        +generateBirthday(LuckyModeInput) Combination
        +generateHoroscope(LuckyModeInput) Combination
        +generatePet(LuckyModeInput) Combination
        +generateFamily(LuckyModeInput) Combination
        +generateLuckyColor(LuckyModeInput) Combination
        +generateLuckyNumber(LuckyModeInput) Combination
        +generateHot(DrawStatistics) Combination
        +generateCold(DrawStatistics) Combination
        +generateTrending(DrawStatistics) Combination
        +generateSmartMix(DrawStatistics) Combination
        -validate(Combination) bool
        -isDuplicate(Combination, List~Combination~) bool
    }

    User "1" --> "1" UserTier
    User "1" --> "*" MyPicksSet
    User "1" --> "1" NotificationPreferences
    User "1" --> "0..1" Subscription
    MyPicksSet "1" --> "*" Combination
    MyPicksSet "1" --> "1" SetStatus
    Combination "1" --> "1" LuckyMode
    Combination "1" --> "1" LuckyModeInput
    EuroMillionsDraw "1" --> "*" PrizeTier
    DrawDatabase "1" --> "*" EuroMillionsDraw
    DrawDatabase "1" --> "1" DrawStatistics
    Subscription "1" --> "1" SubscriptionType
    GenerationEngine ..> DrawStatistics : reads
    GenerationEngine ..> Combination : creates
```

---

##  2. System Component Diagram

```mermaid
graph TB
    subgraph Mobile["Mobile Client (Flutter)"]
        UI[UI Layer\nScreens + Widgets]
        State[State Management\nProvider / Riverpod / BLoC]
        Gen[Generation Engine\n10 Lucky Modes]
        Local[Local Storage\nSQLite / Hive]
        IAP[In-App Purchase\nStoreKit 2 / Google Play Billing]
        Push[Push Notification\nLocal + Remote Handler]
        Share[Social Share\nNative Share Sheet]
    end

    subgraph Backend["Backend Server"]
        API[REST API Server\nNode.js / Go / Python]
        Scraper[Scraper Engine\nCron Tue/Fri 20:45 CET]
        Validator[Draw Validator]
        StatCalc[Statistics Calculator]
        PushDispatch[Push Dispatcher\nFCM + APNs]
        AdminPanel[Owner Admin Panel\nluckypick.eu/admin]
    end

    subgraph Data["Data Layer"]
        DB[(PostgreSQL\nDraw History\n100-draw rolling)]
        Cache[(Redis Cache\nLatest draw + stats)]
    end

    subgraph External["External Services"]
        BNL[Belgian National\nLottery — Official Source]
        FCM[Firebase FCM]
        APNs[Apple APNs]
        AppStore[Apple App Store\nStoreKit 2]
        GooglePlay[Google Play\nBilling]
        DeepLink[Branch.io / Firebase\nDynamic Links]
    end

    UI <--> State
    State <--> Gen
    State <--> Local
    State <--> API
    IAP <--> AppStore
    IAP <--> GooglePlay
    Push <--> FCM
    Push <--> APNs

    API <--> DB
    API <--> Cache
    Scraper --> BNL
    Scraper --> Validator
    Validator --> StatCalc
    StatCalc --> DB
    StatCalc --> Cache
    PushDispatch --> FCM
    PushDispatch --> APNs
    AdminPanel --> API

    Share --> DeepLink
    DeepLink --> Mobile
```

---

##  3. Sequence Diagram — Lucky Mode Generation

```mermaid
sequenceDiagram
    actor User
    participant UI
    participant GenEngine as Generation Engine
    participant Validator
    participant DupChecker as Duplicate Checker
    participant LocalDB as Local Storage

    User->>UI: Select Lucky Mode + Enter Input
    User->>UI: Tap GENERATE MY LUCKY NUMBERS
    UI->>GenEngine: generate(mode, input, stats)

    loop Until valid & unique
        GenEngine->>GenEngine: Apply mode-specific algorithm
        GenEngine->>GenEngine: Immediate exclusion of selected numbers
        GenEngine->>Validator: validate(combination)
        Validator->>Validator: Check 5 unique main 1–50
        Validator->>Validator: Check 2 unique stars 1–12
        alt Validation fails
            Validator-->>GenEngine: INVALID — regenerate
        else Valid
            Validator-->>GenEngine: VALID
            GenEngine->>DupChecker: isDuplicate(combination, activePicks)
            alt Is duplicate
                DupChecker-->>GenEngine: DUPLICATE — regenerate
            else Not duplicate
                DupChecker-->>GenEngine: UNIQUE
            end
        end
    end

    GenEngine-->>UI: Valid unique combination
    UI-->>User: Show result (1–1.5s animation)

    User->>UI: ADD TO MY PICKS
    UI->>Validator: validateBeforeSave(combination)
    Validator-->>UI: VALID
    UI->>LocalDB: save(combination, modeSnapshot)
    LocalDB-->>UI: Saved ✓
    UI-->>User: Added to My Picks ✓
```

---

##  4. Sequence Diagram — Backend Draw Ingestion

```mermaid
sequenceDiagram
    participant Cron as Cron Job\n(Tue/Fri 20:45 CET)
    participant Scraper
    participant BNL as Belgian National Lottery
    participant Validator
    participant DB as PostgreSQL
    participant StatCalc as Statistics Calculator
    participant PushSvc as Push Service
    participant App as Mobile App

    Cron->>Scraper: trigger()
    Scraper->>BNL: fetch draw results
    BNL-->>Scraper: draw data

    Scraper->>Validator: validate(drawData)
    Validator->>Validator: Check 5 unique main 1–50
    Validator->>Validator: Check 2 unique stars 1–12
    Validator->>Validator: Check draw date
    Validator->>Validator: Check no duplicate draw

    alt Validation fails
        Validator-->>Scraper: INVALID
        Scraper->>DB: keep existing 100 draws intact
        Scraper-->>AdminPanel: ATTENTION REQUIRED alert
    else Valid
        Validator-->>Scraper: VALID
        Scraper->>DB: INSERT new draw
        Scraper->>DB: DELETE oldest draw (100 maintained)
        DB-->>Scraper: OK
        Scraper->>StatCalc: recalculate(latest 100 draws)
        StatCalc->>StatCalc: Hot / Cold / Trending / Frequency
        StatCalc->>DB: UPDATE statistics
        Scraper->>PushSvc: sendResultsAvailable(drawId)
        PushSvc->>App: Results Available push notification
    end

    Note over Scraper,DB: Prize breakdown may arrive later

    Scraper->>BNL: fetch prize breakdown
    BNL-->>Scraper: prize data
    Scraper->>Validator: validatePrize(prizeData)
    alt Prize valid
        Validator-->>Scraper: VALID
        Scraper->>DB: UPDATE prize breakdown
        Scraper->>Scraper: Check 5+2 jackpot winners
        alt Winners >= 1
            Scraper->>PushSvc: sendJackpotWon(drawId)
            PushSvc->>App: Jackpot Won push notification
        end
    end
```

---

##  5. Sequence Diagram — Premium Purchase (iOS)

```mermaid
sequenceDiagram
    actor User
    participant App
    participant PremiumScreen
    participant StoreKit as StoreKit 2
    participant AppStore as Apple App Store
    participant Backend

    User->>App: Tap UNLOCK PREMIUM\nor hit free pick limit
    App->>PremiumScreen: open(returnDestination)
    User->>PremiumScreen: Select Yearly / Monthly / Lifetime
    PremiumScreen->>StoreKit: purchase(productId)
    StoreKit->>AppStore: initiate purchase
    AppStore-->>User: Auth prompt
    User->>AppStore: Authenticate
    AppStore-->>StoreKit: Transaction signed
    StoreKit-->>PremiumScreen: Transaction result

    alt Purchase SUCCESS
        PremiumScreen->>Backend: verifyReceipt(transactionId)
        Backend->>AppStore: verify(receipt)
        AppStore-->>Backend: VALID
        Backend-->>App: Premium ACTIVE
        App-->>User: WELCOME TO LUCKYPICK PREMIUM
        App->>App: Navigate back to returnDestination
        Note over App: My Picks & Saved Sets preserved
    else Purchase FAILED / CANCELLED
        PremiumScreen-->>User: Neutral message
        App->>App: Return to previous screen safely
    end
```

---

##  6. State Machine — My Picks Set

```mermaid
stateDiagram-v2
    [*] --> Empty : App first launch / START NEW SET

    Empty --> Active : First combination added\n(ADD TO MY PICKS)

    Active --> Active : Generate Another / Choose Another Mode\ncombinations 2–11

    Active --> Full : 12th combination added

    Full --> Archived : User taps START NEW SET

    Active --> Archived : User taps START NEW SET\n(before reaching 12)

    Archived --> [*] : Stored in SAVED SETS\nnever auto-modified

    state Active {
        [*] --> Generating
        Generating --> ValidatingLayer1 : combination produced
        ValidatingLayer1 --> DuplicateCheck : valid
        ValidatingLayer1 --> Generating : invalid — regenerate
        DuplicateCheck --> SavedToPicks : unique
        DuplicateCheck --> Generating : duplicate — regenerate
        SavedToPicks --> Generating : Generate Another
    }
```

---

##  7. State Machine — Notification Decision

```mermaid
stateDiagram-v2
    [*] --> Idle

    Idle --> PreDrawCheck : Mon/Thu at 19:00 local

    PreDrawCheck --> HighJackpotReminder : Jackpot validated ≥ €100M
    PreDrawCheck --> StandardReminder : Jackpot < €100M\nor unverified

    HighJackpotReminder --> Sent : Push dispatched
    StandardReminder --> Sent : Push dispatched

    Sent --> WaitingForDraw : Awaiting draw completion

    WaitingForDraw --> ValidatingNumbers : Draw data received

    ValidatingNumbers --> PublishResults : Numbers valid
    ValidatingNumbers --> WaitingForDraw : Invalid — retain existing data

    PublishResults --> ResultsAvailableSent : Results Available push dispatched
    ResultsAvailableSent --> WaitingForPrize : Awaiting prize breakdown

    WaitingForPrize --> ValidatingPrize : Prize data received
    ValidatingPrize --> CheckJackpotWinners : Prize valid
    ValidatingPrize --> Idle : Invalid — no jackpot notification

    CheckJackpotWinners --> JackpotWonSent : 5+2 Winners >= 1
    CheckJackpotWinners --> Idle : Winners = 0 — no notification

    JackpotWonSent --> Idle : Cycle complete
```

---

##  8. Deployment Diagram

```mermaid
graph LR
    subgraph UserDevices["User Devices"]
        iOS[iPhone\niOS App\nFlutter]
        Android[Android Phone\nAndroid App\nFlutter]
    end

    subgraph Cloud["Cloud Infrastructure"]
        LB[Load Balancer\nNginx / Cloudflare]
        API1[API Server 1]
        API2[API Server 2]
        ScraperSvc[Scraper Service\nCron Scheduler]
        AdminSvc[Admin Panel\nluckypick.eu/admin]
        PG[(PostgreSQL\nDraw History + Users\n+ Subscriptions)]
        Redis[(Redis\nStats Cache)]
        S3[Object Storage\nShared Card Assets]
    end

    subgraph PushGateways["Push Gateways"]
        FCMSvc[Firebase Cloud\nMessaging]
        APNsSvc[Apple Push\nNotification Service]
    end

    subgraph StoreInfra["Store Infrastructure"]
        AppStoreSvc[Apple App Store\nStoreKit 2]
        PlaySvc[Google Play\nBilling]
    end

    iOS <-->|HTTPS REST| LB
    Android <-->|HTTPS REST| LB
    LB --> API1
    LB --> API2
    API1 <--> PG
    API1 <--> Redis
    API2 <--> PG
    API2 <--> Redis
    ScraperSvc --> PG
    ScraperSvc --> FCMSvc
    ScraperSvc --> APNsSvc
    AdminSvc --> PG

    iOS <--> FCMSvc
    Android <--> FCMSvc
    iOS <--> APNsSvc

    iOS <-->|IAP| AppStoreSvc
    Android <-->|IAP| PlaySvc
    API1 <-->|Receipt verify| AppStoreSvc
    API1 <-->|Receipt verify| PlaySvc

    S3 <--> iOS
    S3 <--> Android
```
