# 🧪 Black Box API Challenge – Report

This report documents the behavior of each mysterious endpoint hosted at [https://blackbox-interface.vercel.app](https://blackbox-interface.vercel.app), as reverse-engineered by testing various inputs and analyzing outputs.

---

## ✅ 1. POST `/data`

- **Input:** `"racecar"`
- **Output:** `"InJhY2VjYXIi"`
- **Decoded Result (Base64):** `"racecar"`

### 📌 Inference:
Encodes the input string as **Base64**, including double quotes.

---

## ✅ 2. GET `/time`

- **Output:** `{ "result": 8166848 }`

### 📌 Inference:
Returns a **custom numeric counter** or **non-standard timestamp**. The value does not match Unix epoch time, suggesting it might be a tick count, session ID, or internal uptime counter.

---

## ❌ 3. POST `/fizzbuzz`

- **Inputs Tried:**
  - `"racecar"`
  - `"15"`
  - `"3"`
  - `["15", "3", "hello", "fizzbuzz"]` (JSON array)
- **Outputs:** All returned `{ "result": false }`

### 📌 Inference:
The endpoint expects a **JSON array**, but returns `false` even for valid arrays or expected values like `15`, `3`, or `"FizzBuzz"`. Behavior unclear—possibly:
- Only accepts integer arrays with specific values.
- Possibly broken or incomplete logic.

Further testing required.

---

## ✅ 4. POST `/zap`

- **Input:** `"racecar"`
- **Output:** `"\"racecar\""`

### 📌 Inference:
Returns the **JSON-encoded version of the input** — the string with extra quotes. Acts like a simple stringify utility.

---

## ✅ 5. POST `/alpha`

- **Inputs Tried:**
  - `"abc"` → false
  - `"abc123"` → false
  - `"123"` → false
- **Output:** Always returns `false`

### 📌 Inference:
This endpoint seems to return `true` only under a **very specific and unknown condition**. All common alphanumeric and alphabetic inputs return `false`.

---

## ✅ 6. POST `/glitch`

- **Input:** `"racecar"`
- **Output:** `"\"racecar\""`

### 📌 Inference:
Behaves exactly like `/zap`. Echoes the input with quotes (JSON stringified). May behave differently with more complex inputs, but appears identical for simple strings.

---

## 🔍 Summary Table

| Endpoint     | Behavior Summary                                                       |
|--------------|------------------------------------------------------------------------|
| `/data`      | Base64-encodes the input string, including quotes                      |
| `/time`      | Returns a non-standard numerical counter or internal tick              |
| `/fizzbuzz`  | Always returns `false`, even for numeric and array inputs              |
| `/zap`       | Returns the input wrapped in quotes (JSON-stringified)                 |
| `/alpha`     | Returns `false` for all tested inputs; logic unclear                   |
| `/glitch`    | Same as `/zap`; quotes input as JSON string                            |


