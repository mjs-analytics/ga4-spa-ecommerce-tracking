# ga4-spa-ecommerce-tracking
Anonymized analytics project showcasing GA4 ecommerce tagging for SPA

# GA4 Ecommerce Tracking for Single-Page Application (SPA)

👋 Hi! I'm Megan Simmons — an analytics professional with 10+ years of experience designing full-funnel data solutions across marketing, web, and CRM ecosystems. This project showcases how I implemented GA4 ecommerce tracking on a single-page application (SPA), using Google Tag Manager and a custom dataLayer structure.

> ⚠️ This project is anonymized and uses mock data and generalized workflows to protect company confidentiality.

---

## 📈 Business Context

This project supported a high-traffic ecommerce platform where marketing campaigns drove significant ad spend and seasonal promotions. Inaccurate or incomplete tracking due to the SPA architecture and legacy scripts made it difficult to evaluate product performance, conversion steps, and ROI across paid media. Ensuring full-funnel visibility and data integrity was critical to drive optimization and budget allocation decisions.

---

## 🔍 Project Overview

**Challenge:**  
Traditional Google Analytics tracking fails in SPAs because there's no full-page reload — meaning core ecommerce events like product views and add-to-cart actions often go untracked.

Additionally, we encountered a major blocker: the `items` array in the ecommerce dataLayer was misconfigured due to a front-end bug. Since the next code release was weeks away, we needed a workaround to fix event integrity in the interim.

**Goal:**  
Track ecommerce behavior (product views, add-to-cart, checkout, and purchases) accurately in GA4 for 100% of traffic on an SPA ecommerce site.

---

## 🛠️ Tools & Technologies

- Google Tag Manager (GTM)
- Google Analytics 4 (GA4)
- JavaScript & Data Layer
- Chrome DevTools
- Single-Page Application framework (e.g., React or Vue-based)

---

## 🔧 Key Implementation Steps

1. **Designed the dataLayer** for all ecommerce actions: `view_item`, `add_to_cart`, `begin_checkout`, `purchase`
2. **Configured GTM tags** to trigger on virtual page transitions and button interactions
3. **Mapped custom events** to GA4's recommended ecommerce schema
4. **Validated events** using GA4 DebugView and real-time reporting

---

## 🛠 Temporary Workaround: Fixing the `items` Array via GTM

Because the front-end SPA did not push a properly formatted `items` array and the dev team could not fix it until the next release, I implemented a short-term solution in GTM:

- Created a **Custom JavaScript Variable** that extracted legacy Universal Analytics-style data from `ecommerce.purchase.products`, parsed and cleaned the data, and transformed it into a GA4-compliant `items` array
- Specifically, the `price` field required cleanup — it was often inflated by a factor of one million due to a known serialization bug. The variable parsed the string, validated numeric formatting, and divided the value by 1,000,000 before mapping to the GA4 schema
- Used **Regex-based triggers** to conditionally fire ecommerce tags only when the corrected data was available
- Set up a **Custom Event listener** to manually push corrected product details if the built-in `add_to_cart` event failed schema validation
- Documented the temporary patch and worked with developers to deploy the fix in the next SPA release

This workaround preserved GA4 event integrity and enabled accurate reporting even during the broken state.

---

## 🔄 Phase 2: Schema Alignment and Legacy Cleanup

After stabilizing tracking via GTM workarounds, I conducted a full audit of the site’s tracking scripts and discovered legacy **UA** (`analytics.js`) and **gtag.js** code still embedded on several routes. This caused duplicate or conflicting dataLayer structures that disrupted GA4 tracking and polluted ecommerce event payloads.

**Importance of Removing Legacy Analytics Code:**  
Maintaining legacy analytics scripts alongside newer platforms like GA4 can significantly degrade website performance by increasing page load times and causing conflicts that result in data inaccuracies. Additionally, redundant scripts create unnecessary complexity and risk data duplication or tracking inconsistencies. Removing outdated analytics code streamlines performance and ensures cleaner, more reliable analytics data.

**Resolution Steps:**
- Coordinated with engineering to **fully remove UA and gtag.js scripts** from the codebase
- Rebuilt the ecommerce tracking system from the ground up using **GTM + GA4 only**
- Replaced the old `ecommerce.purchase` schema with **GA4-native `ecommerce` format**, aligning with Google’s official Enhanced Measurement standards
- Tested against GA4’s schema validator and confirmed alignment for all event types: `view_item`, `add_to_cart`, `begin_checkout`, `purchase`

**Outcome:**
- Reduced event duplication and misfires across all major ecommerce actions
- Created a **scalable, GTM-based tagging system** for future expansion (promotions, refunds, upsell tracking)
- Increased trust in analytics reporting by consolidating around a modern, clean schema

---

## 📸 Project Diagrams

### GTM and GA4 Event Flowchart:
![GTM and GA4 Event Flowchart](images/ecommerce_flowchart.png)

### SPA Event Tracking Flow:
![SPA Event Tracking Flow](images/event_tracking_flowchart.png)

---

## ❓ FAQ & Common Pitfalls

**Q: What common issues arise when implementing GA4 on SPAs?**  
A: Common issues include incomplete or inaccurate event tracking due to virtual pageviews, legacy script conflicts, and misconfigured dataLayer schemas.

**Q: How can I avoid tracking conflicts?**  
A: Fully audit and remove legacy tracking scripts before implementing new GTM and GA4 tracking.

**Q: Where can I find GA4 ecommerce guidelines?**  
A: Google's official GA4 ecommerce documentation can be found [here](https://support.google.com/analytics/answer/9268036?hl=en).

**Q: What are best practices for using GTM with GA4?**  
A: Detailed best practices can be accessed in Google's Tag Manager Help Center [here](https://support.google.com/tagmanager/answer/6102821?hl=en).

---

## 📬 Contact

Feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/iheartscience) or reach out if you're hiring for analytics, product insights, or CRM strategy roles.

---
