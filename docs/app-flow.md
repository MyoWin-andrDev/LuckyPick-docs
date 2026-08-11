#  Application Flow

Complete user journey maps for every major flow in LuckyPick EuroMillions.

---

##  1. First Launch & Onboarding

```mermaid
flowchart TD
    A([App Installed]) --> B[Splash Screen\nLuckyPick Branding ~1s]
    B --> C[Welcome Screen\n+ Legal Disclaimer]
    C --> D{Language\nAuto-Detected?}
    D -->|Yes| E[Apply Detected Language]
    D -->|No| F[Default Language\nUser selects later in Settings]
    E --> G[GET STARTED Button]
    F --> G
    G --> H[Notification Permission\nPre-prompt explanation]
    H --> I{User Grants\nPermission?}
    I -->|Allow| J[Permissions Granted]
    I -->|Decline| K[Proceed — notifications\nnot required for use]
    J --> L[Home Screen]
    K --> L
```

!!! note "Rules"
    - No mandatory account creation.
    - No immediate paywall on launch.
    - Legal disclaimer always visible at the bottom of the Welcome Screen.

---

##  2. Free User Daily Generation Flow

```mermaid
flowchart TD
    A([User Opens App]) --> B[Home Screen]
    B --> C{Free picks\nremaining today?}
    C -->|1–3 remaining| D[GENERATE MY NUMBERS]
    C -->|0 remaining| E[Limit Message:\nYou've used your 3 free\nLucky Picks for today]

    D --> F[Quick Pick / Random\nGeneration Engine]
    F --> G[Validate: 5 unique 1–50\n+ 2 unique Lucky Stars 1–12]
    G --> H{Valid?}
    H -->|No| F
    H -->|Yes| I[Display Result\n1–1.5s animation]
    I --> J[Decrement counter\n e.g. 2 free picks remaining]
    J --> K{User Action}
    K -->|ADD TO MY PICKS| L[Saved to Active Set]
    K -->|GENERATE AGAIN| F
    K -->|SHARE| M[Social Share Flow]

    E --> N[UNLOCK PREMIUM\nButton visible]
    N --> O[Premium Screen]
    O -->|Purchased| P[Unlimited Generations Unlocked]
    O -->|Back / Cancel| Q[Other free areas remain available]
    Q --> R[Next local calendar day\n→ counter resets to 3]
```

---

##  3. Premium Discovery & Purchase Flow

```mermaid
flowchart TD
    A([Trigger]) --> B{Entry Point}
    B -->|Home| C[Discover Premium Banner]
    B -->|Lucky Mode tap| D[Mode Description Screen]
    B -->|3 picks used| E[Limit Reached Screen]
    B -->|More → Premium| F[Settings Menu]

    C --> G[Premium Screen]
    D --> G
    E --> G
    F --> G

    G --> H[Choose Plan:\nMonthly €8.99\nYearly €79.99 BEST VALUE\nLifetime €179.99]
    H --> I[CONTINUE WITH SELECTED PLAN]
    I --> J[Official iOS / Android\nPurchase Flow]
    J --> K{Purchase Result}

    K -->|Success| L[WELCOME TO LUCKYPICK PREMIUM\nPremium active immediately]
    K -->|Failed / Cancelled| M[Neutral message\nReturn to previous screen]

    L --> N[Return to Feature\nthat triggered purchase]
    N --> O[All 10 Lucky Modes unlocked\nUnlimited generations\nAdvanced Statistics]
```

!!! warning "Critical Rules"
    - No free trial at launch.
    - No aggressive retry paywalls after a failed purchase.
    - Existing My Picks and Saved Sets are **never** deleted during the premium flow.
    - Yearly plan marked **BEST VALUE** — MOST POPULAR only once genuine data confirms it.

---

##  4. Lucky Mode Generation Flow (General)

```mermaid
flowchart TD
    A([Lucky Modes Tab]) --> B{User Tier}
    B -->|Free| C[All 10 modes visible\nPremium modes gold-labelled]
    B -->|Premium| D[All 10 modes accessible]

    C --> E{Select Mode}
    E -->|Free mode tapped| F[Mode Description shown]
    F --> G[UNLOCK WITH PREMIUM → Premium Flow]
    D --> H{Select Mode}

    H --> I[Enter / Select Mode Input\ne.g. pet name, birthday, zodiac sign]
    I --> J[GENERATE MY LUCKY NUMBERS]
    J --> K[Mode-Specific Algorithm\n+ Controlled Randomness]
    K --> L[Immediate Exclusion\nselected numbers removed from pool]
    L --> M[Validation Layer 1\n5 unique 1–50, 2 unique 1–12]
    M --> N{Valid?}
    N -->|No| K
    N -->|Yes| O[Full-Combination Duplicate Check\nagainst current session / My Picks]
    O --> P{Duplicate?}
    P -->|Yes| K
    P -->|No| Q[Display Result Screen\nwith 1–1.5s animation]
    Q --> R{User Action}
    R -->|ADD TO MY PICKS| S[Validation Layer 2\nbefore save]
    R -->|GENERATE AGAIN| K
    R -->|CHOOSE ANOTHER MODE| T[Return to Lucky Modes\nMy Picks preserved]
    R -->|CHANGE DETAILS| U[Re-enter mode input]
    R -->|SHARE| V[Social Share Flow]
    S --> W[Added to Active Set ✓\nUp to 12 per set]
    W --> X{Set full?\n12 combinations}
    X -->|No| R
    X -->|Yes| Y[SET COMPLETE\nSTART NEW SET]
    Y --> Z[Current set archived\nto Saved Sets]
    Z --> AA[New empty set begins]
```

---

##  5. Individual Lucky Mode Input Flows

=== "Birthday Mode"
    ```mermaid
    flowchart LR
        A[Enter Name/Nickname\noptional] --> B[Enter Date of Birth\nDay + Month + Year]
        B --> C[Birthday transformed to\ninternal numerical profile\nnot raw day/month values]
        C --> D[Profile seeds\nfull 1–50 range available]
        D --> E[Generate 5+2\nwith entropy filler if needed]
    ```

=== "Horoscope Mode"
    ```mermaid
    flowchart LR
        A[Enter Day + Month only\nno birth year] --> B[LuckyPick determines\nZodiac Sign automatically]
        B --> C[Each sign has its own\nnumerical profile/seed]
        C --> D[Controlled randomness\nprovides variation]
        D --> E[Generate 5+2]
    ```

=== "Pet Mode"
    ```mermaid
    flowchart LR
        A[Enter Pet Name] --> B[Select Animal Type\nDog · Cat · Bird · Horse\nRabbit · Fish · Other]
        B --> C[Name + Type form\npersonal profile]
        C --> D[Generate 5+2]
        D --> E{More pets?}
        E -->|CHANGE PET| A
        E -->|Generate Again| D
    ```

=== "Family Mode"
    ```mermaid
    flowchart TD
        A[Add Family Member\nRelationship + Name + DOB] --> B{Add more?}
        B -->|+ADD FAMILY MEMBER| A
        B -->|Done| C[All members form\ncollective profile]
        C --> D[Generate 5+2]
        D --> E{Action}
        E -->|EDIT FAMILY| A
        E -->|START NEW FAMILY| F[New family profile]
        E -->|Generate Again| D
    ```

=== "Lucky Color Mode"
    ```mermaid
    flowchart LR
        A[Display 10 colour circles\nBlue·Gold·Red·Green·Purple\nOrange·Pink·White·Black·Turquoise] --> B{Select}
        B -->|Pick one| C[Selected colour has\nits own numerical profile]
        B -->|SURPRISE ME| D[Random colour chosen\nuses that colour's profile]
        C --> E[Generate 5+2\nBall colours unchanged]
        D --> E
    ```

=== "Lucky Number Mode"
    ```mermaid
    flowchart LR
        A[Enter 1–3 Lucky Numbers\neach between 1–50] --> B[Selected numbers\nare MANDATORY in every combination]
        B --> C[Insert lucky numbers first\nExclude from remaining pool]
        C --> D[Generate remaining\n4/3/2 Main Numbers\nfrom 1–50 excl. selected]
        D --> E[Generate 2 Lucky Stars\nfrom 1–12 independently]
        E --> F[Valid 5+2 Result]
    ```

=== "Hot / Cold / Trending"
    ```mermaid
    flowchart TD
        A[100-draw rolling DB] --> B{Mode}
        B -->|Hot| C[Top 10 Main Numbers\nTop 4 Lucky Stars]
        B -->|Cold| D[Bottom 10 Main Numbers\nBottom 4 Lucky Stars]
        B -->|Trending| E[Latest 20 vs Latest 100\nTop 10 upward movers\nTop 4 Lucky Stars movers]

        C --> F[3 from Hot Pool\n+ 2 from remaining 40\n1 from Hot Stars\n+ 1 from remaining 8]
        D --> G[3 from Cold Pool\n+ 2 from remaining 40\n1 from Cold Stars\n+ 1 from remaining 8]
        E --> H[3 Trending Main\n+ 2 remaining\n1 Trending Star\n+ 1 remaining]

        F --> I[Controlled distribution\nto avoid excessive repetition]
        G --> I
        H --> I
        I --> J[Valid 5+2 Result]
    ```

=== "Smart Mix Mode"
    ```mermaid
    flowchart TD
        A[No personal input required] --> B[Step 1: Pick 1 Hot Number → exclude it]
        B --> C[Step 2: Pick 1 Cold Number → exclude both]
        C --> D[Step 3: Pick 1 Trending Number\nexclude used; skip if already selected]
        D --> E[Step 4: Pick 1 Random Number\nfrom remaining pool]
        E --> F[Step 5: Pick 1 Random Number\nfrom remaining pool]
        F --> G[Result: 1 Hot + 1 Cold + 1 Trending + 2 Random]
        G --> H[Lucky Stars:\n1 Statistical Star Hot/Cold/Trending\n+ 1 Random Star\nwith immediate exclusion]
        H --> I[Valid 5+2 Result]
    ```

---

##  6. My Picks Management Flow

```mermaid
flowchart TD
    A([MY PICKS Screen]) --> B{Active Set Status}
    B -->|Empty| C[MY PICKS\nNo combinations yet\nCREATE YOUR FIRST LUCKY PICK]
    B -->|1–11 combinations| D[List with mode labels\ne.g. Pet - Charlie, Horoscope - Leo]
    B -->|12 combinations| E[SET COMPLETE\nSTART NEW SET]

    D --> F{Per-combination ••• menu}
    F -->|REPLACE COMBINATION| G[Generate new using\noriginal Mode config snapshot\nValidate → Replace only if valid]
    F -->|REMOVE COMBINATION| H[Confirm: CANCEL / REMOVE\nOnly that combination removed]
    F -->|SHARE LUCKYPICK| I[Social Share Flow\nmode shown, numbers hidden]

    D --> J[START NEW SET]
    J --> K[Archive current set → SAVED SETS\nNew empty active set begins]

    L([SAVED SETS]) --> M[Archived sets by date\ne.g. 8 Aug 2026 – 6 combinations]
    M --> N[Open set: view combinations\nwith mode labels]
```

!!! info "Core Rule"
    Once saved, a combination is **never** changed automatically. Only explicit `REPLACE COMBINATION` or `REMOVE COMBINATION` can modify it.

---

##  7. Results & Draw History Flow

```mermaid
flowchart TD
    A([Results Tab]) --> B[Latest draw displayed immediately\nDraw Date + 5 Main + 2 Stars]
    B --> C[Prize Breakdown shown below\nall available prize tiers]
    C --> D{Prize data available?}
    D -->|Yes| E[Show: Tier · Amount · Winners]
    D -->|No — pending| F[Prize information pending]
    F --> G[Winning numbers still shown\nPrize auto-updates when validated]

    B --> H[DRAW HISTORY Button]
    H --> I[List: latest 100 draws\nnewest first]
    I --> J[Select any draw]
    J --> K[Draw Detail Screen\nDate + 5+2 + Prize Breakdown]
    K --> L[← Back to Draw History]
```

---

##  8. Notification Decision Flow

```mermaid
flowchart TD
    A([Monday / Thursday 19:00 local]) --> B[Backend: check upcoming jackpot]
    B --> C{Jackpot validated\n≥ €100M?}
    C -->|Yes| D[High Jackpot Draw Reminder\n€XXX million EuroMillions\njackpot tomorrow]
    C -->|No or unverified| E[Standard Draw Reminder\nEuroMillions draw tomorrow]
    D --> F[Tap → Combination Generation]
    E --> F

    G([After Draw — Tue/Fri]) --> H[Scraper retrieves draw data]
    H --> I[Validate: 5 unique 1–50\n2 unique 1–12\ncorrect draw date\nno duplicate draw]
    I --> J{Valid?}
    J -->|No| K[Keep existing 100 draws\nDo not remove oldest\nShow ATTENTION REQUIRED]
    J -->|Yes| L[Publish Results\nUpdate 100-draw DB\nRecalculate Stats]
    L --> M[Results Available Notification\nThe latest EuroMillions\nresults are available]
    M --> N[Tap → Results page for this draw]

    L --> O[Wait for Prize Breakdown]
    O --> P{5+2 Winners ≥ 1?}
    P -->|Yes| Q[Jackpot Won Notification\nEuroMillions jackpot won\nView the draw results]
    P -->|No| R[No jackpot notification\nResults Available still sent]
    Q --> S[Tap → Results page for exact draw]
```

!!! warning "Hard Limits"
    - Maximum **3 notifications per draw**: 1 Draw Reminder + 1 Results Available + 1 Jackpot Won.
    - Standard two-draw week: maximum **6 notifications total**.
    - `€100M+` Reminder **replaces** the Standard Reminder — never creates a second pre-draw notification.

---

##  9. Social Sharing Flow

```mermaid
flowchart TD
    A([SHARE Button tapped]) --> B[LuckyPick auto-creates\nbranded promotional card]
    B --> C[Card contents:\nLuckyPick logo\nLucky Mode used\nCall to action\nNo actual numbers]
    C --> D[Select Sharing Platform\nWhatsApp · Facebook · Messenger\nInstagram · TikTok · X · Telegram]
    D --> E[System share sheet]
    E --> F[Shared!]
    F --> G[Return to current result\nGenerated combination preserved\nMy Picks preserved]

    H([Recipient taps LuckyPick link]) --> I{App installed?}
    I -->|Yes| J[Open LuckyPick directly]
    I -->|No| K[Open App Store / Google Play\nLuckyPick listing]
```

!!! danger "Privacy — Absolute Rule"
    Shared content must **never** include: generated Main Numbers, Lucky Stars, pet names, birth dates, names, family info, Lucky Numbers entered, or My Picks combinations. Only the Lucky Mode name may be displayed.

---

##  10. Backend Automation Pipeline

```mermaid
flowchart TD
    A([Tuesday / Friday 20:45 CET]) --> B[Scraper Cron Job fires]
    B --> C[Fetch from Belgian National Lottery\nprimary official source]
    C --> D{Data Retrieved?}
    D -->|No| E[Retry / Fallback source]
    E --> F{Retrieved?}
    F -->|No| G[ATTENTION REQUIRED alert\nOwner notified\nExisting 100 draws intact]
    F -->|Yes| H
    D -->|Yes| H[Validate Draw Data]
    H --> I{Passes validation?\n5 unique 1–50\n2 unique 1–12\ncorrect date, no duplicate}
    I -->|No| J[Do NOT publish\nDo NOT remove oldest draw\nAlert owner]
    I -->|Yes| K[Add new draw to DB]
    K --> L[Remove oldest draw\nMaintain exactly 100 draws]
    L --> M[Update Draw History]
    L --> N[Update Prize Information]
    L --> O[Update Jackpot Information]
    L --> P[Recalculate Statistics\nHot · Cold · Trending · Frequency]
    M --> Q[Publish to App]
    N --> Q
    O --> Q
    P --> Q
    Q --> R[Send Results Available notification]
    R --> S{Jackpot won?}
    S -->|Yes - validated| T[Send Jackpot Won notification]
    S -->|No| U[Done for this draw]
    T --> U
```
