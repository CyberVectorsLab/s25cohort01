# ESP32 Cybersecurity Lab Guide

**for Cohort Members (CV_S2501)**
*Lean Foundations in Embedded Security & Communication*

## What You'll Learn

| Topic             | Objective                        |
| ----------------- | ------------------------------------- |
| ESP32 Programming | Control real embedded hardware        |
| MQTT Messaging    | Lightweight communication used in IoT |
| JSON Structuring  | Secure, readable data formatting      |
| HMAC Integrity    | Verify data hasn't been tampered with |
| Timestamp Checks  | Prevent replay attacks                |
| AES Encryption    | Learn data confidentiality (optional) |

---

## Overview of Exercises

| Exercise | Key Concept               | Outcome                                 |
| -------- | ------------------------- | --------------------------------------- |
| 1        | Structured JSON Messaging | Format and send valid MQTT messages     |
| 2        | HMAC Verification         | Secure message with a shared key        |
| 3        | Replay Detection          | Implement timestamp-based freshness     |
| 4+       | Encryption (Advanced)     | Optionally protect data confidentiality |

Each cohort member will develop and upload their own sketch on ESP32 using Arduino IDE and publish to their assigned MQTT topic using HiveMQ Cloud.

---

## Exercise 1 – JSON Message Format

**Goal**: Create and publish a JSON message to the MQTT topic `test/yourname`.

### What to Read (Use internet or our own Notion library)

* What is JSON format (objects, key-value pairs)
* What is MQTT and what is a "topic"
* How to connect ESP32 to WiFi and MQTT using Arduino IDE

### Message Structure

```json
{
  "student": "cohort_member_CV_S25",
  "exercise": "Intro_JSON",
  "msg": "Hello from CV S25",
  "timestamp": 1721234567
}
```

### ✅ Trainer/Instructor Will Check

* Is the JSON well-formed?
* Did it publish to the correct topic?
* Is the timestamp a valid number?

---

## Exercise 2 – Add HMAC

**Goal**: Secure your message using HMAC with a shared key (provided by trainer).

### What to Read

* What is HMAC and how it works (SHA256, secret key)
* Why HMAC helps detect tampering

### 🔐 Message Hint

Compute HMAC using only the `msg + timestamp` string. Example:

```json
{
  "student": "cohort_member_CV_S25",
  "exercise": "HMAC",
  "msg": "Sensor:OK",
  "timestamp": 1721234600,
  "hmac": "computed_value_here"
}
```

Use Arduino's `mbedtls` or `Crypto` libraries to generate the HMAC.

### ✅ Trainer/Instructor Will Check

* Is HMAC calculated using the correct key and input?
* Does calculated HMAC match trainer-side?
* Is timestamp fresh?

---

## Exercise 3 – Replay Protection

**Goal**: Prevent replay of old messages by incrementing timestamp on every publish.

### What to Read

* What are replay attacks?
* How timestamps can protect message freshness

### You Need to:

* Track your last timestamp in your sketch
* Ensure every new message has a later timestamp

### ✅ Trainer/Instructor Will Check

* Does your timestamp always increase?
* Does trainer detect a replay attempt?

---

## Optional Advanced Exercises

| Topic                          | Learn                                   |
| ------------------------------ | --------------------------------------- |
| AES-CBC Encryption             | Encrypt message body                    |
| CRC or SHA-256 Digest          | Add message digests for extra integrity |
| Diffie-Hellman Key Exchange    | Understand secure key distribution      |
| OTA (Over-the-Air) Mock Update | Simulate secure firmware delivery       |

---

## Tools Checklist: (at Trainer/Instructor's End): Check for yours/Cohort Member's end

| Item                                                     | Status |
| -------------------------------------------------------- | ------ |
| Arduino IDE with ESP32 Board Installed                   | ✅      |
| Libraries: `PubSubClient`, `ArduinoJson`, `Crypto`       | ✅      |
| Internet-connected WiFi network                          | ✅      |
| HiveMQ Cloud credentials                                 | ✅      |
| Access to your assigned MQTT topic (e.g. `test/pratham`) | ✅      |

---

## Submit & Track

After every exercise:

* Publish to your `test/<yourname>` topic
* Use **Serial Monitor** to debug your ESP32 board
* Ask trainer/instructor to verify your result on their trainer console

---

*This project is part of the CV Labs IIoT Embedded Security Foundation Series.*
