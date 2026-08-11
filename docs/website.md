#  Landing Page Website & Smart Deep Links

While LuckyPick is primarily a mobile application for iOS and Android, the ecosystem includes a dedicated promotional landing page and smart deep linking system hosted at **`https://luckypick.eu`**.

---

##  1. Landing Page (`luckypick.eu`)

```

                    LuckyPick EuroMillions                   
                                                             
              The Smart EuroMillions Companion App           
                                                             
         [  Download on App Store ]   [  Get on Google Play ]
                                                             
   • Personalized Lucky Modes  • 13 Tier Automatic Ticket Checker 
   • 100-Draw Statistics       • 100% Ad-Free Experience      

```

* **Purpose:** Acts as the primary web landing page for app discovery, press, privacy policy, terms of service, and support.
* **Tech Stack:** Lightweight static HTML/CSS or MkDocs / Next.js static export.

---

##  2. Smart Deep Linking (`luckypick.eu/share/...`)

When users share a lucky combination link:

```
User clicks link: https://luckypick.eu/share/xyz123
                         
         
                                        
 [App Installed?]                [App NOT Installed?]
                                        
                                        
Open LuckyPick App              Open https://luckypick.eu
Show Generated Numbers          Display App Store / Play Store
in "My Picks"                   Download Buttons
```
