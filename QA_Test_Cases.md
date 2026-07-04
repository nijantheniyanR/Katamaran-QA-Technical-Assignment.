# QA Test Case Document: Tichi App

This document outlines the test cases designed to verify the core functionalities, usability, and robustness of the **Tichi Mobile Application**.

---

## 🛠 Test Cases

### Module 1: User Authentication & Profile Management

#### TC_AUTH_001: User Registration with Valid Details
- **Description:** Verify that a new user (Client or Service Provider) can successfully register using a valid email, mobile phone number, and SMS OTP.
- **Pre-conditions:**
  - The app is installed and launched for the first time.
  - The user has access to a working mobile phone number to receive OTP.
- **Test Steps:**
  1. Open the Tichi app.
  2. Tap on **"Sign Up"**.
  3. Enter a valid name, email address, mobile phone number, and select role as **"Service Provider"**.
  4. Tap on **"Send OTP"**.
  5. Enter the 6-digit OTP received via SMS.
  6. Tap on **"Verify & Register"**.
- **Expected Result:**
  - OTP is verified successfully.
  - User is registered and navigated to the **Profile Setup** screen.
  - User account database entry is created with status "Verified".
- **Priority:** High
- **Severity:** Critical
- **Status:** Pass

#### TC_AUTH_002: Profile Portfolio Character Limits and Input Validation (BVA)
- **Description:** Verify that the "Bio" and "Skills Description" text areas enforce character limits (Min: 20 characters, Max: 500 characters).
- **Pre-conditions:**
  - User is logged in and is on the **Edit Profile** screen.
- **Test Steps:**
  1. Navigate to **Profile > Edit Profile**.
  2. In the "Bio" section, input a short description containing only 10 characters (e.g., `"I paint."`) and tap **"Save"**.
  3. Verify the validation message.
  4. Input a very long description containing 501 characters and tap **"Save"**.
  5. Verify the validation message or truncation.
  6. Input a valid bio containing exactly 250 characters and tap **"Save"**.
- **Expected Result:**
  - Step 2: The app displays an error: `"Bio must be at least 20 characters long."`
  - Step 4: The app either truncates the input at 500 characters or displays: `"Bio cannot exceed 500 characters."`
  - Step 6: Profile is updated successfully and saved without error.
- **Priority:** Medium
- **Severity:** Major
- **Status:** Pass

---

### Module 2: Requirement Posting & Marketplace Feed

#### TC_POST_001: Create Task Requirement - Empty Fields (Negative Test)
- **Description:** Verify that a Client cannot publish a task requirement post with empty mandatory fields (Title, Description, Location).
- **Pre-conditions:**
  - User is logged in as a **Client**.
- **Test Steps:**
  1. Tap on the **"+" (Create Post)** icon on the home screen.
  2. Leave the "Title" and "Description" fields blank.
  3. Enter a location and budget.
  4. Tap **"Publish Post"**.
- **Expected Result:**
  - The requirement is not published.
  - Red error highlights appear under the blank fields indicating `"Title is required"` and `"Description is required"`.
- **Priority:** High
- **Severity:** Major
- **Status:** Pass

#### TC_POST_002: Create Task Requirement - Maximum Budget Edge Case (BVA)
- **Description:** Verify that the system accepts and correctly renders a task requirement with the maximum allowable budget limit ($10,000) and long descriptive terms.
- **Pre-conditions:**
  - User is logged in as a **Client**.
- **Test Steps:**
  1. Tap on the **"+" (Create Post)** icon.
  2. Enter title: `"Complete Villa Interior Renovation & Painting"`.
  3. Enter description: A valid detailed summary of 400 characters detailing requirements.
  4. Enter budget: `10000` (Max limit).
  5. Select Location and tap **"Publish Post"**.
- **Expected Result:**
  - Requirement is successfully published.
  - The marketplace feed correctly displays the post showing the budget formatted as `"$10,000"`.
- **Priority:** Medium
- **Severity:** Medium
- **Status:** Pass

---

### Module 3: SMI Match Engine & Notifications

#### TC_SMI_001: Verify SMI Keyword Matching and Profile Fit Scoring
- **Description:** Verify that the Social Media Intelligence (SMI) matching system properly maps a new task post to providers based on matching skill tags and geographical proximity.
- **Pre-conditions:**
  - Provider A has skill tag: `Plumbing` and location: `Downtown Austin`.
  - Provider B has skill tag: `Graphic Design` and location: `Downtown Austin`.
- **Test Steps:**
  1. Login as Client.
  2. Create a new task requirement: `"Emergency pipe repair for kitchen leak"`.
  3. Set location: `"Downtown Austin"`.
  4. Tap **"Publish"**.
  5. Check matched listings for Provider A and Provider B.
- **Expected Result:**
  - Provider A (Plumber) receives a push notification: `"New matching job found near you!"`.
  - The job appears in Provider A's "Matches" tab with a high matching score.
  - Provider B (Graphic Designer) does not receive any match notification or listing.
- **Priority:** High
- **Severity:** Critical
- **Status:** Pass

---

### Module 4: Connection Fee Payments & Contact Unlocking

#### TC_CONN_001: Attempting to Unlock Client Contact without Payment (Security Test)
- **Description:** Verify that a Service Provider cannot view or unlock a Client's phone number/chat before paying the connection fee.
- **Pre-conditions:**
  - A Service Provider has matched with a Client's task post.
  - The connection fee has not been paid yet.
- **Test Steps:**
  1. Login as the Service Provider.
  2. Open the matched task detail screen.
  3. Locate the "Client Contact Details" section.
  4. Attempt to click on the masked phone number or the "Start Chat" button.
- **Expected Result:**
  - Phone number is masked (e.g., `+1 ***-***-5678`).
  - Tapping "Start Chat" or the phone number triggers a payment modal: `"Pay connection fee ($1.99) to unlock contact details."`
  - Access to raw contact details is blocked on the API level.
- **Priority:** High
- **Severity:** Critical
- **Status:** Pass

#### TC_CONN_002: Successful Connection Fee Payment and Contact Unlocking
- **Description:** Verify that paying the connection fee successfully unlocks the Client's contact details and opens the chat channel.
- **Pre-conditions:**
  - Provider is on the payment modal for a matched requirement.
- **Test Steps:**
  1. Choose payment method: **"Credit/Debit Card"**.
  2. Input valid payment details.
  3. Tap **"Pay $1.99"**.
  4. Wait for transaction approval.
- **Expected Result:**
  - Transaction succeeds.
  - A success animation is shown.
  - The Client's actual contact number is revealed (e.g., `+1 512-555-0199`).
  - The "Start Chat" button is enabled and takes the provider to the direct chat screen.
- **Priority:** High
- **Severity:** Critical
- **Status:** Pass

---

### Module 5: Real-time Chat & In-App Messaging

#### TC_CHAT_001: Direct Message Exchange in Active Chat
- **Description:** Verify that text messages are exchanged in real-time between Client and Provider with read receipts.
- **Pre-conditions:**
  - A connection has been paid for and unlocked.
  - Both Client and Provider are online.
- **Test Steps:**
  1. Client opens the chat screen with Provider.
  2. Client types `"Hello, are you available tomorrow at 9 AM?"` and clicks send.
  3. Observe Provider's screen.
  4. Provider reads the message.
- **Expected Result:**
  - The message is received on the Provider's device in <1 second.
  - A single checkmark appears on Client's screen when sent.
  - A double checkmark (or read receipt indicator) appears on Client's screen when Provider opens the chat.
- **Priority:** High
- **Severity:** Major
- **Status:** Pass

#### TC_CHAT_002: Network Disconnection & Reconnection During Messaging (Robustness Test)
- **Description:** Verify that messages sent while offline are queued and auto-sent when internet connection is restored.
- **Pre-conditions:**
  - An active chat is open.
- **Test Steps:**
  1. Turn off Wi-Fi and Mobile Data on the Client's device (simulating offline state).
  2. Type a message `"Let's confirm the deal."` and click send.
  3. Observe the sending status.
  4. Turn Wi-Fi back on.
  5. Wait for the connection to re-establish.
- **Expected Result:**
  - While offline, the message is marked with a clock icon (pending status).
  - Once connection is restored, the message is automatically sent without user action.
  - The message is successfully received by the Provider.
- **Priority:** Medium
- **Severity:** Major
- **Status:** Pass

---

### Module 6: Review & Rating System

#### TC_REV_001: Rating Submission and Average Recalculation
- **Description:** Verify that a Client can submit a 1 to 5-star rating with text review for a completed provider, and the provider's average score updates correctly.
- **Pre-conditions:**
  - A task is marked as "Completed".
  - Provider's current rating is 4.0 stars (based on 1 review of 4.0 stars).
- **Test Steps:**
  1. Login as Client.
  2. Navigate to the completed task screen.
  3. Tap **"Leave a Review"**.
  4. Select **5 stars** and type: `"Excellent, on-time service!"`.
  5. Tap **"Submit Review"**.
  6. Navigate to the Provider's profile page and check average rating.
- **Expected Result:**
  - Review is successfully saved.
  - The Provider's profile average rating is recalculated to **4.5 stars** (average of 4.0 and 5.0).
  - The text review appears under their "Reviews" tab.
- **Priority:** High
- **Severity:** Major
- **Status:** Pass
