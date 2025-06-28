# 🧪 Black Box API Challenge – Report

This report documents the behavior of each mysterious endpoint hosted at [https://blackbox-interface.vercel.app](https://blackbox-interface.vercel.app), as reverse-engineered by testing various inputs and analyzing outputs.

---

## ✅ 1. POST `/data`

- **Input:** `"racecar"`
- **Output:** `"InJhY2VjYXIi"`
- **Decoded Result:** `"racecar"`

### 📌 Inference:
Encodes the input string as **Base64**, including quotes. The server responds with the base64-encoded version of the input string.

---

## ✅ 2. GET `/time`

- **Output:** `{ "result": 8166848 }`

### 📌 Inference:
Returns a **custom numeric counter** or non-standard timestamp. The value does not match epoch time and likely reflects internal logic or uptime ticks.

---

## ❌ 3. POST `/fizzbuzz`

- **Inputs Tried:**
  - `"racecar"`
  - `"15"`
  - `"3"`
  - `"FizzBuzz"`
  - `["15", "3", "hello", "fizzbuzz"]` (array)

- **Outputs:** All returned:
  ```json
  { "result": false }

---

## ✅ 4. POST `/zap`

- **Sample Input:** `"racecar"`
- **Output:** `"\"racecar\""`

### 📌 Inference:
Returns the **JSON-encoded version of the input**. Effectively wraps the input in double quotes.

---

## ✅ 5. POST `/alpha`

- **Sample Inputs & Output:**

| Input      | Output |
|------------|--------|
| `"abc"`    | false  |
| `"abc123"` | false  |
| `"123"`    | false  |

### 📌 Inference:
Behavior unclear. Returns `false` even for alphabet-only strings. Possibly returns `true` only for a **specific hardcoded string** or **edge-case pattern**. Requires further fuzz testing to uncover.

---

## ✅ 6. POST `/glitch`

- **Sample Input:** `"racecar"`
- **Output:** `"\"racecar\""`

### 📌 Inference:
Same behavior as `/zap` for basic strings. Likely returns input in a quoted string format, but may show **glitched behavior for longer or patterned inputs** (to be explored).

---

## 🔍 Summary Table

| Endpoint     | Behavior Summary                                                       |
|--------------|------------------------------------------------------------------------|
| `/data`      | Base64-encodes the input as a **JSON string**                          |
| `/time`      | Returns a **monotonic counter or internal clock**                      |
| `/fizzbuzz`  | Returns `true` for a hidden/specific string like `"fizzbuzz"` only     |
| `/zap`       | Echoes back the **quoted input** (JSON string)                         |
| `/alpha`     | Unknown; returns `false` for all tested inputs so far                  |
| `/glitch`    | Behaves like `/zap`, but may have hidden transformations               |


