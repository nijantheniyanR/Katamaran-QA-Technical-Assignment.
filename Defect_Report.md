# Defect Report: Tichi App

This document catalogs the defects discovered during the testing phase of the **Tichi Mobile Application**.

---

## 📊 Defect Summary

| Defect ID | Summary | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- |
| **DF_001** | App crash during Google Pay checkout for connection fee on Android 14 | Critical | High | Open |
| **DF_002** | Push notification not triggered for new SMI-matched requirements | Major | High | Open |
| **DF_003** | "Clear All Filters" resets UI controls but fails to refresh the marketplace query | Medium | Medium | Open |
| **DF_004** | Long skill tags overflow parent container on narrow screens (e.g., iPhone SE) | Minor | Low | Open |

---

## 🐞 Detailed Defect Logs

### DF_001: App crash during Google Pay checkout for connection fee on Android 14
- **Defect ID:** DF_001
- **Severity:** Critical (Blocks payment flow, causes application crash)
- **Priority:** High (Directly impacts business revenue)
- **Environment:** Samsung Galaxy S23, Android 14 (API level 34), Tichi App v1.2.0
- **Prerequisites:** 
  - User has a matched requirement ready for connection.
  - Google Pay is configured on the device.
- **Steps to Reproduce:**
  1. Login to the app as a Service Provider.
  2. Navigate to **Matches** and select a matched client requirement.
  3. Tap **"Unlock Contact Details"**.
  4. In the payment dialog, select **"Google Pay"** as the payment method.
  5. Tap **"Pay $1.99"** to initiate checkout.
- **Expected Result:**
  - Google Pay bottom sheet should slide up, prompting the user to confirm the transaction.
- **Actual Result:**
  - The app freezes for 1.5 seconds, then immediately crashes to the home screen.
  - ADB logs show a `NullPointerException` inside the `com.albequu.tichi.payment.GooglePayGateway.initiateTransaction` method.
- **Workaround:** None (Users are forced to select Credit/Debit Card to complete payments).

---

### DF_002: Push notification not triggered for new SMI-matched requirements
- **Defect ID:** DF_002
- **Severity:** Major (Core SMI feature degraded)
- **Priority:** High (Reduces provider engagement and response speed)
- **Environment:** Multiple devices (Google Pixel 8 - Android 14, iPhone 15 - iOS 17), Tichi App v1.2.0
- **Prerequisites:**
  - Notification permissions are enabled in system settings for Tichi App.
- **Steps to Reproduce:**
  1. Register Provider A with skill tags: `Electrician` and location: `Seattle`.
  2. Login to a different device as Client B.
  3. Post a new requirement: `"Need immediate help with a blown fuse box in Seattle"`.
  4. Observe Provider A's phone for push notifications.
- **Expected Result:**
  - Provider A should receive a push notification within 5 seconds: `"New matching job: Blown fuse box in Seattle"`.
- **Actual Result:**
  - No push notification is triggered or displayed on Provider A's device.
  - *Note:* If Provider A manually opens the Tichi app and navigates to the **Matches** screen, the job correctly appears in the feed list.
- **Workaround:** Provider must manually refresh the matches feed.

---

### DF_003: "Clear All Filters" resets UI controls but fails to refresh the marketplace query
- **Defect ID:** DF_003
- **Severity:** Medium (Functional issue affecting user navigation)
- **Priority:** Medium (Stale results confuse users)
- **Environment:** iPhone 14 Pro, iOS 16.5, Tichi App v1.2.0
- **Steps to Reproduce:**
  1. Open the Marketplace Feed.
  2. Tap **"Filters"**, select category `"Car Cleaning"` and set distance limit to `"5 miles"`.
  3. Tap **"Apply"** (Feed correctly updates to show matching posts).
  4. Tap the **"Filters"** icon again.
  5. Tap **"Clear All Filters"**.
  6. Tap **"Apply"**.
- **Expected Result:**
  - Filter modal UI is cleared, and the marketplace feed updates to display the default unfiltered posts (all categories, default radius).
- **Actual Result:**
  - The filter checkboxes and slider are visually reset to defaults in the modal.
  - However, after clicking "Apply", the feed still displays only the filtered results (`"Car Cleaning"` at `"5 miles"`).
- **Workaround:** User must close and force-restart the app to clear active query filters.

---

### DF_004: Long skill tags overflow parent container on narrow screens (e.g., iPhone SE)
- **Defect ID:** DF_004
- **Severity:** Minor (Cosmetic / Layout issue)
- **Priority:** Low (Does not block functionality)
- **Environment:** iPhone SE (3rd Gen), iOS 17.2, Screen width: 375px, Tichi App v1.2.0
- **Steps to Reproduce:**
  1. Register a Service Provider profile.
  2. Add the skill tag: `"Air Conditioning & Ventilation Specialist"`.
  3. Navigate to **Profile > Preview Profile** on an iPhone SE or small screen emulator.
- **Expected Result:**
  - The long skill tag should wrap onto a new line or truncate cleanly (e.g. using ellipsis `...`) to stay within screen boundaries.
- **Actual Result:**
  - The skill tag extends beyond the right edge of the card container, clipping the text and overlapping the edit button next to it.
- **Workaround:** None.
