# Privacy Policy for tabDelta

**Last Updated:** May 2026  
**Author:** Ogroprojukti  
**Project Context:** Local-First Browser Performance Profiler & Task Manager

---

## 1. Core Privacy Philosophy: Local-First
tabDelta is built from the ground up to respect user privacy. Unlike traditional productivity tools that monitor user behavior via cloud tracking platforms, tabDelta operates under a strict **local-first** architecture. 

* **Zero Cloud Transmission:** The extension does not use external cloud servers, maintains no remote user accounts, and never sends your browsing patterns, URLs, or system telemetry data across the internet.
* **No Data Selling or Brokerage:** Because your data never leaves your personal device, it is physically impossible for us to collect, sell, lease, or distribute your information to advertising companies, third-party data brokers, or analytics networks.

---

## 2. Telemetry and Data Collection
To power the live dashboard metrics and historical productivity reports, the extension collects local telemetry packets every **2 seconds** while a tab is active. This data includes:

* **Engagement & Attention Metrics:** Aggregate counts of passive keyboard events, mouse movement magnitudes (pixels shifted), and page scrolling velocities to compute an active "Attention Score".
* **Performance Telemetry:** Live JavaScript heap allocation size (`performance.memory`), active DOM element counts, and resource entry counts to locate browser resource issues.
* **Navigation Tracking:** Page visibility state (`document.hidden`), session tab lifecycles, and page location paths.

---

## 3. URL Sanitization Mechanism
To guarantee that sensitive inline data (such as temporary password reset tokens, security keys, or private form inputs passed via a URL string) is never preserved, tabDelta automatically passes all target web paths through a sanitization filter before committing them to your database. 
* All processed strings are immediately stripped down to their clean base structural origin and routing path: `origin + pathname`.
* **Query strings (`?query=text`) and hash anchors (`#fragment`) are explicitly dropped and are never saved.**

---

## 4. Local Storage and Automated Retention Limits
All telemetry logs and performance data packets are structured locally using an on-device IndexedDB wrapper database (`tabDeltaDB`). 

To prevent your storage framework from infinitely expanding and consuming local disk storage space, the architecture executes an automated cleanup script:
* **90-Day Rolling Purge:** A background job triggers automatically every 6 hours to permanently delete raw activity entries, logs, and site metrics that are older than 90 days.
* **Manual Deletion Control:** Users retain absolute data ownership. You can completely wipe the internal storage state instantly using the **"Clear Data"** module in the extension settings tab, or by standard uninstallation of the extension from your browser.

---

## 5. Justification of Chrome Extension Permissions
tabDelta utilizes several advanced Chrome platform permissions. They are strictly restricted to local-only functions to deliver performance diagnostics:

* **`tabs` / `activeTab`:** Used to map out active browsing windows, compute active foreground timeline blocks, and focus specific tabs from your warning alerts.
* **`storage` / `unlimitedStorage`:** Used to save your custom UI configurations and give the database room to hold your rolling 90-day time-series telemetry.
* **`offscreen`:** Spawns a background worker thread to process analytical data structures and database entry transactions away from your active tab thread, preventing UI lag.
* **`scripting`:** Used to securely place the local, passive telemetry capture scripts into target web pages.
* **`alarms`:** Triggers regular background cycles to write telemetry blocks and clean up old data entries.
* **`notifications`:** Pushes system desktop alerts when a background tab crosses your custom high-RAM or bandwidth warning limits.
* **`webRequest` & `<all_urls>`:** Evaluates response headers locally to track real-time network download and upload bandwidth consumption per tab. No payload content is inspected or recorded.

---

## 6. Compliance and Policy Assurances
This policy explicitly certifies compliance with the Google Chrome Web Store Developer Program Policies regarding User Data privacy. All processed information remains securely locked within your local profile boundaries on your machine.